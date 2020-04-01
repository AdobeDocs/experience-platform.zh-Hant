---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform批次擷取概觀
topic: overview
translation-type: tm+mt
source-git-commit: 79466c78fd78c0f99f198b11a9117c946736f47a

---


# 批次擷取概觀

批次擷取API可讓您將資料以批次檔案的形式內嵌至Adobe Experience Platform。 所吸收的資料可以是CRM系統中平面檔案（例如鑲木地板檔案）的描述檔資料，或是符合Experience Data Model(XDM)註冊表中已知架構的資料。

「資 [料擷取API參考」](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) ，提供這些API呼叫的其他資訊。

下圖概述了批處理過程：

![](../images/batch-ingestion/overview/batch_ingestion.png)

## 使用API

資料擷取API可讓您透過三個基本步驟，將資料以批次形式（由一或多個要以單一單位格式擷取的檔案組成的資料單位）擷取至Experience Platform:

1. 建立新批。
2. 將檔案上傳至符合資料XDM架構的指定資料集。
3. 發出批次結束的信號。


### 資料擷取先決條件

- 要上傳的資料必須採用Parce或JSON格式。
- 在目錄服務中建立的 [資料集](../../catalog/home.md)。
- 拼字檔案的內容必須符合上傳資料集之模式的子集。
- 在驗證後取得您唯一的存取Token。

### 批次擷取最佳實務

- 建議的批處理大小介於256 MB和100 GB之間。
- 每個批次最多應包含1500個檔案。

若要上傳大於512MB的檔案，檔案必須分成較小的區塊。 有關上傳大型檔案的說明，請 [到這裡](#large-file-upload---create-file)。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集必要標題的值

若要呼叫平台API，您必須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

- 授權：生產者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源都隔離至特定的虛擬沙盒。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 如需平台中沙盒的詳細資訊，請參閱沙盒 [概觀檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

### 建立批次

資料必須連結至批次，之後才會上傳至指定的資料集，才能將資料新增至資料集。

```http
POST /batches
```

**請求**

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

您可以使用「小型檔案上 **傳API」上傳檔案**。 不過，如果您的檔案過大且已超出閘道限制（例如延長逾時、超出內文大小的要求，以及其他限制），您可以切換至「大型檔案上傳 **API」**。 此API會以區塊上傳檔案，並使用「大型檔案上傳完成 **API」呼叫將資料連結在一起** 。

>[!NOTE] 以下範例使用 [鑲木地板](https://parquet.apache.org/documentation/latest/) 檔案格式。 如需使用JSON檔案格式的範例，請參閱批次擷取開發 [人員指南](./api-overview.md)。

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

**請求**

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

**請求**

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

建立檔案後，可以通過重複的PATCH請求來上載所有後續的塊，該請求對檔案的每個部分各一個。

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 批的ID。 |
| `{DATASET_ID}` | 上傳檔案至的資料集ID。 |
| `{FILE_NAME}` | 資料集中會看到的檔案名稱。 |

**請求**

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

將所有檔案上傳到批後，可以向批發出完成信號。 通過執行此操作，將為已完 **成的檔案建立目錄DataSetFile** 條目，並與上面生成的批相關聯。 然後目錄批次會標示為成功，這會觸發下游流程，以擷取可用資料。

**請求**

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

**請求**

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

字 `"status"` 段顯示請求的批的當前狀態。 批可以具有以下狀態之一：

## 批次擷取狀態

| 狀態 | 說明 |
| ------ | ----------- |
| 已放棄 | 批未在預期時間範圍內完成。 |
| 已中止 | 已明確呼叫 **(透過** 「批次內嵌API」)指定批次的中止作業。 一旦批處於「已載入 **」狀態** ，便無法中止。 |
| 作用中 | 批已成功升級，可用於下游衝減。 此狀態可與「成功」交替 **使用**。 |
| 已刪除 | 批次的資料已完全移除。 |
| 失敗 | 由錯誤配置和／或錯誤資料引起的終端狀態。 失敗批次的資料 **將不** 顯示。 此狀態可與「故障」( **Failure)互換使用**。 |
| 非活動 | 批已成功升級，但已還原或已過期。 批不再可用於下游衝減。 |
| 已載入 | 批的資料已完成，批已準備好進行升級。 |
| 正在載入 | 正在上載此批的資料，且該批當前尚 **未** 準備升級。 |
| 重試 | 正在處理此批的資料。 但是，由於系統或瞬態錯誤，批次失敗——因此，正在重試此批次。 |
| 已分段 | 批的升級流程的轉移階段已完成，並且已運行提取作業。 |
| 測試 | 正在處理批的資料。 |
| 停止 | 正在處理批的資料。 不過，批次促銷在多次重試後已停止。 |