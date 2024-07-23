---
title: 比較at.js與Experience PlatformWeb SDK
description: 瞭解at.js功能與Experience Platform Web SDK的比較
keywords: target；adobe target；activity.id；experience.id；renderDecisions；decisionScopes；預先隱藏程式碼片段；vec；表單式體驗撰寫器；xdm；對象；決定；範圍；結構；系統圖表；圖表
exl-id: b63fe47d-856a-4cae-9057-51917b3e58dd
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '2175'
ht-degree: 2%

---

# 比較at.js程式庫與Web SDK

## 概觀

本文概述`at.js`資料庫與Experience Platform Web SDK之間的差異。

## 安裝程式庫

### 安裝at.js

我們允許客戶直接從Adobe Experience Cloud的「實作」標籤下載程式庫。 at.js程式庫已根據客戶的下列設定加以自訂： clientCode、imsOrgId等。

### 安裝Web SDK

預先建立的版本可在CDN上取得。 您可以直接在頁面上在CDN上參考程式庫，或將其下載並託管在您自己的基礎架構上。 它提供縮制和未縮制的格式。 未縮制的版本對於除錯而言相當實用。

如需詳細資訊，請參閱[使用JavaScript程式庫安裝Web SDK](/help/web-sdk/install/library.md)。

## 設定程式庫

### 設定at.js

在每個at.js檔案的結尾，您會找到我們會例項化並傳遞設定物件的區段。 這是可自訂的，下載時，我們會將該區段填入目前的客戶設定。

```javascript
window.adobe.target.init(window, document, {
  "clientCode": "demo",
  "imsOrgId": "",
  "serverDomain": "localhost:5000",
  "timeout": 2000,
  "globalMboxName": "target-global-mbox",
  "version": "2.0.0",
  "defaultContentHiddenStyle": "visibility: hidden;",
  "defaultContentVisibleStyle": "visibility: visible;",
  "bodyHiddenStyle": "body {opacity: 0 !important}",
  "bodyHidingEnabled": true,
  "deviceIdLifetime": 63244800000,
  "sessionIdLifetime": 1860000,
  "selectorsPollingTimeout": 5000,
  "visitorApiTimeout": 2000,
  "overrideMboxEdgeServer": false,
  "overrideMboxEdgeServerTimeout": 1860000,
  "optoutEnabled": false,
  "optinEnabled": false,
  "secureOnly": false,
  "supplementalDataIdParamTimeout": 30,
  "authoringScriptUrl": "//cdn.tt.omtrdc.net/cdn/target-vec.js",
  "urlSizeLimit": 2048,
  "endpoint": "/rest/v1/delivery",
  "pageLoadEnabled": true,
  "viewsEnabled": true,
  "analyticsLogging": "server_side",
  "serverState": {},
  "decisioningMethod": "server-side",
  "legacyBrowserSupport":  false
});
```

[了解更多](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html)


### 設定Web SDK

使用[`configure`](/help/web-sdk/commands/configure/overview.md)命令完成SDK的設定。 `configure`命令是&#x200B;*一律*&#x200B;先呼叫。

## 如何請求並自動轉譯頁面載入Target選件

### 使用at.js

使用at.js 2.x時，如果您啟用設定`pageLoadEnabled`，程式庫將會觸發使用`execute -> pageLoad`的Target Edge呼叫。 如果所有設定都設為預設值，則不需要進行自訂編碼。將at.js新增至頁面並由瀏覽器載入後，就會執行Target Edge呼叫。

### 使用Web SDK

SDK可自動擷取及轉譯在Adobe Target [視覺化體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)中建立的內容。

若要要求並自動轉譯Target選件，請使用`sendEvent`命令並將`renderDecisions`選項設定為`true`。 這麼做會強制SDK自動轉譯任何符合自動轉譯條件的個人化內容。

範例：

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

Experience Platform Web SDK會自動傳送包含WEB SDK所執行選件的通知，此為通知要求裝載外觀的範例：

