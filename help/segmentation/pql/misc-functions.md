---
keywords: Experience Platform；主題；熱門主題；分段；分段；分段服務；PQL;PQL；配置檔案查詢語言；雜項功能；misc;
solution: Experience Platform
title: PQL其他函式
description: 以下函式是配置檔案查詢語言(PQL)的其他函式。
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---

# 雜項函式

以下函式是 [!DNL Profile Query Language] (PQL)。 有關其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md)。

## 讓

的 `let` 函式允許將表達式儲存為變數，以便稍後在查詢中使用。

**格式**

```sql
let {VARIABLE} = {EXPRESSION}
```

**範例**

以下PQL查詢以USD形式獲取交易記錄的所有產品合計，其總和大於$100且小於$1000。

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## 後續步驟

現在您已經瞭解了各種函式，可以在PQL查詢中使用它們。 有關其他PQL功能的詳細資訊，請閱讀 [配置檔案查詢語言概述](./overview.md)。
