---
title: Adobe Experience Platform Web SDK擴充功能中的事件類型
description: 了解如何使用Adobe Experience Platform Launch中Adobe Experience Platform Web SDK擴充功能提供的事件類型。
solution: Experience Platform
feature: Web SDK
exl-id: b3162406-c5ce-42ec-ab01-af8ac8c63560
source-git-commit: 8f714933e23e281772cd8633d27096021de14c56
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 1%

---

# 事件類型

本頁說明Adobe Experience Platform Web SDK標籤擴充功能提供的Adobe Experience Platform事件類型。 這些變數會用於[建置規則](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-rules.html)，且不應與XDM](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=zh-Hant)中的[`eventType`欄位混淆。

## [!UICONTROL 傳送事件完成]

通常，您的屬性會有一或多個規則，使用[[!UICONTROL Send event] action](action-types.md#send-event)來傳送事件至Adobe Experience Platform Edge Network。 每次將事件傳送至邊緣網路時，都會傳回回應給包含有用資料的瀏覽器。 若沒有[!UICONTROL 傳送事件complete]事件類型，您就無法存取此傳回的資料。

若要存取傳回的資料，請建立個別規則，然後新增[!UICONTROL 傳送事件complete]事件至規則。 每次從伺服器收到因[!UICONTROL 傳送事件]動作而成功回應時，就會觸發此規則。

當[!UICONTROL 傳送事件complete]事件觸發規則時，它提供從伺服器傳回的資料，這些資料對於完成某些任務可能很有用。 通常，您會將[!UICONTROL 自訂程式碼]動作（來自[!UICONTROL Core]擴充功能）新增至包含[!UICONTROL Send event complete]事件的相同規則。 在[!UICONTROL 自訂程式碼]動作中，您的自訂程式碼將可存取名為`event`的變數。 此`event`變數將包含從伺服器傳回的資料。

處理從邊緣網路傳回資料的規則可能如下所示：

![](./assets/send-event-complete.png)

以下是如何使用此規則中的[!UICONTROL 自訂程式碼]動作執行特定工作的一些範例。

### 手動轉譯個人化內容

在「自訂程式碼」動作（用於處理回應資料的規則）中，您可以存取從伺服器傳回的個人化主張。 若要這麼做，您可輸入下列自訂程式碼：

```javascript
var propositions = event.propositions;
```

如果`event.propositions`存在，則是包含個人化主張物件的陣列。 陣列中包含的主張在很大程度上取決於事件如何發送到伺服器。

對於第一個案例，假設您尚未勾選[!UICONTROL 呈現決策]核取方塊，且未在[!UICONTROL 傳送事件]動作內提供任何[!UICONTROL 決策範圍]，負責傳送事件。

![img.png](assets/send-event-render-unchecked-without-scopes.png)

在此示例中，`propositions`陣列僅包含與事件相關的命題，這些命題適合自動呈現。

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
    "renderAttempted": false
  }
]
```

傳送事件時，未勾選[!UICONTROL 呈現決策]核取方塊，因此SDK不會嘗試自動呈現任何內容。 不過，SDK仍會自動擷取符合自動轉譯資格的內容，並提供給您，供您手動轉譯（如果您想要）。 請注意，每個命題物件的`renderAttempted`屬性都設為`false`。

如果您在傳送事件時已勾選[!UICONTROL 呈現決策]核取方塊，SDK會嘗試呈現任何符合自動呈現資格的主張。 因此，每個命題對象的`renderAttempted`屬性都設為`true`。 在本例中，不需要手動提出這些主張。

到目前為止，您只看過符合自動轉譯資格的個人化內容(例如，在Adobe Target的可視化體驗撰寫器中建立的任何內容)。 若要擷取符合自動轉譯資格的任何個人化內容&#x200B;_not_，請使用[!UICONTROL 傳送事件]動作中的[!UICONTROL 決策範圍]欄位，提供決策範圍以要求內容。 範圍是字串，用於標識要從伺服器中檢索的特定主張。

[!UICONTROL Send event]動作如下所示：

![img.png](assets/send-event-render-unchecked-with-scopes.png)

在此示例中，如果在與`salutation`或`discount`範圍匹配的伺服器上找到了主張，則會返回這些主張並包含在`propositions`陣列中。 請注意，無論如何配置[!UICONTROL Render decisions]或[!UICONTROL Decision scopes][!UICONTROL Send event]操作中的Render decisions欄位，符合自動呈現資格的命題將繼續包含在`propositions`陣列中。 `propositions`陣列在此例中看起來類似於此範例：

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
    "renderAttempted": false
  }
]
```

此時，您可以視需要呈現主張內容。 在此範例中，符合`discount`範圍的主張是使用Adobe Target的表單式體驗撰寫器建立的HTML主張。 假設您的頁面上有一個ID為`daily-special`的元素，並想將`discount`主張中的內容呈現至`daily-special`元素。 請執行下列動作：

1. 從`event`對象中提取命題。
1. 循環瀏覽每個主張，以`discount`範圍查找主張。
1. 如果您找到主張，請重複討論主張中的每個項目，尋找屬於HTML內容的項目。 （檢查好過假設。）
1. 如果您找到包含HTML內容的項目，請在頁面上找到`daily-special`元素，並將其HTML取代為個人化內容。

您在[!UICONTROL 自訂程式碼]動作中的自訂程式碼可能會顯示如下：

```javascript
var propositions = event.propositions;

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
      break;
    }
  }
}

if (discountHtml) {
  // Discount HTML exists. Time to render it.
  var dailySpecialElement = document.getElementById("daily-special");
  dailySpecialElement.innerHTML = discountHtml;
}
```

### 存取Adobe Target回應Token

從Adobe Target傳回的個人化內容包含[回應Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)，這些是關於活動、選件、體驗、使用者設定檔、地理資訊等的詳細資料。 這些詳細資訊可與協力廠商工具共用或用於除錯。 可在Adobe Target使用者介面中設定回應Token。

在「自訂程式碼」動作（用於處理回應資料的規則）中，您可以存取從伺服器傳回的個人化主張。 若要這麼做，請輸入下列自訂程式碼：

```javascript
var propositions = event.propositions;
```

如果`event.propositions`存在，則是包含個人化主張物件的陣列。 如需`result.propositions`內容的詳細資訊，請參閱[手動轉譯個人化內容](#manually-render-personalized-content) 。

假設您想從Web SDK自動呈現的所有主張中收集所有活動名稱，並將其推送至單一陣列。 然後，您可以將單一陣列傳送至第三方。 在此情況下，將[!UICONTROL 自訂程式碼]動作內的自訂程式碼寫入：

1. 從`event`對象中提取命題。
1. 反複討論每個主張。
1. 判斷SDK是否呈現主張。
1. 如果是，請重複討論主張中的每個項目。
1. 從`meta`屬性（包含回應Token的物件）中擷取活動名稱。
1. 推送活動名稱至陣列。
1. 傳送活動名稱給第三方。

```javascript
var propositions = event.propositions;
if (propositions) {
  var activityNames = [];
  propositions.forEach(function(proposition) {
    if (proposition.renderAttempted) {
      proposition.items.forEach(function(item) {
        if (item.meta) {
          // item.meta contains the response tokens.
          var activityName = item.meta["activity.name"];
          // Ignore duplicates
          if (activityNames.indexOf(activityName) === -1) {
            activityNames.push(activityName);  
          }
        }
      });
    }
  });
  // Now that activity names are in an array,
  // you can send them to a third party or use
  // them in some other way.
}
```
