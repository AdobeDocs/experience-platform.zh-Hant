---
title: 邊擴展的操作類型
description: 瞭解如何為邊緣屬性中的標籤擴展定義操作類型庫模組。
exl-id: c0b058aa-f0fe-4fd8-a873-018482c3e4db
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 42%

---

# 邊緣擴充功能的動作類型

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

在標籤規則中，操作是在規則條件通過評估後執行的操作。 操作類型由擴展提供，其效果由擴展作者完全定義。

例如，擴充功能可提供「顯示支援聊天」動作類型，其中可顯示支援聊天對話方塊，協助可能在結帳時遇到問題的使用者。

本文檔介紹如何定義Adobe Experience Platform邊擴展的操作類型。

>[!IMPORTANT]
>
>如果您正在開發 Web 擴充功能，請改為參閱 [Web 擴充功能的動作類型](../web/action-types.md)指南。
>
>本文檔還假定您熟悉庫模組以及它們如何整合到邊擴展中。 如果需要相關說明，請先參閱[程式庫模組格式化](./format.md)的概述文章，再返回閱讀本指南。

操作類型通常包括以下內容：

1. Experience PlatformUI和資料收集UI中顯示的視圖，允許用戶修改操作的設定。
2. 在標籤運行時庫內發出的庫模組解釋設定並執行操作。

例如，將某些資料轉發到第三方端點的模組可能如下所示。

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

如果希望使端點可由用戶配置，並允許端點對模組內的設定對象的輸入和持久性，則該對象看起來與此類似。

```json
{
  "endpoint": "http://someendpoint.com"
}
```

為了在用戶定義的端點上操作，您的模組需要更改為以下示例。

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
