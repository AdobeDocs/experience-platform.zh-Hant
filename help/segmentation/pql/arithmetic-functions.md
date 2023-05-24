---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；PQL;PQL；配置檔案查詢語言；算術函式；算術；
solution: Experience Platform
title: PAL算術函式
description: 算術函式用於對配置檔案查詢語言(PQL)中的值執行基本計算。
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 5%

---

# 算術函式

算術函式用於對中的值執行基本計算 [!DNL Profile Query Language] (PQL)。 有關其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md)。

## 新增

的 `+` (addition)函式用於查找兩個參數表達式的和。

**格式**

```sql
{NUMBER} + {NUMBER}
```

**範例**

以下PQL查詢總計了兩種不同產品的價格。

```sql
product1.price + product2.price
```

## 乘

的 `*` （乘法）函式用於查找兩個參數表達式的乘積。

**格式**

```sql
{NUMBER} * {NUMBER}
```

**範例**

以下PQL查詢會查找庫存的產品和產品的價格，以查找產品的總值。

```sql
product.inventory * product.price
```

## 減

的 `-` （減法）函式用於查找兩個參數表達式的差。

**格式**

```sql
{NUMBER} - {NUMBER}
```

**範例**

以下PQL查詢會查找兩個不同產品之間的價格差異。

```sql
product1.price - product2.price
```

## 除

的 `/` （除法）函式用於求兩個參數表達式的商。

**格式**

```sql
{NUMBER} / {NUMBER}
```

**範例**

以下PQL查詢將查找銷售產品總數與查看每個項目的平均成本所得總金額之間的商數。

```sql
totalProduct.price / totalProduct.sold
```

## 余數

的 `%` (modulo/remainder)函式用於在分割兩個參數表達式後查找余數。

**格式**

```sql
{NUMBER} % {NUMBER}
```

**範例**

以下PQL查詢檢查人員的年齡是否可被5除。

```sql
person.age % 5 = 0
```

## 後續步驟

現在您已學習了算術函式，可以在PQL查詢中使用它們。 有關其他PQL功能的詳細資訊，請閱讀 [配置檔案查詢語言概述](./overview.md)。
