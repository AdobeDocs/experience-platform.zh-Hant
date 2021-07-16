---
title: 網頁擴充功能的事件類型
description: 了解如何為Adobe Experience Platform中的網頁擴充功能定義事件類型程式庫模組。
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 38%

---

# 事件類型

>[!NOTE]
>
>Adobe Experience Platform Launch已重新命名為Experience Platform中的資料收集技術套件。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../term-updates.md)。

事件類型程式庫模組可偵測活動何時發生，然後呼叫函式以引發相關規則。 可自訂偵測到的事件。 它可以偵測使用者何時做出特定手勢、快速捲動或與某個項目互動？

>[!NOTE]
>
>本檔案假設您熟悉程式庫模組，以及這些模組如何整合至標籤擴充功能中。 回到本指南之前，請先參閱[程式庫模組格式化](./format.md)概述文件，概略了解其實作方式。

`module.exports` 同時接受 `settings` 和 `trigger` 參數。如此可自訂事件類型。

```js
module.exports = function(settings, trigger) { … };
```

| 參數 | 說明 |
| --- | --- |
| `settings` | 此物件內含使用者在事件類型檢視中設定的任何設定。至於要在此物件中納入哪些項目，由您全權掌控。 |
| `trigger` | 模組在規則引發時所應呼叫的函數。`settings`物件、`trigger`函式和規則之間有一對一的關係。 這表示您收到的一個規則觸發函式無法用來觸發不同的規則。 |

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

規則觸發時，針對發生的事件提供其他詳細資訊通常很實用。 建立規則的使用者可利用這項資訊來達成特定行為。例如，如果行銷人員想要建立每當使用者滑動畫面時都會傳送分析信標的規則。 擴充功能必須提供`swipe`事件類型，讓行銷人員能使用此事件類型觸發適當規則。 假設行銷人員想要納入滑動在信標上發生的角度，若不提供其他資訊，就很難做到這點。 若要就發生的事件提供其他相關資訊，請在呼叫 `trigger` 函數時傳遞一個物件。例如：

```js
trigger({
  swipeAngle: 90 // the value would be the detected angle
});
```

行銷人員隨後可藉由在文字欄位中指定 `%event.swipeAngle%` 值，在分析信標上使用此值。他們也可以從其他內容 (例如自訂程式碼動作) 中存取 `event.swipeAngle`。可以包含其他類型的選用事件資訊，這些資訊對行銷人員而言可能會以相同方式有用。

### [!DNL nativeEvent]

如果您的事件類型以原生事件為基礎（例如，如果您的擴充功能提供了`click`事件類型），則建議依照下列方式設定`nativeEvent`屬性。

```js
trigger({
  nativeEvent: nativeEvent // the value would be the underlying native event
});
```

這對於嘗試從原生事件存取任何資訊 (例如游標座標) 的行銷人員，可能有其效用。

### [!DNL element]

如果元素與發生的事件之間有強烈關係，建議將`element`屬性設為元素的DOM節點。 例如，如果您的擴充功能提供`click`事件類型，而您允許行銷人員加以設定，這樣只有在選取ID為`herobanner`的元素時，才會觸發規則。 在此情況下，如果使用者選取主圖橫幅，建議呼叫`trigger`，並將`element`設為主圖橫幅的DOM節點。

```js
trigger({
  element: element // the value would be the DOM node
});
```

## 遵循規則順序

Adobe Experience Platform中的標籤可讓使用者排序規則。 例如，使用者可建立兩個規則，兩者都使用方向變更事件類型和自訂規則觸發的順序。 假設Adobe Experience Platform使用者在規則A中為方向變更事件指定順序值`2`，並在規則B中為方向變更事件指定順序值`1`。這表示當行動裝置上的方向變更時，規則B應在規則A之前引發（順序值較低的規則會先引發）。

如前所述，對於已設定為要使用事件類型的每個規則，匯出的函數將在事件模組中呼叫一次。每次呼叫匯出的函數時，都會傳遞一個與特定規則繫結的唯一 `trigger` 函數。在剛才說明的案例中，我們匯出的函數將會以繫結至規則 B 的 `trigger` 函數呼叫一次，然後以繫結至規則 A 的 `trigger` 函數再呼叫一次。規則 B 會先觸發，因為使用者為其指定的順序值比規則 A 低。當我們的程式庫模組偵測到方向變更時，務必要按照提供給程式庫模組的相同順序來呼叫 `trigger` 函數。

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
