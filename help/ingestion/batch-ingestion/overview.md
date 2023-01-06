---
keywords: Experience Platform；首頁；熱門主題；資料擷取；批次；啟用資料集；批次擷取概觀；概觀；批次擷取概觀；
solution: Experience Platform
title: 批次擷取API概觀
description: Adobe Experience Platform資料擷取API可讓您將資料以批次檔案的形式內嵌至Platform。 所擷取的資料可以是CRM系統中一般檔案（例如Parquet檔案）的設定檔資料，或符合Experience Data Model(XDM)註冊表中已知結構的資料。
exl-id: ffd1dc2d-eff8-4ef7-a26b-f78988f050ef
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 6%

---

# 批次內嵌API概觀

Adobe Experience Platform資料擷取API可讓您將資料以批次檔案的形式內嵌至Platform。 擷取的資料可以是來自一般檔案（例如Parquet檔案）的設定檔資料，或符合 [!DNL Experience Data Model] (XDM)註冊表。

此 [資料擷取API參考](https://www.adobe.io/experience-platform-apis/references/data-ingestion/) 提供這些API呼叫的其他資訊。

下圖概述批次擷取程式：

![](../images/batch-ingestion/overview/batch_ingestion.png)

## 快速入門

本指南中使用的API端點屬於 [資料擷取API](https://www.adobe.io/experience-platform-apis/references/data-ingestion/). 繼續之前，請檢閱 [快速入門手冊](getting-started.md) 如需相關檔案的連結，請參閱本檔案中讀取範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需的必要標頭重要資訊。

### [!DNL Data Ingestion] 必要條件

- 要上傳的資料必須採用Parquet或JSON格式。
- 在 [[!DNL Catalog services]](../../catalog/home.md).
- Parquet檔案的內容必須符合上傳至之資料集結構的子集。
- 在驗證後使用您的唯一存取權杖。

### 批次內嵌最佳實務

- 建議的批處理大小介於256 MB和100 GB之間。
- 每個批次最多應包含1500個檔案。

### 批次內嵌限制

批次資料內嵌有一些限制：

- 每批檔案的最大數量：1500
- 最大批大小：100 GB
- 每列的屬性或欄位數上限：10000
- 每用戶每分鐘的最大批次數：138

>[!NOTE]
>
>若要上傳大於512MB的檔案，必須將檔案分割為較小的區塊。 上傳大型檔案的指示位於 [本文檔的大檔案上載部分](#large-file-upload---create-file).

### 類型

擷取資料時，請務必了解 [!DNL Experience Data Model] (XDM)結構可運作。 如需XDM欄位類型如何對應至不同格式的詳細資訊，請參閱 [Schema Registry開發人員指南](../../xdm/api/getting-started.md).

擷取資料時有一些彈性 — 如果類型與目標架構中的內容不符，則資料會轉換為表示的目標類型。 如果無法，則會以 `TypeCompatibilityException`.

例如，JSON或CSV都沒有 `date` 或 `date-time` 類型。 因此，這些值會以 [ISO 8061格式化字串](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15&quot;:05:59.000-08:00英吋)或以毫秒(1531263959000)為單位的Unix時間格式，並會在擷取時轉換為目標XDM類型。

下表顯示擷取資料時支援的轉換。

| 入站（列）與目標（列） | 字串 | 位元組 | 簡短 | 整數 | 長 | 雙倍 | 日期 | 日期-時間 | 物件 | 地圖 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 字串 | X | X | X | X | X | X | X | X |  |  |
| 位元組 | X | X | X | X | X | X |  |  |  |  |
| 簡短 | X | X | X | X | X | X |  |  |  |  |
| 整數 | X | X | X | X | X | X |  |  |  |  |
| 長 | X | X | X | X | X | X | X | X |  |  |
| 雙倍 | X | X | X | X | X | X |  |  |  |  |
| 日期 |  |  |  |  |  |  | X |  |  |  |
| 日期-時間 |  |  |  |  |  |  |  | X |  |  |
| 物件 |  |  |  |  |  |  |  |  | X | X |
| 地圖 |  |  |  |  |  |  |  |  | X | X |

>[!NOTE]
>
>布林值和陣列無法轉換為其他類型。

## 使用 API

此 [!DNL Data Ingestion] API可讓您將資料以批次（資料單位，由一或多個要以單一單位內嵌的檔案組成）內嵌至 [!DNL Experience Platform] 三個基本步驟：

1. 建立新批。
2. 將檔案上傳至符合資料之XDM結構的指定資料集。
3. 發出批次結束的信號。

## 建立批次

必須先將資料連結至批次資料，之後再上傳至指定的資料集，才能將資料新增至資料集。

```http
POST /batches
```

**要求**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
  -d '{ 
          "datasetId": "{DATASET_ID}" 
      }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `datasetId` | 上傳檔案至的資料集ID。 |

**回應**

```JSON
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
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

成功建立新批次以供上傳後，即可將檔案上傳至特定資料集。

您可以使用小型檔案上傳API來上傳檔案。 不過，如果您的檔案太大且超出閘道限制（例如延長逾時、超出主體大小的要求及其他限制），您可以切換至「大型檔案上傳API」。 此API會以區塊上傳檔案，並使用「大型檔案上傳完成API」呼叫將資料匯整在一起。

>[!NOTE]
>
>批次內嵌可用來逐步更新設定檔存放區中的資料。 如需詳細資訊，請參閱 [更新批](#patch-a-batch) 在 [批次匯入開發人員指南](api-overview.md).

>[!INFO]
>
>以下範例使用 [阿帕奇鑲木地板](https://parquet.apache.org/docs/) 檔案格式。 若需使用JSON檔案格式的範例，請參閱 [批次匯入開發人員指南](api-overview.md).

### 小型檔案上傳

建立批次資料後，即可將資料上傳至現有的資料集。  上傳的檔案必須符合其參考的XDM結構。

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 批的ID。 |
| `{DATASET_ID}` | 上傳檔案的資料集ID。 |
| `{FILE_NAME}` | 資料集中顯示的檔案名稱。 |

**要求**

```SHELL
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 要上傳至資料集的檔案路徑和檔案名稱。 |

**回應**

```JSON
#Status 200 OK, with empty response body
```

### 大型檔案上傳 — 建立檔案

若要上傳大型檔案，必須將檔案分割為較小的區塊，並一次上傳一個。

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 批的ID。 |
| `{DATASET_ID}` | 擷取檔案的資料集ID。 |
| `{FILE_NAME}` | 資料集中顯示的檔案名稱。 |

**要求**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet?action=initialize" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**回應**

```JSON
#Status 201 CREATED, with empty response body
```

### 大型檔案上傳 — 上傳後續部件

建立檔案後，可以透過重複的PATCH要求來上傳所有後續區塊，檔案的每個區段各一個。

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 批的ID。 |
| `{DATASET_ID}` | 上傳檔案至的資料集ID。 |
| `{FILE_NAME}` | 資料集中顯示的檔案名稱。 |

**要求**

```SHELL
curl -X PATCH "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "Content-Range: bytes {CONTENT_RANGE}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 要上傳至資料集的檔案路徑和檔案名稱。 |

**回應**

```JSON
#Status 200 OK, with empty response
```

## 信號批完成

將所有檔案上載到批後，可以發出批完成的信號。 通過這樣做， [!DNL Catalog] DataSetFile條目是為已完成的檔案建立的，並與上述生成的批相關聯。 此 [!DNL Catalog] 接著，批次會標示為成功，這會觸發下游流程內嵌可用資料。

**要求**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 要上傳至資料集的批次ID。 |

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
-H "x-gw-ims-org-id: {ORG_ID}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key: {API_KEY}"
```

**回應**

```JSON
#Status 200 OK, with empty response
```

## 檢查批狀態

等待檔案上傳至批次時，可以檢查批次的狀態，以查看其進度。

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
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

**回應**

```JSON
{
    "{BATCH_ID}": {
        "imsOrg": "{ORG_ID}",
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

此 `"status"` 欄位是顯示所請求批的當前狀態的內容。 批可以具有以下任一狀態：

## 批次內嵌狀態

| 狀態 | 說明 |
| ------ | ----------- |
| 放棄 | 批未在預期的時間範圍內完成。 |
| 已中止 | 中止操作具有 **顯式** 已針對指定批次呼叫（透過批次內嵌API）。 一旦批次進入「已載入」狀態，就無法中止。 |
| 作用中 | 批已成功升級，可用於下游衝減。 此狀態可與「Success」交替使用。 |
| 已刪除 | 批次的資料已完全移除。 |
| 已失敗 | 由錯誤配置和/或錯誤資料造成的終端狀態。 失敗批次的資料將 **not** 出現。 此狀態可與「失敗」交互使用。 |
| 非作用中 | 批已成功升級，但已還原或已過期。 該批不再可用於下游衝減。 |
| 已載入 | 批次的資料已完成，且該批次已準備好升級。 |
| 載入 | 正在上載此批的資料，且該批當前正在 **not** 準備升職。 |
| 重試 | 正在處理此批的資料。 但是，由於系統或暫時錯誤，該批處理失敗，因此正在重試該批處理。 |
| 已轉移 | 批的升級進程的分段階段已完成，並且已運行獲取作業。 |
| 預備 | 正在處理批的資料。 |
| 逾時 | 正在處理批的資料。 不過，多次重試後批次促銷已停止。 |
