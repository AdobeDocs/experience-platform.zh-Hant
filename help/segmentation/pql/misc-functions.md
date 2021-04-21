---
keywords: Experience Platform;home；熱門主題；分段；分段；分段服務；pql;PQL；配置檔案查詢語言；雜項函式；misc;
solution: Experience Platform
title: PQL其他函式
topic-legacy: developer guide
description: 以下函式是描述檔查詢語言(PQL)的其他函式。
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---

# 其他函式

以下函式是[!DNL Profile Query Language](PQL)的其他函式。 有關其他PQL函式的詳細資訊，請參閱[[!DNL Profile Query Language] overview](./overview.md)。

## 讓

`let`函式允許將表達式儲存為變數，以便以後在查詢中使用。

**格式**

```sql
let {VARIABLE} = {EXPRESSION}
```

**範例**

以下PQL查詢以USD表示，其總和大於$100且小於$1000的事務處理獲取所有產品總和。

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## 後續步驟

現在您已經瞭解了其他函式，可以在PQL查詢中使用這些函式。 有關其他PQL函式的詳細資訊，請閱讀[配置檔案查詢語言概述](./overview.md)。
