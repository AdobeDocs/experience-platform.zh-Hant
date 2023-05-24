---
title: Adobe Experience PlatformWeb SDK擴展中的事件類型
description: 瞭解如何使用Adobe Experience Platform LaunchAdobe Experience PlatformWeb SDK擴展提供的事件類型。
solution: Experience Platform
exl-id: b3162406-c5ce-42ec-ab01-af8ac8c63560
source-git-commit: 5218e6cf82b74efbbbcf30495395a4fe2ad9fe14
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 1%

---

# 事件類型

本頁介紹由Adobe Experience PlatformWeb SDK標籤擴展提供的Adobe Experience Platform事件類型。 這些 [構建規則](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-rules.html) 不應該和 [`eventType` 欄位](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=zh-Hant)。

## [!UICONTROL 發送事件完成]

通常，您的屬性會使用 [[!UICONTROL 發送事件] 動作](action-types.md#send-event) 向Adobe Experience Platform邊緣網路發送事件。 每次將事件發送到邊緣網路時，都會向瀏覽器返回帶有用資料的響應。 沒有 [!UICONTROL 發送事件完成] 事件類型，您將無權訪問此返回的資料。

要訪問返回的資料，請建立單獨的規則，然後添加 [!UICONTROL 發送事件完成] 事件。 每次從伺服器收到成功響應時，都會觸發此規則 [!UICONTROL 發送事件] 操作。

當 [!UICONTROL 發送事件完成] 事件觸發規則，它提供從伺服器返回的資料，這些資料對於完成某些任務可能非常有用。 通常，您會 [!UICONTROL 自定義代碼] 操作(從 [!UICONTROL 核心] 擴展)到包含 [!UICONTROL 發送事件完成] 的子菜單。 在 [!UICONTROL 自定義代碼] 操作，您的自定義代碼將有權訪問名為 `event`。 此 `event` 變數將包含從伺服器返回的資料。

處理從邊緣網路返回的資料的規則可能如下所示：

![](./assets/send-event-complete.png)

下面是如何使用 [!UICONTROL 自定義代碼] 此規則中的操作。

### 手動呈現個性化內容

在「自定義代碼」操作中，您可以訪問從伺服器返回的個性化主張。 為此，您應鍵入以下自定義代碼：

```javascript
var propositions = event.propositions;
```

如果 `event.propositions` 存在，它是一個包含個性化命題對象的陣列。 在很大程度上，陣列中包含的主張是由事件如何發送到伺服器決定的。

對於第一個方案，假設您尚未檢查 [!UICONTROL 作出決定] 複選框，但未提供任何 [!UICONTROL 決策範圍] 內 [!UICONTROL 發送事件] 負責發送事件的操作。

![img.png](assets/send-event-render-unchecked-without-scopes.png)

在此示例中， `propositions` 陣列只包含與符合自動呈現條件的事件相關的建議。

的 `propositions` 陣列可能與此示例類似：

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

發送事件時， [!UICONTROL 作出決定] 複選框未選中，因此SDK未嘗試自動呈現任何內容。 但是，SDK仍會自動檢索符合自動呈現條件的內容，並提供給您在您願意的情況下手動呈現。 請注意，每個命題對象 `renderAttempted` 屬性設定為 `false`。

如果您選擇 [!UICONTROL 作出決定] 複選框在發送事件時，SDK將嘗試呈現符合自動呈現條件的任何主張。 因此，每個命題對象都會 `renderAttempted` 屬性設定為 `true`。 在本例中，不需要手動提出這些建議。

到目前為止，您只查看了符合自動渲染條件的個性化內容(例如，在Adobe Target的Visual Experience Composer中建立的任何內容)。 檢索任何個性化內容 _不_ 符合自動呈現條件，通過使用 [!UICONTROL 決策範圍] 的 [!UICONTROL 發送事件] 操作。 範圍是一個字串，用於標識要從伺服器中檢索的特定命題。

的 [!UICONTROL 發送事件] 操作如下所示：

![img.png](assets/send-event-render-unchecked-with-scopes.png)

在本示例中，如果在與 `salutation` 或 `discount` 範圍，返回並包含在 `propositions` 陣列。 請注意，符合自動渲染條件的主張將繼續包含在 `propositions` 陣列，無論您如何配置 [!UICONTROL 作出決定] 或 [!UICONTROL 決策範圍] 的 [!UICONTROL 發送事件] 操作。 的 `propositions` 在本例中，array與以下示例類似：

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

此時，您可以根據您所認為的適合情況呈現命題內容。 在本例中，與 `discount` scope是使用Adobe Target基於表單的體驗作曲家構建的HTML命題。 假設您的頁面上有一個ID為 `daily-special` 並希望從 `discount` 建議 `daily-special` 的子菜單。 請執行下列動作：

1. 從 `event` 的雙曲餘切值。
1. 循環查看每個命題，查找包含 `discount`。
1. 如果您找到一個建議，請循環查看建議中的每個項目，查找HTML內容的項目。 （檢查總比假設好。）
1. 如果找到包含HTML內容的項目，請查找 `daily-special` 元素，並將其HTML替換為個性化內容。

您的自定義代碼位於 [!UICONTROL 自定義代碼] 操作可能如下所示：

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

### 訪問Adobe Target響應令牌

從Adobe Target返回的個性化內容包括 [響應令牌](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)，這些是有關活動、服務、體驗、用戶配置檔案、地理資訊等的詳細資訊。 這些詳細資訊可以與第三方工具共用或用於調試。 可以在Adobe Target用戶介面中配置響應令牌。

在「自定義代碼」操作中，您可以訪問從伺服器返回的個性化主張。 為此，請鍵入以下自定義代碼：

```javascript
var propositions = event.propositions;
```

如果 `event.propositions` 存在，它是一個包含個性化命題對象的陣列。 請參閱 [手動呈現個性化內容](#manually-render-personalized-content) 的 `result.propositions`。

假設您希望從所有由Web SDK自動呈現的主張中收集所有活動名稱，並將它們推入單個陣列。 然後，您可以將單個陣列發送到第三方。 在這種情況下，在 [!UICONTROL 自定義代碼] 操作：

1. 從 `event` 的雙曲餘切值。
1. 回答每個命題。
1. 確定SDK是否提出該命題。
1. 如果是，則循環討論命題中的每個項目。
1. 從 `meta` 屬性，該屬性是包含響應令牌的對象。
1. 將活動名稱推入陣列。
1. 將活動名稱發送給第三方。

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
