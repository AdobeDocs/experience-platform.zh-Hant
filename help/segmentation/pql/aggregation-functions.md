---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;aggregation functions;aggregation;
solution: Experience Platform
title: 聚集函式
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 6%

---


# 聚集函式

聚合函式用於將(PQL)陣列中的多 [!DNL Profile Query Language] 個值組合在一起，以形成單個摘要值。 有關其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md)。

## 計數

此函 `count` 數返回給定陣列中的元素數。

**Format**

```sql
{ARRAY}.count()
```

**範例**

以下PQL查詢返回陣列中的訂單數。

```sql
orders.count()
```

## 總和

該 `sum` 函式返回陣列中所有選定值的總和。

**Format**

```sql
{ARRAY}.sum()
```

**範例**

以下PQL查詢返回所有訂單價格的總和。

```sql
orders.sum(order.price)
```

## 平均

該函 `average` 數返回陣列中所有選定值的算術平均值。

**Format**

```sql
{ARRAY}.average()
```

**範例**

以下PQL查詢返回所有訂單的平均價格。

```sql
orders.average(order.price)
```

## 最小

該函 `min` 數返回陣列中所有選定值的最小值。

**Format**

```sql
{ARRAY}.min()
```

**範例**

以下PQL查詢返回所有訂單的最低價格。

```sql
orders.min(order.price)
```

## 最大

函 `max` 數返回陣列中所有選定值中最大的值。

**Format**

```sql
{ARRAY}.max()
```

**範例**

以下PQL查詢返回所有訂單的最高價格。

```sql
orders.max(order.price)
```

## 後續步驟

現在，您已經瞭解了聚合函式，可以在PQL查詢中使用它們。 有關其他PQL函式的詳細資訊，請閱讀配置式查 [詢語言概述](./overview.md)。
