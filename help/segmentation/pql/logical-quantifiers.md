---
solution: Experience Platform
title: PQL邏輯數量詞
description: 邏輯數量詞可用於在設定檔查詢語言(PQL)中判斷陣列的條件。
exl-id: 8b1c9560-02e2-46e0-9646-c64dd4a15df1
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 4%

---

# 邏輯數量詞函式

邏輯數量詞可用於判斷陣列的情況 [!DNL Profile Query Language] (PQL)。 如需其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md).

## 存在

此 `exists` 函式決定陣列中專案是否存在，前提是它符合提供的條件。

**格式**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| 引數 | 說明 |
| ---------- | ----------- |
| `{VARIABLE}` | 變數的名稱。 |
| `{EXPRESSION}` | 正在檢查的陣列。 |
| `{CONDITION}` | 篩選傳回陣列中值的選用運算式。 |

**範例**

以下PQL查詢會取得價格超過$50或具有「PS」SKU的所有事件。

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## 全部

此 `forall` 函式決定陣列中所有滿足指定條件的專案。

**格式**

```sql
forall {VARIABLE} from {EXPRESSION} where {CONDITION}
forall {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| 引數 | 說明 |
| ---------- | ----------- |
| `{VARIABLE}` | 變數的名稱。 |
| `{EXPRESSION}` | 正在檢查的陣列。 |
| `{CONDITION}` | 篩選傳回陣列中值的選用運算式。 |

**範例**

以下PQL查詢會取得價格超過$50且具有「PS」SKU的所有事件。

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## 後續步驟

現在您已瞭解邏輯數量詞，可以在PQL查詢中使用它們。 如需其他PQL函式的詳細資訊，請參閱 [設定檔查詢語言概觀](./overview.md).
