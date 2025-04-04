---
keywords: Experience Platform；首頁；熱門主題；擷取失敗的批次；失敗的批次；批次擷取；批次擷取；失敗的批次；取得失敗的批次；取得失敗的批次；下載失敗的批次；
solution: Experience Platform
title: 使用資料存取API擷取失敗的批次
type: Tutorial
description: 本教學課程涵蓋使用資料擷取API擷取失敗批次相關資訊的步驟。
exl-id: 5fb9f28d-091e-4124-8d8e-b8a675938d3a
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 13%

---

# 使用資料存取API擷取失敗的批次

Adobe Experience Platform提供兩種上傳和擷取資料的方法。 您可以使用批次擷取，這可讓您使用各種檔案型別（例如CSV）插入其資料，或是使用串流擷取，可讓您使用串流端點即時將其資料插入[!DNL Experience Platform]。

本教學課程涵蓋使用[!DNL Data Ingestion] API擷取失敗批次相關資訊的步驟。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
- [[!DNL Data Ingestion]](../home.md)：傳送資料給[!DNL Experience Platform]的方法。

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

所有包含承載 (POST、PUT、PATCH) 的請求都需有額外的標頭：

- `Content-Type: application/json`

### 失敗的批次範例

此教學課程將使用具有錯誤格式時間戳記（將月份值設為&#x200B;**00**）的範例資料，如下所示：

```json
{
    "body": {
        "xdmEntity": {
            "id": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": "2018-00-10T22:07:56Z",
            "environment": {
                "browserDetails": {
                    "userAgent": "Mozilla\/5.0 (Windows NT 5.1) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/29.0.1547.57 Safari\/537.36 OPR\/16.0.1196.62",
                    "acceptLanguage": "en-US",
                    "cookiesEnabled": true,
                    "javaScriptVersion": "1.6",
                    "javaEnabled": true
                },
                "colorDepth": 32,
                "viewportHeight": 799,
                "viewportWidth": 414
            }
        }
    }
}
```

由於時間戳記的格式錯誤，上述裝載無法針對XDM結構正確驗證。

## 擷取失敗的批次

**API格式**

```http
GET /batches/{BATCH_ID}/failed
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 您要查詢之批次的ID。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```json
{
    "data": [
        {
            "name": "_SUCCESS",
            "length": "0",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/{BATCH_ID}/failed?path=_SUCCESS"
                }
            }
        },
        {
            "name": "part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json",
            "length": "1800",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/{BATCH_ID}/failed?path=part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json"
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

透過上述回應，您可以檢視批次的哪些區塊成功和失敗。 從這個回應中，您可以看到檔案`part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json`包含失敗的批次。

## 下載失敗的批次

知道批次中的哪個檔案失敗後，就可以下載失敗的檔案並檢視錯誤訊息。

**API格式**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 包含失敗檔案的批次識別碼。 |
| `{FAILED_FILE}` | 格式設定失敗的檔案名稱。 |

**要求**

以下請求可讓您下載發生擷取錯誤的檔案。

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path={FAILED_FILE}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

由於前一個擷取的批次有無效的日期時間，將會顯示以下驗證錯誤。

```json
{
    "_validationErrors": [
        {
            "causingExceptions": [],
            "keyword": "format",
            "message": "[2018-00-23T22:07:01Z] is not a valid date-time. Expected [yyyy-MM-dd'T'HH:mm:ssZ, yyyy-MM-dd'T'HH:mm:ss.[0-9]{1-9}Z, yyyy-MM-dd'T'HH:mm:ss[+-]HH:mm, yyyy-MM-dd'T'HH:mm:ss.[0-9]{1,9}[+-]HH:mm]",
            "pointerToViolation": "#/timestamp",
            "schemaLocation": "#/properties/timestamp"
        }
    ]
}
```

## 後續步驟

閱讀本教學課程後，您已瞭解如何從失敗的批次擷取錯誤。 如需批次擷取的詳細資訊，請參閱[批次擷取開發人員指南](../batch-ingestion/overview.md)。 如需串流擷取的詳細資訊，請參閱[建立串流連線教學課程](../tutorials/create-streaming-connection.md)。

## 附錄

本節包含其他可能發生之擷取錯誤型別的相關資訊。

### XDM格式不正確

如同上一個範例流程中的時間戳記錯誤，這些錯誤是由於XDM格式錯誤所導致。 這些錯誤訊息會因問題性質而異。 因此，無法顯示特定錯誤範例。

### 組織ID遺失或無效

如果承載無效中缺少組織ID，便會顯示此錯誤。

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{ORG_ID}@AdobeOrg] Message has an absent or wrong ims org in the header"
    }
}
```

### 缺少XDM結構描述

如果`xdmMeta`的`schemaRef`遺失，便會顯示此錯誤。

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{ORG_ID}@AdobeOrg] Message has unknown xdm format"
    }
}
```

### 缺少來源名稱

如果標頭中的`source`缺少其`name`，則會顯示此錯誤。

```json
{
    "_errors":{
        "_streamingValidation": [
            {
                "message": "Payload header is missing Source Name"
            }
        ]
    }
}
```

### 缺少XDM實體

如果沒有`xdmEntity`出現，則會顯示此錯誤。

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
