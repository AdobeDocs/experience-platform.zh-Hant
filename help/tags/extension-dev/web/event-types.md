---
title: 網頁擴充功能的事件類型
description: 了解如何為Adobe Experience Platform中的網頁擴充功能定義事件類型程式庫模組。
exl-id: dbdd1c88-5c54-46be-9824-2f15cce3d160
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 30%

---

# 網頁擴充功能的事件類型

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

在標籤規則中，事件是必須發生的活動，規則才會引發。 例如，網路擴充功能可提供「手勢」事件類型，來監視要發生的特定滑鼠或觸控手勢。 一旦該手勢發生，事件邏輯就會引發規則。

事件類型程式庫模組可偵測活動何時發生，然後呼叫函式以引發相關規則。 可自訂偵測到的事件。 例如，可偵測使用者何時做出特定手勢、快速捲動或與某個項目互動。

本檔案說明如何在Adobe Experience Platform中定義網頁擴充功能的事件類型。

>[!NOTE]
>
>本檔案假設您熟悉程式庫模組，以及這些模組如何整合至網頁擴充功能。 回到本指南之前，請先參閱[程式庫模組格式化](./format.md)概述文件，概略了解其實作方式。

事件類型由擴充功能定義，通常包含下列項目：

1. A [檢視](./views.md) 顯示於Experience PlatformUI和資料收集UI中，供使用者修改事件的設定。
2. 在標籤執行階段程式庫內發出的程式庫模組，用於解譯設定並監視要發生的特定活動。

`module.exports` 接受兩者 `settings` 和 `trigger` 參數。 如此可自訂事件類型。

```js
module.exports = function(settings, trigger) { … };
```

| 參數 | 說明 |
| --- | --- |
| `settings` | 此物件內含使用者在事件類型檢視中設定的任何設定。至於要在此物件中納入哪些項目，由您全權掌控。 |
| `trigger` | 模組在規則引發時所應呼叫的函數。在 `settings` 對象，a `trigger` 函式和規則。 這表示您收到的一個規則觸發函式無法用來觸發不同的規則。 |

>[!NOTE]
>
>對於已設定為要使用事件類型的每個規則，匯出的函數將會呼叫一次。

以傳入5秒的活動為例，5秒過後，活動已發生，規則將引發。 模組看起來會類似於此範例。

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, 5000);
};
```

如果要讓Adobe Experience Platform使用者可設定持續時間，則需要輸入並儲存持續時間至設定物件的選項。 該物件可能如下所示：

```js
{
  "duration": 25000
}
```

若要運用於使用者定義的持續時間，需要更新模組以包含此項目。

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, settings.duration);
};
```

## 傳遞內容事件資料

規則觸發時，針對發生的事件提供其他詳細資訊通常很實用。 建立規則的使用者可利用這項資訊來達成特定行為。例如，如果行銷人員想要建立每當使用者滑動畫面時都會傳送分析信標的規則。 擴充功能必須提供 `swipe` 事件類型，讓行銷人員可使用此事件類型來觸發適當規則。 假設行銷人員想要納入滑動在信標上發生的角度，若不提供其他資訊，就很難做到這點。 若要就發生的事件提供其他相關資訊，請在呼叫 `trigger` 函數時傳遞一個物件。例如：

```js
trigger({
  swipeAngle: 90 // the value would be the detected angle
});
```

行銷人員隨後可藉由在文字欄位中指定 `%event.swipeAngle%` 值，在分析信標上使用此值。他們也可以從其他內容 (例如自訂程式碼動作) 中存取 `event.swipeAngle`。可以包含其他類型的選用事件資訊，這些資訊對行銷人員而言可能會以相同方式有用。

### [!DNL nativeEvent]

如果您的事件類型以原生事件為基礎(例如，如果您的擴充功能提供 `click` 事件類型)，建議您設定 `nativeEvent` 屬性如下。

```js
trigger({
  nativeEvent: nativeEvent // the value would be the underlying native event
});
```

這對於嘗試從原生事件存取任何資訊 (例如游標座標) 的行銷人員，可能有其效用。

### [!DNL element]

如果元素與發生的事件之間有強烈的關係，建議設定 `element` 屬性至元素的DOM節點。 例如，如果您的擴充功能提供 `click` 事件類型，而您可讓行銷人員加以設定，以便只有在ID為的元素 `herobanner` 中所有規則的URL。 在此情況下，如果使用者選取主圖橫幅，建議呼叫 `trigger` 設定 `element` 至主圖橫幅的DOM節點。

```js
trigger({
  element: element // the value would be the DOM node
});
```

## 遵循規則順序

標籤可讓使用者排序規則。 例如，使用者可建立兩個規則，兩者都使用方向變更事件類型和自訂規則觸發的順序。 假設Adobe Experience Platform使用者指定 `2` 規則A中的方向變更事件和順序值 `1` 規則B中的方向變更事件。這表示當行動裝置上的方向變更時，規則B應在規則A之前引發（順序較低的值會先引發規則）。

如前所述，對於已設定為要使用事件類型的每個規則，匯出的函數將在事件模組中呼叫一次。每次呼叫匯出的函數時，都會傳遞一個與特定規則繫結的唯一 `trigger` 函數。在剛才說明的案例中，我們匯出的函式將會以 `trigger` 函式系結至規則B，然後以 `trigger` 函式系結至規則A。規則B會先出現，因為使用者為其指定的順序比規則A低。我們的程式庫模組偵測到方向變更時，請務必呼叫 `trigger` 函式的順序與提供給程式庫模組的順序相同。

在以下範例程式碼中應留意，當偵測到方向變更時，觸發函數將會按照其提供至匯出函數時的順序進行呼叫：

```js
var triggers = [];

window.addEventListener('orientationchange', function() {
  triggers.forEach(function(trigger) {
    trigger();
  });
});

module.exports = function(settings, trigger) {
  triggers.push(trigger);
};
```

這可確實保留使用者指定的順序。

若以不同的順序呼叫觸發函數，將是不當的實作：

```js
var triggers = [];

window.addEventListener('orientationchange', function() {
  for (var i = triggers.length - 1; i >= 0; i--) {
    triggers[i]();
  }
});

module.exports = function(settings, trigger) {
  triggers.push(trigger);
};
```

自然程式設計實務準則通常會維持正確的順序，但仍須了解其影響並據此進行開發。
