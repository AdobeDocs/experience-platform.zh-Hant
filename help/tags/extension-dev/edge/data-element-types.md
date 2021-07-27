---
title: 邊緣擴充功能的資料元素類型
description: 了解如何為Edge屬性中的標籤擴充功能定義資料元素類型程式庫模組。
source-git-commit: 99780f64c8f09acea06e47ebf5cabc762e05cab2
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 18%

---

# 邊緣擴充功能中的資料元素類型

>[!NOTE]
>
>Adobe Experience Platform Launch已重新命名為Experience Platform中的資料收集技術套件。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../term-updates.md)。

在標籤中，資料元素是網頁或行動頁面上資料片段的別名，無論該資料在伺服器收到的事件內的何處找到。 資料元素可供規則參照，並可作為據以存取這些資料片段的抽象概念。當資料的位置在未來變更時（例如變更包含值的事件索引鍵），單一資料元素可重新設定，而所有參考該資料元素的規則可能維持不變。

資料元素類型由擴充功能提供，而擴充功能作者會決定擷取此資料片段的方式。 例如，您可以使用資料元素類型，讓Adobe Experience Platform使用者從XDM層或其自訂資料層擷取資料片段。

本檔案說明如何為Adobe Experience Platform中的邊緣擴充功能定義資料元素類型。

>[!IMPORTANT]
>
>如果您正在開發網頁擴充功能，請參閱[網頁擴充功能資料元素類型](../web/data-element-types.md)上的指南。
>
>本檔案也假設您熟悉程式庫模組，以及這些模組如何整合至邊緣擴充功能。 如果需要相關說明，請先參閱[程式庫模組格式化](./format.md)的概述文章，再返回閱讀本指南。

資料元素類型通常包含下列項目：

1. 資料收集UI中顯示的檢視，可讓使用者修改資料元素的設定。
2. 在標籤執行階段程式庫內發出的程式庫模組，用於解譯設定及擷取資料片段。

如果您想要讓使用者從自訂資料層擷取資料片段，您的模組可能如下範例所示。

```js
module.exports = (context) => {
  const productName = context.arc.event.data.productName;
  return productName;
};
```

如果要讓Adobe Experience Platform使用者能夠設定為資料層傳回的資料，則可允許使用者輸入索引鍵名稱，然後將該名稱儲存至`settings`物件。 物件可能如下所示。

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
