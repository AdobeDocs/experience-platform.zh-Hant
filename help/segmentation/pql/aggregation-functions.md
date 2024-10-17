---
solution: Experience Platform
title: PQL彙總函式
description: 彙總函式可用來將Profile Query Language (PQL)陣列中的多個值分組，以形成單一摘要值。
exl-id: 6c0c0f6d-98c5-4b5d-b440-3e5e18c0f34b
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 5%

---

# 聚合函式

彙總函式可用來將[!DNL Profile Query Language] (PQL)陣列中的多個值群組在一起，以形成單一摘要值。 如需其他PQL函式的詳細資訊，請參閱[[!DNL Profile Query Language] 總覽](./overview.md)。

## 計數

`count`函式會以數字傳回指定陣列中的元素數目。

**格式**

```sql
{ARRAY}.count()
```

**範例**

下列PQL查詢會傳回陣列中的訂單數。

```sql
orders.count()
```

## 總和

`sum`函式以數字傳回陣列中所有選取值的總和。

**格式**

```sql
{ARRAY}.sum()
```

**範例**

下列PQL查詢會傳回所有訂單價格的總和。

```sql
orders.sum(order.price)
```

## 平均

`average`函式以數字傳回陣列中所有選取值的算術平均值。

**格式**

```sql
{ARRAY}.average()
```

**範例**

下列PQL查詢會傳回所有訂單的平均價格。

```sql
orders.average(order.price)
```

## 最小值

`min`函式以數字傳回陣列中所有選取值的最小值。

**格式**

```sql
{ARRAY}.min()
```

**範例**

下列PQL查詢會傳回所有訂單的最低價格。

```sql
orders.min(order.price)
```

## 最大值

`max`函式會以數字傳回陣列中所有選取值的最大值。

**格式**

```sql
{ARRAY}.max()
```

**範例**

下列PQL查詢會傳回所有訂單的最高價格。

```sql
orders.max(order.price)
```

## 後續步驟

現在您已瞭解彙總函式，可以在PQL查詢中使用它們。 如需其他PQL功能的詳細資訊，請參閱[Profile Query Language概觀](./overview.md)。
