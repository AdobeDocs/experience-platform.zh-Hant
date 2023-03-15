---
title: 使用Web SDK和邊緣網路伺服器API的混合個人化
description: 本文示範如何搭配使用Web SDK和伺服器API，在您的Web屬性上部署混合個人化。
keywords: 個人化；混合；伺服器api;伺服器端；混合實施；
exl-id: 506991e8-701c-49b8-9d9d-265415779876
source-git-commit: a9887535b12b8c4aeb39bb5a6646da88db4f0308
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 3%

---

# 使用Web SDK和邊緣網路伺服器API的混合個人化

## 總覽 {#overview}

Hybdrid個人化說明在伺服器端擷取個人化內容的程式，使用 [邊緣網路伺服器API](../..//server-api/overview.md)，並在用戶端呈現，使用 [Web SDK](../home.md).

您可以搭配Adobe Target或Offer decisioning等個人化解決方案使用混合個人化，差異在於 [!UICONTROL 伺服器API] 裝載。

## 先決條件 {#prerequisites}

在Web屬性上實作混合個人化之前，請確定您符合下列條件：

* 您已決定要使用哪個個人化解決方案。 這會影響 [!UICONTROL 伺服器API] 裝載。
* 您可以存取應用程式伺服器，以便用來 [!UICONTROL 伺服器API] 呼叫。
* 您可以存取 [邊緣網路伺服器API](../../server-api/authentication.md).
* 您已正確 [配置和部署](../fundamentals/configuring-the-sdk.md) 網頁上的網頁SDK。

## 流程圖 {#flow-diagram}

以下流程圖表說明提供混合個人化所採取步驟的順序。

![視覺化流程圖表，顯示提供混合個人化所採取步驟的順序。](assets/hybrid-personalization-diagram.png)

1. 瀏覽器先前儲存的任何現有Cookie，首碼為 `kndctr_`，會包含在瀏覽器請求中。
1. 客戶端Web瀏覽器向應用伺服器請求該網頁。
1. 應用程式伺服器收到頁面請求時，會發出 `POST` 請求 [伺服器API互動式資料收集端點](../../server-api/interactive-data-collection.md) 擷取個人化內容。 此 `POST` 要求包含 `event` 和 `query`. 前一步驟的Cookie（若有）會包含在 `meta>state>entries` 陣列。
1. 伺服器API會將個人化內容傳回至您的應用程式伺服器。
1. 應用程式伺服器會傳回HTML回應給用戶端瀏覽器，其中包含 [身分和叢集Cookie](#cookies).
1. 在用戶端頁面上， [!DNL Web SDK] `applyResponse` 會呼叫，並傳遞標題和內文 [!UICONTROL 伺服器API] 回應。
1. 此 [!DNL Web SDK] 呈現頁面載入 [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) 自動提供，因為 `renderDecisions` 標幟設為 `true`.
1. 表單式 [!DNL JSON] 選件會透過手動套用 `applyPersonalization` 方法，要更新 [!DNL DOM] 根據個人化選件。
1. 對於表單式活動，必須手動傳送顯示事件，以指出已顯示選件。 這是透過 `sendEvent` 命令。

## Cookie {#cookies}

Cookie可用來保存使用者身分和叢集資訊。  使用混合實作時，Web應用程式伺服器會在請求生命週期期間處理這些Cookie的儲存和傳送。

| Cookie | 用途 | 儲存者 | 傳送者 |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | 包含使用者身分詳細資料。 | 應用程式伺服器 | 應用程式伺服器 |
| `kndctr_AdobeOrg_cluster` | 指示應使用哪個邊緣網路群集來滿足請求。 | 應用程式伺服器 | 應用程式伺服器 |

## 請求投放 {#request-placement}

需要伺服器API請求才能獲取命題併發送顯示通知。 使用混合式實作時，應用程式伺服器會向伺服器API提出這些要求。

| 請求 | 製作者 |
|---|---|
| Interact請求以檢索主張 | 應用程式伺服器 |
| 傳送顯示通知的互動請求 | 應用程式伺服器 |

## Analytics含意 {#analytics}

實作混合個人化時，您必須特別注意，這樣Analytics就不會多次計算頁面點擊。

當您 [設定資料流](../datastreams/overview.md) 若為Analytics，事件會自動轉送，以便擷取頁面點擊。

此實作的範例使用兩種不同的資料流：

* 為Analytics設定的資料流。 此資料流用於Web SDK互動。
* 不使用Analytics設定的第二個資料流。 此資料流用於伺服器API請求。

如此一來，伺服器端請求就不會註冊任何Analytics事件，但用戶端請求會註冊。 這會導致Analytics請求被準確計算。


## 伺服器端要求 {#server-side-request}

以下範例要求說明您的應用程式伺服器可用於擷取個人化內容的伺服器API要求。

>[!IMPORTANT]
>
>此範例要求使用Adobe Target作為個人化解決方案。 您的請求可能會因您選擇的個人化解決方案而異。


**API格式**

```http
POST /ee/v2/interact
```

### 請求 {#request}

```shell
curl -X POST "https://edge.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Content-Type: text/plain" 
-d '{
   "event":{
      "xdm":{
         "web":{
            "webPageDetails":{
               "URL":"http://localhost/"
            },
            "webReferrer":{
               "URL":""
            }
         },
         "identityMap":{
            "FPID":[
               {
                  "id":"xyz",
                  "authenticatedState":"ambiguous",
                  "primary":true
               }
            ]
         },
         "timestamp":"2022-06-23T22:21:00.878Z"
      },
      "data":{
         
      }
   },
   "query":{
      "identity":{
         "fetch":[
            "ECID"
         ]
      },
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/default-content-item",
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "__view__",
            "sample-json-offer"
         ]
      }
   },
   "meta":{
      "state":{
         "domain":"localhost",
         "cookiesEnabled":true,
         "entries":[
            {
               "key":"kndctr_XXX_AdobeOrg_identity",
               "value":"abc123"
            },
            {
               "key":"kndctr_XXX_AdobeOrg_cluster",
               "value":"or2"
            }
         ]
      }
   }
}'
```

| 參數 | 類型 | 必填 | 說明 |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | 可以。 | 用來將互動傳遞至邊緣網路之資料流的ID。 請參閱 [資料流概觀](../datastreams/overview.md) 了解如何設定資料流。 |
| `requestId` | `String` | 無 | 用於關聯內部伺服器請求的隨機ID。 若未提供，邊緣網路將產生一個，並在回應中傳回。 |

### 伺服器端回應 {#server-response}

以下範例回應顯示伺服器API回應的外觀。


```json
{
   "requestId":"5c539bd0-33bf-43b6-a054-2924ac58038b",
   "handle":[
      {
         "payload":[
            {
               "id":"XXX",
               "namespace":{
                  "code":"ECID"
               }
            }
         ],
         "type":"identity:result"
      },
      {
         "payload":[
            {
               "..."
            },
            {
               "..."
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      }
   ]
}
```

## 用戶端要求 {#client-request}

在用戶端頁面上， [!DNL Web SDK] `applyResponse` 會呼叫命令，並傳遞伺服器端回應的標題和內文。

```js
   alloy("applyResponse", {
      "renderDecisions": true,
      "responseHeaders": {
         "cache-control": "no-cache, no-store, max-age=0, no-transform, private",
         "connection": "close",
         "content-encoding": "deflate",
         "content-type": "application/json;charset=utf-8",
         "date": "Mon, 11 Jul 2022 19:42:01 GMT",
         "server": "jag",
         "strict-transport-security": "max-age=31536000; includeSubDomains",
         "transfer-encoding": "chunked",
         "vary": "Origin",
         "x-adobe-edge": "OR2;9",
         "x-content-type-options": "nosniff",
         "x-konductor": "22.6.78-BLACKOUTSERVERDOMAINS:7fa23f82",
         "x-rate-limit-remaining": "599",
         "x-request-id": "5c539bd0-33bf-43b6-a054-2924ac58038b",
         "x-xss-protection": "1; mode=block"
      },
      "responseBody": {
         "requestId": "5c539bd0-33bf-43b6-a054-2924ac58038b",
         "handle": [
         {
            "payload": [
               {
               "id": "XXX",
               "namespace": {
                  "code": "ECID"
               }
               }
            ],
            "type": "identity:result"
         },
         {
            "payload": [
               {...}, 
               {...}
            ],
            "type": "personalization:decisions",
            "eventIndex": 0
         }
         ]
      }
   }
   ).then(applyPersonalization("sample-json-offer"));
```

表單式 [!DNL JSON] 選件會透過手動套用 `applyPersonalization` 方法，要更新 [!DNL DOM] 根據個人化選件。 對於表單式活動，必須手動傳送顯示事件，以指出已顯示選件。 這是透過 `sendEvent` 命令。

```js
function sendDisplayEvent(decision) {
    const { id, scope, scopeDetails = {} } = decision;

    alloy("sendEvent", {
        xdm: {
            eventType: "decisioning.propositionDisplay",
            _experience: {
                decisioning: {
                    propositions: [
                        {
                            id: id,
                            scope: scope,
                            scopeDetails: scopeDetails,
                        },
                    ],
                },
            },
        },
    });
}
```

## 範例應用程式 {#sample-app}

為協助您實驗並深入了解此類個人化，我們提供範例應用程式，供您下載並用於測試。 您可以從以下網址下載應用程式，以及如何使用應用程式的詳細指示 [GitHub存放庫](https://github.com/adobe/alloy-samples).