```json
{
  "events": [{
      "xdm": {
        "_experience": {
          "decisioning": {
            "propositions": [
              {
                "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                "scope": "cart",
                "scopeDetails": {
                  "decisionProvider": "TGT",
                  "activity": {
                    "id": "127019"
                  },
                  "experience": {
                    "id": "0"
                  },
                  "strategies": [
                    {
                      "step": "entry",
                      "algorithmID": "0",
                      "trafficType": "0"
                    },
                    {
                      "step": "display",
                      "algorithmID": "0",
                      "trafficType": "0"
                    }
                  ],
                  "characteristics": {
                    "eventToken": "bKMxJ8dCR1XlPfDCx+2vSGqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                  }
                }
              }
            ]
          }
        },
        "eventType": "display",
        "web": {
          "webPageDetails": {
            "viewName": "cart",
            "URL": "https://alloyio.com/personalizationSpa/cart"
          },
          "webReferrer": {
            "URL": ""
          }
        },
        "device": {
          "screenHeight": 800,
          "screenWidth": 1280,
          "screenOrientation": "landscape"
        },
        "environment": {
          "type": "browser",
          "browserDetails": {
            "viewportWidth": 1280,
            "viewportHeight": 284
          }
        },
        "placeContext": {
          "localTime": "2021-12-10T15:50:34.467+02:00",
          "localTimezoneOffset": -120
        },
        "timestamp": "2021-12-10T13:50:34.467Z",
        "implementationDetails": {
          "name": "https://ns.adobe.com/experience/alloy",
          "version": "2.6.2",
          "environment": "browser"
        }
      }
    }
  ]
}
```

[更多詳情](../rendering-personalization-content.md)

## 如何請求且不會自動轉譯頁面載入Target選件

### 使用at.js

有兩種方法可以觸發對Target Edge的呼叫，該呼叫會擷取選件以供頁面載入。

