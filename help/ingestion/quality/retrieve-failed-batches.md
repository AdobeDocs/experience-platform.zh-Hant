---
keywords: Experience Platform；主題；熱門主題；檢索失敗的批；失敗的批；批處理；失敗的批；獲取失敗的批；獲取失敗的批；下載失敗的批；下載失敗的批；
solution: Experience Platform
title: 使用資料存取API檢索失敗的批
type: Tutorial
description: 本教程介紹使用資料接收API檢索有關失敗批處理的資訊的步驟。
exl-id: 5fb9f28d-091e-4124-8d8e-b8a675938d3a
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 2%

---

# 使用資料存取API檢索失敗的批

Adobe Experience Platform提供了兩種資料上傳和接收方法。 您可以使用批處理接收(允許您使用各種檔案類型（如CSV）插入其資料)，也可以使用流式處理接收(允許您將資料插入到 [!DNL Platform] 即時使用流端點。

本教程介紹使用以下方法檢索有關失敗批處理的資訊的步驟 [!DNL Data Ingestion] API。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
- [[!DNL Data Ingestion]](../home.md):資料可通過以下方法發送 [!DNL Experience Platform]。

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

包含負載(POST、PUT、PATCH)的所有請求都需要附加的標頭：

- `Content-Type: application/json`

### 示例失敗批

本教程將使用帶有錯誤格式時間戳的示例資料，該時間戳將月值設定為 **00**，如下所示：

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

由於時間戳格式錯誤，上述負載無法針對XDM架構進行正確驗證。

## 檢索失敗的批

**API格式**

```http
GET /batches/{BATCH_ID}/failed
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 您要查找的批的ID。 |

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

通過上述響應，您可以看到批的哪些塊成功和失敗。 從此響應中，您可以看到 `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` 包含失敗的批。

## 下載失敗的批

一旦知道批處理中哪個檔案失敗，就可以下載失敗的檔案並查看錯誤消息。

**API格式**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BATCH_ID}` | 包含失敗檔案的批的ID。 |
| `{FAILED_FILE}` | 格式化失敗的檔案的名稱。 |

**要求**

以下請求允許您下載包含攝取錯誤的檔案。

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

由於上一個接收的批具有無效的日期時間，因此將顯示以下驗證錯誤。

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

閱讀本教程後，您已學習如何從失敗的批中檢索錯誤。 有關批量攝取的詳細資訊，請閱讀 [批量攝取顯影劑指南](../batch-ingestion/overview.md)。 有關流式接收的詳細資訊，請閱讀 [建立流連接教程](../tutorials/create-streaming-connection.md)。

## 附錄

本節包含有關可能發生的其他接收錯誤類型的資訊。

### 格式不正確的XDM

與上一個示例流中的時間戳錯誤一樣，這些錯誤是由於XDM格式不正確所致。 這些錯誤消息會因問題的性質而異。 因此，不能顯示特定的錯誤示例。

### 缺少或無效的組織ID

如果負載中缺少組織ID，則顯示此錯誤。

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

如果 `schemaRef` 為 `xdmMeta` 缺少。

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

### 缺少源名稱

如果 `source` 標題中缺少 `name`。

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

如果沒有，則顯示此錯誤 `xdmEntity` 現在。

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
