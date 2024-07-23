---
keywords: Experience Platform；首頁；熱門主題；擷取的資料；疑難排解；faq；擷取；批次擷取；批次擷取；
solution: Experience Platform
title: 批次擷取疑難排解指南
description: 本檔案可協助回答有關Adobe Experience Platform批次資料擷取API的常見問題。
exl-id: 0a750d7e-a4ee-4a79-a697-b4b732478b2b
source-git-commit: 37b241f15f297263cc7aa20f382c115a2d131c7e
workflow-type: tm+mt
source-wordcount: '1426'
ht-degree: 1%

---

# 批次擷取疑難排解指南

本檔案可協助回答有關Adobe Experience Platform [!DNL Batch Data Ingestion] API的常見問題。

## 批次API呼叫

### 從CompleteBatch API收到HTTP 200 OK後，批次是否會立即啟用？

來自API的`200 OK`回應表示已接受批次處理 — 該批次在轉換為最終狀態（例如「作用中」或「失敗」）之前不會處於活動狀態。

### 在CompleteBatch API呼叫失敗後重試是否安全？

是 — 重試API呼叫是安全的。 儘管失敗，但作業可能實際成功，且已成功接受批次。 不過，如果API失敗，使用者端應該有重試機制，實際上建議重試。 如果操作實際成功，API會傳回成功，即使在重試後亦然。

### 何時應使用大型檔案上傳API？

