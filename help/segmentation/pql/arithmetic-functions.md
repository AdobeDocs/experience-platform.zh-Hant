---
solution: Experience Platform
title: PAL算術函式
description: 算術函式用於對設定檔查詢語言(PQL)中的值執行基本計算。
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 6%

---

# 算術函式

算術函式用於對中的值執行基本計算 [!DNL Profile Query Language] (PQL)。 如需其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md).

## 新增

此 `+` （加法）函式用於找出兩個引數運算式的總和。

**格式**

```sql
{NUMBER} + {NUMBER}
```

**範例**

下列PQL查詢會加總兩個不同產品的價格。

```sql
product1.price + product2.price
```

## 乘

此 `*` （乘法）函式用於尋找兩個引數運算式的乘積。

**格式**

```sql
{NUMBER} * {NUMBER}
```

**範例**

下列PQL查詢會尋找存貨的產品與產品價格，以尋找產品的總值。

```sql
product.inventory * product.price
```

## 減

此 `-` （減法）函式用於找出兩個引數運算式的差異。

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

此 `/` (division)函式用於尋找兩個引數運算式的商。

**格式**

```sql
{NUMBER} / {NUMBER}
```

**範例**

下列PQL查詢會找出產品銷售總計與收入總計之間的商，以檢視每個專案的平均成本。

```sql
totalProduct.price / totalProduct.sold
```

## 餘數

此 `%` （模數/餘數）函式用來找出兩個引數運算式相除後的餘數。

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

現在您已了解算術函式，可以在PQL查詢中使用它們。 如需其他PQL函式的詳細資訊，請參閱 [設定檔查詢語言概觀](./overview.md).
