---
title: 邊緣擴充功能的條件型別
description: 瞭解如何在Adobe Experience Platform中定義邊緣擴充功能的條件型別程式庫模組。
exl-id: fe13420e-ffa7-49d6-92c4-965ebd9d7390
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 50%

---

# 邊緣擴充功能的條件類型

>[!NOTE]
>
> Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

在標籤規則中，會在事件發生後評估條件。 所有條件都必須傳回 true，才會繼續處理規則。條件型別由擴充功能提供，會評估某條件是否成立，傳回布林值。

例如，擴充功能可提供「檢視區包含」條件類型，讓 使用者可在其中指定 CSS 選擇器。在用戶端的網站上評估條件時，擴充功能將可尋找符合 CSS 選擇器的元素，並傳回結果指出其中是否有任何元素包含在使用者的檢視區中。

本文介紹如何在Adobe Experience Platform中定義邊緣擴充功能的條件型別。

>[!IMPORTANT]
>
>如果您正在開發 Web 擴充功能，請改為參閱 [Web 擴充功能的條件類型](../web/condition-types.md)指南。
>
>本檔案也假設您熟悉程式庫模組，以及如何將這些模組整合在Edge擴充功能中。 如果需要相關說明，請先參閱[程式庫模組格式化](./format.md)的概述文章，再返回閱讀本指南。

條件型別通常包含下列專案：

1. Experience PlatformUI和資料收集UI中顯示的檢視，可讓使用者修改條件的設定。
2. 在標籤執行階段程式庫內發出的程式庫模組，用於解譯設定及評估條件。

例如，如果您想要評估使用者是否在主機上 `example.com`，您的模組可能如下所示。

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith("adobelaunch.com");
};
```

如果您想要讓使用者能夠設定主機名稱，以允許輸入主機名稱並將其儲存到設定物件，該物件看起來可能類似於此範例。

```js
{
  "hostname": "example.com"
}
```

若要運用於使用者定義的主機名稱，您的模組必須變更為：

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith(settings.hostname);
};
```

## 條件結果

條件模組傳回的結果可能是下列任一項目：

1. 布林值 (`true` 或 `false`)。
1. 解析後傳回布林值的 [Promise](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise)。

## 程式庫模組內容

所有條件模組都可存取您呼叫模組時，系統所提供的 `context` 變數。如需詳細資訊，請參閱[此處](./context.md)。
