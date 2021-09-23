---
title: 使用Adobe Experience Platform Web SDK轉譯個人化內容
description: 了解如何使用Adobe Experience Platform Web SDK轉譯個人化內容。
keywords: 個人化；renderDecisions;sendEvent;decisionScopes；命題；
exl-id: 6a3252ca-cdec-48a0-a001-2944ad635805
source-git-commit: 0246de5810c632134288347ac7b35abddf2d4308
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 1%

---

# 轉譯個人化內容

Adobe Experience Platform Web SDK支援在Adobe從個人化解決方案擷取個人化內容，包括[Adobe Target](https://business.adobe.com/products/target/adobe-target.html)和[Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=zh-Hant)。 在Adobe Target的[可視化體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)中建立的內容可由SDK自動擷取及轉譯。 在Adobe Target的[表單式體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)或Offer decisioning中建立的內容，無法由SDK自動轉譯。 請改為使用SDK要求此內容，然後自行手動轉譯內容。

## 自動轉譯內容

將事件發送到伺服器時，可將`renderDecisions`選項設定為`true`。 這麼做會強制SDK自動轉譯任何符合自動轉譯資格的個人化內容。

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

若要存取任何個人化內容，您可提供回撥函式，此函式將在SDK收到來自伺服器的成功回應後呼叫。 您的回呼會提供`result`物件，其中可能包含包含任何傳回個人化內容的`propositions`屬性。 以下範例說明您在傳送事件時如何提供回呼函式。

```javascript
alloy("sendEvent", {
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions and send "display" event
    }
  });
```

在此範例中，`result.propositions`（如果存在）是包含與事件相關的個人化主張的陣列。 預設情況下，它只包含適合自動呈現的主張。

`propositions`陣列看起來可能類似於此示例：

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

在範例中，執行`sendEvent`命令時，`renderDecisions`選項未設為`true`，因此SDK不會嘗試自動轉譯任何內容。 SDK仍會自動擷取符合自動轉譯資格的內容，但是您若想要手動轉譯，則可將此內容提供給您。 請注意，每個命題物件的`renderAttempted`屬性都設為`false`。

若您已改為在傳送事件時將`renderDecisions`選項設為`true`,SDK會嘗試呈現任何符合自動呈現資格的主張（如先前所述）。 因此，每個命題對象的`renderAttempted`屬性都設為`true`。 在本例中，不需要手動提出這些主張。

到目前為止，我們僅討論適合自動轉譯的個人化內容(即在Adobe Target的可視化體驗撰寫器中建立的任何內容)。 若要擷取符合自動轉譯資格的任何個人化內容&#x200B;_not_，您必須在傳送事件時填入`decisionScopes`選項，以要求內容。 範圍是字串，用於標識要從伺服器中檢索的特定主張。

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

在此示例中，如果在與`salutation`或`discount`範圍匹配的伺服器上找到了主張，則會返回這些主張並包含在`result.propositions`陣列中。 請注意，無論配置`renderDecisions`或`decisionScopes`選項的方式如何，`propositions`陣列中將繼續包含符合自動呈現資格的命題。 `propositions`陣列在此例中看起來類似於此範例：

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

此時，您可以視需要呈現主張內容。 在此範例中，符合`discount`範圍的主張是使用Adobe Target的表單式體驗撰寫器建置的HTML主張。 假設您的頁面上有ID為`daily-special`的元素，且想將`discount`主張的內容呈現至`daily-special`元素，請執行下列動作：

1. 從`result`對象中提取命題。
1. 循環瀏覽每個主張，以`discount`範圍查找主張。
1. 如果您找到主張，請重複討論主張中的每個項目，尋找屬於HTML內容的項目。 （檢查好過假設。）
1. 如果您找到包含HTML內容的項目，請在頁面上找到`daily-special`元素，並將其HTML取代為個人化內容。
1. 呈現內容後，傳送`display`事件。

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
        eventType: "display",
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
>如果您使用Adobe Target，範圍會對應至伺服器上的mbox，但是所有mbox都會一次請求，而非個別請求。 一律會傳回全域mbox。

### 管理忽隱忽現

SDK提供在個人化程式期間[管理忽隱忽現](../personalization/manage-flicker.md)的工具。
