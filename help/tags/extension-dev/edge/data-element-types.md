---
title: 邊擴展的資料元素類型
description: 瞭解如何在邊緣屬性中為標籤擴展定義資料元素類型庫模組。
exl-id: ddbc3912-1c25-4d21-bde8-e40e583b4278
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 24%

---

# 邊緣擴展中的資料元素類型

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

在標籤中，資料元素是Web或移動頁上資料段的別名，而不管該資料在伺服器接收的事件中位於何處。 資料元素可供規則參照，並可作為據以存取這些資料片段的抽象概念。當資料的位置將來發生變化（例如更改包含該值的事件鍵）時，可以重新配置單個資料元素，而引用該資料元素的所有規則都可以保持不變。

資料元素類型由擴展提供，擴展作者確定如何檢索該資料。 例如，您可以使用資料元素類型來允許Adobe Experience Platform用戶從XDM層或其自定義資料層檢索一段資料。

本文檔介紹如何定義Adobe Experience Platform邊擴展的資料元素類型。

>[!IMPORTANT]
>
>如果正在開發Web擴展，請參閱上的指南 [Web擴展的資料元素類型](../web/data-element-types.md) 的雙曲餘切值。
>
>本文檔還假定您熟悉庫模組以及它們如何整合到邊擴展中。 如果需要相關說明，請先參閱[程式庫模組格式化](./format.md)的概述文章，再返回閱讀本指南。

資料元素類型通常由以下組成：

1. Experience PlatformUI和資料收集UI中顯示的視圖，允許用戶修改資料元素的設定。
2. 在標籤運行時庫內發出的庫模組解釋設定並檢索資料片段。

如果希望允許用戶從自定義資料層檢索一段資料，則您的模組可能就像此示例。

```js
module.exports = (context) => {
  const productName = context.arc.event.data.productName;
  return productName;
};
```

如果要使為資料層返回的資料可由Adobe Experience Platform用戶配置，則可以允許用戶輸入鍵名，然後將該名稱保存到 `settings` 的雙曲餘切值。 這個物體可能是像這樣的。

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
