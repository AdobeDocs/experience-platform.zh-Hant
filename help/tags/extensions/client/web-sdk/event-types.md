---
title: Adobe Experience Platform Web SDK擴充功能中的事件型別
description: 瞭解如何使用Adobe Experience Platform Launch中Adobe Experience Platform Web SDK擴充功能提供的事件型別。
solution: Experience Platform
exl-id: b3162406-c5ce-42ec-ab01-af8ac8c63560
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 0%

---

# 事件類型

本頁說明Adobe Experience Platform Web SDK標籤擴充功能提供的Adobe Experience Platform事件型別。 這些已用來 [建置規則](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-rules.html) 且不應與 `eventType` 中的欄位 [`xdm` 物件](/help/web-sdk/commands/sendevent/xdm.md).

## [!UICONTROL 傳送事件完成]

通常，您的屬性會有一或多個使用下列專案的規則： [[!UICONTROL 傳送事件] 動作](action-types.md#send-event) 傳送事件給Adobe Experience Platform Edge Network。 每次將事件傳送至Edge Network時，系統都會將回應傳回至瀏覽器，其中包含有用的資料。 不含 [!UICONTROL 傳送事件完成] 事件型別時，您將無法存取此傳回的資料。

若要存取傳回的資料，請建立個別規則，然後新增 [!UICONTROL 傳送事件完成] 事件至規則。 每次從伺服器收到因產生的成功回應時，就會觸發此規則 [!UICONTROL 傳送事件] 動作。

當 [!UICONTROL 傳送事件完成] 事件會觸發規則，提供從伺服器傳回的有助於完成特定工作的資料。 通常，您會新增 [!UICONTROL 自訂程式碼] 動作(來自 [!UICONTROL 核心] 副檔名)至包含 [!UICONTROL 傳送事件完成] 事件。 在 [!UICONTROL 自訂程式碼] 動作，您的自訂程式碼將能存取名為的變數 `event`. 這個 `event` 變數會包含從伺服器傳回的資料。

處理從Edge Network傳回之資料的規則可能如下所示：

![](assets/send-event-complete.png)

以下是如何使用執行特定工作的一些範例 [!UICONTROL 自訂程式碼] 動作。

### 手動呈現個人化內容

在自訂程式碼動作中（位於處理回應資料的規則中），您可以存取從伺服器傳回的個人化主張。 若要這麼做，您應輸入下列自訂程式碼：

```javascript
var propositions = event.propositions;
```

如果 `event.propositions` 存在，它是一個包含個人化主張物件的陣列。 陣列中包含的建議很大程度上是由事件傳送至伺服器的方式所決定。

對於第一個案例，假設您尚未核取 [!UICONTROL 呈現決定] 核取方塊，且尚未提供任何 [!UICONTROL 決定範圍] 內部 [!UICONTROL 傳送事件] 負責傳送事件的動作。

![img.png](assets/send-event-render-unchecked-without-scopes.png)

在此範例中， `propositions` 陣列僅包含與符合自動轉譯資格之事件相關的主張。

此 `propositions` 陣列看起來可能類似於此範例：

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

傳送事件時， [!UICONTROL 呈現決定] 未勾選核取方塊，因此SDK不會嘗試自動轉譯任何內容。 不過，SDK仍會自動擷取符合自動轉譯資格的內容，並會在您想要時提供給您手動轉譯。 請注意，每個主張物件都有 `renderAttempted` 屬性設定為 `false`.

如果您選擇檢查 [!UICONTROL 呈現決定] 核取方塊傳送事件時，SDK會嘗試轉譯任何符合自動轉譯條件的建議。 因此，每個主張物件都會有其 `renderAttempted` 屬性設定為 `true`. 在此情況下，不需要手動轉譯這些主張。

到目前為止，您只檢視了符合自動轉譯資格的個人化內容(例如，在Adobe Target的視覺化體驗撰寫器中建立的任何內容)。 擷取任何個人化內容 _非_ 符合自動轉譯的資格，請使用 [!UICONTROL 決定範圍] 中的欄位 [!UICONTROL 傳送事件] 動作。 範圍是字串，可識別您要從伺服器擷取的特定主張。

此 [!UICONTROL 傳送事件] 動作如下：

![img.png](assets/send-event-render-unchecked-with-scopes.png)

在此範例中，如果在伺服器上找到與相符的主張 `salutation` 或 `discount` 範圍，它們會傳回並包含在 `propositions` 陣列。 請注意，符合自動轉譯資格的主張將繼續包含在 `propositions` 陣列，無論您如何設定 [!UICONTROL 呈現決定] 或 [!UICONTROL 決定範圍] 中的欄位 [!UICONTROL 傳送事件] 動作。 此 `propositions` 在此範例中，陣列看起來與此範例類似：

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

此時，您可以視需要演算主張內容。 在此範例中，主張符合 `discount` scope是使用Adobe Target的表單式體驗撰寫器建立的HTML主張。 假設您的頁面上有一個元素，其ID為 `daily-special` 並希望轉譯以下專案的內容： `discount` 中的主張 `daily-special` 元素。 請執行下列動作：

1. 從擷取主張 `event` 物件。
1. 循環瀏覽每個主張，尋找具有範圍的主張 `discount`.
1. 如果您找到主張，會在主張中的每個專案中進行回圈，尋找是HTML內容的專案。 （檢查勝於假設）。
1. 如果您找到包含HTML內容的專案，請找到 `daily-special` 元素，並以個人化內容取代其HTML。

您在中的自訂程式碼 [!UICONTROL 自訂程式碼] 動作可能如下所示：

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

Adobe Target傳回的個人化內容包括 [回應Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)，此為活動、選件、體驗、使用者設定檔、地理資訊等的詳細資訊。 這些詳細資料可與協力廠商工具共用或用於偵錯。 回應Token可在Adobe Target使用者介面中設定。

在自訂程式碼動作中（位於處理回應資料的規則中），您可以存取從伺服器傳回的個人化主張。 若要這麼做，請輸入下列自訂程式碼：

```javascript
var propositions = event.propositions;
```

如果 `event.propositions` 存在，它是一個包含個人化主張物件的陣列。 另請參閱 [手動呈現個人化內容](#manually-render-personalized-content) 以取得有關以下專案的內容的詳細資訊： `result.propositions`.

假設您想從Web SDK自動轉譯的所有主張中收集所有活動名稱，並將其推入單一陣列中。 然後，您可以將單一陣列傳送給第三方。 在這種情況下，請在內編寫自訂程式碼 [!UICONTROL 自訂程式碼] 動作至：

1. 從擷取主張 `event` 物件。
1. 在每個主張中重複執行。
1. 判斷SDK是否轉譯了主張。
1. 若是如此，會重複檢查主張中的每個專案。
1. 從擷取活動名稱 `meta` 屬性，包含回應Token的物件。
1. 將活動名稱推送至陣列。
1. 將活動名稱傳送給第三方。

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
