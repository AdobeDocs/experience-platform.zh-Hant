---
title: Adobe Experience Platform Web SDK擴充功能中的事件型別
description: 瞭解如何使用Adobe Experience Platform Launch中Adobe Experience Platform Web SDK擴充功能提供的事件型別。
solution: Experience Platform
exl-id: b3162406-c5ce-42ec-ab01-af8ac8c63560
source-git-commit: b37bf09e3ec16f29d6acee3bca71463fa2c876ce
workflow-type: tm+mt
source-wordcount: '1490'
ht-degree: 0%

---

# 事件類型

本頁說明Adobe Experience Platform Web SDK標籤擴充功能提供的Adobe Experience Platform事件型別。 這些是用於[建置規則](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-rules.html?lang=zh-Hant)，不應該與[`xdm`物件](/help/web-sdk/commands/sendevent/xdm.md)中的`eventType`欄位混淆。

## 監視勾點已觸發 {#monitoring-hook-triggered}

Adobe Experience Platform Web SDK包含監視掛接，可用來監視各種系統事件。 這些工具對於開發您自己的偵錯工具以及擷取Web SDK記錄很有用。

如需有關每個監控掛接事件包含哪些引數的完整詳細資料，請參閱[Web SDK監控掛接檔案](../../../../web-sdk/monitoring-hooks.md)。

![標籤使用者介面影像顯示監視連結事件型別](assets/monitoring-hook-triggered.png)

Web SDK標籤擴充功能支援下列監視鉤點：

* **[!UICONTROL onInstanceCreated]**：當您成功建立新的Web SDK執行個體時，就會觸發此監視連結事件。
* **[!UICONTROL onInstanceConfigured]**：成功解析[`configure`](../../../../web-sdk/commands/configure/overview.md)命令時，Web SDK會觸發此監視掛接事件
* **[!UICONTROL onBeforeCommand]**：此監視掛接事件是在執行任何其他命令之前由Web SDK觸發。 您可以使用此監視掛接來擷取特定命令的組態選項。
* **[!UICONTROL onCommandResolved]**：在解析命令Promise之前，會觸發此監視掛接事件。 您可以使用此函式來檢視命令選項和結果。
* **[!UICONTROL onCommandRejected]**：當命令Promise被拒絕且包含錯誤原因相關資訊時，就會觸發此監視掛接事件。
* **[!UICONTROL onBeforeNetworkRequest]**：此監視掛接事件是在執行網路要求之前觸發。
* **[!UICONTROL onNetworkResponse]**：瀏覽器收到回應時會觸發此監視勾點事件。
* **[!UICONTROL onNetworkError]**：網路要求失敗時會觸發此監視掛接事件。
* **[!UICONTROL onBeforeLog]**：此監視連結事件是在Web SDK將任何內容記錄到主控台之前觸發。
* **[!UICONTROL onContentRendering]**：此監視連結事件是由`personalization`元件觸發，可協助您偵錯個人化內容的呈現。 此事件可能有不同的狀態：
   * `rendering-started`：表示Web SDK即將呈現主張。 在Web SDK開始轉譯決定範圍或檢視之前，您可以在`data`物件中看到即將由`personalization`元件轉譯的建議以及範圍名稱。
   * `no-offers`：表示未收到要求之引數的裝載。
   * `rendering-failed`：表示Web SDK無法轉譯主張。
   * `rendering-succeeded`：表示已針對決定範圍完成轉譯。
   * `rendering-redirect`：表示Web SDK將執行重新導向主張。
* **[!UICONTROL onContentHiding]**：套用或移除預先隱藏樣式時會觸發此監視勾點事件。


## [!UICONTROL 傳送事件完成]

