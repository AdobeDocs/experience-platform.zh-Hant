---
title: 邊緣擴充功能的動作類型
description: 了解如何為Edge屬性中的標籤擴充功能定義動作類型程式庫模組。
exl-id: c0b058aa-f0fe-4fd8-a873-018482c3e4db
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 42%

---

# 邊緣擴充功能的動作類型

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

在標籤規則中，動作是在規則條件通過評估後執行的動作。 動作類型由擴充功能提供，其效果由擴充功能作者完全定義。

例如，擴充功能可提供「顯示支援聊天」動作類型，其中可顯示支援聊天對話方塊，協助可能在結帳時遇到問題的使用者。

本檔案說明如何在Adobe Experience Platform中定義邊緣擴充功能的動作類型。

>[!IMPORTANT]
>
>如果您正在開發 Web 擴充功能，請改為參閱 [Web 擴充功能的動作類型](../web/action-types.md)指南。
>
>本檔案也假設您熟悉程式庫模組，以及這些模組如何整合至邊緣擴充功能。 如果需要相關說明，請先參閱[程式庫模組格式化](./format.md)的概述文章，再返回閱讀本指南。

動作類型通常包含下列項目：

1. 顯示於Experience PlatformUI和資料收集UI中的檢視，可讓使用者修改動作的設定。
2. 在標籤執行階段程式庫內發出的程式庫模組，用於解譯設定並執行動作。

例如，將某些資料轉送至協力廠商端點的模組可能如下所示。

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  return fetch('http://someendpoint.com', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

如果要使用者可設定端點，並允許端點輸入和持續存在模組內的設定物件，則該物件看起來會類似於此。

```json
{
  "endpoint": "http://someendpoint.com"
}
```

若要運用於使用者定義的端點，您的模組必須變更為下列範例。

```js
module.exports = (context) {
  const { arc, utils } = context;
  const { fetch } = utils;
  const { event: { xdm } } = arc;
  const  { endpoint } = settings;
  return fetch(endpoint, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(xdm)
  })
};
```

## 動作結果

動作模組傳回的結果可能是任何項目。如果動作必須執行非同步工作，您可以傳回 [Promise](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise)，這會在解析後傳回所需結果。

動作結果會儲存在 `ruleStash` 索引鍵中，可透過 `context` 參數 (`context.arc.ruleStash`) 供所有模組使用。如需深入了解 `ruleStash`，請參閱[此處](./context.md#rulestash)。
