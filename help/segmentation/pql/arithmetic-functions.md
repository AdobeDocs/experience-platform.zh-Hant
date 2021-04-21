---
keywords: Experience Platform;home；熱門話題；分段；分段；分段服務；pql;PQL；配置檔案查詢語言；算術函式；算術；
solution: Experience Platform
title: PAL算術函式
topic-legacy: developer guide
description: 算術函式用於對配置檔案查詢語言(PQL)中的值執行基本計算。
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 5%

---

# 算術函式

算術函式用於對[!DNL Profile Query Language](PQL)中的值執行基本計算。 有關其他PQL函式的詳細資訊，請參閱[[!DNL Profile Query Language] overview](./overview.md)。

## 新增

`+`（加法）函式用於查找兩個引數表達式的總和。

**格式**

```sql
{NUMBER} + {NUMBER}
```

**範例**

以下PQL查詢總結了兩個不同產品的價格。

```sql
product1.price + product2.price
```

## 乘

`*`（乘法）函式用於查找兩個參數表達式的乘積。

**格式**

```sql
{NUMBER} * {NUMBER}
```

**範例**

以下PQL查詢可查找庫存的產品和產品價格，以查找產品的總值。

```sql
product.inventory * product.price
```

## 去除

`-`（減法）函式用於查找兩個參數表達式的差。

**格式**

```sql
{NUMBER} - {NUMBER}
```

**範例**

以下PQL查詢可查找兩個不同產品之間的價格差異。

```sql
product1.price - product2.price
```

## 除法

`/`（除法）函式用於查找兩個引數表達式的商。

**格式**

```sql
{NUMBER} / {NUMBER}
```

**範例**

以下PQL查詢會查找售出產品總數與收入總額之間的商數，以查看每個項目的平均成本。

```sql
totalProduct.price / totalProduct.sold
```

## 剩餘

`%`(modulo/remainder)函式用於在將兩個引數表達式除以後查找余數。

**格式**

```sql
{NUMBER} % {NUMBER}
```

**範例**

以下PQL查詢會檢查人員的年齡是否可除以5。

```sql
person.age % 5 = 0
```

## 後續步驟

現在您已瞭解算術函式，可以在PQL查詢中使用它們。 有關其他PQL函式的詳細資訊，請閱讀[配置檔案查詢語言概述](./overview.md)。
