---
solution: Experience Platform
title: PQL其他函式
description: 下列函式為Profile Query Language (PQL)的其他函式。
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 3%

---

# 其他函式

下列函式是[!DNL Profile Query Language] (PQL)的其他函式。 如需其他PQL函式的詳細資訊，請參閱[[!DNL Profile Query Language] 總覽](./overview.md)。

## Let

`let`函式允許將運算式儲存為變數，以便稍後在查詢中使用。

**格式**

```sql
let {VARIABLE} = {EXPRESSION}
```

**範例**

下列PQL查詢取得交易總和大於$100且小於$1000的所有產品總和（以USD為單位）。

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## 後續步驟

現在您已瞭解其他函式，可以在PQL查詢中使用它們。 如需其他PQL功能的詳細資訊，請參閱[Profile Query Language概觀](./overview.md)。
