---
title: 使用Web SDK和Edge Network伺服器API的混合個人化
description: 本文會示範如何使用Web SDK搭配伺服器API，在Web屬性上部署混合式個人化。
keywords: 個人化；混合；伺服器api；伺服器端；混合實作；
exl-id: 506991e8-701c-49b8-9d9d-265415779876
source-git-commit: 9489b5345c2b13b9d05b26d646aa7f1576840fb8
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 2%

---

# 使用Web SDK和Edge Network伺服器API的混合個人化

## 概觀 {#overview}

Hybdrid個人化說明使用[Edge Network伺服器API](../../server-api/overview.md)擷取個人化內容伺服器端，並使用[Web SDK](../home.md)在使用者端轉譯該內容的程式。

您可以將混合式個人化與Adobe Target、Adobe Journey Optimizer或Offer Decisioning等個人化解決方案搭配使用，差異在於[!UICONTROL 伺服器API]裝載的內容。

## 先決條件 {#prerequisites}

在Web屬性上實作混合個人化之前，請確定您符合下列條件：

* 您已決定要使用的個人化解決方案。 這會影響[!UICONTROL 伺服器API]裝載的內容。
* 您可以存取應用程式伺服器，以用來進行[!UICONTROL 伺服器API]呼叫。
* 您有權存取[Edge Network伺服器API](../../server-api/authentication.md)。
* 您已正確[設定](/help/web-sdk/commands/configure/overview.md)並在您想要個人化的頁面上部署Web SDK。

## 流程圖 {#flow-diagram}

以下流程圖說明傳遞混合個人化所採取步驟的順序。

![顯示傳遞混合式個人化步驟順序的視覺流程圖。](assets/hybrid-personalization-diagram.png)

1. 先前由瀏覽器儲存且前置詞為`kndctr_`的任何現有Cookie都會包含在瀏覽器請求中。
1. 使用者端網頁瀏覽器會向應用程式伺服器要求網頁。
1. 應用程式伺服器收到頁面要求時，會向[伺服器API互動式資料收集端點](../../server-api/interactive-data-collection.md)發出`POST`要求，以擷取個人化內容。 `POST`要求包含`event`和`query`。 先前步驟的Cookie （若有）包含在`meta>state>entries`陣列中。
1. 伺服器API會將個人化內容傳回至您的應用程式伺服器。
1. 應用程式伺服器傳回HTML回應給使用者端瀏覽器，其中包含[識別與叢集Cookie](#cookies)。
1. 在使用者端頁面上呼叫[!DNL Web SDK] `applyResponse`命令，傳入上一步驟之[!UICONTROL 伺服器API]回應的標題和內文。
1. [!DNL Web SDK]會自動轉譯Target [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)選件和Journey Optimizer Web Channel專案，因為`renderDecisions`標幟已設為`true`。
1. 透過`applyProposition`方法手動套用Target表單式[!DNL HTML]/[!DNL JSON]選件和Journey Optimizer程式碼式體驗，以根據主張中的個人化內容更新[!DNL DOM]。
1. 對於Target表單式[!DNL HTML]/[!DNL JSON]選件和Journey Optimizer程式碼式體驗，必須手動傳送顯示事件，以指出已顯示傳回內容的時間。 這是透過`sendEvent`命令完成的。

## Cookie {#cookies}

Cookie可用來儲存使用者身分和叢集資訊。  使用混合實作時，Web應用程式伺服器會在請求生命週期期間處理這些Cookie的儲存和傳送。

| Cookie | 目的 | 儲存者 | 傳送者 |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | 包含使用者身分詳細資訊。 | 應用程式伺服器 | 應用程式伺服器 |
| `kndctr_AdobeOrg_cluster` | 指出應使用哪個Edge Network叢集來履行要求。 | 應用程式伺服器 | 應用程式伺服器 |

## 請求刊登 {#request-placement}

需要伺服器API要求才能取得主張並傳送顯示通知。 使用混合實作時，應用程式伺服器會向伺服器API提出這些要求。

| 請求 | 製作者 |
|---|---|
| 擷取主張的互動請求 | 應用程式伺服器 |
| 傳送顯示通知的互動請求 | 應用程式伺服器 |

## 分析影響 {#analytics}

實施混合個人化時，您必須特別注意，才不會在Analytics中多次計算頁面點選。

當您[為Analytics設定資料流](../../datastreams/overview.md)時，會自動轉送事件，以便擷取頁面點選。

此實作的範例使用兩個不同的資料串流：

* 為Analytics設定的資料串流。 此資料流用於Web SDK互動。
* 沒有Analytics設定的第二個資料串流。 此資料流用於伺服器API請求。 您必須使用與您為Analytics設定的資料流相同的目的地設定來設定此資料流。

如此一來，伺服器端要求不會註冊任何Analytics事件，但使用者端要求會註冊。 如此一來，Analytics請求就會被精確計算。


## 伺服器端要求 {#server-side-request}

以下範例請求說明您的應用程式伺服器可用來擷取個人化內容的伺服器API請求。

>[!IMPORTANT]
>
>此範例請求使用Adobe Target作為個人化解決方案。 您的請求可能會因您選擇的個人化解決方案而異。


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

| 參數 | 類型 | 必要 | 說明 |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | 可以。 | 您用來將互動傳遞至Edge Network的資料串流的ID。 請參閱[資料串流總覽](../../datastreams/overview.md)，瞭解如何設定資料串流。 |
| `requestId` | `String` | 無 | 關聯內部伺服器請求的隨機ID。 如果未提供任何專案，Edge Network將會產生一個專案，並在回應中傳回。 |

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

## 使用者端請求 {#client-request}

在使用者端頁面上，呼叫[!DNL Web SDK] `applyResponse`命令，傳入伺服器端回應的標題和內文。

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

透過`applyPersonalization`方法手動套用表單式[!DNL JSON]優惠，以根據個人化優惠更新[!DNL DOM]。 針對表單式活動，必須手動傳送顯示事件，以指出何時已顯示選件。 這是透過`sendEvent`命令完成的。

```js
function sendDisplayEvent(decision) {
    const { id, scope, scopeDetails = {} } = decision;

    alloy("sendEvent", {
        "xdm": {
            "eventType": "decisioning.propositionDisplay",
            "_experience": {
                "decisioning": {
                    "propositions": [{
                        "id": id,
                        "scope": scope,
                        "scopeDetails": scopeDetails
                    }],
                    "propositionEventType": {
                        "display": 1
                    }
                }
            }
        }
    });
}
```

## 範例應用程式 {#sample-app}

為協助您實驗並深入瞭解這類個人化，我們提供範例應用程式，供您下載及用於測試。 您可以從此[GitHub存放庫](https://github.com/adobe/alloy-samples)下載應用程式，以及有關如何使用的詳細說明。
