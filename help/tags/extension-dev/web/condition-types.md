---
title: Web擴充功能的條件型別
description: 瞭解如何為Web屬性中的標籤擴充功能定義條件型別程式庫模組。
exl-id: db504455-858b-4ac8-aa42-de516b0f1d5a
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 52%

---

# Web 擴充功能的條件類型

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品檔案中出現了幾項術語變更。 請參閱下列[檔案](../../term-updates.md)，以取得術語變更的彙總參考資料。

在規則的內容中，會在事件發生後評估條件。 所有條件都必須傳回 true，才會繼續處理規則。使用者明確將條件放入「例外」貯體時則屬例外，在此情況下，貯體中的所有條件都必須傳回false，才會繼續處理規則。

例如，擴充功能可提供「檢視區包含」條件型別，讓使用者可在其中指定CSS選取器。 在用戶端的網站上評估條件時，擴充功能將可尋找符合 CSS 選擇器的元素，並傳回結果指出其中是否有任何元素包含在使用者的檢視區中。

本文說明如何在Adobe Experience Platform中定義Web擴充功能的條件型別。

>[!NOTE]
>
>如果您正在開發邊緣擴充功能，請改為參閱[邊緣擴充功能的條件類型](../edge/condition-types.md)指南。
>
>本檔案假設您熟悉程式庫模組，以及如何將這些模組整合在Web擴充功能中。 如果需要相關說明，請先參閱[程式庫模組格式化](./format.md)的概述文章，再返回閱讀本指南。

條件型別通常包含下列專案：

1. 顯示於Experience PlatformUI和資料收集UI中的[檢視](./views.md)，可讓使用者修改條件的設定。
2. 在標籤執行階段程式庫內發出的程式庫模組，用以解譯設定及評估條件。

條件型別程式庫模組有一個目標：評估某條件是否成立。 其評估標的由您決定。

例如，如果您想評估使用者是否在主機 `example.com` 上，您的模組可能如下所示：

```js
module.exports = function(settings) {
  return document.location.hostname === 'example.com';
};
```

現在，假設您希望讓Adobe Experience Platform使用者能夠設定主機名稱。 您可以允許使用者輸入主機名稱，然後將主機名稱儲存至設定物件。該物件可能如下所示：

```js
{
  "hostname": "example.com"
}
```

若要運用於使用者定義的主機名稱，您的模組必須變更為：

```js
module.exports = function(settings) {
  return document.location.hostname === settings.hostname;
};
```

## 內容事件資料

第二個引數會傳至您的模組，其中包含與引發規則的事件有關的內容資訊。此模組在某些情況下可能有所助益，可透過下列方式存取：

```js
module.exports = function(settings, event) {
  // event contains information regarding the event that fired the rule
};
```

`event` 物件必須包含下列屬性：

| 屬性 | 說明 |
| --- | --- |
| `$type` | 說明擴充功能名稱和事件名稱的字串，需以句點連接，例如 `youtube.play`。 |
| `$rule` | 包含當前所執行規則相關資訊的物件。物件必須包含下列子屬性：<ul><li>`id`：當前所執行規則的 ID。</li><li>`name`：當前所執行規則的名稱。</li></ul> |

提供觸發規則之事件類型的擴充功能可選擇性地將任何其他有用的資訊新增至此 `event` 物件。
