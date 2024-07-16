---
solution: Experience Platform
title: PQL邏輯數量詞
description: 邏輯數量詞可用來在Profile Query Language (PQL)中判斷陣列的條件。
exl-id: 8b1c9560-02e2-46e0-9646-c64dd4a15df1
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 3%

---

# 邏輯數量詞函式

邏輯數量詞可用於斷言[!DNL Profile Query Language] (PQL)中陣列的條件。 如需其他PQL函式的詳細資訊，請參閱[[!DNL Profile Query Language] 總覽](./overview.md)。

## 存在

`exists`函式決定陣列中專案是否存在，前提是它符合提供的條件。

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

下列PQL查詢會取得價格超過$50或具有「PS」SKU的所有事件。

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## 全部

`forall`函式決定陣列中符合所有指定條件的所有專案。

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

下列PQL查詢會取得價格超過$50且具有「PS」SKU的所有事件。

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## 後續步驟

現在您已瞭解邏輯數量詞，可以在PQL查詢中使用它們。 如需其他PQL功能的詳細資訊，請參閱[Profile Query Language概觀](./overview.md)。