範例 1：

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox", 
   success: console.log,
   error: console.error
});
```

範例 2：

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

[了解更多](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html)

### 使用Web SDK

在`decisionScopes`下執行具有特殊領域的`sendEvent`命令： `__view__`。 我們使用此範圍當作訊號，從Target擷取所有頁面載入活動，並預先擷取所有檢視。 Web SDK也會嘗試評估所有VEC檢視型活動。 Web SDK目前不支援停用檢視預先擷取。

若要存取任何個人化內容，您可以提供回呼函式，SDK從伺服器收到成功回應後，就會呼叫此函式。 系統會為您的回呼提供結果物件，其中可能包含包含任何傳回之個人化內容的建議屬性。

範例：

```javascript
alloy("sendEvent", {
    xdm: {...},
    decisionScopes: ["__view__"]
  }).then(function(result) {
    if (result.propositions) {
      result.propositions.forEach(proposition => {
        proposition.items.forEach(item => {
          if (item.schema === HTML_SCHEMA) {
            // manually apply offer
            document.getElementById("form-based-offer-container").innerHTML =
              item.data.content;
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
          // manually send the display notification event, so that Target/Analytics impressions aare increased
            alloy("sendEvent",{
              "xdm": {
                "eventType": "decisioning.propositionDisplay",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          }
        });
      });
    }
  });
```

[更多詳情](../rendering-personalization-content.md#manually-rendering-content)


## 如何請求特定的表單式Target mbox


### 使用at.js

您可以使用`getOffer`函式擷取表單式撰寫器活動：

範例 1：

```javascript
adobe.target.getOffer({
   mbox: "hero-banner", 
   success: console.log,
   error: console.error
});
```

範例 2：

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        mboxes: [
        {
          index: 0,
          name: "hero-banner"
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

[了解更多](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/cmp-atjs-functions.html)


### 使用Web SDK

您可以使用`sendEvent`命令並將mbox名稱傳遞至`decisionScopes`選項下，擷取表單式撰寫器式活動。 `sendEvent`命令將傳回Promise，此承諾會以包含所請求活動/主張的物件來解析：
這是`propositions`陣列的外觀：

```javascript
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
      }
    },
    "items": [
      {
        "id": "1184844",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434689",
          "experience.id": "0",
          "activity.name": "a4t test form based activity",
          "offer.id": "1184844",
          "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
        },
        "data": {
          "id": "1184844",
          "format": "text/html",
          "content": "<div> analytics impressions </div>"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg=="
      }
    },
    "items": [
      {
        "id": "434689",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  }
]
```

範例：

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];
        if (item.schema === HTML_SCHEMA) {
          // apply offer
          document.getElementById("form-based-offer-container").innerHTML =
            item.data.content;
          const executedPropositions = [
            {
              id: proposition.id,
              scope: proposition.scope,
              scopeDetails: proposition.scopeDetails
            }
          ];

          alloy("sendEvent", {
            "xdm": {
              "eventType": "decisioning.propositionDisplay",
              "_experience": {
                "decisioning": {
                  "propositions": executedPropositions
                }
              }
            }
          });
        }
      }
    }
  }
});
```

[更多詳情](../rendering-personalization-content.md#manually-rendering-content)

## 如何套用Target活動

### 使用at.js

您可以使用`applyOffers`函式套用Target活動： `adobe.target.applyOffer(options)`

範例：

```javascript
adobe.target.getOffers({...})
  .then(response => adobe.target.applyOffers({ response: response }))
  .then(() => console.log("Success"))
  .catch(error => console.log("Error", error));
```

從[專屬檔案](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-applyoffers-atjs-2.html)進一步瞭解`applyOffers`命令。


### 使用Web SDK

您可以使用`applyPropositions`命令套用Target活動。

範例：

```javascript
alloy("applyPropositions", {
    propositions: [...]
});
```

從[專屬檔案](../../personalization/rendering-personalization-content.md#applypropositions)進一步瞭解`applyPropositions`命令。

## 如何追蹤事件

### 使用at.js

您可以使用`trackEvent`函式或使用`sendNotifications`來追蹤事件。

此函式會引發要求來報告使用者動作，例如點按和轉換。 它不會在回應中傳遞活動。


**範例1**

```javascript
adobe.target.trackEvent({ 
    "type": "click",
    "mbox": "some-mbox"
});
```

**範例2**

```javascript
adobe.target.sendNotifications({ 
    request: {
       notifications: [{
          ...,
          mbox: {
            name: "some-mbox"
          },
          type: "click",
          ...
       }]
    }
});
```

[了解更多](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-trackevent.html)

### 使用Web SDK

您可以呼叫`sendEvent`命令、填入`_experience.decisioning.propositions` XDM欄位群組，並將`eventType`設定為2個值中的其中一個來追蹤事件和使用者動作：

* `decisioning.propositionDisplay`：代表Target活動的轉譯。
* `decisioning.propositionInteract`：代表使用者與活動的互動，例如滑鼠點按。

`_experience.decisioning.propositions` XDM欄位群組是物件陣列。 每個物件的屬性衍生自`sendEvent`命令中傳回的`result.propositions`： `{ id, scope, scopeDetails }`

**範例1 — 呈現活動後追蹤`decisioning.propositionDisplay`事件**

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['discount']
}).then(function(result) {
  var propositions = result.propositions;

  var discountProposition;
  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      if (proposition.scope === "discount") {
        discountProposition = proposition;
        break;
      }
    }
  }

  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        var discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a single place to update in the HTML.
        break;  
      }
    }
      // Send a "decisioning.propositionDisplay" event signaling that the proposition has been rendered.
    alloy("sendEvent", {
      xdm: {
        eventType: "decisioning.propositionDisplay",
        _experience: {
          decisioning: {
            propositions: [
              {
                id: discountProposition.id,
                scope: discountProposition.scope,
                scopeDetails: discountProposition.scopeDetails
              }
            ]
          }
        }
      }
    });
  }
});
```

**範例2 — 發生點選量度後追蹤`decisioning.propositionInteract`事件**

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items.length; j++) {
        var item = proposition.items[j];

        if (item.schema === "https://ns.adobe.com/personalization/measurement") {
          // add metric to the DOM element
          const button = document.getElementById("form-based-click-metric");

          button.addEventListener("click", event => {
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
            // send the click track event
            alloy("sendEvent", {
              "xdm": {
                "eventType": "decisioning.propositionInteract",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          });
        }
      }
    }
  }
});
```

