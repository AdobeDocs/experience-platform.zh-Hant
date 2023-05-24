---
title: Web擴展的操作類型
description: 瞭解如何為Web屬性中的標籤擴展定義操作類型庫模組。
exl-id: d4539132-a72c-40b0-84b6-50cbe3785d2d
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 50%

---

# Web 擴充功能的動作類型

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

在資料收集標籤的上下文中，操作是在發生規則事件並且所有條件都通過評估後執行的操作。

例如，擴充功能可提供「顯示支援聊天」動作類型，其中可顯示支援聊天對話方塊，協助可能在結帳時遇到問題的使用者。

本文檔介紹如何定義Adobe Experience PlatformWeb擴展的操作類型。

>[!IMPORTANT]
>
>本文介紹 Web 擴充功能的動作類型。如果您正在開發邊緣擴充功能，請改為參閱[邊緣擴充功能的動作類型](../edge/action-types.md)指南。
>
>本文檔還假定您熟悉庫模組以及它們如何整合到Web擴展中。 如果需要相關說明，請先參閱[程式庫模組格式化](./format.md)的概述文章，再返回閱讀本指南。

操作類型通常包括以下內容：

1. A [視圖](./views.md) 顯示在Experience PlatformUI和資料收集UI中，允許用戶修改操作的設定。
2. 在標籤運行時庫內發出的庫模組解釋設定並執行操作。

```js
module.exports = function(settings) {
  alert('Thanks for visiting our site!');
};
```

例如，要使消息可由Adobe Experience Platform用戶配置，您可以允許用戶輸入消息並將消息保存到設定對象。 該對象的外觀如下：

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

然後，必須將第二個參數傳遞給包含觸發規則事件的上下文資訊的模組。 此模組在某些情況下可能有所助益，可透過下列方式存取：

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
