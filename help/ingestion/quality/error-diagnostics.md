---
keywords: Experience Platform；主題；熱門主題；批處理；批處理；部分提取；部分提取；檢索錯誤；檢索錯誤；部分批處理；部分批處理；提取；部分；提取；錯誤診斷；檢索錯誤診斷；獲取錯誤；獲取錯誤；檢索錯誤；
solution: Experience Platform
title: 檢索資料提取錯誤診斷
topic-legacy: overview
description: 本文檔提供有關監控批處理提取、管理部分批處理提取錯誤的資訊，以及有關部分批處理提取類型的參考。
exl-id: b885fb00-b66d-453b-80b7-8821117c2041
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 2%

---

# 檢索資料攝取錯誤診斷

Adobe Experience Platform提供兩種上傳和收錄資料的方法。 您可以使用批次擷取功能(可讓您使用各種檔案類型（例如CSV）插入資料)或串流擷取功能（可讓您使用串流端點將資料即時插入[!DNL Platform]）。

本文檔提供有關監控批處理提取、管理部分批處理提取錯誤的資訊，以及有關部分批處理提取類型的參考。

## 快速入門

本指南需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
- [[!DNL Adobe Experience Platform Data Ingestion]](../home.md):可傳送資料的方法 [!DNL Experience Platform]。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Schema Registry]的資源）都與特定虛擬沙盒隔離。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙盒的詳細資訊，請參閱[沙盒概述檔案](../../sandboxes/home.md)。

## 下載錯誤診斷{#download-diagnostics}

Adobe Experience Platform允許用戶下載輸入檔案的錯誤診斷程式。 診斷程式將在[!DNL Platform]內保留30天。

### 列出輸入檔案{#list-files}

下列請求會擷取已完成批次中提供之所有檔案的清單。

**API格式**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 您正在查找的批的ID。 |

**要求**

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

### 檢索輸入檔案診斷{#retrieve-diagnostics}

檢索到所有不同輸入檔案的清單後，可以使用以下請求檢索單個檔案的診斷。

**API格式**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files/{FILE}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 您正在查找的批的ID。 |
| `{FILE}` | 您正在訪問的檔案的名稱。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含`path`物件的JSON物件，其中詳列診斷程式的儲存位置。 回應會傳回[JSON Lines](https://jsonlines.org/)格式的`path`物件。

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## 擷取批次擷取錯誤{#retrieve-errors}

如果批包含失敗，則應檢索有關這些失敗的錯誤資訊，以便重新收錄資料。

### 檢查狀態{#check-status}

要檢查收錄批的狀態，您必須在GET請求的路徑中提供批的ID。

**API格式**

```http
GET /catalog/batches/{BATCH_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 要檢查狀態的批的`id`值。 |

**要求**

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
| `metrics.failedRecordCount` | 由於剖析、轉換或驗證而無法處理的列數。 此值可從`outputRecordCount`中減去`inputRecordCount`來衍生。 無論`errorDiagnostics`是否啟用，都會在所有批上生成此值。 |

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
| `metrics.failedRecordCount` | 由於剖析、轉換或驗證而無法處理的列數。 此值可從`outputRecordCount`中減去`inputRecordCount`來衍生。 無論`errorDiagnostics`是否啟用，都會在所有批上生成此值。 |
| `errors.recordCount` | 指定錯誤代碼失敗的行數。 如果`errorDiagnostics`已啟用，則此值僅為&#x200B;****。 |

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
>```

## 下一步 {#next-steps}

本教學課程說明如何監控部分批次擷取錯誤。 有關批次擷取的詳細資訊，請閱讀[批次擷取開發人員指南](../batch-ingestion/api-overview.md)。

## 附錄 {#appendix}

本節提供有關擷取錯誤類型的補充資訊。

### 部分批處理提取錯誤類型{#partial-ingestion-types}

部分批次擷取在擷取資料時有三種不同的錯誤類型：

- [無法讀取的檔案](#unreadable)
- [無效的結構或標題](#schemas-headers)
- [不可分的行](#unparsable)

### 無法讀取的檔案{#unreadable}

如果接受的批具有無法讀取的檔案，則批的錯誤將附加到批本身。 有關檢索失敗批的詳細資訊，請參閱[檢索失敗批指南](../quality/retrieve-failed-batches.md)。

### 無效的結構或標題{#schemas-headers}

如果所收錄的批具有無效的方案或無效標題，則批的錯誤將附加在批本身上。 有關檢索失敗批的詳細資訊，請參閱[檢索失敗批指南](../quality/retrieve-failed-batches.md)。

### 不可分的行{#unparsable}

如果您收集的批具有不可分解的行，則可以使用以下請求查看包含錯誤的檔案清單。

**API格式**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 從中檢索錯誤資訊的批的`id`值。 |

**要求**

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

然後，可以使用[診斷檢索端點](#retrieve-diagnostics)檢索有關錯誤的詳細資訊。

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
