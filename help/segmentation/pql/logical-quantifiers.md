---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;logical quantifiers;logical quantifier;
solution: Experience Platform
title: 邏輯量詞
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 5%

---


# 邏輯量詞函式

邏輯量詞可用來斷言(PQL)中的 [!DNL Profile Query Language] 陣列條件。 有關其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md)。

## 存在

該函 `exists` 數確定在滿足所提供條件的陣列中項的存在。

**Format**

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

該函 `forall` 數確定陣列中滿足所有給定條件的所有項目。

**Format**

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

現在，您已經瞭解了邏輯量詞，可以在PQL查詢中使用它們。 有關其他PQL函式的詳細資訊，請閱讀配置式查 [詢語言概述](./overview.md)。
