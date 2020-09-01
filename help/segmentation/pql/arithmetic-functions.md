---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;arithmetic functions;arithmetic;
solution: Experience Platform
title: 算術函式
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 5%

---


# 算術函式

算術函式用於對(PQL)中的值執 [!DNL Profile Query Language] 行基本計算。 有關其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md)。

## 新增

( `+` addition)函式用於查找兩個參數表達式的和。

**Format**

```sql
{NUMBER} + {NUMBER}
```

**範例**

以下PQL查詢總結了兩個不同產品的價格。

```sql
product1.price + product2.price
```

## 乘

( `*` 乘法)函式用於查找兩個參數表達式的乘積。

**Format**

```sql
{NUMBER} * {NUMBER}
```

**範例**

以下PQL查詢可查找庫存的產品和產品價格，以查找產品的總值。

```sql
product.inventory * product.price
```

## 去除

利用 `-` （減法）函式來尋找兩個引數表達式的差異。

**Format**

```sql
{NUMBER} - {NUMBER}
```

**範例**

以下PQL查詢可查找兩個不同產品之間的價格差異。

```sql
product1.price - product2.price
```

## 除法

( `/` 除法)函式用於查找兩個引數表達式的商。

**Format**

```sql
{NUMBER} / {NUMBER}
```

**範例**

以下PQL查詢會查找售出產品總數與收入總額之間的商數，以查看每個項目的平均成本。

```sql
totalProduct.price / totalProduct.sold
```

## 剩餘

( `%` modulo/remainder)函式用於在將兩個引數表達式除以後查找余數。

**Format**

```sql
{NUMBER} % {NUMBER}
```

**範例**

以下PQL查詢會檢查人員的年齡是否可除以5。

```sql
person.age % 5 = 0
```

## 後續步驟

現在您已瞭解算術函式，可以在PQL查詢中使用它們。 有關其他PQL函式的詳細資訊，請閱讀配置式查 [詢語言概述](./overview.md)。
