---
keywords: Experience Platform;home；熱門主題；分段；分段；分段服務；pql;PQL；配置檔案查詢語言；布爾函式；布林值；
solution: Experience Platform
title: PQL布爾函式
topic-legacy: developer guide
description: 布林函式用於對配置檔案查詢語言(PQL)中的不同元素執行布爾邏輯。
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 5%

---

# 布爾函式

布林函式用於對[!DNL Profile Query Language](PQL)中的不同元素執行布林邏輯。  有關其他PQL函式的詳細資訊，請參閱[[!DNL Profile Query Language] overview](./overview.md)。

## 和

`and`函式用於建立邏輯連接。

**格式**

```sql
{QUERY} and {QUERY}
```

**範例**

以下PQL查詢將返回所有在加拿大和1985年出生的人。

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## 或

`or`函式用於建立邏輯分離。

**格式**

```sql
{QUERY} or {QUERY}
```

**範例**

以下PQL查詢將返回所有在加拿大或1985年出生的人。

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## Not

`not`（或`!`）函式用於建立邏輯否定。

**格式**

```sql
not ({QUERY})
!({QUERY})
```

**範例**

以下PQL查詢將返回所有沒有其祖國為加拿大的人員。

```sql
not (homeAddress.countryISO = "CA")
```

## 若  

`if`函式用於解析表達式，具體取決於指定的條件是否為真。

**格式**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | 正在測試的布爾表達式。 |
| `{TRUE_EXPRESSION}` | 如果`{TEST_EXPRESSION}`為true，則使用其值的表達式。 |
| `{FALSE_EXPRESSION}` | 如果`{TEST_EXPRESSION}`為false，則使用其值的運算式。 |

**範例**

以下PQL查詢將將值設定為`1`（如果原始國家為加拿大），如果原始國家為`2`（如果原始國家為加拿大）。

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## 後續步驟

現在，您已經瞭解了布爾函式，您可以在PQL查詢中使用它們。 有關其他PQL函式的詳細資訊，請閱讀[配置檔案查詢語言概述](./overview.md)。
