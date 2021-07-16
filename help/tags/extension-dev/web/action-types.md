---
title: 網頁擴充功能的動作類型
description: 了解如何為Web屬性中的標籤擴充功能定義動作類型程式庫模組。
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 54%

---

# Web 擴充功能的動作類型

>[!NOTE]
>
>Adobe Experience Platform Launch已重新命名為Experience Platform中的資料收集技術套件。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../term-updates.md)。

動作類型程式庫模組旨在執行預先定義的動作。 此動作的功用完全由您決定。想傳送信標、顯示優惠活動、感謝使用者造訪、儲存 Cookie，或開啟線上交談支援功能嗎？

>[!IMPORTANT]
>
>本文介紹 Web 擴充功能的動作類型。如果您正在開發邊緣擴充功能，請改為參閱[邊緣擴充功能的動作類型](../edge/action-types.md)指南。
>
>本檔案也假設您熟悉程式庫模組，以及這些模組如何整合至標籤擴充功能中。 如果需要相關說明，請先參閱[程式庫模組格式化](./format.md)的概述文章，再返回閱讀本指南。

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
