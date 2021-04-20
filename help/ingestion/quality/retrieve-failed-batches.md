---
keywords: Experience Platform;home；常用主題；檢索失敗的批；失敗的批；批處理；失敗的批處理；失敗的批處理；獲取失敗的批處理；獲取失敗的批處理；下載失敗的批處理；下載失敗的批處理；
solution: Experience Platform
title: 使用Data Access API檢索失敗的批
topic: tutorial
type: Tutorial
description: 本教學課程涵蓋使用資料擷取API擷取失敗批次資訊的步驟。
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 2%

---


# 使用Data Access API檢索失敗的批處理

Adobe Experience Platform提供兩種上傳和收錄資料的方法。 您可以使用批次擷取功能(可讓您使用各種檔案類型（例如CSV）插入其資料)或串流擷取功能（可讓您使用串流端點將資料即時插入[!DNL Platform]）。

本教程介紹使用[!DNL Data Ingestion] API檢索失敗批的資訊的步驟。

## 快速入門

本指南需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
- [[!DNL Data Ingestion]](../home.md):可傳送資料的方法 [!DNL Experience Platform]。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

- 授權：載體`{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Schema Registry]的資源）都與特定虛擬沙盒隔離。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙盒的詳細資訊，請參閱[沙盒概述檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- Content-Type: `application/json`

### 失敗批示例

本教學課程將使用格式錯誤的時間戳記格式化的範例資料，將月份值設定為&#x200B;**00**，如下所示：

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

由於時間戳記格式錯誤，上述裝載無法正確驗證XDM架構。

## 檢索失敗的批

**API格式**

```http
GET /batches/{BATCH_ID}/failed
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 您正在查找的批的ID。 |

**請求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}
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

通過上述響應，您可以看到哪些批成功和失敗。 從此響應中，您可以看到檔案`part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json`包含失敗的批處理。

## 下載失敗的批次

一旦您知道批次中的哪個檔案失敗，就可以下載失敗的檔案並查看錯誤訊息。

**API格式**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 包含失敗檔案的批次的ID。 |
| `{FAILED_FILE}` | 格式化失敗的檔案的名稱。 |

**請求**

下列要求可讓您下載有擷取錯誤的檔案。

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path={FAILED_FILE}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

由於上一個收錄批次的日期時間無效，因此會顯示下列驗證錯誤。

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

閱讀本教學課程後，您已學習如何從失敗的批次擷取錯誤。 有關批次擷取的詳細資訊，請閱讀[批次擷取開發人員指南](../batch-ingestion/overview.md)。 有關串流擷取的詳細資訊，請閱讀[建立串流連線教學課程](../tutorials/create-streaming-connection.md)。

## 附錄

本節包含可能發生的其他擷取錯誤類型的相關資訊。

### 格式錯誤的XDM

與上一個示例流中的時間戳錯誤一樣，這些錯誤是由於XDM格式不正確造成的。 這些錯誤消息會因問題的性質而有所不同。 因此，不能顯示特定的錯誤範例。

### 遺失或無效的IMS組織ID

如果IMS組織ID在裝載中遺失或無效，則會顯示此錯誤。

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{IMS_ORG}@AdobeOrg] Message has an absent or wrong ims org in the header"
    }
}
```

### 缺少XDM模式

如果`xdmMeta`的`schemaRef`遺失，則會顯示此錯誤。

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{IMS_ORG}@AdobeOrg] Message has unknown xdm format"
    }
}
```

### 缺少源名稱

如果標題中的`source`遺失其`name`，則會顯示此錯誤。

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

如果沒有`xdmEntity`存在，則顯示此錯誤。

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
