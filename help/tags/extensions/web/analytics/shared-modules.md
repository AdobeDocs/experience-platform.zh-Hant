---
title: Adobe Analytics 擴充功能的共用模組
description: 了解Adobe Experience Platform中Adobe Analytics標籤擴充功能提供的共用程式庫模組。
source-git-commit: 8dfb7bdc16d0654ee1d76dc5f5af50938b122d33
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 71%

---

# Adobe Analytics 擴充功能的共用模組

>[!NOTE]
>
>Adobe Experience Platform Launch已重新命名為Experience Platform中的資料收集技術套件。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../../term-updates.md)。

[Adobe Analytics 擴充功能](./overview.md)提供兩個不同的[共用模組](../../../extension-dev/web/shared.md)，您可將其整合至體驗應用程式。下列各節會介紹這些模組。

## [!DNL get-tracker]

Adobe Analytics 必須先初始化追蹤器物件，才能傳送任何信標。初始化程序會先載入 [AppMeasurement](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html)，接著建立追蹤器物件。

您可使用 `get-tracker` 共用模組，在追蹤器物件完全初始化後加以存取，如下所示：

```js
var getTracker = turbine.getSharedModule('adobe-analytics', 'get-tracker');

getTracker().then(function(tracker) {
  // Use tracker in some way
});
```

### 確認系統已安裝 Adobe Analytics

Adobe Analytics可能尚未安裝或包含在與您的擴充功能相同的標籤程式庫中。 因此，強烈建議您確認程式碼並妥善處理。以下 JavaScript 是可供您實作的確認方法範例：

```js
var getTracker = turbine.getSharedModule('adobe-analytics', 'get-tracker');

if (getTracker) {
  getTracker().then(function(tracker) {
    // Use tracker in some way
  });
} else {
  turbine.logger.error("The Adobe Analytics extension is required for Extension XYZ to function properly.");
}
```

如果`getTracker`為`undefined`，標籤資料庫中不存在Adobe Analytics擴充功能。 您可以自訂記錄訊息，以精確反映未安裝 Adobe Analytics 時可能遺失的功能。


## [!DNL augment-tracker]

初始化追蹤器物件後，緊接著是增強程序。此步驟可讓您的擴充功能在從Adobe Analytics擴充功能設定套用任何變數或傳送任何信標之前，以任何必要項目擴大追蹤器。

此外，您的擴充功能也可在執行任何非同步工作時 (例如從伺服器擷取資料或 JavaScript)，暫停追蹤器初始化程序。

您可以實作 `augment-tracker` 模組，如下所示：

```js
var augmentTracker = turbine.getSharedModule('adobe-analytics', 'augment-tracker');

augmentTracker(function(tracker) {
  // Augment tracker in some way
});
```

一旦追蹤器初始化程序進入增強階段，系統就會呼叫傳遞至 `augmentTracker()` 的函數。

如果您的擴充功能必須完成非同步工作才能增強追蹤器，您可以如下所示傳回函數的 Promise：

```js
var Promise = require('@adobe/reactor-promise');
var augmentTracker = turbine.getSharedModule('adobe-analytics', 'augment-tracker');

augmentTracker(function(tracker) {
  return new Promise(function(resolve) {
    // Augment the tracker object, then call resolve()
  });
});
```

透過傳回 Promise，您的擴充功能會通知 Adobe Analytics 在解析 Promise 前，應暫停追蹤器初始化程序。

>[!WARNING]
>
>暫停追蹤器初始化程序可能會延遲傳送信標，導致未能如期收集資料 (例如使用者在信標傳送之前就離開該頁面)，請謹慎為之。
