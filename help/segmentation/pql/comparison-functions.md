---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；pql;PQL；配置檔案查詢語言；比較函式；比較；
solution: Experience Platform
title: PQL比較函式
description: 比較函式用於比較不同的表達式和值，並相應地返回"true"或"false"。
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 9%

---

# 比較函式

比較函式用於比較不同表達式和值，返回 `true` 或 `false` 因此。 有關其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md)。

## 等於

的 `=` （等於）函式檢查一個值或表達式是否等於另一個值或表達式。

**格式**

```sql
{EXPRESSION} = {VALUE}
```

**範例**

以下PQL查詢檢查家庭地址國家/地區是否在加拿大。

```sql
homeAddress.countryISO = "CA"
```

## 不等於

的 `!=` （不相等）函式檢查一個值或表達式 **不** 等於另一個值或表達式。

**格式**

```sql
{EXPRESSION} != {VALUE}
```

**範例**

以下PQL查詢檢查家庭地址國家/地區是否不在加拿大。

```sql
homeAddress.countryISO != "CA"
```

## Greater than

的 `>` （大於）函式用於檢查第一值是否大於第二值。

**格式**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**範例**

以下PQL查詢定義生日不在1月或2月的人。

```sql
person.birthMonth > 2
```

## 大於或等於

的 `>=` （大於或等於）函式用於檢查第一值是否大於或等於第二值。

**格式**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**範例**

以下PQL查詢定義生日不在1月或2月的人。

```sql
person.birthMonth >= 3
```

## 少於

的 `<` （小於）比較函式用於檢查第一值是否小於第二值。

**格式**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**範例**

以下PQL查詢定義生日在1月的人。

```sql
person.birthMonth < 2
```

## Less than or equal to

的 `<=` 比較函式用於檢查第一值是否小於或等於第二值。

**格式**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**範例**

以下PQL查詢定義生日在1月或2月的人。

```sql
person.birthMonth <= 2
```

## 後續步驟

現在您已經瞭解了比較函式，可以在PQL查詢中使用它們。 有關其他PQL功能的詳細資訊，請閱讀 [配置檔案查詢語言概述](./overview.md)。
