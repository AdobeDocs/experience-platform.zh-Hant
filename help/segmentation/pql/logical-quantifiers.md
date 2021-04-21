---
keywords: Experience Platform;home；熱門主題；分段；分段；分段服務；pql;PQL；配置檔案查詢語言；邏輯量詞；邏輯量詞；
solution: Experience Platform
title: PQL邏輯量詞
topic-legacy: developer guide
description: 邏輯量詞可用於在配置檔案查詢語言(PQL)中用陣列來斷言條件。
exl-id: 8b1c9560-02e2-46e0-9646-c64dd4a15df1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 4%

---

# 邏輯量詞函式

邏輯量詞可用於對[!DNL Profile Query Language](PQL)中的陣列斷言條件。 有關其他PQL函式的詳細資訊，請參閱[[!DNL Profile Query Language] overview](./overview.md)。

## 存在

`exists`函式確定在滿足所提供條件的陣列中是否存在項。

**格式**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| 引數 | 說明 |
| ---------- | ----------- |
| `{VARIABLE}` | 變數的名稱。 |
| `{EXPRESSION}` | 正在檢查的陣列。 |
| `{CONDITION}` | 可選運算式，可篩選傳回之陣列中的值。 |

**範例**

以下PQL查詢獲取所有價格高於$50或SKU為&quot;PS&quot;的事件。

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## 適合所有人

`forall`函式確定陣列中滿足所有給定條件的所有項。

**格式**

```sql
forall {VARIABLE} from {EXPRESSION} where {CONDITION}
forall {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| 引數 | 說明 |
| ---------- | ----------- |
| `{VARIABLE}` | 變數的名稱。 |
| `{EXPRESSION}` | 正在檢查的陣列。 |
| `{CONDITION}` | 可選運算式，可篩選傳回之陣列中的值。 |

**範例**

以下PQL查詢獲取所有價格大於$50且SKU為&quot;PS&quot;的事件。

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## 後續步驟

現在，您已經瞭解了邏輯量詞，可以在PQL查詢中使用它們。 有關其他PQL函式的詳細資訊，請閱讀[配置檔案查詢語言概述](./overview.md)。
