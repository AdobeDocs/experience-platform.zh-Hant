---
keywords: Experience Platform;home；熱門主題；分段；分段；分段服務；pql;PQL；配置檔案查詢語言；比較函式；比較；
solution: Experience Platform
title: PQL比較函式
topic-legacy: developer guide
description: 比較函式可用來比較不同的運算式和值，並據以傳回"true"或"false"。
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 9%

---

# 比較函式

比較函式用於比較不同的運算式和值，並據以傳回`true`或`false`。 有關其他PQL函式的詳細資訊，請參閱[[!DNL Profile Query Language] overview](./overview.md)。

## 等於

`=`(equals)函式會檢查一個值或運算式是否等於另一個值或運算式。

**格式**

```sql
{EXPRESSION} = {VALUE}
```

**範例**

以下PQL查詢檢查主地址國家／地區是否位於加拿大。

```sql
homeAddress.countryISO = "CA"
```

## 不等於

`!=`（不等於）函式會檢查一個值或運算式是否為&#x200B;**not**&#x200B;等於另一個值或運算式。

**格式**

```sql
{EXPRESSION} != {VALUE}
```

**範例**

以下PQL查詢會檢查主地址國家／地區是否不在加拿大。

```sql
homeAddress.countryISO != "CA"
```

## Greater than

`>`（大於）函式用於檢查第一值是否大於第二值。

**格式**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**範例**

以下PQL查詢定義生日不在1月或2月的人。

```sql
person.birthMonth > 2
```

## Greater than or equal to

使用`>=`（大於或等於）函式來檢查第一值是否大於或等於第二值。

**格式**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**範例**

以下PQL查詢定義生日不在1月或2月的人。

```sql
person.birthMonth >= 3
```

## Less than

使用`<`（小於）比較函式來檢查第一值是否小於第二值。

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

使用`<=`（小於或等於）比較函式來檢查第一值是否小於或等於第二值。

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

現在您已瞭解了比較函式，可以在PQL查詢中使用它們。 有關其他PQL函式的詳細資訊，請閱讀[配置檔案查詢語言概述](./overview.md)。
