---
keywords: Experience Platform；首頁；熱門主題；資料擷取；批次；批次；啟用資料集；批次擷取總覽；總覽；批次擷取總覽；
solution: Experience Platform
title: 批次擷取API概觀
description: Adobe Experience Platform批次擷取API可讓您將資料以批次檔案的形式擷取到Platform。 所擷取的資料可以是CRM系統中平面檔案（例如Parquet檔案）的設定檔資料，或是符合Experience Data Model (XDM)登入中已知結構的資料。
exl-id: ffd1dc2d-eff8-4ef7-a26b-f78988f050ef
source-git-commit: 9d3a8aac120119ce0361685f9cb8d3bfc28dc7fd
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 6%

---

# 批次擷取API總覽

Adobe Experience Platform批次擷取API可讓您將資料以批次檔案的形式擷取到Platform。 所擷取的資料可以是平面檔案（例如Parquet檔案）的設定檔資料，或是符合 [!DNL Experience Data Model] (XDM)登入。

此 [批次擷取API參考資料](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) 提供有關這些API呼叫的其他資訊。

下圖概述批次擷取程式：

![](../images/batch-ingestion/overview/batch_ingestion.png)

## 快速入門

本指南中使用的API端點屬於 [批次擷取API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). 在繼續之前，請檢閱 [快速入門手冊](getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的指南，以及有關成功呼叫任何Experience PlatformAPI所需標題的重要資訊。

### [!DNL Data Ingestion] 必備條件

- 要上傳的資料必須是Parquet或JSON格式。
- 在中建立的資料集 [[!DNL Catalog services]](../../catalog/home.md).
- Parquet檔案的內容必須符合要上傳到之資料集的結構描述子集。
- 在驗證後取得您唯一的存取Token。

### 批次擷取最佳實務

- 建議的批次大小介於256 MB和100 GB之間。
- 每個批次最多可包含1500個檔案。

### 批次擷取限制

批次資料擷取有一些限制：

- 每批次的最大檔案數： 1500
- 最大批次大小：100 GB
- 每列的屬性或欄位數上限： 10000
- 每個使用者每分鐘資料湖的批次數量上限： 138

>[!NOTE]
>
>若要上傳大於512MB的檔案，檔案必須分成較小的區塊。 上傳大型檔案的指示可在以下連結中找到： [此檔案的大型檔案上傳區段](#large-file-upload---create-file).

### 型別

擷取資料時，請務必瞭解如何 [!DNL Experience Data Model] (XDM)結構描述有效。 如需XDM欄位型別如何對應至不同格式的詳細資訊，請參閱 [Schema Registry開發人員指南](../../xdm/api/getting-started.md).

擷取資料時有一些彈性 — 如果型別不符合目標結構描述中的內容，資料將會轉換為表達的目標型別。 如果失敗，則會讓批次失敗 `TypeCompatibilityException`.

例如，JSON和CSV都不會使用 `date` 或 `date-time` 型別。 因此，這些值會使用 [ISO 8061格式字串](https://www.iso.org/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15:05:59.000-08:00英吋)或Unix時間(以毫秒為單位，1531263959000會在擷取時轉換為目標XDM型別。

下表顯示擷取資料時支援的轉換。

| 傳入（列）與目標（欄） | 字串 | 位元組 | 短 | 整數 | 長 | 雙倍 | 日期 | 日期 — 時間 | 物件 | 地圖 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 字串 | X | X | X | X | X | X | X | X |   |   |
| 位元組 | X | X | X | X | X | X |   |   |   |   |
| 短 | X | X | X | X | X | X |   |   |   |   |
| 整數 | X | X | X | X | X | X |   |   |   |   |
| 長 | X | X | X | X | X | X | X | X |   |   |
| 雙倍 | X | X | X | X | X | X |   |   |   |   |
| 日期 |   |   |   |   |   |   | X |   |   |   |
| 日期 — 時間 |   |   |   |   |   |   |   | X |   |   |
| 物件 |   |   |   |   |   |   |   |   | X | X |
| 地圖 |   |   |   |   |   |   |   |   | X | X |

>[!NOTE]
>
>布林值和陣列無法轉換為其他型別。

## 使用 API

此 [!DNL Data Ingestion] API可讓您將資料以批次（由一或多個要當作單一單位內嵌的檔案組成的一個資料單位）的形式內嵌到 [!DNL Experience Platform] 基本步驟如下：

1. 建立新批次。
2. 將檔案上傳到與資料的XDM結構描述相符的指定資料集。
3. 表示批次結束。

## 建立批次

必須先將資料連結至批次，之後再將其上傳至指定的資料集，才能將資料新增至資料集。

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
| `datasetId` | 要上傳檔案的資料集識別碼。 |

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
| `id` | 剛建立的批次ID （用於後續請求）。 |
| `relatedObjects.id` | 要上傳檔案的資料集識別碼。 |

## 檔案上傳

在成功建立要上傳的新批次之後，檔案可以上傳到特定資料集。

您可以使用「小型檔案上傳API」來上傳檔案。 不過，如果您的檔案過大，且已超過閘道限制（例如延長逾時、請求內文大小已超出及其他限制），您可以切換至大型檔案上傳API。 此API會以區塊上傳檔案，並使用大型檔案上傳完成API呼叫將資料彙整在一起。

>[!NOTE]
>
>批次內嵌可用於以增量方式更新設定檔存放區中的資料。 如需詳細資訊，請參閱以下章節： [更新批次](#patch-a-batch) 在 [批次內嵌開發人員指南](api-overview.md).

>[!INFO]
>
>以下範例使用 [Apache Parquet](https://parquet.apache.org/docs/) 檔案格式。 以下是使用JSON檔案格式的範例： [批次內嵌開發人員指南](api-overview.md).

### 小檔案上傳

建立批次後，即可將資料上傳到預先存在的資料集。  要上傳的檔案必須符合其參考的XDM結構描述。

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 批次的ID。 |
| `{DATASET_ID}` | 要上傳檔案的資料集識別碼。 |
| `{FILE_NAME}` | 在資料集中看到的檔案名稱。 |

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
| `{FILE_PATH_AND_NAME}` | 要上傳至資料集的檔案的路徑和檔案名稱。 |

**回應**

```JSON
#Status 200 OK, with empty response body
```

### 大型檔案上傳 — 建立檔案

若要上傳大型檔案，必須將檔案分割為較小的區塊，並一次上傳一個區塊。

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 批次的ID。 |
| `{DATASET_ID}` | 擷取檔案的資料集識別碼。 |
| `{FILE_NAME}` | 在資料集中看到的檔案名稱。 |

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

### 大型檔案上傳 — 上傳後續部分

建立檔案後，可以透過重複的PATCH請求（檔案的每個區段各一個）上傳所有後續的區塊。

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 批次的ID。 |
| `{DATASET_ID}` | 要上傳檔案的資料集識別碼。 |
| `{FILE_NAME}` | 將在資料集中看到的檔案名稱。 |

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
| `{FILE_PATH_AND_NAME}` | 要上傳至資料集的檔案的路徑和檔案名稱。 |

**回應**

```JSON
#Status 200 OK, with empty response
```

## 訊號批次完成

將所有檔案都上傳到批次之後，就可以發出完成批次的訊號。 藉由執行此動作， [!DNL Catalog] DataSetFile專案是為已完成的檔案建立的，並與上面產生的批次相關聯。 此 [!DNL Catalog] 然後批次會標籤為成功，這會觸發下游流程擷取可用資料。

**要求**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 要上傳至資料集的批次識別碼。 |

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

## 檢查批次狀態

在等待檔案上傳到批次時，可以檢查批次的狀態以檢視其進度。

**API格式**

```http
GET /batch/{BATCH_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 正在檢查的批次識別碼。 |

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
| `{USER_ID}` | 建立或更新批次的使用者ID。 |

此 `"status"` 欄位會顯示所請求批次的目前狀態。 批次可以有下列其中一種狀態：

## 批次擷取狀態

| 狀態 | 說明 |
| ------ | ----------- |
| 已放棄 | 批次未在預期時間範圍內完成。 |
| 已中止 | 中止作業具有 **明確** 已針對指定的批次呼叫（透過批次擷取API）。 批次一旦處於「已載入」狀態，就無法中止。 |
| 作用中 | 已成功提升批次，並可用於下游消耗。 此狀態可與「成功」互換使用。 |
| 已刪除 | 批次的資料已完全移除。 |
| 失敗 | 因設定錯誤和/或資料錯誤而導致的終端機狀態。 失敗批次的資料將 **非** 顯示。 此狀態可與「失敗」互換使用。 |
| 非使用中 | 批次已成功提升，但已還原或已過期。 該批次不再可用於下游沖銷。 |
| 已載入 | 批次的資料已完成，且批次已準備好進行升級。 |
| 正在載入 | 此批次的資料正在上傳，批次目前正在上傳 **非** 已準備好提升。 |
| 正在重試 | 此批次的資料正在處理中。 但由於系統或暫時性錯誤，批次失敗 — 因此，將重試此批次。 |
| 已分段 | 批次升級流程的準備階段已完成，且擷取工作已執行。 |
| 預備 | 正在處理批次的資料。 |
| 已擱置 | 批次的資料正在處理中。 但是，在多次重試後，批次促銷活動已停止。 |
