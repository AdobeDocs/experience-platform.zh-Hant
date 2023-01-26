---
title: 使用Adobe Experience Platform Web SDK轉譯個人化內容
description: 了解如何使用Adobe Experience Platform Web SDK轉譯個人化內容。
keywords: 個人化；renderDecisions;sendEvent;decisionScopes；命題；
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: c75a8bdeaba67259b5f4b4ce025d5e128d763040
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 2%

---

# 轉譯個人化內容

Adobe Experience Platform Web SDK支援從Adobe個人化解決方案擷取個人化內容，包括 [Adobe Target](https://business.adobe.com/products/target/adobe-target.html), [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=zh-Hant) 和 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=zh-Hant).

此外，Web SDK可透過Adobe Experience Platform個人化目的地(例如 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 和 [自訂個人化連線](../../destinations/catalog/personalization/custom-personalization.md). 若要了解如何為同一頁和下一頁個人化設定Experience Platform，請參閱 [專屬指南](../../destinations/ui/configure-personalization-destinations.md).

在Adobe Target中建立的內容 [可視化體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) 和Adobe Journey Optimizer [網頁行銷活動UI](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) 可由SDK自動擷取及呈現。 在Adobe Target中建立的內容 [表單式體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) 或Offer decisioning無法由SDK自動轉譯。 請改為使用SDK要求此內容，然後自行手動轉譯內容。

## 自動轉譯內容

將事件傳送至伺服器時，您可以設定 `renderDecisions` 選項 `true`. 這麼做會強制SDK自動轉譯任何符合自動轉譯資格的個人化內容。

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

呈現個人化內容為非同步，因此您不應就特定內容片段何時會完成呈現做出假設。

## 手動轉譯內容

若要存取任何個人化內容，您可提供回撥函式，此函式將在SDK收到來自伺服器的成功回應後呼叫。 您的回呼會提供 `result` 對象，可包含 `propositions` 包含任何傳回的個人化內容的屬性。 以下範例說明您在傳送事件時如何提供回呼函式。

```javascript
alloy("sendEvent", {
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

在此範例中， `result.propositions`，如果存在，則是包含與事件相關的個人化主張的陣列。 預設情況下，它只包含適合自動呈現的主張。

此 `propositions` 陣列看起來可能類似於以下範例：

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      ...
    },
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      ...
    },
    "renderAttempted": false
  }
]
```

在範例中， `renderDecisions` 選項未設為 `true` 當 `sendEvent` 命令已執行，因此SDK未嘗試自動轉譯任何內容。 SDK仍會自動擷取符合自動轉譯資格的內容，但是您若想要手動轉譯，則可將此內容提供給您。 請注意，每個主張物件都有 `renderAttempted` 屬性設定為 `false`.

若您已改為設定 `renderDecisions` 選項 `true` 傳送事件時，SDK會嘗試呈現任何符合自動呈現資格的主張（如先前所述）。 因此，每個命題對象都有 `renderAttempted` 屬性設定為 `true`. 在本例中，不需要手動提出這些主張。

到目前為止，我們僅討論適合自動轉譯的個人化內容(亦即在Adobe Target的可視化體驗撰寫器或Adobe Journey Optimizer的網頁促銷活動UI中建立的任何內容)。 擷取任何個人化內容 _not_ 符合自動轉譯的資格，您需要借由填入 `decisionScopes` 選項。 範圍是字串，用於標識要從伺服器中檢索的特定主張。

其範例如下：

```javascript
alloy("sendEvent", {
    xdm: {},
    decisionScopes: ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

在此示例中，如果在與 `salutation` 或 `discount` 範圍，則會傳回並納入 `result.propositions` 陣列。 請注意，符合自動呈現資格的主張將繼續包含在 `propositions` 陣列，無論您如何設定 `renderDecisions` 或 `decisionScopes` 選項。 此 `propositions` 陣列在此案例中看起來類似於此範例：

```json
[
  {
    "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
    "scope": "salutation",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/json-content-item",
        "data": {
          "id": "4433221",
          "content": {
            "salutation": "Welcome, esteemed visitor!"
          }
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:cZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ2",
      "activity": {
        "id": "384456"
      }
    },  
    "renderAttempted": false
  },
  {
    "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
    "scope": "discount",
    "items": [
      {
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "data": {
          "id": "4433222",
          "content": "<div>50% off your order!</div>",
          "format": "text/html"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:FZJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ0",
      "activity": {
        "id": "384457"
      }
    },
    "renderAttempted": false
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "__view__",
    "items": [
      {
        "id": "11223344",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">An HTML proposition.</h2>",
          "selector": "#hero",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
      "activity": {
        "id": "384459"
      }
    },
    "renderAttempted": false
  },
  {
    "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
    "scope": "__view__",
    "items": [
      {
        "id": "11223345",
        "schema": "https://ns.adobe.com/personalization/dom-action",
        "data": {
          "content": "<h2 style=\"color: yellow\">Another HTML proposition.</h2>",
          "selector": "#sidebar",
          "type": "setHtml"
        },
        "meta": {}
      }
    ],
    "scopeDetails": {
      "id": "AT:PyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ8",
      "activity": {
        "id": "384459"
      }
    },
    "renderAttempted": false
  }
]
```

此時，您可以視需要呈現主張內容。 在此範例中，與 `discount` 範圍是使用Adobe Target的表單式體驗撰寫器建立的HTML主張。 假設您的頁面上有一個元素，其ID為 `daily-special` 並想從 `discount` 對 `daily-special` 元素，請執行下列動作：

1. 從 `result` 物件。
1. 重複討論每個主張，並在 `discount`.
1. 如果您找到主張，請重複討論主張中的每個項目，尋找屬於HTML內容的項目。 （檢查好過假設。）
1. 如果您找到包含HTML內容的項目，請尋找 `daily-special` 元素，並以個人化內容取代其HTML。
1. 內容呈現後，請傳送 `display` 事件。

您的程式碼如下所示：

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['salutation', 'discount']
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

  var discountHtml;
  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a signle place to update in the HTML.
        break;  
      }
    }
      // Send a "display" event 
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


>[!TIP]
>
>如果您使用Adobe Target，範圍會對應至伺服器上的mbox，但是所有mbox都會同時請求，而非個別請求。 一律會傳回全域mbox。

### 管理忽隱忽現

SDK提供的設施 [管理忽隱忽現](../personalization/manage-flicker.md) 在個人化過程中。

## 在單頁應用程式中呈現主張，無需增加度量 {#applypropositions}

此 `applyPropositions` 命令允許您呈現或執行 [!DNL Target] 整合至單頁應用程式，而不會增加 [!DNL Analytics] 和 [!DNL Target] 量度。 這會提高報表正確性。

>[!IMPORTANT]
>
>如果 `__view__` 範圍（或網頁表面）是在頁面載入、其 `renderAttempted` 標幟將設為 `true`. 此 `applyPropositions` 命令不會重新呈現 `__view__` 範圍（或web surface）命題 `renderAttempted: true` 標籤。

### 使用案例1:重新呈現單頁應用程式視圖主張

以下範例中說明的使用案例會重新呈現先前擷取和呈現的購物車檢視主張，而不會傳送顯示通知。

在以下範例中， `sendEvent` 在視圖更改時觸發命令，並將生成的對象保存為常數。

接下來，檢視或元件更新時， `applyPropositions` 命令被調用，前面的命令 `sendEvent` 命令，重新呈現視圖主張。

```js
var cartPropositions = alloy("sendEvent", {
    renderDecisions: true,
    xdm: {
        web: {
            webPageDetails: {
                viewName: "cart"
            }
        }
    }
}).then(function(result) {
    var propositions = result.propositions;

    // Collect response tokens, etc.
    return propositions;
});

// Call applyPropositions to re-render the view propositions from the previous sendEvent command.
alloy("applyPropositions", {
    propositions: cartPropositions
});
```

### 使用案例2:提供沒有選擇器的主張

此使用案例適用於使用 [!DNL Target Form-based Experience Composer].

您必須在 `applyPropositions` 呼叫。

支援 `actionTypes` 為：

* `setHtml`
* `replaceHtml`
* `appendHtml`

```js
// Retrieve propositions for salutation and discount scopes
alloy("sendEvent", {
    decisionScopes: ["salutation", "discount"]
}).then(function(result) {
    var retrievedPropositions = result.propositions;
    // Render propositions on the page by providing additional metadata

    return alloy("applyPropositions", {
        propositions: retrievedPropositions,
        metadata: {
            salutation: {
                selector: "#first-form-based-offer",
                actionType: "setHtml"
            },
            discount: {
                selector: "#second-form-based-offer",
                actionType: "replaceHtml"
            }
        }
    }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
        alloy("sendEvent", {
            xdm: {
                eventType: "decisioning.propositionDisplay",
                _experience: {
                    decisioning: {
                        propositions: renderedPropositions
                    }
                }
            }
        });
    });
});
```

如果您沒有提供決策範圍的元資料，則不會呈現相關命題。
