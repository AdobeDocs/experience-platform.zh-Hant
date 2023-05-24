---
title: 使用Adobe Experience PlatformWeb SDK呈現個性化內容
description: 瞭解如何使用Adobe Experience PlatformWeb SDK呈現個性化內容。
keywords: 個性化；renderDecisions;sendEvent;decisionScopes；命題；
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: c75a8bdeaba67259b5f4b4ce025d5e128d763040
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 2%

---

# 呈現個性化內容

Adobe Experience PlatformWeb SDK支援從Adobe個性化解決方案檢索個性化內容，包括 [Adobe Target](https://business.adobe.com/products/target/adobe-target.html)。 [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=zh-Hant) 和 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=zh-Hant)。

此外，Web SDK還通過Adobe Experience Platform個性化目標(如 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 和 [自定義個性化連接](../../destinations/catalog/personalization/custom-personalization.md)。 要瞭解如何為同頁和下一頁個性化配置Experience Platform，請參閱 [專用指南](../../destinations/ui/configure-personalization-destinations.md)。

在Adobe Target內建立的內容 [視覺體驗作曲家](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) 和Adobe Journey Optimizer [Web市場活動UI](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) 可由SDK自動檢索和呈現。 在Adobe Target內建立的內容 [基於表單的體驗作曲家](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) 或SDK無法自動呈現Offer decisioning。 相反，您必須使用SDK請求此內容，然後自行手動呈現該內容。

## 自動呈現內容

向伺服器發送事件時，可以設定 `renderDecisions` 選項 `true`。 這樣做會強制SDK自動呈現任何符合自動呈現條件的個性化內容。

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

呈現個性化內容是非同步的，因此您不應對特定內容何時完成呈現做出假設。

## 手動呈現內容

要訪問任何個性化內容，您可以提供回調函式，該函式將在SDK從伺服器收到成功響應後調用。 您的回叫已提供 `result` 對象，它可能包含 `propositions` 包含任何返回的個性化內容的屬性。 下面是在發送事件時如何提供回調函式的示例。

```javascript
alloy("sendEvent", {
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

在本例中， `result.propositions`，如果存在，則是包含與事件相關的個性化建議的陣列。 預設情況下，它只包括符合自動渲染條件的主張。

的 `propositions` array可能與此示例類似：

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

在示例中， `renderDecisions` 選項未設定為 `true` 當 `sendEvent` 命令已執行，因此SDK未嘗試自動呈現任何內容。 但是，SDK仍會自動檢索符合自動呈現條件的內容，並將此內容提供給您以便手動呈現（如果您願意）。 請注意，每個命題對象 `renderAttempted` 屬性設定為 `false`。

如果您 `renderDecisions` 選項 `true` 在發送事件時，SDK會嘗試提供符合自動呈現條件的任何主張（如前所述）。 因此，每個命題對象都會 `renderAttempted` 屬性設定為 `true`。 在本例中，不需要手動提出這些建議。

到目前為止，我們只討論了符合自動呈現條件的個性化內容(即在Adobe Target的Visual Experience Composer或Adobe Journey Optimizer的Web Campaign UI中建立的任何內容)。 檢索任何個性化內容 _不_ 符合自動呈現條件，您需要通過填充內容來請求內容 `decisionScopes` 選項。 範圍是一個字串，用於標識要從伺服器中檢索的特定命題。

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

在本示例中，如果在與 `salutation` 或 `discount` 範圍，返回並包含在 `result.propositions` 陣列。 請注意，符合自動渲染條件的主張將繼續包含在 `propositions` 陣列，無論您如何配置 `renderDecisions` 或 `decisionScopes` 頁籤 的 `propositions` 在本例中，array與以下示例類似：

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

此時，您可以根據您所認為的適合情況呈現命題內容。 在本例中，與 `discount` scope是使用Adobe Target基於表單的體驗作曲家構建的HTML命題。 假設您的頁面上有一個ID為 `daily-special` 並希望從 `discount` 建議 `daily-special` 元素，執行以下操作：

1. 從 `result` 的雙曲餘切值。
1. 循環查看每個命題，查找包含 `discount`。
1. 如果您找到一個建議，請循環查看建議中的每個項目，查找HTML內容的項目。 （檢查總比假設好。）
1. 如果找到包含HTML內容的項目，請查找 `daily-special` 元素，並將其HTML替換為個性化內容。
1. 在呈現內容後，發送 `display` 的子菜單。

您的代碼如下所示：

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
>如果使用Adobe Target，作用域與伺服器上的框相對應，但它們都是一次性請求的，而不是單獨請求的。 全局框始終返回。

### 管理閃爍

SDK提供了 [管理閃爍](../personalization/manage-flicker.md) 在個性化過程中。

## 在單頁應用程式中呈現主張，而不增加度量 {#applypropositions}

的 `applyPropositions` 命令允許您呈現或執行命題陣列 [!DNL Target] 到單頁應用程式，而不增加 [!DNL Analytics] 和 [!DNL Target] 度量。 這提高了報告的準確性。

>[!IMPORTANT]
>
>如果 `__view__` 範圍（或Web曲面）在頁面載入、其 `renderAttempted` 標誌將設定為 `true`。 的 `applyPropositions` 命令不會重新呈現 `__view__` 範圍（或Web曲面）命題 `renderAttempted: true` 。

### 用例1:重新呈現單頁應用程式視圖主張

下面的示例中描述的使用案例將重新呈現先前提取和呈現的購物車視圖主張，而不發送顯示通知。

在下面的示例中， `sendEvent` 命令在視圖更改時觸發，並將生成的對象保存為常數。

接下來，當視圖或元件更新時， `applyPropositions` 命令被調用，其命題來自 `sendEvent` 命令，以重新呈現視圖主題。

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

### 用例2:呈現沒有選擇器的命題

此使用案例適用於使用 [!DNL Target Form-based Experience Composer]。

必須在 `applyPropositions` 呼叫。

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

如果沒有為決策範圍提供元資料，則不會呈現相關建議。
