---
title: 網頁擴充功能的資料元素類型
description: 了解如何為Web屬性中的標籤擴充功能定義資料元素類型程式庫模組。
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 61%

---

# 邊緣擴充功能的資料元素類型

>[!NOTE]
>
>Adobe Experience Platform Launch已重新命名為Experience Platform中的資料收集技術套件。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../term-updates.md)。

資料元素類型程式庫模組的用途是擷取資料片段。 可自定義此檢索的方法。 不同的資料元素類型可讓Adobe Experience Platform使用者從本機儲存體、Cookie或DOM元素擷取資料。

>[!IMPORTANT]
>
>本檔案提供有關網頁擴充功能之資料元素類型的資訊。 如果您正在開發邊緣擴充功能，請改為參閱[邊緣擴充功能資料元素類型](../edge/data-element-types.md)指南。
>
>本檔案也假設您熟悉程式庫模組，以及這些模組如何整合至標籤擴充功能中。 如果需要相關說明，請先參閱[程式庫模組格式化](./format.md)的概述文章，再返回閱讀本指南。

請考量您想要讓使用者從名為 `productName` 的本機儲存體項目中擷取資料片段的情況。您的模組可能如下所示：

```js
module.exports = function(settings) {
  return localStorage.getItem('productName');
}
```

如果要使Adobe Experience Platform用戶可以配置本地儲存項名稱，則可以允許用戶輸入名稱，然後將該名稱保存到`settings`對象。 該物件可能如下所示：

```js
{
  itemName: "campaignId"
}
```

若要運用於使用者定義的本機儲存體項目名稱，您的模組必須變更為：

```js
module.exports = function(settings) {
  return localStorage.getItem(settings.itemName);
}
```

## 預設值支援

請注意，使用者可以選擇為任何資料元素設定預設值。如果您的資料元素程式庫模組傳回 `undefined` 或 `null` 值，則會自動取代為使用者針對資料元素而設定的預設值。

## 內容事件資料

如果是因引規則而擷取資料元素 (例如，資料元素用於規則的條件和動作中)，則會將第二個引數傳至與引發規則的事件有關的內容資訊所在的模組。此模組在某些情況下可能有所助益，可透過下列方式存取：

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
