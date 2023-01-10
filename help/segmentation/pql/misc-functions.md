---
keywords: Experience Platform；首頁；熱門主題；細分；細分；細分服務；PQL;PQL；設定檔查詢語言；其他功能；雜項功能；
solution: Experience Platform
title: PQL其他功能
description: 以下函式是設定檔查詢語言(PQL)的其他函式。
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---

# 其他函式

以下函式是 [!DNL Profile Query Language] (PQL)。 有關其他PQL函式的詳細資訊，請參見 [[!DNL Profile Query Language] 概述](./overview.md).

## 讓

此 `let` 函式可讓運算式儲存為變數，以供稍後在查詢中使用。

**格式**

```sql
let {VARIABLE} = {EXPRESSION}
```

**範例**

以下PQL查詢以美元表示，其總和大於$100且小於$1000的事務處理的所有產品總和。

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## 後續步驟

現在您已了解了各種功能，可以在PQL查詢中使用這些功能。 有關其他PQL功能的詳細資訊，請閱讀 [設定檔查詢語言概觀](./overview.md).
