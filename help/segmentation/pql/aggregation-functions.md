---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；PQL;PQL；配置式查詢語言；聚合函式；聚合；
solution: Experience Platform
title: PQL聚合函式
description: 聚合函式用於將配置檔案查詢語言(PQL)陣列中的多個值組合在一起，以形成單個摘要值。
exl-id: 6c0c0f6d-98c5-4b5d-b440-3e5e18c0f34b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 6%

---

# 聚合函式

聚合函式用於將內部的多個值組合在一起 [!DNL Profile Query Language] (PQL)陣列，以形成單個摘要值。 有關其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md)。

## 計數

的 `count` 函式返回給定陣列中的元素數。

**格式**

```sql
{ARRAY}.count()
```

**範例**

以下PQL查詢返回陣列中的訂單數。

```sql
orders.count()
```

## 和

的 `sum` 函式返回陣列中所有選定值的總和。

**格式**

```sql
{ARRAY}.sum()
```

**範例**

以下PQL查詢返回所有訂單價格之和。

```sql
orders.sum(order.price)
```

## 平均

的 `average` 函式返回陣列中所有選定值的算術平均值。

**格式**

```sql
{ARRAY}.average()
```

**範例**

以下PQL查詢返回所有訂單的平均價格。

```sql
orders.average(order.price)
```

## 最小

的 `min` 函式返回陣列中所有選定值中最小的值。

**格式**

```sql
{ARRAY}.min()
```

**範例**

以下PQL查詢返回所有訂單的最低價格。

```sql
orders.min(order.price)
```

## 最大

的 `max` 函式返回陣列中所有選定值中的最大值。

**格式**

```sql
{ARRAY}.max()
```

**範例**

以下PQL查詢返回所有訂單的最高價格。

```sql
orders.max(order.price)
```

## 後續步驟

現在您已經瞭解了聚合函式，可以在PQL查詢中使用它們。 有關其他PQL功能的詳細資訊，請閱讀 [配置檔案查詢語言概述](./overview.md)。
