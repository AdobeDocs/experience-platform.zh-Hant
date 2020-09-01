---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;miscellaneous functions;misc;
solution: Experience Platform
title: 其他函式
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 3%

---


# 其他函式

以下函式是(PQL)的 [!DNL Profile Query Language] 其他函式。 有關其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md)。

## 讓

此函 `let` 數允許將表達式儲存為變數，以便稍後在查詢中使用。

**Format**

```sql
let {VARIABLE} = {EXPRESSION}
```

**範例**

以下PQL查詢以USD表示，其總和大於$100且小於$1000的事務處理獲取所有產品總和。

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## 後續步驟

現在您已經瞭解了其他函式，可以在PQL查詢中使用這些函式。 有關其他PQL函式的詳細資訊，請閱讀配置式查 [詢語言概述](./overview.md)。