通常您的屬性會有一或多個規則使用[[!UICONTROL 傳送事件]動作](action-types.md#send-event)將事件傳送至Adobe Experience PlatformEdge Network。 每次將事件傳送至Edge Network時，系統都會將回應傳回至瀏覽器，其中包含有用的資料。 如果沒有[!UICONTROL 傳送事件完成]事件型別，您將無法存取此傳回的資料。

若要存取傳回的資料，請建立個別規則，然後新增[!UICONTROL 傳送事件完成]事件至規則。 每次因[!UICONTROL 傳送事件]動作而從伺服器收到成功回應時，就會觸發此規則。

當[!UICONTROL 傳送事件完成]事件觸發規則時，它會提供伺服器傳回的有助於完成特定工作的資料。 通常，您會將[!UICONTROL 自訂程式碼]動作（來自[!UICONTROL 核心]擴充功能）新增至包含[!UICONTROL 傳送事件完成]事件的相同規則。 在[!UICONTROL 自訂程式碼]動作中，您的自訂程式碼將可存取名為`event`的變數。 此`event`變數將包含伺服器傳回的資料。

您用於處理從Edge Network傳回之資料的規則可能如下所示：

![](assets/send-event-complete.png)

以下是如何使用此規則中的[!UICONTROL 自訂程式碼]動作執行某些工作的範例。

### 手動呈現個人化內容

在自訂程式碼動作中（位於處理回應資料的規則中），您可以存取從伺服器傳回的個人化主張。 若要這麼做，您應輸入下列自訂程式碼：

```javascript
var propositions = event.propositions;
```

如果`event.propositions`存在，則為包含個人化主張物件的陣列。 陣列中包含的建議很大程度上是由事件傳送至伺服器的方式所決定。

對於第一個案例，假設您尚未核取[!UICONTROL 轉譯決定]核取方塊，且未在負責傳送事件的[!UICONTROL 傳送事件]動作中提供任何[!UICONTROL 決定範圍]。

![img.png](assets/send-event-render-unchecked-without-scopes.png)

在此範例中，`propositions`陣列僅包含與事件相關的主張，這些主張符合自動轉譯的條件。

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

傳送事件時，未勾選[!UICONTROL 轉譯決策]核取方塊，因此SDK不會嘗試自動轉譯任何內容。 不過，SDK仍會自動擷取符合自動轉譯資格的內容，並會在您想要時提供給您手動轉譯。 請注意，每個主張物件的`renderAttempted`屬性都設定為`false`。

如果您在傳送事件時改為勾選[!UICONTROL 轉譯決定]核取方塊，SDK就會嘗試轉譯任何符合自動轉譯資格的建議。 因此，每個主張物件都會將其`renderAttempted`屬性設定為`true`。 在此情況下，不需要手動轉譯這些主張。

到目前為止，您只檢視了符合自動轉譯資格的個人化內容(例如，在Adobe Target的視覺化體驗撰寫器中建立的任何內容)。 若要擷取任何符合自動轉譯資格的個人化內容&#x200B;__，請使用[!UICONTROL 傳送事件]動作中的[!UICONTROL 決定範圍]欄位，提供決定範圍來要求內容。 範圍是字串，可識別您要從伺服器擷取的特定主張。

[!UICONTROL 傳送事件]動作如下所示：

![img.png](assets/send-event-render-unchecked-with-scopes.png)

在此範例中，如果在符合`salutation`或`discount`範圍的伺服器上找到主張，則會傳回它們並包含在`propositions`陣列中。 請注意，無論您在[!UICONTROL 傳送事件]動作中如何設定[!UICONTROL 轉譯決定]或[!UICONTROL 決定範圍]欄位，符合自動轉譯資格的主張將繼續包含在`propositions`陣列中。 在此案例中，`propositions`陣列看起來與此範例類似：

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

此時，您可以視需要演算主張內容。 在此範例中，符合`discount`範圍的主張是使用Adobe Target的表單式體驗撰寫器建立的HTML主張。 假設您的頁面上有ID為`daily-special`的元素，且想要將內容從`discount`主張轉譯為`daily-special`元素。 請執行下列動作：

1. 從`event`物件擷取主張。
1. 重複每個主張，尋找範圍為`discount`的主張。
1. 如果您找到主張，會在主張中的每個專案中進行回圈，尋找是HTML內容的專案。 （檢查勝於假設）。
1. 如果您找到包含HTML內容的專案，請在頁面上找到`daily-special`元素，並以個人化內容取代其HTML。

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

從Adobe Target傳回的Personalization內容包含[回應Token](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)，其為有關活動、選件、體驗、使用者設定檔、地理資訊等的詳細資料。 這些詳細資料可與協力廠商工具共用或用於偵錯。 回應Token可在Adobe Target使用者介面中設定。

在自訂程式碼動作中（位於處理回應資料的規則中），您可以存取從伺服器傳回的個人化主張。 若要這麼做，請輸入下列自訂程式碼：

```javascript
var propositions = event.propositions;
```

如果`event.propositions`存在，則為包含個人化主張物件的陣列。 如需有關`result.propositions`內容的詳細資訊，請參閱[手動轉譯個人化內容](#manually-render-personalized-content)。

假設您想從Web SDK自動轉譯的所有主張中收集所有活動名稱，並將其推入單一陣列中。 然後，您可以將單一陣列傳送給第三方。 在這種情況下，請在[!UICONTROL 自訂程式碼]動作中寫入自訂程式碼至：

1. 從`event`物件擷取主張。
1. 在每個主張中重複執行。
1. 判斷SDK是否轉譯了主張。
1. 若是如此，會重複檢查主張中的每個專案。
1. 從`meta`屬性（包含回應Token的物件）擷取活動名稱。
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

## [!UICONTROL 訂閱規則集專案] {#subscribe-ruleset-items}

**[!UICONTROL 訂閱規則集專案]**&#x200B;事件型別可讓您訂閱介面的Adobe Journey Optimizer內容卡。 每當評估規則集時，提供給此命令的回呼都會收到一個結果物件，其中包含儲存內容卡片資料的建議。

![顯示[訂閱規則集]專案事件型別的Experience Platform標籤使用者介面影像。](assets/subscribe-ruleset-items.png)

此事件型別支援下列可設定的屬性：

* **[!UICONTROL 結構描述]**：要訂閱內容卡的結構描述陣列。 您可以手動輸入結構描述，或提供資料元素來輸入。
* **[!UICONTROL 介面]**：您要訂閱內容卡片的介面陣列。 您可以手動或提供資料元素來輸入曲面。
