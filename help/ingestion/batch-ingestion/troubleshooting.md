---
keywords: Experience Platform;home；熱門主題；收錄資料；疑難排解；常見問題；擷取；批次擷取；批次擷取；批次擷取；
solution: Experience Platform
title: 批次擷取疑難排解指南
topic-legacy: troubleshooting
description: 本檔案將協助解答有關Adobe Experience Platform批次資料擷取API的常見問題。
exl-id: 0a750d7e-a4ee-4a79-a697-b4b732478b2b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 1%

---

# 批次擷取疑難排解指南

本檔案將幫助解答有關Adobe Experience Platform[!DNL Batch Data Ingestion] API的常見問題。

## 批次API呼叫

### 從CompleteBatch API接收HTTP 200確定後，批是否立即處於活動狀態？

來自API的`200 OK`回應表示批已接受處理——直到它轉換為最終狀態（如「活動」或「失敗」），才會處於活動狀態。

### CompleteBatch API呼叫失敗後，是否可安全重試？

是——可以安全地重試API呼叫。 儘管失敗，但操作仍有可能實際成功並成功接受批。 但是，在API失敗時，客戶端應該有重試機制，事實上，建議重試。 如果操作實際成功，API將返回成功，即使在重試後亦然。

### 何時應使用大型檔案上傳API?

使用大型檔案上傳API的建議檔案大小為256 MB或更大。 有關如何使用大型檔案上傳API的詳細資訊，請參閱[這裡](./api-overview.md#ingest-large-parquet-files)。

### 為什麼大型檔案完整API呼叫失敗？

如果發現大型檔案的區塊重疊或遺失，伺服器會以HTTP 400錯誤要求回應。 之所以會發生這種情況，是因為上傳重疊的區塊是可能的，因為範圍驗證是在檔案完成時，當檔案區塊連結在一起時完成的。

## 擷取支援

### 支援哪些收錄格式？

目前支援Parce和JSON。 舊版支援CSV —— 雖然資料將提升為主要檢查並進行初步檢查，但不支援轉換、分割或列驗證等現代功能。

### 應在何處指定批輸入格式？

輸入格式應在裝載的批次建立時指定。 如需如何指定批次輸入格式的範例，請參閱以下：

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
    }'
```

### 為什麼上傳的資料不會出現在資料集中？

為了讓資料顯示在資料集中，批次必須標示為完成。 您要收錄的所有檔案都必須先上傳，才能將批次標示為完成。 以下是將批標籤為完成的示例：

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### 多行JSON如何收錄？

若要收錄多行JSON,`isMultiLineJson`標幟必須在建立批次時設定。 以下是此範例：

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json",
                "isMultiLineJson": true
           }
      }'
```

### JSON行（單行JSON）和多行JSON之間有何差異？

對於JSON行，每行有一個JSON物件。 例如：

```json
{"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}}
{"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}}
{"string":"string3","int":3,"array":[3,6,9],"dict": {"key": "value3", "extra_key": "extra_value3"}}
```

對於多行JSON，一個物件可佔據多行，而所有物件都封裝在JSON陣列中。 例如：

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

依預設，[!DNL Batch Data Ingestion]使用單行JSON。

### 是否支援CSV擷取？

CSV擷取僅支援平面結構描述。 目前不支援以CSV格式擷取階層式資料。

若要取得所有資料擷取功能，必須使用JSON或Parke格式。

### 對資料執行哪些類型的驗證？

對資料執行的驗證分為三個層級：

- 模式——批次擷取可確保所擷取資料的模式符合資料集的模式。
- 資料類型——批次擷取可確保擷取的每個欄位類型符合資料集架構中定義的類型。
- 約束——批次擷取可確保架構定義中正確定義約束，例如「必要」、「列舉」和「格式」。

### 如何更換已收錄的批？

