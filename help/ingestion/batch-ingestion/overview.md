---
keywords: Experience Platform; home；熱門主題；資料提取；batch;Batch；啟用資料集；批處理提取概述；概述；批處理提取概述；
solution: Experience Platform
title: 批次擷取概觀
topic-legacy: overview
description: Adobe Experience Platform資料擷取API可讓您將資料以批次檔案的形式，收錄到平台中。 所吸收的資料可以是CRM系統中平面檔案（例如Parce檔案）的描述檔資料，或是符合Experience Data Model(XDM)註冊表中已知架構的資料。
exl-id: ffd1dc2d-eff8-4ef7-a26b-f78988f050ef
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 2%

---

# 批次擷取概觀

Adobe Experience Platform資料擷取API可讓您將資料以批次檔案的形式，收錄到平台中。 所吸收的資料可以是CRM系統中平面檔案（例如Parce檔案）的描述檔資料，或符合[!DNL Experience Data Model](XDM)註冊表中已知架構的資料。

[資料擷取API參考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)提供這些API呼叫的其他資訊。

下圖概述了批處理過程：

![](../images/batch-ingestion/overview/batch_ingestion.png)

## 使用API

[!DNL Data Ingestion] API可讓您透過三個基本步驟，將資料內嵌為批次（由一或多個要以單一單位收錄的檔案組成的資料單位）至[!DNL Experience Platform]:

1. 建立新批。
2. 將檔案上傳至符合資料XDM架構的指定資料集。
3. 發出批次結束的信號。


### [!DNL Data Ingestion] 先決條件

- 要上傳的資料必須採用Parce或JSON格式。
- 在[[!DNL Catalog services]](../../catalog/home.md)中建立的資料集。
- Parce檔案的內容必須符合上傳資料集之模式的子集。
- 在驗證後取得您唯一的存取Token。

### 批次擷取最佳實務

- 建議的批處理大小介於256 MB和100 GB之間。
- 每個批次最多應包含1500個檔案。

