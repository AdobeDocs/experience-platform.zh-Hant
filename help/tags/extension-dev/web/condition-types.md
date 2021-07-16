---
title: 網頁擴充功能的條件類型
description: 了解如何為Web屬性中的標籤擴充功能定義條件類型程式庫模組。
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 75%

---

# Web 擴充功能的條件類型

>[!NOTE]
>
>Adobe Experience Platform Launch已重新命名為Experience Platform中的資料收集技術套件。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../term-updates.md)。

條件類型程式庫模組有一個目標：評估某條件是否成立。其評估標的由您決定。

>[!NOTE]
>
>本文介紹 Web 擴充功能的條件類型。如果您正在開發邊緣擴充功能，請改為參閱[邊緣擴充功能的條件類型](../edge/condition-types.md)指南。
>
>本檔案也假設您熟悉程式庫模組，以及這些模組如何整合至標籤擴充功能中。 如果需要相關說明，請先參閱[程式庫模組格式化](./format.md)的概述文章，再返回閱讀本指南。

例如，如果您想評估使用者是否在主機 `example.com` 上，您的模組可能如下所示：

```js
module.exports = function(settings) {
  return document.location.hostname === 'example.com';
};
```

現在，請考量您希望讓 Adobe Experience Platform 使用者能夠設定主機名稱的情況。您可以允許使用者輸入主機名稱，然後將主機名稱儲存至設定物件。該物件可能如下所示：

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
