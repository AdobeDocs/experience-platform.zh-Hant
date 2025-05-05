---
keywords: Experience Platform；首頁；熱門主題；批次擷取；批次擷取；部分擷取；擷取錯誤；擷取錯誤；部分批次擷取；部分批次擷取；部分；擷取；擷取；錯誤診斷；擷取錯誤診斷；取得錯誤診斷；取得錯誤；取得錯誤；擷取錯誤；
solution: Experience Platform
title: 正在擷取資料擷取錯誤診斷
description: 本檔案提供有關監視批次擷取、管理部分批次擷取錯誤的資訊，以及部分批次擷取型別的參考。
exl-id: b885fb00-b66d-453b-80b7-8821117c2041
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 8%

---

# 正在擷取資料擷取錯誤診斷

Adobe Experience Platform提供兩種上傳和擷取資料的方法。 您可以使用批次擷取，這可讓您使用各種檔案型別（例如CSV）插入資料，或是使用串流擷取，可讓您使用串流端點即時將其資料插入[!DNL Experience Platform]。

本檔案提供有關監視批次擷取、管理部分批次擷取錯誤的資訊，以及部分批次擷取型別的參考。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
- [[!DNL Adobe Experience Platform Data Ingestion]](../home.md)：傳送資料給[!DNL Experience Platform]的方法。

### 讀取範例 API 呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集所需標頭的值

若要呼叫[!DNL Experience Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Schema Registry]的資源）都與特定的虛擬沙箱隔離。 對[!DNL Experience Platform] API的所有請求都需要標頭，以指定將在其中執行作業的沙箱名稱：

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Experience Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

## 正在下載錯誤診斷 {#download-diagnostics}

Adobe Experience Platform可讓使用者下載輸入檔案的錯誤診斷。 診斷將在[!DNL Experience Platform]內保留最多30天。

### 列出輸入檔案 {#list-files}

下列請求會擷取已完成批次中提供的所有檔案清單。

**API格式**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 您要查詢之批次的ID。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應將傳回JSON物件，詳細說明診斷的儲存位置。

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

### 擷取輸入檔案診斷 {#retrieve-diagnostics}

擷取所有不同輸入檔案的清單後，您可以使用以下請求來擷取個別檔案的診斷。

**API格式**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files/{FILE}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 您要查詢之批次的ID。 |
| `{FILE}` | 您正在存取的檔案名稱。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應將傳回包含`path`個物件的JSON物件，詳細說明診斷的儲存位置。 回應將傳回[JSON行](https://jsonlines.readthedocs.io/en/latest/)格式的`path`物件。

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## 擷取批次擷取錯誤 {#retrieve-errors}

如果批次包含失敗，您應該擷取有關這些失敗的錯誤資訊，以便您可以重新擷取資料。

### 檢查狀態 {#check-status}

若要檢查所擷取批次的狀態，您必須在GET請求的路徑中提供批次ID。 若要進一步瞭解如何使用此API呼叫，請參閱[目錄端點指南](../../catalog/api/list-objects.md)。

**API格式**

```http
GET /catalog/batches/{BATCH_ID}
GET /catalog/batches/{BATCH_ID}?{FILTER}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您要檢查其狀態之批次的`id`值。 |
| `{FILTER}` | 用來篩選回應中傳回結果的查詢引數。 多個引數以&amp;符號(`&`)分隔。 如需詳細資訊，請閱讀[篩選目錄資料](../../catalog/api/filter-data.md)的指南。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/af838510-2233-11ea-acf0-f3edfcded2d2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**沒有錯誤的回應**

成功回應會傳回批次狀態的詳細資訊。

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
        "imsOrg": "{ORG_ID}",
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
| `metrics.failedRecordCount` | 由於剖析、轉換或驗證而無法處理的列數。 此值可以透過從`outputRecordCount`中減去`inputRecordCount`而衍生。 此值會在所有批次上產生，無論是否啟用`errorDiagnostics`。 |

**回應發生錯誤**

如果批次發生一或多個錯誤，且已啟用錯誤診斷，回應會傳回錯誤的相關詳細資訊，包括有效負載本身以及可下載的錯誤檔案。 請注意，包含錯誤的批次狀態可能仍會具有「成功」狀態。

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
        "imsOrg": "{ORG_ID}",
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
| `metrics.failedRecordCount` | 由於剖析、轉換或驗證而無法處理的列數。 此值可以透過從`outputRecordCount`中減去`inputRecordCount`而衍生。 此值會在所有批次上產生，無論是否啟用`errorDiagnostics`。 |
| `errors.recordCount` | 指定的錯誤碼失敗的列數。 如果啟用`errorDiagnostics`，則此值只會&#x200B;**產生**。 |

>[!NOTE]
>
>如果無法使用錯誤診斷，則會改為顯示下列錯誤訊息：
>
>```json
>{
>       "errors": [{
>               "code": "INGEST-1211-400",
>               "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>       }]
>}
>```

## 後續步驟 {#next-steps}

本教學課程說明如何監控部分批次擷取錯誤。 如需批次擷取的詳細資訊，請參閱[批次擷取開發人員指南](../batch-ingestion/api-overview.md)。

## 附錄 {#appendix}

本節提供內嵌錯誤型別的相關補充資訊。

### 部分批次擷取錯誤型別 {#partial-ingestion-types}

擷取資料時，部分批次擷取有三種不同的錯誤型別：

- [無法讀取的檔案](#unreadable)
- [無效的結構描述或標題](#schemas-headers)
- [無法剖析的列](#unparsable)

### 無法讀取的檔案 {#unreadable}

如果擷取的批次有無法讀取的檔案，該批次的錯誤將附加到該批次本身。 在[擷取失敗的批次指南](../quality/retrieve-failed-batches.md)中可以找到更多有關擷取失敗的批次的資訊。

### 無效的結構描述或標題 {#schemas-headers}

如果擷取的批次具有無效的結構描述或無效的標頭，批次的錯誤將附加到批次本身。 在[擷取失敗的批次指南](../quality/retrieve-failed-batches.md)中可以找到更多有關擷取失敗的批次的資訊。

### 無法剖析的列 {#unparsable}

如果您擷取的批次有無法剖析的列，您可以使用以下請求來檢視包含錯誤的檔案清單。

**API格式**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 您正在擷取錯誤資訊之批次的`id`值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回含有錯誤的檔案清單。

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

然後，您可以使用[診斷擷取端點](#retrieve-diagnostics)來擷取有關錯誤的詳細資訊。

擷取錯誤檔案的範例回應如下所示：

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
