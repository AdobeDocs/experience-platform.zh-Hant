---
solution: Experience Platform
title: PQL比較函式
description: 比較函式是用來比較不同運算式和值之間的差異，並傳回「true」或「false」。
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 10%

---

# 比較函式

比較函式是用來比較不同運算式和值之間的差異，傳回 `true` 或 `false` 視情況而定。 如需其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md).

## 等於

此 `=` （等於）函式檢查一個值或運算式是否等於另一個值或運算式。

**格式**

```sql
{EXPRESSION} = {VALUE}
```

**範例**

下列PQL查詢會檢查住家地址國家/地區是否位於加拿大。

```sql
homeAddress.countryISO = "CA"
```

## 不等於

此 `!=` （不等於）函式檢查一個值或運算式是否為 **非** 等於另一個值或運算式。

**格式**

```sql
{EXPRESSION} != {VALUE}
```

**範例**

下列PQL查詢會檢查住家地址國家/地區是否不在加拿大。

```sql
homeAddress.countryISO != "CA"
```

## Greater than

此 `>` （大於）函式來檢查第一個值是否大於第二個值。

**格式**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**範例**

以下PQL查詢定義生日在1月或2月以下的人。

```sql
person.birthMonth > 2
```

## 大於或等於

此 `>=` （大於或等於）函式來檢查第一個值是否大於或等於第二個值。

**格式**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**範例**

以下PQL查詢定義生日在1月或2月以下的人。

```sql
person.birthMonth >= 3
```

## 少於

此 `<` （小於）比較函式用於檢查第一個值是否小於第二個值。

**格式**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**範例**

以下PQL查詢定義生日在一月的人員。

```sql
person.birthMonth < 2
```

## Less than or equal to

此 `<=` （小於或等於）比較函式用於檢查第一個值是否小於或等於第二個值。

**格式**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**範例**

以下PQL查詢定義生日在一月或二月的人員。

```sql
person.birthMonth <= 2
```

## 後續步驟

現在您已瞭解比較函式，可以在PQL查詢中使用它們。 如需其他PQL函式的詳細資訊，請參閱 [設定檔查詢語言概觀](./overview.md).
