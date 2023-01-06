---
keywords: Experience Platform；首頁；熱門主題；內嵌資料；疑難排解；faq；內嵌；批次內嵌；批次內嵌；
solution: Experience Platform
title: 批次內嵌疑難排解指南
description: 本檔案將協助您解答Adobe Experience Platform批次資料擷取API的常見問題。
exl-id: 0a750d7e-a4ee-4a79-a697-b4b732478b2b
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 1%

---

# 批次內嵌疑難排解指南

本檔案將協助您解答有關Adobe Experience Platform的常見問題 [!DNL Batch Data Ingestion] API。

## 批次API呼叫

### 從CompleteBatch API收到HTTP 200 OK後，批次是否會立即啟用？

此 `200 OK` 來自API的回應表示已接受批次處理 — 在其轉變為最終狀態（如「作用中」或「失敗」）前，該批次不會作用中。

### 失敗後重試CompleteBatch API呼叫是否安全？

是 — 可以安全地重試API呼叫。 儘管出現了故障，但操作實際上是成功的，並且批被成功接受。 但是，在API失敗時，用戶端應具有重試機制，事實上，建議您重試。 如果操作實際成功，API將會傳回成功，即使重試後亦然。

### 何時應使用大型檔案上傳API?

使用大型檔案上傳API的建議檔案大小為256 MB或更大。 如需如何使用大型檔案上傳API的詳細資訊，請參閱 [此處](./api-overview.md#ingest-large-parquet-files).

### 為何大型檔案完成API呼叫失敗？

如果發現大檔案的區塊重疊或遺失，伺服器會使用HTTP 400 Bad Request回應。 這可能是因為可以上傳重疊的區塊，因為在檔案完成時，當檔案區塊拼接在一起時，就會執行範圍驗證。

## 擷取支援

### 支援的內嵌格式為何？

目前支援Parquet和JSON。 舊版支援CSV — 雖然資料將升級為主檢查且將完成初步檢查，但不支援轉換、分割或列驗證等現代功能。

### 應在何處指定批輸入格式？

應在裝載內的批次建立時指定輸入格式。 如需如何指定批次輸入格式的範例，請參閱下文：

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
    }'
```

### 上傳的資料為何沒有顯示在資料集中？

若要在資料集中顯示資料，必須將批次標示為已完成。 您必須先上傳您要內嵌的所有檔案，才能將批次標示為完成。 以下是將批標籤為完成的示例：

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### 如何擷取多行JSON?

若要內嵌多行JSON，請 `isMultiLineJson` 標幟必須在建立批次時設定。 以下是此範例：

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json",
                "isMultiLineJson": true
           }
      }'
```

### JSON行（單行JSON）和多行JSON有何不同？

若為JSON行，每行會有一個JSON物件。 例如：

```json
{"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}}
{"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}}
{"string":"string3","int":3,"array":[3,6,9],"dict": {"key": "value3", "extra_key": "extra_value3"}}
```

若為多行JSON，一個物件可能佔據多行，而所有物件都包裝在JSON陣列中。 例如：

```json
[
    {"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}},
    {"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}},
    {
        "string": "string3",
        "int": 3,
        "array": [
            3,
            6,
            9
        ],
        "dict": {
            "key": "value3",
            "extra_key": "extra_value3"
        }
    }
]
```

依預設， [!DNL Batch Data Ingestion] 使用單行JSON。

### 是否支援CSV擷取？

CSV擷取僅支援一般結構。 目前不支援擷取CSV中的階層資料。

若要取得所有資料擷取功能，需使用JSON或Parquet格式。

### 對資料執行哪些類型的驗證？

對資料執行的驗證有三個層級：

- 結構 — 批次擷取可確保所擷取資料的結構符合資料集的結構。
- 資料類型 — 批次內嵌可確保擷取的每個欄位類型與資料集結構中定義的類型相符。
- 限制 — 批次擷取可確保在架構定義中正確定義「必要」、「列舉」和「格式」等限制。

### 如何更換已擷取的批次？

