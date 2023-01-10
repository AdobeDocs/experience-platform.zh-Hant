---
keywords: Experience Platform；首頁；熱門主題；分段；分段服務；PQL;PQL；設定檔查詢語言；算術函式；算術；
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

運算函式用於對 [!DNL Profile Query Language] (PQL)。 有關其他PQL函式的詳細資訊，請參見 [[!DNL Profile Query Language] 概述](./overview.md).

## 新增

此 `+` (addition)函式可用來尋找兩個引數運算式的總和。

**格式**

```sql
{NUMBER} + {NUMBER}
```

**範例**

以下PQL查詢會加總兩種不同產品的價格。

```sql
product1.price + product2.price
```

## 乘

此 `*` （乘法）函式用於查找兩個參數表達式的乘積。

**格式**

```sql
{NUMBER} * {NUMBER}
```

**範例**

以下PQL查詢將查找庫存的產品和產品價格，以查找產品的總值。

```sql
product.inventory * product.price
```

## 減去

此 `-` （減法）函式用於尋找兩個引數運算式的差異。

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

此 `/` （除法）函式用於求兩個參數表達式的商。

**格式**

```sql
{NUMBER} / {NUMBER}
```

**範例**

以下PQL查詢將查找銷售產品總數與收入總額之間的商，以查看每項的平均成本。

```sql
totalProduct.price / totalProduct.sold
```

## 余數

此 `%` (modulo/remaind)函式用於在將兩個參數表達式除以後查找余數。

**格式**

```sql
{NUMBER} % {NUMBER}
```

**範例**

以下PQL查詢會檢查人員的年齡是否可除以5歲。

```sql
person.age % 5 = 0
```

## 後續步驟

現在您已了解算術函式，可以在PQL查詢中使用這些函式。 有關其他PQL功能的詳細資訊，請閱讀 [設定檔查詢語言概觀](./overview.md).
