---
keywords: Experience Platform；主題；熱門主題；攝取的資料；故障排除；常見問題；攝取；批量攝取；批量攝取；
solution: Experience Platform
title: 批量攝取故障排除指南
description: 本文檔將幫助回答有關Adobe Experience Platform批資料接收API的常見問題。
exl-id: 0a750d7e-a4ee-4a79-a697-b4b732478b2b
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 1%

---

# 批量攝取故障排除指南

本文檔將幫助回答有關Adobe Experience Platform的常見問題 [!DNL Batch Data Ingestion] API。

## 批處理API調用

### 在從CompleteBatch API接收HTTP 200 OK後，批是否立即處於活動狀態？

的 `200 OK` 來自API的響應表示批已被接受處理 — 在它轉變到其最終狀態（如「活動」或「失敗」）之前，它不處於活動狀態。

### 在CompleteBatch API調用失敗後重試是否安全？

是 — 可以安全地重試API調用。 儘管失敗，但操作可能實際成功，並且批被成功接受。 但是，在API失敗時，客戶端應具有重試機制，並且實際上鼓勵客戶端重試。 如果操作實際成功，則API將返回成功，即使在重試後也是如此。

### 何時應使用大檔案上載API?

使用「大檔案上傳API」的建議檔案大小為256 MB或更大。 有關如何使用大檔案上載API的詳細資訊 [這裡](./api-overview.md#ingest-large-parquet-files)。

### 為什麼大型檔案完成API調用失敗？

如果發現大檔案的塊重疊或丟失，伺服器會使用HTTP 400錯誤請求進行響應。 這可能是因為上載重疊的區塊是可能的，因為在檔案完成時，當檔案區塊拼合在一起時，會完成範圍驗證。

## 攝取支援

### 支援的接收格式是什麼？

目前，支援Parke和JSON。 CSV在舊版基礎上受支援 — 雖然資料將提升為主資料並進行初步檢查，但不支援轉換、分區或行驗證等現代功能。

### 應在何處指定批輸入格式？

輸入格式應在負載內的批處理建立時指定。 有關如何指定批處理輸入格式的示例如下所示：

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

### 為什麼上載的資料未出現在資料集中？

要使資料顯示在資料集中，必須將批標籤為完成。 必須先上載要接收的所有檔案，然後才能將批標籤為完成。 以下是將批標籤為完成的示例：

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### 多行JSON如何接收？

要接收多行JSON, `isMultiLineJson` 需要在建立批時設定標誌。 下面可以看到此示例：

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

### JSON行（單行JSON）和多行JSON之間有何區別？

對於JSON行，每行有一個JSON對象。 例如：

```json
{"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}}
{"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}}
{"string":"string3","int":3,"array":[3,6,9],"dict": {"key": "value3", "extra_key": "extra_value3"}}
```

對於多行JSON，一個對象可以佔用多行，而所有對象都包裝在JSON陣列中。 例如：

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

預設情況下， [!DNL Batch Data Ingestion] 使用單行JSON。

### 是否支援CSV攝取？

僅平面架構支援CSV接收。 當前，不支援在CSV中接收分層資料。

要獲取所有資料接收功能，需要使用JSON或Parke格式。

### 對資料執行了哪些類型的驗證？

對資料執行了三個級別的驗證：

- 模式 — 批處理接收確保所接收資料的模式與資料集的模式匹配。
- 資料類型 — 批處理接收確保所接收的每個欄位的類型與資料集架構中定義的類型相匹配。
- 約束 — 批處理接收確保在架構定義中正確定義約束，如「必需」、「枚舉」和「格式」。

### 如何替換已攝取的批？

可以使用「批重放」功能替換已攝取的批。 有關批重放的詳細資訊 [這裡](./api-overview.md#replay-a-batch)。

### 如何監控批量攝取？

一旦已發出批處理提升的信號，便可通過以下請求監視批接收進度：

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

使用此請求，您將得到類似以下內容的響應：

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

## 批處理狀態

### 可能的批處理狀態是什麼？

批可以在其生命週期中通過以下狀態：

| 狀態 | 寫入主資料 | 說明 |
| ------ | ---------------------- | ----------- |
| 已放棄 |  | 客戶端未能在預期時間範圍內完成批處理。 |
| 中止 |  | 客戶端已通過 [!DNL Batch Data Ingestion] API，指定批的中止操作。 一旦批處於「已載入」狀態，則無法中止該批。 |
| 活動/成功 | x | 批已成功從階段提升到主階段，現在可用於下游衝減。 **注：** 「活動」和「成功」可互換使用。 |
| 存檔 |  | 批已存檔到冷儲存中。 |
| 失敗/失敗 |  | 由錯誤配置和/或錯誤資料導致的終端狀態。 記錄一個可操作的錯誤以及批，以使客戶端能夠更正和重新提交資料。 **注：** 「失敗」和「失敗」可互換使用。 |
| 非活動 | x | 已成功提升批，但已還原或已過期。 批將不再可用於下游衝減，但基礎資料將保留在主資料中，直到其保留、存檔或刪除。 |
| 正在載入 |  | 客戶端當前正在為批處理寫入資料。 批為 **不** 準備升職，此時。 |
| 已載入 |  | 客戶端已完成寫入批的資料。 批已準備好進行升級。 |
| 保留 |  | 資料已從Master中取出，並存放在Adobe資料湖中的指定存檔中。 |
| 預備 |  | 客戶端已成功發出升級批的信號，資料正在下游暫存以用於消耗。 |
| 正在重試 |  | 客戶端已發出批處理升級的信號，但由於錯誤，批處理正在由批處理監視服務重試。 此狀態可用於告訴客戶端在接收資料時可能存在延遲。 |
| 停止 |  | 客戶端已發出批號要升級，但在 `n` 批監視服務重試，批升級已停止。 |

### 「轉移」對批意味著什麼？

當批處於「轉移」時，這意味著已成功發出批的升級信號，並且正在將資料轉移到下游以供衝減。

### 當批處理為「重試」時，它意味著什麼？

當批處於「重試」狀態時，這意味著由於間歇性問題，批的資料接收已暫時停止。 當這種情況發生時，不需要客戶干預。

### 當批處理為「停止」時，這意味著什麼？

當批處於「停止」時，表示 [!DNL Data Ingestion Services] 正在嘗試批處理時遇到困難，並且已用盡所有重試次數。

### 如果批仍處於「正在載入」狀態，則該說明是什麼？

當批處於「載入」中時，這意味著尚未調用CompleteBatch API來提升批。

### 是否有方法知道批次是否已成功攝取？

一旦批狀態為「活動」，則已成功接收批。 要瞭解批的狀態，請執行詳細步驟 [早](#how-is-batch-ingestion-monitored)。

### 批處理失敗後會發生什麼？

當批失敗時，可以在 `errors` 的下界。 錯誤示例如下：

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

更正錯誤後，可以重新上載批。

## 批支援

### 如何刪除批？

而不是直接從 [!DNL Catalog]，應使用以下任一方法刪除批：

1. 如果批處理中，則應中止該批處理。
2. 如果成功掌握了批，則應還原批。

### 可用的批級度量是什麼？

以下批級度量可用於處於「活動/成功」狀態的批：

| 量度 | 說明 |
| ------ | ----------- |
| inputByteSize | 暫存的位元組總數 [!DNL Data Ingestion Services] 處理。 |
| inputRecordSize | 暫存的行總數 [!DNL Data Ingestion Services] 處理。 |
| 輸出位元組大小 | 輸出的位元組總數 [!DNL Data Ingestion Services] 至 [!DNL Data Lake]。 |
| outputRecordSize | 由 [!DNL Data Ingestion Services] 至 [!DNL Data Lake]。 |
| 分區計數 | 寫入的分區總數 [!DNL Data Lake]。 |

### 為什麼某些批中沒有度量？

批中可能沒有度量有兩個原因：

1. 該批從未成功使其進入「活動/成功」狀態。
2. 批已使用舊式升級路徑（如CSV接收）進行升級。

### 不同的狀態代碼意味著什麼？

| 狀態代碼 | 說明 |
| ----------- | ----------- |
| 106 | 資料集檔案為空。 |
| 118 | CSV檔案包含空標題行。 |
| 200 | 批已被接受以進行處理，並將轉換為最終狀態，如「活動」或「失敗」。 提交後，可以使用 `GetBatch` 端點。 |
| 400 | Bad Request. 如果批處理中缺少塊或重疊塊，則返回。 |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
