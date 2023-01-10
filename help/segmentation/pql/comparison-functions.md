---
keywords: Experience Platform；首頁；熱門主題；分段；分段服務；PQL;PQL；設定檔查詢語言；比較函式；比較；
solution: Experience Platform
title: PQL比較功能
description: 比較函式可用來比較不同運算式和值，並據以傳回「true」或「false」。
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 9%

---

# 比較函式

比較函式可用來比較不同運算式和值，並傳回 `true` 或 `false` 因此。 有關其他PQL函式的詳細資訊，請參見 [[!DNL Profile Query Language] 概述](./overview.md).

## 等於

此 `=` （等於）函式會檢查某個值或運算式是否等於另一個值或運算式。

**格式**

```sql
{EXPRESSION} = {VALUE}
```

**範例**

下列PQL查詢會檢查首頁地址國家/地區是否位於加拿大。

```sql
homeAddress.countryISO = "CA"
```

## 不等於

此 `!=` （不等於）函式檢查一個值或表達式是否為 **not** 等於其他值或運算式。

**格式**

```sql
{EXPRESSION} != {VALUE}
```

**範例**

以下PQL查詢會檢查主地址國家/地區是否不在加拿大。

```sql
homeAddress.countryISO != "CA"
```

## Greater than

此 `>` （大於）函式用來檢查第一值是否大於第二值。

**格式**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**範例**

以下PQL查詢會定義生日不會在1月或2月的人。

```sql
person.birthMonth > 2
```

## 大於或等於

此 `>=` （大於或等於）函式用來檢查第一值是否大於或等於第二值。

**格式**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**範例**

以下PQL查詢會定義生日不會在1月或2月的人。

```sql
person.birthMonth >= 3
```

## 少於

此 `<` （小於）比較函式用來檢查第一值是否小於第二值。

**格式**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**範例**

以下PQL查詢定義生日為1月的人。

```sql
person.birthMonth < 2
```

## Less than or equal to

此 `<=` （小於或等於）比較函式用於檢查第一值是否小於或等於第二值。

**格式**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**範例**

以下PQL查詢定義生日為1月或2月的人。

```sql
person.birthMonth <= 2
```

## 後續步驟

現在您已了解比較功能，可以在PQL查詢中使用這些功能。 有關其他PQL功能的詳細資訊，請閱讀 [設定檔查詢語言概觀](./overview.md).