若要上傳大於512MB的檔案，檔案必須分成較小的區塊。 有關上傳大型檔案的說明，請參閱[此處](#large-file-upload---create-file)。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

- 授權：載體`{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有資源都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙盒的詳細資訊，請參閱[沙盒概述檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

### 建立批次

資料必須連結至批次，之後才會上傳至指定的資料集，才能將資料新增至資料集。

```http
POST /batches
```

**要求**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{ 
          "datasetId": "{DATASET_ID}" 
      }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `datasetId` | 上傳檔案至的資料集ID。 |

**Reponse**

```JSON
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 剛建立的批次ID（用於後續請求）。 |
| `relatedObjects.id` | 上傳檔案至的資料集ID。 |

## 檔案上傳

成功建立新批次以上傳後，檔案就可以上傳到特定資料集。

您可以使用「小型檔案上傳API」來上傳檔案。 不過，如果您的檔案過大且已超出閘道限制（例如延長逾時、超出內文大小的要求以及其他限制），您可以切換至「大型檔案上傳API」。 此API會以區塊上傳檔案，並使用「大型檔案上傳完成API」呼叫將資料連結在一起。

>[!NOTE]
>
>以下示例使用[Apache Parce](https://parquet.apache.org/documentation/latest/)檔案格式。 使用JSON檔案格式的範例，請參閱[批次擷取開發人員指南](./api-overview.md)。

### 小型檔案上傳

建立批次後，資料就可以上傳至預先存在的資料集。  上傳的檔案必須符合其參考的XDM架構。

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 批的ID。 |
| `{DATASET_ID}` | 上傳檔案的資料集ID。 |
| `{FILE_NAME}` | 資料集中會看到的檔案名稱。 |

**要求**

```SHELL
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 要上傳至資料集的檔案路徑和檔案名稱。 |

**Reponse**

```JSON
#Status 200 OK, with empty response body
```

### 大型檔案上傳——建立檔案

若要上傳大型檔案，檔案必須分割為較小的區塊，並一次上傳一個。

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 批的ID。 |
| `{DATASET_ID}` | 收錄檔案的資料集ID。 |
| `{FILE_NAME}` | 資料集中會看到的檔案名稱。 |

**要求**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet?action=initialize" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Reponse**

```JSON
#Status 201 CREATED, with empty response body
```

### 大型檔案上傳——上傳後續部件

在建立檔案後，可以透過重複的PATCH要求來上傳所有後續區塊，對檔案的每個區段各一個。

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 批的ID。 |
| `{DATASET_ID}` | 上傳檔案至的資料集ID。 |
| `{FILE_NAME}` | 資料集中會看到的檔案名稱。 |

**要求**

```SHELL
curl -X PATCH "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "Content-Range: bytes {CONTENT_RANGE}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 要上傳至資料集的檔案路徑和檔案名稱。 |

**Reponse**

```JSON
#Status 200 OK, with empty response
```

## 信號批次完成

將所有檔案上傳到批後，可以向批發出完成信號。 通過執行此操作，將為已完成的檔案建立[!DNL Catalog] DataSetFile條目，並與上面生成的批關聯。 然後，[!DNL Catalog]批次會標示為成功，這會觸發下游流量以擷取可用資料。

**要求**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 要上傳至資料集的批次ID。 |

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
-H "x-gw-ims-org-id: {IMS_ORG}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key : {API_KEY}"
```

**Reponse**

```JSON
#Status 200 OK, with empty response
```

## 檢查批狀態

等待檔案上傳到批時，可以檢查批的狀態以查看其進度。

**API格式**

```http
GET /batch/{BATCH_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 正在檢查的批的ID。 |

**要求**

```shell
curl GET "https://platform.adobe.io/data/foundation/catalog/batch/{BATCH_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

**Reponse**

```JSON
{
    "{BATCH_ID}": {
        "imsOrg": "{IMS_ORG}",
        "created": 1494349962314,
        "createdClient": "MCDPCatalogService",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1494349963467,
        "externalId": "{EXTERNAL_ID}",
        "status": "success",
        "errors": [
            {
                "code": "err-1494349963436"
            }
        ],
        "version": "1.0.3",
        "availableDates": {
            "startDate": 1337,
            "endDate": 4000
        },
        "relatedObjects": [
            {
                "type": "batch",
                "id": "foo_batch"
            },
            {
                "type": "connection",
                "id": "foo_connection"
            },
            {
                "type": "connector",
                "id": "foo_connector"
            },
            {
                "type": "dataSet",
                "id": "foo_dataSet"
            },
            {
                "type": "dataSetView",
                "id": "foo_dataSetView"
            },
            {
                "type": "dataSetFile",
                "id": "foo_dataSetFile"
            },
            {
                "type": "expressionBlock",
                "id": "foo_expressionBlock"
            },
            {
                "type": "service",
                "id": "foo_service"
            },
            {
                "type": "serviceDefinition",
                "id": "foo_serviceDefinition"
            }
        ],
        "metrics": {
            "foo": 1337
        },
        "tags": {
            "foo_bar": [
                "stuff"
            ],
            "bar_foo": [
                "woo",
                "baz"
            ],
            "foo/bar/foo-bar": [
                "weehaw",
                "wee:haw"
            ]
        },
        "inputFormat": {
            "format": "parquet",
            "delimiter": ".",
            "quote": "`",
            "escape": "\\",
            "nullMarker": "",
            "header": "true",
            "charset": "UTF-8"
        }
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{USER_ID}` | 建立或更新批的用戶的ID。 |

`"status"`欄位會顯示所請求批次的目前狀態。 批可以具有以下狀態之一：

## 批次擷取狀態

| 狀態 | 說明 |
| ------ | ----------- |
| 已放棄 | 批未在預期時間範圍內完成。 |
| 已中止 | 中止操作已為指定批調用&#x200B;**顯式**（通過批次收錄API）。 一旦批處於「已載入」狀態，便無法中止。 |
| 作用中 | 批已成功升級，可用於下游衝減。 此狀態可與「成功」交替使用。 |
| 已刪除 | 批次的資料已完全移除。 |
| 已失敗 | 由錯誤配置和／或錯誤資料引起的終端狀態。 失敗批次的資料將顯示&#x200B;**not**。 此狀態可與「故障」交替使用。 |
| 非活動 | 批已成功升級，但已還原或已過期。 批不再可用於下游衝減。 |
| 已載入 | 批的資料已完成，批已準備好進行升級。 |
| 正在載入 | 正在上載此批的資料，且該批當前&#x200B;**not**&#x200B;已準備升級。 |
| 重試 | 正在處理此批的資料。 但是，由於系統或瞬態錯誤，批次失敗——因此，正在重試此批次。 |
| 已分段 | 批的升級流程的轉移階段已完成，並且已運行提取作業。 |
| 預備 | 正在處理批的資料。 |
| 停止 | 正在處理批的資料。 不過，批次促銷在多次重試後已停止。 |