[更多詳情](../rendering-personalization-content.md#manually-rendering-content)

**範例3 — 追蹤執行動作後引發的事件**

此範例會追蹤在執行特定動作（例如按一下按鈕）後引發的事件。
您可以透過`__adobe.target`資料物件新增任何其他自訂引數。

```js
//replicates an at.js trackEvent call
alloy("sendEvent", {
    "type": "decisioning.propositionDisplay",
    "xdm": {
        "_experience": {
            "decisioning": {
                "propositions": [{
                    "scope": "sumbitButtonClick" // Or any mbox/location name you want to use in Adobe Target
                }]
            }
        }
    }
});
```

## 如何在單頁應用程式中觸發檢視變更

### 使用at.js

使用`adobe.target.triggerView`函式。 每當新頁面載入或頁面上的元件重新呈現時，就可呼叫此函式。 應該為單頁應用程式(SPA)實作adobe.target.triggerView()，以便使用視覺化體驗撰寫器(VEC)來建立A/B測試和體驗鎖定目標(XT)活動。 如果網站上未實作adobe.target.triggerView()，VEC就無法用於SPA。

**範例**

```javascript
adobe.target.triggerView("homeView")
```

[了解更多](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-triggerview-atjs-2.html)


### 使用Web SDK

若要觸發或表示單頁應用程式檢視變更，請在`sendEvent`命令的`xdm`選項下設定`web.webPageDetails.viewName`屬性。 Web SDK將會檢查檢視快取，如果`sendEvent`中指定的`viewName`有選件，SDK將會執行這些選件並傳送顯示通知事件。

**範例**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  xdm:{
    web:{
      webPageDetails:{
        viewName: "homeView"
      }
    }
  }
});
```

[更多詳情](./spa-implementation.md#implementing-xdm-views)

## 如何運用回應Token

從Adobe Target傳回的Personalization內容包含[回應Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)，其為有關活動、選件、體驗、使用者設定檔、地理資訊等的詳細資料。 這些詳細資料可與協力廠商工具共用或用於偵錯。 回應Token可在Adobe Target使用者介面中設定。

### 使用at.js

使用at.js自訂事件接聽Target回應並讀取回應Token。

**範例**

```javascript
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(e) { 
  console.log("Request succeeded", e.detail); 
}); 
```

[了解更多](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)


### 使用Web SDK

>[!IMPORTANT]
>
>確保您使用Platform Web SDK 2.6.0版或更新版本。

回應Token是`propositions`的一部分，在`sendEvent`命令的結果中顯示。 每個主張包含陣列`items`，而且如果在Target管理員UI中啟用回應Token，則每個專案都會填入`meta`物件。 [了解更多](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)

**範例**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Format of result.propositions:
      /*
        [
            {
                "id": "",
                "scope": "",
                "items": [
                    {
                        "id": "",
                        "schema": "",
                        "data": {},
                        "meta": { // RESPONSE TOKENS
                            "activity.name": ...,
                            "offer.id": ...,
                            "profile.activeActivities": ...
                        }
                    }
                ],
                "scopeDetails": {}
                "renderAttempted": false
            }
        ]
      */
    }
  });
```

[更多詳情](./accessing-response-tokens.md)

## 如何管理忽隱忽現情形

### 使用at.js

使用at.js時，您可以設定`bodyHidingEnabled: true`來管理忽隱忽現的情形，讓at.js妥善處理
在擷取及套用DOM變更之前，預先隱藏個人化容器。
可以覆寫at.js `bodyHiddenStyle`，預先隱藏包含個人化內容的頁面區段。
依預設，`bodyHiddenStyle`會隱藏整個HTML`body`。
可使用`window.targetGlobalSettings`覆寫這兩個設定。 載入at.js之前應先放置`window.targetGlobalSettings`。

### 使用Web SDK

客戶可以使用Web SDK，在configure命令中設定其預先隱藏樣式，如下列範例所示：

```javascript
alloy("configure", {
  datastreamId: "configurationId",
  orgId: "orgId@AdobeOrg",
  debugEnabled: true,
  prehidingStyle: "body { opacity: 0 !important }"
});
```

非同步載入Web SDK時，建議在插入Web SDK之前，先在頁面中插入下列程式碼片段：

```html
<script>
  !function(e,a,n,t){
  if (a) return;
  var i=e.head;if(i){
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
  setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

## 如何處理A4T

### 使用at.js

使用at.js支援兩種A4T記錄：

* Analytics使用者端記錄
* Analytics伺服器端記錄

#### Analytics使用者端記錄

**範例1：使用Target全域設定**

可透過在at.js設定中設定`analyticsLogging: client_side`或覆寫`window.targetglobalSettings`物件來啟用Analytics使用者端記錄。
設定此選項時，傳回的裝載格式如下所示：

```json
{
  "analytics": {
    "payload": {
      "pe": "tnt",
      "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
    }
  }
}
```

接著，裝載可透過資料插入API轉送至Analytics。

範例2：在每個`getOffers`函式中進行設定：

```javascript
adobe.target.getOffers({
      request: {
        experienceCloud: {
          analytics: {
            logging: "client_side"
          }
        },
        prefetch: {
          mboxes: [{
            index: 0,
            name: "a1-serverside-xt"
          }]
        }
      }
    })
    .then(console.log)