已內嵌的批次可使用「批次重播」功能來取代。 如需批次重播的詳細資訊，請參閱 [此處](./api-overview.md#replay-a-batch).

### 如何監控批次內嵌？

一旦為批升級發出了批信號，即可使用以下請求監控批獲取進度：

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

透過此請求，您會收到類似以下的回應：

```http
200 OK
```

```json
{
    "{BATCH_ID}":{
        "imsOrg":"{ORG_ID}",
        "created":1494349962314,
        "createdClient":"{API_KEY}",
        "createdUser":"{USER_ID}",
        "updatedUser":"{USER_ID}",
        "completed":1494349963467,
        "externalId":"{EXTERNAL_ID}",
        "status":"staging",
        "errors":[],
    }
}
```

## 批次狀態

### 可能的批次狀態為何？

批次在其生命週期中可以執行下列狀態：

| 狀態 | 寫入主資料 | 說明 |
| ------ | ---------------------- | ----------- |
| 放棄 |  | 客戶端未能在預期的時間範圍內完成批處理。 |
| 已中止 |  | 用戶端已透過 [!DNL Batch Data Ingestion] API，指定批次的中止操作。 一旦批次處於「已載入」狀態，該批次就無法中止。 |
| 作用中/成功 | x | 批次已成功從階段提升至主版，現在可用於下游耗用。 **注意：** 「作用中」和「成功」可交互使用。 |
| 已封存 |  | 該批已存檔到冷儲存中。 |
| 失敗/失敗 |  | 由錯誤配置和/或錯誤資料造成的終端狀態。 會記錄可操作的錯誤以及批次，讓客戶能更正並重新提交資料。 **注意：** 「失敗」和「失敗」可交互使用。 |
| 非作用中 | x | 批已成功升級，但已還原或已過期。 該批將不再可用於下游衝減，但基礎資料將保留在主資料中，直到它被保留、存檔或以其他方式刪除為止。 |
| 載入 |  | 客戶端當前正在為批處理寫入資料。 批次為 **not** 已準備好升級，此時已可。 |
| 已載入 |  | 客戶端已完成寫入批資料。 批已準備好升級。 |
| 保留 |  | 資料已從Master中取出，並在Adobe資料湖的指定存檔中取出。 |
| 預備 |  | 客戶端已成功發出批次升級的信號，並且正在儲存資料以供下游消耗。 |
| 重試 |  | 客戶端已發出批次升級的信號，但由於錯誤，批次正在由批次監視服務重試。 此狀態可用來告知用戶端資料擷取可能會延遲。 |
| 逾時 |  | 客戶端已發出批號以進行升級，但在 `n` 批次監控服務重試，批次促銷已中止。 |

### 批次的「測試」代表什麼？

當批處於「暫存」時，表示已成功發出該批的升級信號，且資料正在暫存以供下游耗用。

### 批次為「重試」時，代表什麼意思？

當批次處於「重試」狀態時，這表示該批次的資料擷取已因間歇性問題而暫時暫停。 發生此情況時，不需要客戶干預。

### 當批次「逾時」時，代表什麼意思？

當批處於「停頓」狀態時，表示 [!DNL Data Ingestion Services] 正在嘗試讀取批，且所有重試已用盡。

### 如果批次仍為「正在載入」，代表什麼意思？

當批次處於「載入」狀態時，表示尚未呼叫CompleteBatch API以促銷該批次。

### 是否有方法可知道批次是否已成功擷取？

批次狀態為「作用中」後，即已成功內嵌該批次。 要了解批的狀態，請按照詳細步驟操作 [較早](#how-is-batch-ingestion-monitored).

### 批次失敗後會發生什麼事？

批次失敗時，可在 `errors` 裝載的區段。 錯誤的範例如下：

```json
    "errors":[
        {
            "code":"106",
            "description":"Dataset file is empty. Please upload file with data.",
            "rows":[]
        },
        {
            "code":"118",
            "description":"CSV file contains empty header row.",
            "rows":[]
        }
    ]
```

更正錯誤後，即可重新上傳批次。

## 批次支援

### 如何刪除批？

而非直接從 [!DNL Catalog]，批次應使用下列其中一種方法來移除：

1. 如果正在處理該批，應該中止該批。
2. 如果成功掌握了批，則應還原該批。

### 哪些批次層級量度可供使用？

下列批次層級量度適用於「作用中/成功」狀態的批次：

| 量度 | 說明 |
| ------ | ----------- |
| inputByteSize | 為 [!DNL Data Ingestion Services] 來處理。 |
| inputRecordSize | 為 [!DNL Data Ingestion Services] 來處理。 |
| outputByteSize | 輸出的總位元組數 [!DNL Data Ingestion Services] to [!DNL Data Lake]. |
| outputRecordSize | 輸出的總行數 [!DNL Data Ingestion Services] to [!DNL Data Lake]. |
| partitionCount | 寫入的分區總數 [!DNL Data Lake]. |

### 為何某些批次無法使用量度？

量度可能無法用於批次的原因有兩：

1. 批次從未成功進入「作用中/成功」狀態。
2. 批次是使用舊版促銷路徑（例如CSV擷取）來促銷。

### 不同的狀態代碼代表什麼？

| 狀態代碼 | 說明 |
| ----------- | ----------- |
| 106 | 資料集檔案為空。 |
| 118 | CSV檔案包含空白的標題列。 |
| 200 | 批已接受處理，並將轉變為最終狀態，如「活動」或「失敗」。 提交後，即可使用監控批次 `GetBatch` 端點。 |
| 400 | Bad Request. 如果批次中缺少區塊或重疊區塊，則傳回。 |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