使用「大型檔案上傳API」的建議檔案大小為256 MB或更大。 如需有關如何使用大型檔案上傳API的詳細資訊，請參閱[這裡](./api-overview.md#ingest-large-parquet-files)。

### 大型檔案完成API呼叫為何失敗？

如果發現大型檔案的區塊重疊或遺失，伺服器會以HTTP 400 Bad Request回應。 發生這種情況是因為有可能上傳重疊的區塊，因為範圍驗證是在檔案完成時、檔案區塊拼接在一起時完成的。

## 內嵌支援

### 支援哪些擷取格式？

目前同時支援Parquet和JSON。 舊版支援CSV — 雖然資料將會升級為主版並完成初步檢查，但不支援新式功能，例如轉換、分割或列驗證。

### 應在何處指定批次輸入格式？

輸入格式應在批次建立時在承載內指定。 如何指定批次輸入格式的範例，如下所示：

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

### 為何上傳的資料未出現在資料集中？

資料必須標籤為完成，資料才會出現在資料集中。 在將批次標籤為完成之前，必須上傳您要擷取的所有檔案。 標示批次為完成的範例如下所示：

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### 如何擷取多行JSON？

若要內嵌多行JSON，必須在建立批次時設定`isMultiLineJson`標幟。 其範例如下：

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

### JSON行（單行JSON）與多行JSON有何不同？

若為JSON行，每行有一個JSON物件。 例如：

```json
{"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}}
{"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}}
{"string":"string3","int":3,"array":[3,6,9],"dict": {"key": "value3", "extra_key": "extra_value3"}}
```

若使用多行JSON，一個物件可佔據多行，而所有物件皆包裝在JSON陣列中。 例如：

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

根據預設，[!DNL Batch Data Ingestion]使用單行JSON。

### 是否支援CSV內嵌？

CSV擷取僅支援一般結構描述。 目前不支援在CSV中擷取階層資料。

若要取得所有資料擷取功能，需要使用JSON或Parquet格式。

### 對資料執行什麼型別的驗證？

針對資料執行的驗證層級有三個：

- 結構 — 批次擷取可確保擷取資料的結構描述與資料集的結構描述相符。
- 資料型別 — 批次擷取可確保擷取的每個欄位的型別都與資料集結構描述中定義的型別相符。
- 限制 — 批次擷取可確保結構描述定義中正確定義限制，例如「必要」、「列舉」和「格式」。

### 如何取代已內嵌的批次？

已內嵌的批次可以使用「批次重播」功能來取代。 您可以在[這裡](./api-overview.md#replay-a-batch)找到有關批次重播的詳細資訊。

### 如何監控批次內嵌？

在發出批次升級的訊號後，可以使用以下請求來監視批次擷取進度：

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

透過此請求，您會獲得類似以下的回應：

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

批次在其生命週期中可以經歷以下狀態：

| 狀態 | 資料已寫入主版 | 說明 |
| ------ | ---------------------- | ----------- |
| 已放棄 | | 使用者端無法在預期時間範圍內完成批次。 |
| 已中止 | | 使用者端已透過[!DNL Batch Data Ingestion] API明確呼叫指定批次的中止作業。 批次一旦處於「已載入」狀態，就無法中止批次。 |
| 作用中/成功 | x | 已成功將批次從階段提升到主階段，現在可用於下游消耗。 **注意：**&#x200B;作用中及成功可互換使用。 |
| 已封存 | | 批次已封存到冷儲存。 |
| 失敗/失敗 | | 因設定錯誤和/或資料錯誤而導致的終端機狀態。 系統會記錄可操作錯誤及批次，讓使用者端修正並重新提交資料。 **注意：**&#x200B;失敗和失敗可互換使用。 |
| 停用中 | x | 批次已成功提升，但已還原或已過期。 該批次將無法再用於下游使用，但基礎資料將保留在主版中，直到其被保留、封存或以其他方式刪除。 |
| 載入中 | | 使用者端目前正在寫入批次的資料。 此時批次&#x200B;**尚未**&#x200B;準備好進行升級。 |
| 已載入 | | 使用者端已完成批次資料的寫入。 批次已準備好進行升級。 |
| 已保留 | | 資料已從Master和Adobe Data Lake的指定封存中取出。 |
| 預備 | | 使用者端已順利傳送批次訊號給促銷，而資料正在下游進行沖銷。 |
| 正在重試 | | 使用者端已發出要升級的批次訊號，但由於發生錯誤，批次正由「批次監視」服務重試。 此狀態可用來告訴使用者端擷取資料時可能發生延遲。 |
| 已過時 | | 使用者端已發出升級批次的訊號，但在批次監視服務重試`n`次之後，批次升級已停止。 |

### 「分段」對批次代表什麼意思？

當批次處於「暫存」中時，表示已成功將批次通知為促銷，且資料正暫存於下游以供沖銷。

### 批次為「重試」是什麼意思？

當批次處於「正在重試」中時，這表示由於間歇性問題，批次的資料擷取已暫時停止。 發生此情況時，不需要客戶介入。

### 當批次「已擱置」是什麼意思？

當批次處於「已擱置」狀態時，表示[!DNL Data Ingestion Services]在擷取批次時遇到困難，並且所有重試都已耗盡。

### 如果批次仍在「載入」是什麼意思？

當批次正在「載入」時，這表示尚未呼叫CompleteBatch API來升級批次。

### 是否有辦法知道批次是否已成功擷取？

可以，當批次狀態為「作用中」時，表示已成功擷取批次。 若要瞭解批次的狀態，請遵循詳細步驟[early](#how-is-batch-ingestion-monitored)。

### 批次失敗後會發生什麼事？ {#what-if-a-batch-fails}

當批次失敗時，處理程式會停止並傳回`Failure`狀態。 可在承載的`errors`區段中識別其失敗的原因。 錯誤範例如下所示：

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

錯誤更正後，批次就可以重新上傳。

## 批次支援

### 應如何刪除批次？

批次應該使用下面提供的任一方法來移除，而不是直接從[!DNL Catalog]中刪除：

1. 如果批次正在進行中，該批次應該中止。
2. 如果成功掌握批次，則應還原批次。

### 有哪些批次層級量度可供使用？

以下批次層級量度適用於處於作用中/成功狀態的批次：

| 量度 | 說明 |
| ------ | ----------- |
| inputByteSize | 要處理[!DNL Data Ingestion Services]的暫存位元組總數。 |
| inputRecordSize | [!DNL Data Ingestion Services]要處理的暫存資料列總數。 |
| outputByteSize | [!DNL Data Ingestion Services]輸出至[!DNL Data Lake]的位元組總數。 |
| outputRecordSize | 由[!DNL Data Ingestion Services]輸出至[!DNL Data Lake]的資料列總數。 |
| partitionCount | 寫入[!DNL Data Lake]的分割區總數。 |

### 為什麼某些批次沒有量度可用？

批次中無法使用量度有兩個原因：

1. 批次從未成功變成「作用中/成功」狀態。
2. 使用舊版促銷活動路徑（例如CSV擷取）促銷批次。

### 不同的狀態代碼代表什麼？

| 狀態代碼 | 說明 |
| ----------- | ----------- |
| 106 | 資料集檔案空白。 |
| 118 | CSV檔案包含一個空白標頭列。 |
| 200 | 該批次已接受處理，並將轉換為最終狀態，例如「作用中」或「失敗」。 提交之後，可以使用`GetBatch`端點監視批次。 |
| 400 | 錯誤請求。 如果批次中有遺漏或重疊的區塊，則會傳回。 |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
