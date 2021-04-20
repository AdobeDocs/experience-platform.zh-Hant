---
keywords: Experience Platform;home；熱門主題；流；流處理；流處理驗證；驗證；流處理驗證；驗證；同步驗證；同步驗證；非同步驗證；非同步驗證；
solution: Experience Platform
title: 串流擷取驗證
topic: tutorial
type: Tutorial
description: 串流擷取可讓您使用串流端點即時將資料上傳至Adobe Experience Platform。 串流擷取API支援同步和非同步兩種驗證模式。
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 3%

---


# 串流擷取驗證

串流擷取可讓您使用串流端點即時將資料上傳至Adobe Experience Platform。 串流擷取API支援同步和非同步兩種驗證模式。

## 快速入門

本指南需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
- [[!DNL Streaming Ingestion]](../streaming-ingestion/overview.md):其中一種方法可傳送資料 [!DNL Experience Platform]。

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

### 驗證涵蓋範圍

[!DNL Streaming Validation Service] 涵蓋下列方面的驗證：
- Range
- Presence
- Enum
- 圖樣
- 類型
- 格式

## 同步驗證

同步驗證是一種驗證方法，可立即提供有關擷取失敗原因的意見回應。 但是，失敗時，驗證失敗的記錄會被丟棄，並且無法下游發送。 因此，同步驗證只應在開發程式期間使用。 在執行同步驗證時，呼叫者會得知XDM驗證的結果，以及失敗的原因。

依預設，同步驗證不會開啟。 若要啟用它，您必須在進行API呼叫時傳入選用的查詢參數`synchronousValidation=true`。 此外，同步驗證目前僅在您的串流端點位於VA7資料中心時才可用。

如果消息在同步驗證期間失敗，則不會將該消息寫入輸出隊列，從而為用戶提供立即反饋。

>[!NOTE]
>
>由於會快取變更，因此架構變更可能無法立即使用。 最多需要15分鐘的時間刷新快取。

**API格式**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 先前建立的串流連接的`id`值。 |

**請求**

提交下列要求，透過同步驗證將資料收錄至您的資料匯入：

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| 參數 | 說明 |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | 您要收錄之資料的JSON內文。 |

**回應**

啟用同步驗證後，成功的回應會在其裝載中包含任何遇到的驗證錯誤：

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [6aca7aa2d87ebd6b2780ca5724d94324a14475f140a2b69373dd5c714430dfd4] imsOrgId: [7BF122A65C5B3FE40A494026@AdobeOrg] Message is invalid",
        "cause": {
            "_streamingValidation": [
                {
                    "schemaLocation": "#",
                    "pointerToViolation": "#",
                    "causingExceptions": [
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [workEmail] is not permitted"
                        },
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [person] is not permitted"
                        },
                        {
                            "schemaLocation": "#/properties/_id",
                            "pointerToViolation": "#/_id",
                            "causingExceptions": [],
                            "keyword": "type",
                            "message": "expected type: String, found: Long"
                        }
                    ],
                    "message": "3 schema violations found"
                }
            ]
        }
    }
}
```

上述回應會列出發現多少個架構違規，以及哪些違規。 例如，此響應表示`workEmail`和`person`鍵未在模式中定義，因此不允許。 它也會將`_id`的值標示為不正確，因為模式預期為`string`，但是插入了`long`。 請注意，一旦遇到5個錯誤，驗證服務將&#x200B;**stop**&#x200B;處理該消息。 但是，其他消息將繼續被解析。

## 非同步驗證

非同步驗證是驗證方法，不會立即提供意見回應。 而是將資料傳送至[!DNL Data Lake]中的失敗批次，以防止資料遺失。 此失敗的資料稍後可以擷取以供進一步分析和重播。 這種方法應用於生產中。 除非另有要求，否則串流擷取會在非同步驗證模式中運作。

**API格式**

```http
POST /collection/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 先前建立的串流連接的`id`值。 |

**請求**

提交下列要求，透過非同步驗證將資料收錄至您的資料匯入：

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| 參數 | 說明 |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | 您要收錄之資料的JSON內文。 |

>[!NOTE]
>
>不需要額外的查詢參數，因為非同步驗證預設會啟用。

**回應**

啟用非同步驗證後，成功的回應會傳回下列內容：

```json
{
    "inletId": "f6ca9706d61de3b78be69e2673ad68ab9fb2cece0c1e1afc071718a0033e6877",
    "xactionId": "1555445493896:8600:8",
    "receivedTimeMs": 1555445493932,
    "synchronousValidation": {
        "skipped": true
    }
}
```

請注意響應如何表示已跳過同步驗證，因為尚未明確請求同步驗證。

## 附錄

本節包含各種狀態代碼對於接收資料的響應有何意義的資訊。

### 狀態代碼

| 狀態代碼 | 這意味著什麼 |
| ----------- | ------------- |
| 200 | 成功. 對於同步驗證，這表示它已通過驗證檢查。 對於非同步驗證，這表示它只成功接收了訊息。 使用者可透過觀察資料集來找出最終的訊息狀態。 |
| 400 | 錯誤. 您的要求有問題。 從串流驗證服務接收含有詳細資訊的錯誤訊息。 |
| 401 | 錯誤. 您的要求未經授權——您需要使用不記名代號來要求。 有關如何請求訪問的詳細資訊，請查看本[教程](https://www.adobe.com/go/platform-api-authentication-en)或本[部落格](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)。 |
| 500 | 錯誤. 出現內部系統錯誤。 |
| 501 | 錯誤. 這表示此位置支援同步驗證&#x200B;**not**。 |
| 503 | 錯誤. 服務目前無法使用。 客戶端至少應使用指數式回退策略重試三次。 |