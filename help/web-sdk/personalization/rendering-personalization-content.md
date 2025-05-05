---
title: 使用Adobe Experience Platform Web SDK呈現個人化內容
description: 瞭解如何使用Adobe Experience Platform Web SDK呈現個人化內容。
keywords: 個人化；renderDecisions；sendEvent；decisionScopes；主張；
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 9489b5345c2b13b9d05b26d646aa7f1576840fb8
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---

# 呈現個人化內容

Adobe Experience Platform Web SDK支援從Adobe個人化解決方案擷取個人化內容，包括[Adobe Target](https://business.adobe.com/products/target/adobe-target.html)、[Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=zh-Hant)和[Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=zh-Hant)。

此外，Web SDK透過Adobe Experience Platform個人化目的地(例如[Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md)和[自訂個人化連線](../../destinations/catalog/personalization/custom-personalization.md))，提供相同頁面和下一頁個人化功能。 若要瞭解如何設定相同頁面和下一頁個人化的Experience Platform，請參閱[專屬指南](../../destinations/ui/activate-edge-personalization-destinations.md)。

SDK可自動擷取及轉譯在Adobe Target的[視覺化體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=zh-Hant)及Adobe Journey Optimizer的[Web Campaign UI](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=zh-Hant)中建立的內容。 在Adobe Target的[表單式體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=zh-Hant)、Adobe Journey Optimizer的[程式碼式體驗管道](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/code-based-experience/get-started-code-based)或Offer decisioning中建立的內容，無法由SDK自動轉譯。 相反地，您必須使用SDK請求此內容，然後自行手動轉譯內容。

## 自動呈現內容 {#automatic}

將事件傳送至伺服器時，您可以將`renderDecisions`選項設為`true`。 這麼做會強制SDK自動轉譯任何符合自動轉譯條件的個人化內容。

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

個人化內容的呈現是非同步的，因此您不應就特定內容何時將完成呈現做出假設。

## 手動呈現內容 {#manual}

若要存取任何個人化內容，您可以提供回呼函式，SDK從伺服器收到成功回應後，就會呼叫此函式。 您的回呼提供了一個`result`物件，其中可能包含包含任何傳回的個人化內容的`propositions`屬性。 以下範例說明在傳送事件時，如何提供回呼函式。

```javascript
alloy("sendEvent", {
    "xdm": {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

在此範例中，`result.propositions` （如果存在）是包含與事件相關之個人化主張的陣列。 依預設，它僅包含符合自動演算資格的主張。

`propositions`陣列可能類似於以下範例：

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

在範例中，執行`sendEvent`命令時，`renderDecisions`選項未設為`true`，因此SDK不會嘗試自動轉譯任何內容。 不過，SDK仍會自動擷取符合自動轉譯條件的內容，並會在您想要這麼做時，提供此內容給您以手動轉譯。 請注意，每個主張物件的`renderAttempted`屬性都設定為`false`。

如果您在傳送事件時改為將`renderDecisions`選項設為`true`，SDK就會嘗試轉譯任何符合自動轉譯資格的建議（如先前所述）。 因此，每個主張物件都會將其`renderAttempted`屬性設定為`true`。 在此情況下，不需要手動轉譯這些主張。

到目前為止，我們僅討論適用於自動轉譯的個人化內容(亦即在Adobe Target的視覺化體驗撰寫器或Adobe Journey Optimizer的Web Campaign UI中建立的任何內容)。 若要擷取任何符合自動轉譯資格的個人化內容&#x200B;__，您必須在傳送事件時填入`decisionScopes`選項來要求內容。 範圍是字串，可識別您要從伺服器擷取的特定主張。

其範例如下：

```javascript
alloy("sendEvent", {
    "xdm": {},
    "decisionScopes": ['salutation', 'discount']
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

在此範例中，如果在符合`salutation`或`discount`範圍的伺服器上找到主張，則會傳回它們並包含在`result.propositions`陣列中。 請注意，無論如何設定`renderDecisions`或`decisionScopes`選項，符合自動轉譯資格的主張仍會繼續包含在`propositions`陣列中。 在此案例中，`propositions`陣列看起來與此範例類似：

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

此時，您可以視需要演算主張內容。 在此範例中，符合`discount`範圍的主張是使用Adobe Target的表單式體驗撰寫器建立的HTML主張。 假設您的頁面上有一個識別碼為`daily-special`的元素，且您想要將內容從`discount`主張轉譯為`daily-special`元素，請執行下列動作：

1. 從`result`物件擷取主張。
1. 重複每個主張，尋找範圍為`discount`的主張。
1. 如果您找到主張，會在主張中的每個專案中進行回圈，尋找是HTML內容的專案。 （檢查勝於假設）。
1. 如果您找到包含HTML內容的專案，請在頁面上找到`daily-special`元素，並以個人化內容取代其HTML。
1. 呈現內容之後，傳送`display`事件。

您的程式碼如下所示：

```javascript
alloy("sendEvent", {
  "xdm": {},
  "decisionScopes": ['salutation', 'discount']
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
      "xdm": {
        "eventType": "decisioning.propositionDisplay",
        "_experience": {
          "decisioning": {
            "propositions": [
              {
                "id": discountProposition.id,
                "scope": discountProposition.scope,
                "scopeDetails": discountProposition.scopeDetails
              }
            ],
            "propositionEventType": {
              "display": 1
            }
          }
        }
      }
    });
  }
});
```


>[!TIP]
>
>如果您使用Adobe Target，領域會對應至伺服器上的mbox，只是所有領域會一次要求完成，而非個別要求。 一律會傳回全域mbox。

### 管理忽隱忽現情形

SDK提供在個人化程式期間[管理忽隱忽現情況的工具](../personalization/manage-flicker.md)。

## 在不增加量度的情況下在單頁應用程式中轉譯主張 {#applypropositions}

`applyPropositions`命令可讓您將[!DNL Target]或Adobe Journey Optimizer中的主張陣列轉譯或執行為單頁應用程式，而不增加[!DNL Analytics]和[!DNL Target]量度。 這會提高報表的正確性。

>[!IMPORTANT]
>
>如果`__view__`範圍（或網頁表面）的建議在頁面載入時轉譯，其`renderAttempted`標幟將設定為`true`。 `applyPropositions`命令將不會重新呈現具有`renderAttempted: true`旗標的`__view__`領域（或網頁表面）主張。

### 使用案例1：重新呈現單頁應用程式檢視主張

下列範例中說明的使用案例會重新呈現先前擷取和轉譯的購物車檢視主張，而不會傳送顯示通知。

在下列範例中，`sendEvent`指令會在檢視變更時觸發，並將產生的物件儲存為常數。

接著，當檢視或元件更新時，會使用先前`sendEvent`命令中的主張呼叫`applyPropositions`命令，以重新呈現檢視主張。

```js
var cartPropositions = alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
        "web": {
            "webPageDetails": {
                "viewName": "cart"
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
    "propositions": cartPropositions
});
```

### 使用案例2：沒有選擇器的演算主張

此使用案例適用於使用[!DNL Target Form-based Experience Composer]或Adobe Journey Optimizer的[程式碼型體驗管道](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/code-based-experience/get-started-code-based)所編寫的體驗。

您必須在`applyPropositions`呼叫中提供選取器、動作和範圍。

支援的`actionTypes`為：

* `setHtml`
* `replaceHtml`
* `appendHtml`

```js
// Retrieve propositions for salutation and discount scopes
alloy("sendEvent", {
    "decisionScopes": ["salutation", "discount"]
}).then(function(result) {
    var retrievedPropositions = result.propositions;
    // Render propositions on the page by providing additional metadata

    return alloy("applyPropositions", {
        "propositions": retrievedPropositions,
        "metadata": {
            "salutation": {
                "selector": "#first-form-based-offer",
                "actionType": "setHtml"
            },
            "discount": {
                "selector": "#second-form-based-offer",
                "actionType": "replaceHtml"
            }
        }
    }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
        function sendDisplayEvent(proposition) {
            const {
                id,
                scope,
                scopeDetails = {}
            } = proposition;

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
    });
});
```

如果您沒有為決定範圍提供中繼資料，將不會轉譯關聯的提議。