```

此為回應裝載的外觀：

```json
{
  "prefetch": {
    "mboxes": [{
      "index": 0,
      "name": "a1-serverside-xt",
      "options": [{
        "content": "<img src=\"http://s7d2.scene7.com/is/image/TargetAdobeTargetMobile/L4242-xt-usa?tm=1490025518668&fit=constrain&hei=491&wid=980&fmt=png-alpha\"/>",
        "type": "html",
        "eventToken": "n/K05qdH0MxsiyH4gX05/2qipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
        "responseTokens": {
          "profile.memberlevel": "0",
          "geo.city": "bucharest",
          "activity.id": "167169",
          "experience.name": "USA Experience",
          "geo.country": "romania"
        }
      }],
      "analytics": {
        "payload": {
          "pe": "tnt",
          "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
        }
      }
    }]
  }
}
```

Analytics裝載(`tnta` Token)應包含在使用[資料插入API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)的Analytics點選中。

#### Analytics伺服器端記錄

可透過在at.js設定中設定`analyticsLogging: server_side`或覆寫`window.targetglobalSettings`物件來啟用Analytics伺服器端記錄。
然後資料會以下列方式流動：

![顯示Analytics伺服器端記錄工作流程的圖表](assets/a4t-server-side-atjs.png)

[了解更多](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html)

### 使用Web SDK

Web SDK也支援：

* Analytics使用者端記錄
* Analytics伺服器端記錄

#### Analytics使用者端記錄

在該DataStream設定中停用Adobe Analytics時，會啟用Analytics使用者端記錄。

![顯示Analytics使用者端記錄工作流程的圖表](assets/analytics-disabled-datastream-config.png)

客戶有權存取需要使用[資料插入API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)與Analytics共用的Analytics權杖(`tnta`)
以鏈結`sendEvent`命令的方式加入，並逐一檢視產生的主張陣列。

**範例**

```javascript
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function (results) {
  var analyticsPayloads = new Set();
  for (var i = 0; i < results.propositions.length; i++) {
    var proposition = results.propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getAnalyticsPayload(proposition);
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // send the page view Analytics hit with collected Analytics payload using Data Insertion API
});
```

下圖顯示啟用Analytics Client Side時資料的流程：

![Analytics使用者端記錄中的資料流程圖](assets/analytics-client-side-logging.png)

#### Analytics伺服器端記錄

為該DataStream設定啟用Analytics時，便會啟用Analytics伺服器端記錄。

![顯示Analytics設定的Datastreams UI。](assets/analytics-enabled-datastream-config.png)

啟用伺服器端Analytics記錄時，需要與Analytics共用的A4T裝載，以便Analytics報告顯示
在Edge Network層級共用正確的曝光和轉換，因此客戶不需要執行任何其他處理。

以下是啟用伺服器端Analytics記錄時，資料如何流入我們的系統：

![顯示伺服器端Analytics記錄中的資料流的圖表](assets/analytics-server-side-logging.png)

## 如何設定Target全域設定

### 使用at.js

您可以使用`window.targetGlobalSettings`覆寫at.js資料庫中的設定，而非在Target Standard/Premium UI中或使用REST API進行設定。

覆寫應在載入at.js之前或在「管理>實作>編輯at.js設定>程式碼設定>資料庫標題」中定義。

範例：

```javascript
window.targetGlobalSettings = {  
   timeout: 200, // using custom timeout  
   visitorApiTimeout: 500, // using custom API timeout  
   enabled: document.location.href.indexOf('https://www.adobe.com') >= 0 // enabled ONLY on adobe.com  
};
```

[了解更多](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html)

### 使用Web SDK

Web SDK不支援此功能。

## 如何更新Target設定檔屬性

### 使用at.js

**範例1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "profile.name": "test",
     "profile.gender": "female"
   },
   success: console.log,
   error: console.error
});
```

**範例2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          profileParameters: {
            name: "test",
            gender: "female"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

### 使用Web SDK

若要更新Target設定檔，請使用`sendEvent`命令並設定`data.__adobe.target`屬性，並使用`profile`加上索引鍵名稱的前置詞。

**範例**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## 如何使用Target Recommendations

### 使用at.js

**範例1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "entity.name": "T-shirt",
     "entity.id": "1234"
   },
   success: console.log,
   error: console.error
});
```

**範例2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          parameters: {
            "entity.name": "T-shirt",
            "entity.id": "1234"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

[了解更多](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-getoffers-atjs-2.html)


### 使用Web SDK

若要傳送Recommendation資料，請使用`sendEvent`命令並設定`data.__adobe.target`屬性，使用`entity`為索引鍵名稱加上前置詞。

**範例**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.name": "T-shirt",
        "entity.id": "1234"
      }
    }
  }
});
```

## 如何使用第三方ID

### 使用at.js

使用at.js有多種傳送`mbox3rdPartyId`的方式，可使用`getOffer`或`getOffers`：

