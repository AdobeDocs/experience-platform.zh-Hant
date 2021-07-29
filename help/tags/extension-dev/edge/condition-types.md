---
title: 邊緣擴充功能的條件類型
description: 了解如何為Adobe Experience Platform中的邊緣擴充功能定義條件類型程式庫模組。
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 44%

---

# 邊緣擴充功能的條件類型

>[!NOTE]
>
> Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../term-updates.md)。

在標籤規則中，會在事件發生後評估條件。 所有條件都必須傳回 true，才會繼續處理規則。條件類型由擴充功能提供，並評估某項為true或false，傳回布林值。

例如，擴充功能可提供「檢視區包含」條件類型，讓 使用者可在其中指定 CSS 選擇器。在用戶端的網站上評估條件時，擴充功能將可尋找符合 CSS 選擇器的元素，並傳回結果指出其中是否有任何元素包含在使用者的檢視區中。

本檔案說明如何在Adobe Experience Platform中定義邊緣擴充功能的條件類型。

>[!IMPORTANT]
>
>如果您正在開發 Web 擴充功能，請改為參閱 [Web 擴充功能的條件類型](../web/condition-types.md)指南。
>
>本檔案也假設您熟悉程式庫模組，以及這些模組如何整合至邊緣擴充功能。 如果需要相關說明，請先參閱[程式庫模組格式化](./format.md)的概述文章，再返回閱讀本指南。

條件類型通常包含下列項目：

1. 資料收集UI中顯示的檢視，可讓使用者修改條件的設定。
2. 在標籤執行階段程式庫內發出的程式庫模組，用於解譯設定及評估條件。

例如，如果要評估用戶是否在主機`example.com`上，您的模組可能如下所示。

```js
module.exports = (context) => {
  const URL = context.arc.event.xdm.web.webpageDetails.URL;
  return URL.endsWith("adobelaunch.com");
};
```

如果希望用戶能夠配置主機名以允許輸入主機名並將其保存到設定對象，則該對象看起來可能類似於此示例。

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
