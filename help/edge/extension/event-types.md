---
title: Adobe Experience Platform Web SDK擴充功能中的事件類型
description: 了解如何使用Adobe Experience Platform Launch中Adobe Experience Platform Web SDK擴充功能提供的事件類型。
solution: Experience Platform
exl-id: b3162406-c5ce-42ec-ab01-af8ac8c63560
source-git-commit: 5218e6cf82b74efbbbcf30495395a4fe2ad9fe14
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 1%

---

# 事件類型

本頁說明Adobe Experience Platform Web SDK標籤擴充功能提供的Adobe Experience Platform事件類型。 這些用於 [建置規則](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-rules.html) 不應與 [`eventType` XDM中的欄位](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=zh-Hant).

## [!UICONTROL 傳送事件完成]

通常，您的屬性會使用 [[!UICONTROL 傳送事件] 動作](action-types.md#send-event) 將事件傳送至Adobe Experience Platform Edge Network。 每次將事件傳送至邊緣網路時，都會傳回回應給包含有用資料的瀏覽器。 沒有 [!UICONTROL 傳送事件完成] 事件類型，則您無法存取這個傳回的資料。

若要存取傳回的資料，請建立個別規則，然後新增 [!UICONTROL 傳送事件完成] 事件。 每次從伺服器收到成功回應，即會因 [!UICONTROL 傳送事件] 動作。

當 [!UICONTROL 傳送事件完成] 事件會觸發規則，提供從伺服器傳回的資料，這些資料對於完成特定任務可能很有用。 通常，您會將 [!UICONTROL 自訂程式碼] 動作(從 [!UICONTROL 核心] 擴充功能)到包含 [!UICONTROL 傳送事件完成] 事件。 在 [!UICONTROL 自訂程式碼] 動作，您的自訂程式碼將可存取名為 `event`. 此 `event` 變數將包含從伺服器傳回的資料。

處理從邊緣網路傳回資料的規則可能如下所示：

![](./assets/send-event-complete.png)

以下是如何使用 [!UICONTROL 自訂程式碼] 動作。

### 手動轉譯個人化內容

在「自訂程式碼」動作（用於處理回應資料的規則）中，您可以存取從伺服器傳回的個人化主張。 若要這麼做，您可輸入下列自訂程式碼：

```javascript
var propositions = event.propositions;
```

若 `event.propositions` 存在，此為包含個人化主張物件的陣列。 陣列中包含的主張在很大程度上取決於事件如何發送到伺服器。

對於第一個案例，假設您尚未核取 [!UICONTROL 呈現決策] 複選框和未提供任何 [!UICONTROL 決策範圍] 內 [!UICONTROL 傳送事件] 負責傳送事件的動作。

![img.png](assets/send-event-render-unchecked-without-scopes.png)

在此範例中， `propositions` 陣列僅包含與事件相關的主張，這些主張適用於自動呈現。

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

傳送事件時， [!UICONTROL 呈現決策] 核取方塊未勾選，因此SDK未嘗試自動轉譯任何內容。 不過，SDK仍會自動擷取符合自動轉譯資格的內容，並提供給您，供您手動轉譯（如果您想要）。 請注意，每個主張物件都有 `renderAttempted` 屬性設定為 `false`.

若您已改為勾選 [!UICONTROL 呈現決策] 核取方塊在傳送事件時，SDK會嘗試呈現任何符合自動呈現資格的主張。 因此，每個命題對象都有 `renderAttempted` 屬性設定為 `true`. 在本例中，不需要手動提出這些主張。

到目前為止，您只看過符合自動轉譯資格的個人化內容(例如，在Adobe Target的可視化體驗撰寫器中建立的任何內容)。 擷取任何個人化內容 _not_ 符合自動轉譯的資格，請使用 [!UICONTROL 決策範圍] 欄位 [!UICONTROL 傳送事件] 動作。 範圍是字串，用於標識要從伺服器中檢索的特定主張。

此 [!UICONTROL 傳送事件] 動作如下所示：

![img.png](assets/send-event-render-unchecked-with-scopes.png)

在此示例中，如果在與 `salutation` 或 `discount` 範圍，則會傳回並納入 `propositions` 陣列。 請注意，符合自動呈現資格的主張將繼續包含在 `propositions` 陣列，無論您如何設定 [!UICONTROL 呈現決策] 或 [!UICONTROL 決策範圍] 欄位 [!UICONTROL 傳送事件] 動作。 此 `propositions` 陣列在此案例中看起來類似於此範例：

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

此時，您可以視需要呈現主張內容。 在此範例中，與 `discount` 範圍是使用Adobe Target的表單式體驗撰寫器建立的HTML主張。 假設您的頁面上有一個元素，其ID為 `daily-special` 並想從 `discount` 對 `daily-special` 元素。 請執行下列動作：

1. 從 `event` 物件。
1. 重複討論每個主張，並在 `discount`.
1. 如果您找到主張，請重複討論主張中的每個項目，尋找屬於HTML內容的項目。 （檢查好過假設。）
1. 如果您找到包含HTML內容的項目，請尋找 `daily-special` 元素，並以個人化內容取代其HTML。

您的自訂程式碼位於 [!UICONTROL 自訂程式碼] 動作可能如下所示：

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

從Adobe Target傳回的個人化內容包括 [回應token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)，這些是活動、選件、體驗、使用者設定檔、地理資訊等的詳細資訊。 這些詳細資訊可與協力廠商工具共用或用於除錯。 可在Adobe Target使用者介面中設定回應Token。

在「自訂程式碼」動作（用於處理回應資料的規則）中，您可以存取從伺服器傳回的個人化主張。 若要這麼做，請輸入下列自訂程式碼：

```javascript
var propositions = event.propositions;
```

若 `event.propositions` 存在，此為包含個人化主張物件的陣列。 請參閱 [手動轉譯個人化內容](#manually-render-personalized-content) 以取得 `result.propositions`.

假設您想從Web SDK自動呈現的所有主張中收集所有活動名稱，並將其推送至單一陣列。 然後，您可以將單一陣列傳送至第三方。 在此情況下，請在 [!UICONTROL 自訂程式碼] 動作：

1. 從 `event` 物件。
1. 反複討論每個主張。
1. 判斷SDK是否呈現主張。
1. 如果是，請重複討論主張中的每個項目。
1. 從擷取活動名稱 `meta` 屬性，此物件包含回應Token。
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