**範例1**

```javascript
adobe.target.getOffer({
  mbox:"test",
  params:{
    "mbox3rdPartyId": "1234"
  },
  success: console.log,
  error: console.error
});
```

**範例2**

```javascript
adobe.target.getOffers({
    request: {
      id:{
        thirdPartyId: "1234"
      },
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

或者，有方法可在`targetPageParams`或`targetPageParamsAll`中設定`mbox3rdPartyId`。
在`targetPageParams`中設定時，會以`target-global-mbox` （也稱為`pag-lLoad`）的要求傳送它。
建議將使用`targetPageParamsAll`設定，因為它將在每個目標請求中傳送。
使用`targetPageParamsAll`的優點在於您可以在頁面上定義一次`mbox3rdPartyId`，這將確保所有目標請求都有正確的`mbox3rdPartyId`。

```javascript
window.targetPageParamsAll = function() {
      return {
        "mbox3rdPartyId": "1234"
      };
    };
```

```javascript
window.targetPageParams = function() {
  return {
    "mbox3rdPartyId": "1234"
  };
};
```

[了解更多](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetpageparams.html)

### 使用Web SDK

Web SDK支援Target協力廠商ID。 不過，還需要執行幾個步驟。 在深入研究解決方案之前，我們應該先談談`identityMap`。
身分對應可讓客戶傳送多個身分。 所有身分識別都已設定名稱空間。 每個名稱空間可以有一或多個身分。 特定身分可以標示為主要身分。
有了這些知識，我們就可以瞭解設定Web sdk以使用Target第三方ID的必要步驟。

1. 設定在資料流設定頁面中包含Target第三方ID的名稱空間：

![顯示Target第三方ID名稱空間欄位的Datastreams UI](assets/mbox-3-party-id-setup.png)

1. 在每個sendEvent命令中傳送該身分名稱空間，如下所示：

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "identityMap": {
      "TGT3PID": [
        {
          "id": "1234",
          "primary": true
        }
      ]
    }
  }
});
```

## 如何設定屬性代號

### 使用at.js

使用at.js有兩種方法可設定屬性代號：使用`targetPageParams`或`targetPageParamsAll`。 使用`targetPageParams`會將屬性權杖新增至`target-global-mbox`呼叫，但使用`targetPageParamsAll`會將權杖新增至所有目標呼叫：

**範例1**

```javascript
   window.targetPageParamsAll = function() {
      return {
        "at_property": "1234"
      };
    };
```

**範例2**

```javascript
window.targetPageParams = function() {
      return {
        "at_property": "1234"
      };
    };
```

### 使用Web SDK

使用Web SDK，客戶在設定Adobe Target名稱空間下的資料流設定時，可以在更高層級設定屬性：
![顯示Adobe Target設定的Datastreams UI。](assets/at-property-setup.png)
這表示該特定資料流設定的每個Target呼叫都將包含該屬性Token。

## 如何預先擷取mbox

### 使用at.js

此功能僅適用於at.js 2.x。 at.js 2.x有一個名為`getOffers`的新函式。 `getOffers`允許客戶預先擷取一或多個mbox的內容。 其範例如下：

```javascript
adobe.target.getOffers({
    request: {
      prefetch: {
        mboxes: [{
          index: 0,
          name: "test-mbox",
          parameters: {
            ...
          },
          profileParameters: {
            ...
          }
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

注意：強烈建議確保`mboxes`陣列中的每個`mbox`都有自己的索引。 通常第一個mbox有`index=0`、下一個`index=1`等。

### 使用Web SDK

Web SDK目前不支援此功能。

## 如何為Target實作除錯

### 使用at.js

At.js會公開這些偵錯功能：

* Mbox停用 — 停用Target的擷取和轉譯功能，以檢查頁面是否損毀，而不進行Target互動
* Mbox除錯 — at.js會記錄每個動作
* 目標追蹤 — 在Bullseye中產生mbox追蹤權杖時，`window.___target_trace`物件下可以使用包含參與決策程式之詳細資訊的追蹤物件

注意：所有這些偵錯功能都可以在[Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)的增強功能中使用

### 使用Web SDK

使用Web SDK時，您擁有多項偵錯功能：

* 使用[保證](/help/assurance/home.md)
* [Web SDK偵錯已啟用](/help/web-sdk/use-cases/debugging.md)
* 使用[Web SDK監視掛接](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)
* 使用[Adobe Experience Platform Debugger](/help/debugger/home.md)
* 目標追蹤
