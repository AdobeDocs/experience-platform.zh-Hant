---
title: Web擴展的資料元素類型
description: 瞭解如何為Web屬性中的標籤擴展定義資料元素類型庫模組。
exl-id: 3aa79322-2237-492f-82ff-0ba4d4902f70
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 60%

---

# Web擴展的資料元素類型

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

在資料收集標籤中，資料元素實質上是頁面上資料的別名。 可以在查詢字串參數、cookie、DOM元素或其他位置中找到此資料。 資料元素可供規則參照，並可作為據以存取這些資料片段的抽象概念。

資料元素類型由擴展提供，並使用戶能夠配置資料元素以特定方式訪問資料片段。 例如，擴充功能可提供「本機儲存體項目」資料元素類型，讓 使用者可在其中指定本機儲存體項目名稱。當規則參考資料元素時，擴充功能將可利用使用者在設定資料元素時提供的本機儲存體項目名稱，來尋找本機儲存體項目值。

本文檔介紹如何為Adobe Experience Platform的Web擴展定義資料元素類型。

>[!IMPORTANT]
>
>如果正在開發邊延伸，請參閱上的指南 [邊緣擴展的資料元素類型](../edge/data-element-types.md) 的雙曲餘切值。
>
>本文檔還假定您熟悉庫模組以及它們如何整合到Web擴展中。 如果需要相關說明，請先參閱[程式庫模組格式化](./format.md)的概述文章，再返回閱讀本指南。

資料元素類型通常由以下組成：

1. A [視圖](./views.md) 顯示在Experience PlatformUI和資料收集UI中，允許用戶修改資料元素的設定。
2. 在標籤運行時庫內發出的庫模組解釋設定並檢索資料片段。

請考量您想要讓使用者從名為 `productName` 的本機儲存體項目中擷取資料片段的情況。您的模組可能如下所示：

```js
module.exports = function(settings) {
  return localStorage.getItem('productName');
}
```

如果要使本地儲存項名稱可由Adobe Experience Platform用戶配置，則可以允許用戶輸入一個名稱，然後將該名稱保存到 `settings` 的雙曲餘切值。 該物件可能如下所示：

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
