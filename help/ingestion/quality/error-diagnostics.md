---
keywords: Experience Platform；主題；熱門主題；批處理接收；批處理接收；部分接收；檢索錯誤；部分接收；部分接收；部分接收；部分接收；錯誤診斷；檢索錯誤診斷；獲取錯誤；獲取錯誤；檢索錯誤；
solution: Experience Platform
title: 檢索資料接收錯誤診斷
description: 本文檔提供了有關監視批處理接收、管理部分批處理接收錯誤的資訊，以及對部分批處理接收類型的參考。
exl-id: b885fb00-b66d-453b-80b7-8821117c2041
source-git-commit: edd285c3d0638b606876c015dffb18309887dfb5
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 2%

---

# 正在檢索資料攝取錯誤診斷

Adobe Experience Platform提供了兩種資料上傳和接收方法。 您可以使用批處理接收(允許您使用各種檔案類型（如CSV）插入資料)，也可以使用流式處理接收(允許您將資料插入到 [!DNL Platform] 即時使用流端點。

本文檔提供了有關監視批處理接收、管理部分批處理接收錯誤的資訊，以及對部分批處理接收類型的參考。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
- [[!DNL Adobe Experience Platform Data Ingestion]](../home.md):資料可通過以下方法發送 [!DNL Experience Platform]。

### 讀取示例API調用

本教程提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

### 收集所需標題的值

為了呼叫 [!DNL Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform]包括那些 [!DNL Schema Registry]，與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有關中的沙箱的詳細資訊 [!DNL Platform]，請參見 [沙盒概述文檔](../../sandboxes/home.md)。

## 下載錯誤診斷 {#download-diagnostics}

Adobe Experience Platform允許用戶下載輸入檔案的錯誤診斷。 診斷程式將保留在 [!DNL Platform] 最多30天。

### 列出輸入檔案 {#list-files}

以下請求檢索最終批中提供的所有檔案的清單。

**API格式**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 您要查找的批的ID。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應將返回JSON對象，詳細說明診斷的保存位置。

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

檢索到所有不同輸入檔案的清單後，可以使用以下請求檢索單個檔案的診斷資訊。

**API格式**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files/{FILE}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 您要查找的批的ID。 |
| `{FILE}` | 您正在訪問的檔案的名稱。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功響應將返回包含 `path` 詳細列出診斷保存位置的對象。 響應將返回 `path` 對象 [JSON行](https://jsonlines.readthedocs.io/en/latest/) 的子菜單。

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## 檢索批處理接收錯誤 {#retrieve-errors}

如果批包含故障，則應檢索有關這些故障的錯誤資訊，以便可以重新攝取資料。

### 檢查狀態 {#check-status}

要檢查所攝取批的狀態，必須在GET請求路徑中提供批的ID。 要瞭解有關使用此API調用的更多資訊，請閱讀 [目錄終結點指南](../../catalog/api/list-objects.md)。

**API格式**

```http
GET /catalog/batches/{BATCH_ID}
GET /catalog/batches/{BATCH_ID}?{FILTER}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 的 `id` 要檢查狀態的批的值。 |
| `{FILTER}` | 用於篩選在響應中返回的結果的查詢參數。 多個參數用和符號分隔(`&`)。 有關詳細資訊，請閱讀上的指南 [篩選目錄資料](../../catalog/api/filter-data.md)。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/af838510-2233-11ea-acf0-f3edfcded2d2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**無錯誤響應**

成功的響應將返回，並提供有關批狀態的詳細資訊。

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
| `metrics.failedRecordCount` | 由於分析、轉換或驗證而無法處理的行數。 通過減去 `inputRecordCount` 從 `outputRecordCount`。 此值將在所有批上生成，而不管 `errorDiagnostics` 的子菜單。 |

**有錯誤的響應**

如果批處理有一個或多個錯誤並且啟用了錯誤診斷，則響應將返回有關這些錯誤的詳細資訊，包括負載本身以及可下載的錯誤檔案。 請注意，包含錯誤的批的狀態可能仍為成功狀態。

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
| `metrics.failedRecordCount` | 由於分析、轉換或驗證而無法處理的行數。 通過減去 `inputRecordCount` 從 `outputRecordCount`。 此值將在所有批上生成，而不管 `errorDiagnostics` 的子菜單。 |
| `errors.recordCount` | 指定錯誤代碼失敗的行數。 此值為 **僅** 生成 `errorDiagnostics` 的子菜單。 |

>[!NOTE]
>
>如果錯誤診斷不可用，將出現以下錯誤消息：
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

本教程介紹了如何監視部分批處理接收錯誤。 有關批量攝取的詳細資訊，請閱讀 [批量攝取顯影劑指南](../batch-ingestion/api-overview.md)。

## 附錄 {#appendix}

本節提供有關攝取錯誤類型的補充資訊。

### 部分批接收錯誤類型 {#partial-ingestion-types}

部分批處理接收在接收資料時有三種不同的錯誤類型：

- [無法讀取的檔案](#unreadable)
- [架構或標頭無效](#schemas-headers)
- [不可分行](#unparsable)

### 無法讀取的檔案 {#unreadable}

如果接收的批具有不可讀的檔案，則批的錯誤將附加在批本身上。 有關檢索失敗批的詳細資訊，請參閱 [檢索失敗的批處理指南](../quality/retrieve-failed-batches.md)。

### 架構或標頭無效 {#schemas-headers}

如果接收的批具有無效的架構或無效的標頭，則批的錯誤將附加在批本身上。 有關檢索失敗批的詳細資訊，請參閱 [檢索失敗的批處理指南](../quality/retrieve-failed-batches.md)。

### 不可分行 {#unparsable}

如果您攝取的批具有不可分配的行，則可以使用以下請求查看包含錯誤的檔案清單。

**API格式**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BATCH_ID}` | 的 `id` 從中檢索錯誤資訊的批的值。 |

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

然後，可以使用 [診斷檢索端點](#retrieve-diagnostics)。

以下是檢索錯誤檔案的示例響應：

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
