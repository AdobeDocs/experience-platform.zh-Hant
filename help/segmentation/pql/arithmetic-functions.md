---
solution: Experience Platform
title: PAL算術函式
description: 算術函式可用來對Profile Query Language (PQL)中的值執行基本計算。
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 4%

---

# 算術函式

算術函式是用來對[!DNL Profile Query Language] (PQL)中的值執行基本計算。 如需其他PQL函式的詳細資訊，請參閱[[!DNL Profile Query Language] 總覽](./overview.md)。

## 新增

`+` （加法）函式是用來尋找兩個引數運算式的加總。

**格式**

```sql
{NUMBER} + {NUMBER}
```

**範例**

以下PQL查詢會加總兩個不同產品的價格。

```sql
product1.price + product2.price
```

## 乘

`*` （乘法）函式用於尋找兩個引數運算式的乘積。

**格式**

```sql
{NUMBER} * {NUMBER}
```

**範例**

下列PQL查詢會尋找庫存的產品和產品價格，以尋找產品的總值。

```sql
product.inventory * product.price
```

## 減

`-` （減法）函式是用來找出兩個引數運算式的差異。

**格式**

```sql
{NUMBER} - {NUMBER}
```

**範例**

下列PQL查詢會找出兩個不同產品之間的價格差異。

```sql
product1.price - product2.price
```

## 除

`/` （除法）函式用於尋找兩個引數運算式的商。

**格式**

```sql
{NUMBER} / {NUMBER}
```

**範例**

下列PQL查詢會找出已售出產品總數與已賺取總金額之間的商數，以檢視每個專案的平均成本。

```sql
totalProduct.price / totalProduct.sold
```

## 餘數

`%` （模數/餘數）函式用來找出兩個引數運算式相除後的餘數。

**格式**

```sql
{NUMBER} % {NUMBER}
```

**範例**

以下PQL查詢檢查個人的年齡是否可被5整除。

```sql
person.age % 5 = 0
```

## 後續步驟

現在您已了解算術函式，可以在PQL查詢中使用它們。 如需其他PQL功能的詳細資訊，請參閱[Profile Query Language概觀](./overview.md)。
