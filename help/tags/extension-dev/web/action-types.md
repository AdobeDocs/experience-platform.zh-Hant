---
title: 網頁擴充功能的動作類型
description: 了解如何為Web屬性中的標籤擴充功能定義動作類型程式庫模組。
exl-id: d4539132-a72c-40b0-84b6-50cbe3785d2d
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 50%

---

# Web 擴充功能的動作類型

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

在資料收集標籤的內容中，動作是在發生規則事件且所有條件都通過評估後所執行的動作。

例如，擴充功能可提供「顯示支援聊天」動作類型，其中可顯示支援聊天對話方塊，協助可能在結帳時遇到問題的使用者。

本檔案說明如何在Adobe Experience Platform中定義網頁擴充功能的動作類型。

>[!IMPORTANT]
>
>本文介紹 Web 擴充功能的動作類型。如果您正在開發邊緣擴充功能，請改為參閱[邊緣擴充功能的動作類型](../edge/action-types.md)指南。
>
>本檔案也假設您熟悉程式庫模組，以及這些模組如何整合至網頁擴充功能。 如果需要相關說明，請先參閱[程式庫模組格式化](./format.md)的概述文章，再返回閱讀本指南。

動作類型通常包含下列項目：

1. A [檢視](./views.md) 顯示於「Experience PlatformUI」和「資料收集UI」中，供使用者修改動作的設定。
2. 在標籤執行階段程式庫內發出的程式庫模組，用於解譯設定並執行動作。

```js
module.exports = function(settings) {
  alert('Thanks for visiting our site!');
};
```

例如，若要讓Adobe Experience Platform使用者可設定訊息，您可以允許使用者輸入訊息，並將訊息儲存至設定物件。 物件看起來類似：

```json
{
  "message": "Thank you for being one of our VIP members!"
}
```

若要運用於使用者定義的訊息，您的模組必須變更為：

```js
module.exports = function(settings) {
  alert(settings.message);
}
```

## 內容事件資料

接著，必須將第二個引數傳遞至您的模組，其中包含與觸發規則之事件相關的內容資訊。 此模組在某些情況下可能有所助益，可透過下列方式存取：

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
