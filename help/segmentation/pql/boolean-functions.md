---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；pql;PQL；配置檔案查詢語言；布爾函式；布爾函式；
solution: Experience Platform
title: PQL布爾函式
description: 布爾函式用於對配置檔案查詢語言(PQL)中的不同元素執行布爾邏輯。
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 5%

---

# 布爾函式

布爾函式用於對中的不同元素執行布爾邏輯 [!DNL Profile Query Language] (PQL)。  有關其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md)。

## 和

的 `and` 函式用於建立邏輯連接。

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

的 `or` 函式用於建立邏輯斷開。

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

的 `not` 或 `!`)函式用於建立邏輯否定。

**格式**

```sql
not ({QUERY})
!({QUERY})
```

**範例**

以下PQL查詢將返回所有沒有其祖國為加拿大的人。

```sql
not (homeAddress.countryISO = "CA")
```

## 若  

的 `if` 函式用於根據指定的條件是否為true來解析表達式。

**格式**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | 正在測試的布爾表達式。 |
| `{TRUE_EXPRESSION}` | 在 `{TEST_EXPRESSION}` 是真的。 |
| `{FALSE_EXPRESSION}` | 在 `{TEST_EXPRESSION}` 為false。 |

**範例**

以下PQL查詢將值設定為 `1` 如果母國是加拿大 `2` 不是加拿大。

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## 後續步驟

現在您已經瞭解了布爾函式，可以在PQL查詢中使用它們。 有關其他PQL功能的詳細資訊，請閱讀 [配置檔案查詢語言概述](./overview.md)。
