---
title: Web擴展的事件類型
description: 瞭解如何為Adobe Experience Platform的Web擴展定義事件類型庫模組。
exl-id: dbdd1c88-5c54-46be-9824-2f15cce3d160
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 30%

---

# Web擴展的事件類型

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

在標籤規則中，事件是必須發生的活動，以便觸發規則。 例如，Web擴展可提供「手勢」事件類型，用於監視特定滑鼠或觸摸手勢的發生。 一旦該手勢發生，事件邏輯就會引發規則。

事件類型庫模組被設計為檢測何時發生活動，然後調用函式以觸發關聯規則。 正在檢測的事件是可自定義的。 例如，可以檢測用戶何時做出某種手勢、快速滾動或與某些東西進行交互。

本文檔介紹如何定義Adobe Experience PlatformWeb擴展的事件類型。

>[!NOTE]
>
>本文檔假定您熟悉庫模組以及它們如何整合到Web擴展中。 回到本指南之前，請先參閱[程式庫模組格式化](./format.md)概述文件，概略了解其實作方式。

事件類型由擴展定義，通常由以下組成：

1. A [視圖](./views.md) 顯示在Experience PlatformUI和資料收集UI中，允許用戶修改事件的設定。
2. 在標籤運行時庫中發出的庫模組解釋設定並監視特定活動的發生。

`module.exports` 接受兩者 `settings` 和 `trigger` 參數。 這允許自定義事件類型。

```js
module.exports = function(settings, trigger) { … };
```

| 參數 | 說明 |
| --- | --- |
| `settings` | 此物件內含使用者在事件類型檢視中設定的任何設定。至於要在此物件中納入哪些項目，由您全權掌控。 |
| `trigger` | 模組在規則引發時所應呼叫的函數。在一個 `settings` 對象，a `trigger` 函式和規則。 這意味著您為一個規則接收的觸發器函式不能用於觸發其他規則。 |

>[!NOTE]
>
>對於已設定為要使用事件類型的每個規則，匯出的函數將會呼叫一次。

以5秒過程的活動為例，在5秒過後，活動已發生，規則將觸發。 該模組將與此示例類似。

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, 5000);
};
```

如果要使持續時間由Adobe Experience Platform用戶配置，則需要為設定對象輸入並保存持續時間的選項。 該物件可能如下所示：

```js
{
  "duration": 25000
}
```

為了在用戶定義的持續時間上操作，需要更新模組以包括這些。

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, settings.duration);
};
```

## 傳遞上下文事件資料

觸發規則時，通常會提供有關所發生事件的更多詳細資訊。 建立規則的使用者可利用這項資訊來達成特定行為。例如，如果商家希望建立規則，在規則中，用戶每次刷新螢幕時都會發送分析信標。 延期必須提供 `swipe` 事件類型，以便商家可以使用此事件類型來觸發相應的規則。 假設商家希望包括信標上發生刷卡的角度，如果不提供其他資訊，將很難做到這一點。 若要就發生的事件提供其他相關資訊，請在呼叫 `trigger` 函數時傳遞一個物件。例如：

```js
trigger({
  swipeAngle: 90 // the value would be the detected angle
});
```

行銷人員隨後可藉由在文字欄位中指定 `%event.swipeAngle%` 值，在分析信標上使用此值。他們也可以從其他內容 (例如自訂程式碼動作) 中存取 `event.swipeAngle`。可以包括其它類型的可選事件資訊，這些資訊可能以同樣的方式對營銷者有用。

### [!DNL nativeEvent]

如果事件類型基於本機事件(例如，如果擴展提供 `click` 事件類型)，建議設定 `nativeEvent` 屬性，如下所示。

```js
trigger({
  nativeEvent: nativeEvent // the value would be the underlying native event
});
```

這對於嘗試從原生事件存取任何資訊 (例如游標座標) 的行銷人員，可能有其效用。

### [!DNL element]

如果元素與發生的事件之間存在強關係，建議設定 `element` 屬性。 例如，如果擴展提供 `click` 事件類型，並且您允許商家配置它，以便僅當ID為 `herobanner` 的子菜單。 在這種情況下，如果用戶選擇了英雄橫幅，則建議調用 `trigger` 設定 `element` 到英雄旗的DOM節點。

```js
trigger({
  element: element // the value would be the DOM node
});
```

## 遵循規則順序

標籤使用戶能夠訂購規則。 例如，用戶可能會建立兩個規則，這兩個規則既使用方向更改事件類型，又自定義規則觸發的順序。 假定Adobe Experience Platform用戶指定的訂單值 `2` 對於規則A中的方向更改事件和 `1` 規則B中的方向更改事件。這表示當移動設備上的方向發生更改時，規則B應在規則A（低階值的規則首先觸發）之前觸發。

如前所述，對於已設定為要使用事件類型的每個規則，匯出的函數將在事件模組中呼叫一次。每次呼叫匯出的函數時，都會傳遞一個與特定規則繫結的唯一 `trigger` 函數。在剛才介紹的方案中，將使用 `trigger` 函式與規則B綁定，然後使用 `trigger` 函式。規則B是第一位的，因為用戶給它賦值的次序低於規則A。當我們的庫模組檢測到方向更改時，我們必須將 `trigger` 功能按提供給庫模組的相同順序排列。

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