已收錄的批次可使用「批次重播」功能來取代。 有關批次重放的詳細資訊，請參閱[此處](./api-overview.md#replay-a-batch)。

### 如何監控批次擷取？

在向批促銷發出批信號後，可以使用以下請求監控批提取進度：

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

透過此請求，您會收到類似下列的回應：

```http
200 OK
```

```json
{
    "{BATCH_ID}":{
        "imsOrg":"{IMS_ORG}",
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

批可以在其生命週期中經歷以下狀態：

| 狀態 | 寫入主版的資料 | 說明 |
| ------ | ---------------------- | ----------- |
| 已放棄 |  | 客戶端未能在預期的時間範圍內完成批處理。 |
| 已中止 |  | 客戶端已通過[!DNL Batch Data Ingestion] API明確調用指定批的中止操作。 一旦批處於「已載入」狀態，便無法中止該批。 |
| 作用中／成功 | x | 批已成功從階段升級到主批，現在可用於下游衝減。 **注意： 「** 作用中」和「成功」可互換使用。 |
| 已封存 |  | 批已存檔到冷儲存中。 |
| 失敗／失敗 |  | 由錯誤配置和／或錯誤資料引起的終端狀態。 系統會記錄可操作的錯誤以及批次，讓客戶能夠更正並重新提交資料。 **注意：「** 失敗」(Failed)和「失敗」(Failure)可互換使用。 |
| 非活動 | x | 批已成功升級，但已還原或過期。 批將不再可用於下游衝減，但基礎資料將保留在「主」中，直到保留、存檔或以其他方式刪除。 |
| 正在載入 |  | 客戶端當前正在編寫批的資料。 此時，批處於&#x200B;**不**&#x200B;狀態，可供升級。 |
| 已載入 |  | 客戶端已完成編寫批處理資料。 批已準備好升級。 |
| 保留 |  | 資料已從Master中取出，並在Adobe資料湖中的指定存檔中。 |
| 預備 |  | 用戶端已成功發出批次促銷的信號，且資料正在儲存以供下游消費。 |
| 重試 |  | 客戶端已發出批次升級的信號，但由於錯誤，批次正在由批次監控服務重試。 此狀態可用來告知用戶端在擷取資料時可能會有延遲。 |
| 停止 |  | 客戶端已發出批次升級的信號，但在批次監控服務`n`重試後，批次升級已停止。 |

### 「階移」對批次有何意義？

當批處於「轉移」中時，這表示已成功發出批的促銷信號，並且正在將資料轉移到下游以供衝減。

### 當批處理為「重試」時，它意味著什麼？

當批處於「重試」狀態時，這表示該批的資料提取由於間歇性問題而暫時停止。 發生這種情況時，不需要客戶干預。

### 當批處理為「停止」時，它意味著什麼？

當批處於「停止」狀態時，表示[!DNL Data Ingestion Services]在接收批時遇到困難，且所有重試都已用完。

### 如果批仍然是「正在載入」，這意味著什麼？

當批次處於「載入」中時，表示尚未呼叫CompleteBatch API來提升批次。

### 有沒有方法可以知道批是否已成功攝取？

批狀態為「活動」後，批就已成功吸收。 要瞭解批的狀態，請遵循[erier](#how-is-batch-ingestion-monitored)中詳細說明的步驟。

### 批次失敗後會發生什麼？

當批失敗時，可以在裝載的`errors`部分中確定其失敗的原因。 錯誤範例如下：

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

更正錯誤後，即可重新上傳批。

## 批次支援

### 如何刪除批？

不應直接從[!DNL Catalog]刪除，應使用以下任一方法刪除批：

1. 如果批正在進行中，則應中止該批。
2. 如果批已成功掌握，應還原批。

### 哪些批次層級度量可用？

下列批次層級度量適用於「作用中／成功」狀態的批次：

| 量度 | 說明 |
| ------ | ----------- |
| inputByteSize | 要處理的[!DNL Data Ingestion Services]分段的位元組總數。 |
| inputRecordSize | [!DNL Data Ingestion Services]要處理的分段行總數。 |
| outputByteSize | [!DNL Data Ingestion Services]輸出到[!DNL Data Lake]的位元組總數。 |
| outputRecordSize | 由[!DNL Data Ingestion Services]輸出到[!DNL Data Lake]的總行數。 |
| partitionCount | 寫入[!DNL Data Lake]的分區總數。 |

### 為什麼某些批次無法使用量度？

量度可能無法用於您的批次有兩個原因：

1. 批次從未成功進入「作用中／成功」狀態。
2. 批已使用舊有的促銷路徑（例如CSV擷取）進行促銷。

### 不同的狀態碼代表什麼意思？

| 狀態代碼 | 說明 |
| ----------- | ----------- |
| 106 | 資料集檔案為空。 |
| 118 | CSV檔案包含空的標題列。 |
| 200 | 批已接受處理，並將轉換到最終狀態，如「活動」或「失敗」。 提交後，可使用`GetBatch`端點監視批。 |
| 400 | Bad Request. 如果批中缺少或重疊的塊，則返回。 |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
