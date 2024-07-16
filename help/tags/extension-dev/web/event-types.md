---
title: Web擴充功能的事件型別
description: 瞭解如何在Adobe Experience Platform中為Web擴充功能定義事件型別程式庫模組。
exl-id: dbdd1c88-5c54-46be-9824-2f15cce3d160
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 28%

---

# Web擴充功能的事件型別

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品檔案中出現了幾項術語變更。 請參閱下列[檔案](../../term-updates.md)，以取得術語變更的彙總參考資料。

在標籤規則中，事件是必須發生的活動，才會引發規則。 例如，網頁擴充功能可提供「手勢」事件型別，來監視應發生的特定滑鼠或觸控手勢。 一旦該手勢發生，事件邏輯就會引發規則。

事件型別程式庫模組的設計目的，是偵測活動是否發生，然後呼叫函式以引發相關規則。 偵測到的事件是可自訂的。 例如，可以偵測使用者何時做出特定手勢、快速捲動或互動某物。

本文說明如何在Adobe Experience Platform中定義Web擴充功能的事件型別。

>[!NOTE]
>
>本檔案假設您熟悉程式庫模組，以及如何將這些模組整合在Web擴充功能中。 回到本指南之前，請先參閱[程式庫模組格式化](./format.md)概述文件，概略了解其實作方式。

事件型別由擴充功能定義，通常包含下列專案：

1. 顯示於Experience PlatformUI和資料收集UI中的[檢視](./views.md)，可讓使用者修改事件的設定。
2. 在標籤執行階段程式庫內發出的程式庫模組，用以解譯設定及監視應發生的特定活動。

`module.exports`同時接受`settings`和`trigger`引數。 這可啟用事件型別的自訂。

```js
module.exports = function(settings, trigger) { … };
```

| 參數 | 說明 |
| --- | --- |
| `settings` | 此物件內含使用者在事件類型檢視中設定的任何設定。至於要在此物件中納入哪些項目，由您全權掌控。 |
| `trigger` | 模組在規則引發時所應呼叫的函數。`settings`物件、`trigger`函式與規則之間有一對一的關係。 這表示您收到的某個規則觸發函式，無法用來引發另一個規則。 |

>[!NOTE]
>
>對於已設定為要使用事件類型的每個規則，匯出的函數將會呼叫一次。

以經過5秒的活動為例，經過5秒後，活動已發生且規則將引發。 此模組看起來與此範例類似。

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, 5000);
};
```

如果要讓Adobe Experience Platform使用者能夠設定持續時間，則需要輸入並儲存設定物件的持續時間選項。 該物件可能如下所示：

```js
{
  "duration": 25000
}
```

若要運用於使用者定義的持續時間，需要更新模組以包含此專案。

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, settings.duration);
};
```

## 傳遞內容事件資料

觸發規則時，就發生的事件提供其他詳細資訊，通常有其效用。 建立規則的使用者可利用這項資訊來達成特定行為。例如，如果行銷人員想要建立每當使用者滑動畫面時就會傳送分析信標的規則。 擴充功能必須提供`swipe`事件型別，行銷人員才能使用此事件型別觸發適當規則。 假設行銷人員想要納入信標上發生撥動時的角度，這很難在不提供其他資訊的情況下完成。 若要就發生的事件提供其他相關資訊，請在呼叫 `trigger` 函數時傳遞一個物件。例如：

```js
trigger({
  swipeAngle: 90 // the value would be the detected angle
});
```

行銷人員隨後可藉由在文字欄位中指定 `%event.swipeAngle%` 值，在分析信標上使用此值。他們也可以從其他內容 (例如自訂程式碼動作) 中存取 `event.swipeAngle`。也有可能包含其他型別的選用事件資訊，這些資訊可能以相同的方式對行銷人員有所幫助。

### [!DNL nativeEvent]

如果您的事件型別以原生事件為基礎（例如，如果您的擴充功能提供了`click`事件型別），建議您依照下列方式設定`nativeEvent`屬性。

```js
trigger({
  nativeEvent: nativeEvent // the value would be the underlying native event
});
```

這對於嘗試從原生事件存取任何資訊 (例如游標座標) 的行銷人員，可能有其效用。

### [!DNL element]

如果專案與發生的事件之間有強烈的關係，建議將`element`屬性設定為專案的DOM節點。 例如，如果您的擴充功能提供`click`事件型別，而您允許行銷人員加以設定，唯有選取ID為`herobanner`的元素時才會觸發規則。 在此案例中，如果使用者選取主圖橫幅，建議呼叫`trigger`並將`element`設定為主圖橫幅的DOM節點。

```js
trigger({
  element: element // the value would be the DOM node
});
```

## 遵循規則順序

標籤讓使用者能夠排序規則。 例如，使用者可建立兩個規則，這兩個規則都會使用方向變更事件型別，並且會自訂規則引發的順序。 假設Adobe Experience Platform使用者在規則A中為方向變更事件指定了順序值`2`，並且在規則B中為方向變更事件指定了順序值`1`。這表示當行動裝置上的方向變更時，規則B應在規則A之前引發（先引發順序值較低的規則）。

如前所述，對於已設定為要使用事件類型的每個規則，匯出的函數將在事件模組中呼叫一次。每次呼叫匯出的函數時，都會傳遞一個與特定規則繫結的唯一 `trigger` 函數。在剛才說明的案例中，我們匯出的函式將會以繫結至規則B的`trigger`函式呼叫一次，然後以繫結至規則A的`trigger`函式再呼叫一次。規則B會先觸發，因為使用者為其指定的順序值比規則A低。當我們的程式庫模組偵測到方向變更時，請務必按照提供給程式庫模組的相同順序來呼叫`trigger`函式。

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
