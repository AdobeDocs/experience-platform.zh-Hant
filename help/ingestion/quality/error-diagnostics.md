---
keywords: Experience Platform；首頁；熱門主題；批次內嵌；批次內嵌；部分內嵌；擷取錯誤；擷取錯誤；部分批次內嵌；部分批次內嵌；部分內嵌；部分內嵌；擷取；錯誤診斷；擷取錯誤診斷；取得錯誤；擷取錯誤；
solution: Experience Platform
title: 檢索資料獲取錯誤診斷
description: 本文檔提供了有關監控批次內嵌、管理部分批次內嵌錯誤的資訊，以及部分批次內嵌類型的參考。
exl-id: b885fb00-b66d-453b-80b7-8821117c2041
source-git-commit: edd285c3d0638b606876c015dffb18309887dfb5
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 2%

---

# 擷取資料擷取錯誤診斷

Adobe Experience Platform提供兩種上傳和擷取資料的方法。 您可以使用批次內嵌(可讓您使用各種檔案類型（例如CSV）插入資料)，或使用串流內嵌(可讓您將資料插入 [!DNL Platform] 即時使用串流端點。

本文檔提供了有關監控批次內嵌、管理部分批次內嵌錯誤的資訊，以及部分批次內嵌類型的參考。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
- [[!DNL Adobe Experience Platform Data Ingestion]](../home.md):資料可透過哪些方法傳送至 [!DNL Experience Platform].

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

若要對 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform]，包括 [!DNL Schema Registry]，會與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊，請參閱 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

## 下載錯誤診斷 {#download-diagnostics}

Adobe Experience Platform可讓使用者下載輸入檔案的錯誤診斷程式。 診斷程式將保留在 [!DNL Platform] 最多30天。

### 清單輸入檔案 {#list-files}

下列請求會擷取已完成批次中提供的所有檔案清單。

**API格式**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 要查找的批的ID。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回JSON物件，詳細說明診斷程式的儲存位置。

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
| `{BATCH_ID}` | 要查找的批的ID。 |
| `{FILE}` | 您要存取的檔案名稱。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回包含 `path` 詳細說明診斷保存位置的對象。 回應會傳回 `path` 對象 [JSON行](https://jsonlines.readthedocs.io/en/latest/) 格式。

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## 擷取批次內嵌錯誤 {#retrieve-errors}

如果批包含故障，則應檢索有關這些故障的錯誤資訊，以便可以重新內嵌資料。

### 檢查狀態 {#check-status}

若要檢查擷取批次的狀態，您必須在GET請求的路徑中提供批次ID。 若要進一步了解如何使用此API呼叫，請參閱 [目錄端點指南](../../catalog/api/list-objects.md).

**API格式**

```http
GET /catalog/batches/{BATCH_ID}
GET /catalog/batches/{BATCH_ID}?{FILTER}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 此 `id` 要檢查狀態的批的值。 |
| `{FILTER}` | 用於篩選回應中傳回結果的查詢參數。 多個參數以&amp;符號分隔(`&`)。 欲知更多資訊，請閱讀 [篩選目錄資料](../../catalog/api/filter-data.md). |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/af838510-2233-11ea-acf0-f3edfcded2d2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**無錯誤的回應**

成功的回應會傳回，其中包含批次狀態的詳細資訊。

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
| `metrics.failedRecordCount` | 由於解析、轉換或驗證而無法處理的列數。 此值可借由減去 `inputRecordCount` 從 `outputRecordCount`. 此值是在所有批上生成的，無論 `errorDiagnostics` 啟用。 |

**有錯誤的回應**

如果批次有一或多個錯誤並啟用了錯誤診斷，則回應會傳回關於錯誤的更多資訊，包括裝載本身內的錯誤以及可下載的錯誤檔案。 請注意，包含錯誤的批次狀態可能仍具有成功狀態。

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
| `metrics.failedRecordCount` | 由於解析、轉換或驗證而無法處理的列數。 此值可借由減去 `inputRecordCount` 從 `outputRecordCount`. 此值是在所有批上生成的，無論 `errorDiagnostics` 啟用。 |
| `errors.recordCount` | 指定的錯誤代碼失敗的行數。 此值為 **僅限** 產生 `errorDiagnostics` 啟用。 |

>[!NOTE]
>
>如果錯誤診斷不可用，則會改為顯示以下錯誤消息：
>
```json
>{
>       "errors": [{
>               "code": "INGEST-1211-400",
>               "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>       }]
>}
>```

## 後續步驟 {#next-steps}

本教學課程說明如何監控部分批次擷取錯誤。 如需批次內嵌的詳細資訊，請參閱 [批次匯入開發人員指南](../batch-ingestion/api-overview.md).

## 附錄 {#appendix}

本節提供擷取錯誤類型的補充資訊。

### 部分批次內嵌錯誤類型 {#partial-ingestion-types}

擷取資料時，部分批次內嵌有三種不同的錯誤類型：

- [不可讀檔案](#unreadable)
- [結構或標題無效](#schemas-headers)
- [不可剖析的列](#unparsable)

### 不可讀檔案 {#unreadable}

如果所擷取的批次具有無法讀取的檔案，則該批次的錯誤會附加在該批次本身上。 有關檢索失敗批處理的更多資訊，請參見 [檢索失敗的批處理指南](../quality/retrieve-failed-batches.md).

### 結構或標題無效 {#schemas-headers}

如果所擷取的批次具有無效的結構或標題無效，則批次的錯誤會附加在批次本身。 有關檢索失敗批處理的更多資訊，請參見 [檢索失敗的批處理指南](../quality/retrieve-failed-batches.md).

### 不可剖析的列 {#unparsable}

如果您擷取的批次有無法剖析的列，您可以使用下列請求來檢視包含錯誤的檔案清單。

**API格式**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 此 `id` 要從中檢索錯誤資訊的批的值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回有錯誤的檔案的清單。

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

然後，您可以使用 [診斷檢索終端](#retrieve-diagnostics).

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
