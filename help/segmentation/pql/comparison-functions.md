---
solution: Experience Platform
title: PQL比較函式
description: 比較函式是用來比較不同運算式和值之間的差異，並傳回「true」或「false」。
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
source-git-commit: a4385d8872b71ded7e9121d445e10f1ffbd83cfe
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 7%

---

# 比較函式

比較函式是用來比較不同的運算式和值，並傳回`true`或`false`。 如需其他PQL函式的詳細資訊，請參閱[[!DNL Profile Query Language] 總覽](./overview.md)。

## 等於

`=` （等於）函式檢查一個值或運算式是否等於另一個值或運算式。

**格式**

```sql
{EXPRESSION} = {VALUE}
```

**範例**

以下PQL查詢會檢查住家地址國家/地區是否位於加拿大。

```sql
homeAddress.countryISO = "CA"
```

## 不等於

`!=` （不等於）函式檢查一個值或運算式是否為&#x200B;**不**&#x200B;等於另一個值或運算式。

**格式**

```sql
{EXPRESSION} != {VALUE}
```

**範例**

以下PQL查詢會檢查住家地址國家/地區是否不在加拿大。

```sql
homeAddress.countryISO != "CA"
```

## 大於

`>` （大於）函式用於檢查第一個值是否大於第二個值。

**格式**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**範例**

下列PQL查詢定義生日在一月或二月以下的人員。

```sql
person.birthMonth > 2
```

## 大於或等於

`>=` （大於或等於）函式用於檢查第一個值是否大於或等於第二個值。

**格式**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**範例**

下列PQL查詢定義生日在一月或二月以下的人員。

```sql
person.birthMonth >= 3
```

## 小於

`<` （小於）比較函式可用來檢查第一個值是否小於第二個值。

**格式**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**範例**

下列PQL查詢定義了一月生日的使用者。

```sql
person.birthMonth < 2
```

## 小於或等於

`<=` （小於或等於）比較函式是用來檢查第一個值是否小於或等於第二個值。

**格式**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**範例**

下列PQL查詢定義生日在一月或二月的人員。

```sql
person.birthMonth <= 2
```

## 後續步驟

現在您已瞭解比較函式，可以在PQL查詢中使用它們。 如需其他PQL功能的詳細資訊，請參閱[Profile Query Language概觀](./overview.md)。
