---
solution: Experience Platform
title: PQL彙總函式
description: 彙總函式用於將設定檔查詢語言(PQL)陣列中的多個值群組在一起，以形成單一摘要值。
exl-id: 6c0c0f6d-98c5-4b5d-b440-3e5e18c0f34b
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 7%

---

# 聚合函式

彙總函式用於將內的多個值群組在一起 [!DNL Profile Query Language] (PQL)陣列來形成單一摘要值。 如需其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概觀](./overview.md).

## 計數

此 `count` 函式傳回給定陣列中的元素數。

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

此 `sum` 函式會傳回陣列中所有選取值的總和。

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

此 `average` 函式傳回陣列中所有選取值的算術平均值。

**格式**

```sql
{ARRAY}.average()
```

**範例**

下列PQL查詢會傳回所有訂單的平均價格。

```sql
orders.average(order.price)
```

## 最小

此 `min` 函式傳回陣列中所有選取值的最小值。

**格式**

```sql
{ARRAY}.min()
```

**範例**

下列PQL查詢會傳回所有訂單的最低價格。

```sql
orders.min(order.price)
```

## 最大

此 `max` 函式會傳回陣列中所有選取值的最大值。

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

現在您已瞭解彙總函式，可以在PQL查詢中使用它們。 如需其他PQL功能的詳細資訊，請參閱 [設定檔查詢語言概觀](./overview.md).
