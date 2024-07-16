---
title: Adobe Analytics 擴充功能的共用模組
description: 瞭解Adobe Experience Platform中的Adobe Analytics標籤擴充功能所提供的共用程式庫模組。
exl-id: f1d7cb2b-0058-46f9-983c-079079e06057
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 70%

---

# Adobe Analytics 擴充功能的共用模組

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品檔案中出現了幾項術語變更。 請參閱下列[檔案](../../../term-updates.md)，以取得術語變更的彙總參考資料。

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

Adobe Analytics可能尚未安裝，或尚未包含在與您的擴充功能相同的標籤程式庫中。 因此，強烈建議您確認程式碼並妥善處理。以下 JavaScript 是可供您實作的確認方法範例：

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

如果`getTracker`是`undefined`，則標籤程式庫中不會有Adobe Analytics擴充功能。 您可以自訂記錄訊息，以精確反映未安裝 Adobe Analytics 時可能遺失的功能。


## [!DNL augment-tracker]

初始化追蹤器物件後，緊接著是增強程序。此步驟可讓您的擴充功能在Adobe Analytics擴充功能組態套用任何變數或傳送任何信標之前，先使用必要專案來增強追蹤器。

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
