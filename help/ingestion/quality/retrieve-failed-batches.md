---
keywords: Experience Platform；首頁；熱門主題；檢索失敗批次；失敗批次；批次擷取；批次擷取；失敗批次；取得失敗批次；取得失敗批次；下載失敗批次；下載失敗批次；下載失敗批次；
solution: Experience Platform
title: 使用資料存取API擷取失敗的批次
type: Tutorial
description: 本教學課程涵蓋使用資料擷取API擷取失敗批次相關資訊的步驟。
exl-id: 5fb9f28d-091e-4124-8d8e-b8a675938d3a
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 2%

---

# 使用資料存取API擷取失敗的批次

Adobe Experience Platform提供兩種上傳和擷取資料的方法。 您可以使用批次內嵌(可讓您使用各種檔案類型（例如CSV）插入其資料)，或使用串流內嵌(可讓您將其資料插入 [!DNL Platform] 即時使用串流端點。

本教學課程涵蓋使用 [!DNL Data Ingestion] API。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
- [[!DNL Data Ingestion]](../home.md):資料可透過哪些方法傳送至 [!DNL Experience Platform].

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

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- `Content-Type: application/json`

### 失敗批次示例

本教學課程將使用格式不正確的時間戳記來設定月份值為的範例資料 **00**，如下所示：

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

由於時間戳記格式錯誤，上述裝載無法針對XDM架構正確驗證。

## 檢索失敗的批

**API格式**

```http
GET /batches/{BATCH_ID}/failed
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 要查找的批的ID。 |

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

通過上述響應，您可以看到哪些批次成功和失敗。 從此回應中，您可以看到該檔案 `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` 包含失敗的批。

## 下載失敗的批處理

一旦您知道批處理中的哪個檔案失敗，就可以下載失敗的檔案，並查看錯誤消息。

**API格式**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 包含失敗檔案的批處理的ID。 |
| `{FAILED_FILE}` | 格式化失敗的檔案的名稱。 |

**要求**

下列要求可讓您下載有擷取錯誤的檔案。

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

由於上一個擷取的批次的日期時間無效，因此會顯示下列驗證錯誤。

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

閱讀本教學課程後，您已學習如何從失敗的批次擷取錯誤。 如需批次內嵌的詳細資訊，請參閱 [批次匯入開發人員指南](../batch-ingestion/overview.md). 如需串流獲取的詳細資訊，請參閱 [建立串流連線教學課程](../tutorials/create-streaming-connection.md).

## 附錄

本節包含可能發生的其他擷取錯誤類型的相關資訊。

### 格式不正確的XDM

與上一個範例流程中的時間戳記錯誤相同，這些錯誤是因為XDM格式不正確。 這些錯誤消息會因問題的性質而有所不同。 因此，無法顯示特定的錯誤範例。

### 遺失或無效的IMS組織ID

如果裝載中缺少IMS組織ID無效，就會顯示此錯誤。

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

### 缺少XDM架構

若 `schemaRef` 針對 `xdmMeta` 缺少。

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

### 缺少源名

若 `source` 在標題中缺少 `name`.

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

如果沒有，則會顯示此錯誤 `xdmEntity` 現在。

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
