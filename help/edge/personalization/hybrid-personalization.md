---
title: 使用Web SDK和邊緣網路伺服器API的混合個性化
description: 本文演示了如何將Web SDK與伺服器API結合使用以在Web屬性上部署混合個性化。
keywords: 個性化；混合；伺服器api;伺服器端；混合實現；
exl-id: 506991e8-701c-49b8-9d9d-265415779876
source-git-commit: a9887535b12b8c4aeb39bb5a6646da88db4f0308
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 3%

---

# 使用Web SDK和邊緣網路伺服器API的混合個性化

## 總覽 {#overview}

Hybdrid個性化描述了使用 [邊緣網路伺服器API](../..//server-api/overview.md)，並使用 [Web SDK](../home.md)。

您可以將混合個性化與個性化解決方案結合使用，如Adobe Target或Offer decisioning，其區別在於 [!UICONTROL 伺服器API] 負載。

## 先決條件 {#prerequisites}

在Web屬性上實施混合個性化之前，請確保滿足以下條件：

* 您已決定要使用什麼個性化解決方案。 這將影響 [!UICONTROL 伺服器API] 負載。
* 您有權訪問可用於 [!UICONTROL 伺服器API] 呼叫。
* 您有權訪問 [邊緣網路伺服器API](../../server-api/authentication.md)。
* 您正確 [配置和部署](../fundamentals/configuring-the-sdk.md) 要個性化的頁面上的Web SDK。

## 流程圖 {#flow-diagram}

下面的流程圖描述了為實現混合個性化而採取的步驟的順序。

![可視化流程圖顯示了為提供混合個性化而採取的步驟的順序。](assets/hybrid-personalization-diagram.png)

1. 瀏覽器先前儲存的任何現有Cookie，前置詞為 `kndctr_`，包含在瀏覽器請求中。
1. 客戶端Web瀏覽器從應用伺服器請求網頁。
1. 當應用伺服器接收到頁面請求時， `POST` 請求 [伺服器API互動式資料收集終結點](../../server-api/interactive-data-collection.md) 獲取個性化內容。 的 `POST` 請求包含 `event` 和 `query`。 上一步中的Cookie（如果可用）包含在 `meta>state>entries` 陣列。
1. 伺服器API將個性化內容返回到應用伺服器。
1. 應用伺服器返回對客戶端瀏覽器的HTML響應，其中包含 [標識和群集cookie](#cookies)。
1. 在客戶端頁面上， [!DNL Web SDK] `applyResponse` 命令被調用，傳遞到 [!UICONTROL 伺服器API] 響應。
1. 的 [!DNL Web SDK] 呈現頁載入 [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) 自動提供，因為 `renderDecisions` 標誌設定為 `true`。
1. 基於表單 [!DNL JSON] 通過 `applyPersonalization` 方法，更新 [!DNL DOM] 基於個性化服務。
1. 對於基於表單的活動，必須手動發送顯示事件，以指示何時顯示優惠。 此操作通過 `sendEvent` 的子菜單。

## Cookie {#cookies}

Cookie用於保留用戶標識和群集資訊。  當使用混合實現時，Web應用程式伺服器在請求生命週期中處理這些cookie的儲存和發送。

| Cookie | 用途 | 儲存者 | 發送者 |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | 包含用戶標識詳細資訊。 | 應用程式伺服器 | 應用程式伺服器 |
| `kndctr_AdobeOrg_cluster` | 指示應使用哪個邊緣網路群集來滿足請求。 | 應用程式伺服器 | 應用程式伺服器 |

## 請求放置 {#request-placement}

需要伺服器API請求才能獲取主張併發送顯示通知。 當使用混合實現時，應用伺服器向伺服器API發出這些請求。

| 請求 | 製作者 |
|---|---|
| 交互請求以檢索主張 | 應用程式伺服器 |
| 交互請求以發送顯示通知 | 應用程式伺服器 |

## 分析影響 {#analytics}

在實施混合個性化時，您必須特別注意，以便在分析中不會多次計算頁面命中。

當你 [配置資料流](../datastreams/overview.md) 對於分析，自動轉發事件以捕獲頁面命中。

此實現的示例使用兩種不同的資料流：

* 為分析配置的資料流。 此資料流用於Web SDK交互。
* 沒有分析配置的第二個資料流。 此資料流用於伺服器API請求。

這樣，伺服器端請求不會註冊任何分析事件，但客戶端請求會註冊。 這將導致準確計算分析請求。


## 伺服器端請求 {#server-side-request}

下面的示例請求說明了應用程式伺服器可用於檢索個性化內容的伺服器API請求。

>[!IMPORTANT]
>
>此示例請求將Adobe Target用作個性化解決方案。 您的請求可能會根據您選擇的個性化解決方案而有所不同。


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
| `dataStreamId` | `String` | 可以。 | 用於將交互傳遞到邊緣網路的資料流的ID。 查看 [資料流概述](../datastreams/overview.md) 瞭解如何配置資料流。 |
| `requestId` | `String` | 無 | 用於關聯內部伺服器請求的隨機ID。 如果未提供，則邊緣網路將生成一個並在響應中返回。 |

### 伺服器端響應 {#server-response}

下面的示例響應顯示伺服器API響應可能的樣式。


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

## 客戶端請求 {#client-request}

在客戶端頁面上， [!DNL Web SDK] `applyResponse` 命令被調用，並傳遞伺服器端響應的標頭和正文。

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

基於表單 [!DNL JSON] 通過 `applyPersonalization` 方法，更新 [!DNL DOM] 基於個性化服務。 對於基於表單的活動，必須手動發送顯示事件，以指示何時顯示優惠。 此操作通過 `sendEvent` 的子菜單。

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

## 示例應用程式 {#sample-app}

為了幫助您進行實驗並瞭解有關這種個性化類型的更多資訊，我們提供了一個示例應用程式，您可以下載該應用程式並將其用於測試。 您可以從此下載應用程式以及有關如何使用它的詳細說明 [GitHub儲存庫](https://github.com/adobe/alloy-samples)。
