---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 比較函式
topic: developer guide
translation-type: tm+mt
source-git-commit: 84a5b992639c1cabfdeaec5262964c9873826592
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 10%

---


# 比較函式

比較函式可用來比較不同的運算式和值，並傳回 `true` 或相 `false` 應。 有關其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md)。

## 等於

( `=` equals)函式會檢查一個值或運算式是否等於另一個值或運算式。

**Format**

```sql
{EXPRESSION} = {VALUE}
```

**範例**

以下PQL查詢檢查主地址國家／地區是否位於加拿大。

```sql
homeAddress.countryISO = "CA"
```

## 不等於

( `!=` 不等於)函式會檢查一個值或運算式是否 **不等於** 其他值或運算式。

**Format**

```sql
{EXPRESSION} != {VALUE}
```

**範例**

以下PQL查詢會檢查主地址國家／地區是否不在加拿大。

```sql
homeAddress.countryISO != "CA"
```

## Greater than

( `>` 大於)函式用於檢查第一值是否大於第二值。

**Format**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**範例**

以下PQL查詢定義生日不在1月或2月的人。

```sql
person.birthMonth > 2
```

## Greater than or equal to

使 `>=` 用（大於或等於）函式來檢查第一值是否大於或等於第二值。

**Format**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**範例**

以下PQL查詢定義生日不在1月或2月的人。

```sql
person.birthMonth >= 3
```

## Less than

該 `<` （小於）比較函式用於檢查第一值是否小於第二值。

**Format**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**範例**

以下PQL查詢定義生日在1月的人。

```sql
person.birthMonth < 2
```

## Less than or equal to

比 `<=` 較函式（小於或等於）用於檢查第一值是否小於或等於第二值。

**Format**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**範例**

以下PQL查詢定義生日在1月或2月的人。

```sql
person.birthMonth <= 2
```

## 後續步驟

現在您已瞭解了比較函式，可以在PQL查詢中使用它們。 有關其他PQL函式的詳細資訊，請閱讀配置式查 [詢語言概述](./overview.md)。
