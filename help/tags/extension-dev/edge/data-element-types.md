---
title: Edge擴充功能的資料元素型別
description: 瞭解如何為Edge屬性中的標籤擴充功能定義資料元素型別程式庫模組。
exl-id: ddbc3912-1c25-4d21-bde8-e40e583b4278
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 18%

---

# 邊緣擴充功能中的資料元素型別

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品檔案中出現了幾項術語變更。 請參閱下列[檔案](../../term-updates.md)，以取得術語變更的彙總參考資料。

在標籤中，資料元素是網頁或行動頁面上資料片段的別名，無論該資料位於伺服器收到的事件內的何處。 資料元素可供規則參照，並可作為據以存取這些資料片段的抽象概念。若資料的位置日後有所變更（例如變更包含值的事件索引鍵），您可重新設定單一資料元素，而所有參考該資料元素的規則可能維持不變。

資料元素型別由擴充功能提供，擴充功能作者會決定如何擷取此資料片段。 例如，您可以使用資料元素型別，讓Adobe Experience Platform使用者從XDM層或其自訂資料層中擷取資料片段。

本文介紹如何在Adobe Experience Platform中定義邊緣擴充功能的資料元素型別。

>[!IMPORTANT]
>
>如果您正在開發Web擴充功能，請改為參閱Web擴充功能的[資料元素型別指南](../web/data-element-types.md)。
>
>本文也假設您熟悉程式庫模組，以及如何將這些模組整合在邊緣擴充功能中。 如果需要相關說明，請先參閱[程式庫模組格式化](./format.md)的概述文章，再返回閱讀本指南。

資料元素型別通常包含下列專案：

1. Experience PlatformUI和資料收集UI中顯示的檢視，可讓使用者修改資料元素的設定。
2. 在標籤執行階段程式庫內發出的程式庫模組，用以解譯設定及擷取資料片段。

如果您希望允許使用者從自訂資料層擷取資料片段，您的模組可能如以下範例所示。

```js
module.exports = (context) => {
  const productName = context.arc.event.data.productName;
  return productName;
};
```

如果要讓Adobe Experience Platform使用者能夠設定針對資料層傳回的資料，您可以允許使用者輸入索引鍵名稱，然後將該名稱儲存到`settings`物件。 物件看起來可能像這樣。

```js
{
  keyName: "campaignId"
}
```

若要運用於使用者定義的本機儲存體項目名稱，您的模組必須變更為：

```js
module.exports = (context) => {
  const data = context.arc.event.data;
  return data[keyName];
};
```

## 程式庫模組內容

所有資料元素模組都可存取呼叫模組時系統所提供的 `context` 變數。如需詳細資訊，請參閱[此處](./context.md)。
