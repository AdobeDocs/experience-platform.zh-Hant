---
title: 邊緣擴充功能的動作類型
description: 了解如何為Edge屬性中的標籤擴充功能定義動作類型程式庫模組。
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 37%

---

# 邊緣擴充功能的動作類型

>[!NOTE]
>
>Adobe Experience Platform Launch已重新命名為Experience Platform中的資料收集技術套件。 因此，產品檔案中已推出數個術語變更。 有關術語更改的綜合參考，請參閱以下[document](../../term-updates.md)。

動作類型程式庫模組旨在執行預先定義的動作。 此動作的效果完全由作者定義。 模組可建立為信標，或甚至轉換事件中的某些資料。

>[!IMPORTANT]
>
>本文介紹邊緣擴充功能的動作類型。如果您正在開發 Web 擴充功能，請改為參閱 [Web 擴充功能的動作類型](../web/action-types.md)指南。
>
>本檔案也假設您熟悉程式庫模組，以及這些模組如何整合至標籤擴充功能中。 如果需要相關說明，請先參閱[程式庫模組格式化](./format.md)的概述文章，再返回閱讀本指南。

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
