---
keywords: Experience Platform;home;popular topics;batch ingestion;Batch ingestion;partial ingestion;Partial ingestion;Retrieve error;retrieve error;Partial batch ingestion;partial batch ingestion;partial;ingestion;Ingestion;error diagnostics;retrieve error diagnostics;get error diagnostics;get error;get errors;retrieve errors;
solution: Experience Platform
title: Adobe Experience Platform部分批次擷取概觀
topic: overview
translation-type: tm+mt
source-git-commit: a345efca3c38c3077c89b47271f54b924d58db45
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 2%

---


# 檢索錯誤診斷

Adobe Experience Platform提供兩種上傳和接收資料的方法。 您可以使用批次擷取功能(可讓您使用各種檔案類型（例如CSV）插入資料)或串流擷取功能（可讓您即時將資料插入使用串流端點）, [!DNL Platform] 以進行資料擷取。

本文檔提供有關監控批處理提取、管理部分批處理提取錯誤的資訊，以及有關部分批處理提取類型的參考。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

- [[!DNL體驗資料模型(XDM)系統]](../../xdm/home.md):組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
- [[!DNL Adobe Experience Platform資料擷取]](../home.md):可傳送資料的方法 [!DNL Experience Platform]。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

中的所有資 [!DNL Experience Platform]源（包括屬於的資源）都 [!DNL Schema Registry]被隔離到特定的虛擬沙盒中。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙盒的詳細資訊 [!DNL Platform]，請參閱沙 [盒概述檔案](../../sandboxes/home.md)。

## 下載錯誤診斷 {#download-diagnostics}

Adobe Experience Platform可讓使用者下載輸入檔案的錯誤診斷程式。 診斷程式將在30 [!DNL Platform] 天內保留。

### 列出輸入檔案 {#list-files}

下列請求會擷取已完成批次中提供之所有檔案的清單。

**API格式**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 您正在查找的批的ID。 |

**請求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回JSON物件，其中詳列診斷程式的儲存位置。

```json
{
    "_page": {
        "count": 1,
        "limit": 100
    },
    "data": [
        {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json"
                }
            },
            "length": "1337",
            "name": "fileMetaData1.json"
        },
                {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2}/meta?path=input_files/fileMetaData2.json"
                }
            },
            "length": "1042",
            "name": "fileMetaData2.json"
        }
    ]
}
```

### 檢索輸入檔案診斷 {#retrieve-diagnostics}

檢索到所有不同輸入檔案的清單後，可以使用以下請求檢索單個檔案的診斷。

**API格式**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files/{FILE}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 您正在查找的批的ID。 |
| `{FILE}` | 您正在訪問的檔案的名稱。 |

**請求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含物件的JSON物 `path` 件，其中詳列診斷程式的儲存位置。 回應會傳回 `path` JSON [行格](https://jsonlines.org/) 式的物件。

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## 擷取批次擷取錯誤 {#retrieve-errors}

如果批包含失敗，則應檢索有關這些失敗的錯誤資訊，以便重新收錄資料。

### 檢查狀態 {#check-status}

要檢查收錄批的狀態，您必須在GET請求的路徑中提供批的ID。

**API格式**

```http
GET /catalog/batches/{BATCH_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要 `id` 檢查狀態的批的值。 |

**請求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/af838510-2233-11ea-acf0-f3edfcded2d2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應無錯誤**

成功的響應返回，並返回有關批狀態的詳細資訊。

```json
{
    "af838510-2233-11ea-acf0-f3edfcded2d2": {
        "status": "success",
        "tags": {
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "externalId": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{IMS_ORG}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 497,
            "failedRecordCount": 0
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5"
    }    
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `metrics.failedRecordCount` | 由於剖析、轉換或驗證而無法處理的列數。 此值可從中減去 `inputRecordCount` 來衍生 `outputRecordCount`。 無論啟用與否，此值都會在所有批次 `errorDiagnostics` 上產生。 |

**回應有錯誤**

如果批次有一或多個錯誤並啟用錯誤診斷，則回應會傳回更多有關錯誤的資訊，包括裝載本身以及可下載的錯誤檔案。 請注意，包含錯誤的批的狀態可能仍具有成功狀態。

```json
{
    "01E8043CY305K2MTV5ANH9G1GC": {
        "status": "success",
        "tags": {
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "01E8043CY305K2MTV5ANH9G1GC",
        "externalId": "01E8043CY305K2MTV5ANH9G1GC",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{IMS_ORG}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 514,
            "failedRecordCount": 5
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5",
        "errors": [
           {
             "code": "INGEST-1212-400",
             "description": "Encountered 5 errors in the data. Successfully ingested 514 rows. Please review the associated diagnostic files for more details."
           },
           {
             "code": "INGEST-1401-400",
             "description": "The row has corrupted data and cannot be read or parsed. Fix the corrupted data and try again.",
             "recordCount": 2
           },
           {
             "code": "INGEST-1555-400",
             "description": "A required field is either missing or has a value of null. Add the required field to the input row and try again.",
             "recordCount": 3
           }
        ]
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `metrics.failedRecordCount` | 由於剖析、轉換或驗證而無法處理的列數。 此值可從中減去 `inputRecordCount` 來衍生 `outputRecordCount`。 無論啟用與否，此值都會在所有批次 `errorDiagnostics` 上產生。 |
| `errors.recordCount` | 指定錯誤代碼失敗的行數。 此值僅 **在啟用**`errorDiagnostics` 時產生。 |

>[!NOTE]
>
>如果錯誤診斷不可用，則會出現以下錯誤消息：
>
```json
>{
>       "errors": [{
>               "code": "INGEST-1211-400",
>               "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>       }]
>}
> ```

## 部分批次擷取錯誤類型 {#appendix}

部分批次擷取在擷取資料時有三種不同的錯誤類型：

- [無法讀取的檔案](#unreadable)
- [無效的結構或標題](#schemas-headers)
- [不可分的行](#unparsable)

### 無法讀取的檔案 {#unreadable}

如果接受的批具有無法讀取的檔案，則批的錯誤將附加到批本身。 有關檢索失敗批的詳細資訊，請參閱檢索失敗 [批的指南](../quality/retrieve-failed-batches.md)。

### 無效的結構或標題 {#schemas-headers}

如果所收錄的批具有無效的方案或無效標題，則批的錯誤將附加在批本身上。 有關檢索失敗批的詳細資訊，請參閱檢索失敗 [批的指南](../quality/retrieve-failed-batches.md)。

### 不可分的行 {#unparsable}

如果您收集的批具有不可分解的行，則可以使用以下請求查看包含錯誤的檔案清單。

**API格式**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 從 `id` 中檢索錯誤資訊的批的值。 |

**請求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回有錯誤的檔案清單。

```json
{
    "data": [
        {
            "name": "conversion_errors_0.json",
            "length": "1162",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors%2Fconversion_errors_0.json"
                }
            }
        },
        {
            "name": "parsing_errors_0.json",
            "length": "153",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors%2Fparsing_errors_0.json"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

然後，可以使用診斷檢索端點檢索有關錯誤 [的詳細資訊](#retrieve-diagnostics)。

檢索錯誤檔案的示例響應如下：

```json
{
    "_corrupt_record": "{missingQuotes: 'v1'}",
    "_errors": [{
        "code": "1401",
        "message": "Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "parsing_errors_0.json"
}
```

## 下一步 {#next-steps}

本教學課程說明如何監控部分批次擷取錯誤。 如需批次擷取的詳細資訊，請閱讀批次擷取開 [發人員指南](../batch-ingestion/api-overview.md)。