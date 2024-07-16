---
solution: Experience Platform
title: PQL布林函式
description: 布林值函式可用來對Profile Query Language (PQL)中的不同元素執行布林值邏輯。
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 4%

---

# 布林函式

布林函式是用來對[!DNL Profile Query Language] (PQL)中不同的元素執行布林邏輯。  如需其他PQL函式的詳細資訊，請參閱[[!DNL Profile Query Language] 總覽](./overview.md)。

## 及

`and`函式用來建立邏輯結合。

**格式**

```sql
{QUERY} and {QUERY}
```

**範例**

以下PQL查詢將傳回所有具有加拿大國籍和1985年出生年份的人。

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## 或

`or`函式用來建立邏輯分離。

**格式**

```sql
{QUERY} or {QUERY}
```

**範例**

下列PQL查詢將傳回所有居住國為加拿大或1985年出生年份的人。

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## 不是

`not` （或`!`）函式用來建立邏輯否定。

**格式**

```sql
not ({QUERY})
!({QUERY})
```

**範例**

以下PQL查詢將傳回所有沒有祖國為加拿大的人。

```sql
not (homeAddress.countryISO = "CA")
```

## If

`if`函式用於解析運算式，需視指定的條件是否為true而定。

**格式**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | 正在測試的布林運算式。 |
| `{TRUE_EXPRESSION}` | `{TEST_EXPRESSION}`為true時將使用其值的運算式。 |
| `{FALSE_EXPRESSION}` | 如果`{TEST_EXPRESSION}`為False，則會使用運算式的值。 |

**範例**

如果主國家/地區是加拿大，下列PQL查詢會將值設定為`1`，如果主國家/地區不是加拿大，則設定為`2`。

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## 後續步驟

現在您已瞭解布林函式，可以在PQL查詢中使用它們。 如需其他PQL功能的詳細資訊，請參閱[Profile Query Language概觀](./overview.md)。
