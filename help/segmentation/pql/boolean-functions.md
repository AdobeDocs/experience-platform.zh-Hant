---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 布爾函式
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 6%

---


# 布爾函式

布爾函式用於對(PQL)中的不同元素執行 [!DNL Profile Query Language] 布爾邏輯。  有關其他PQL函式的詳細資訊，請參閱「配置檔案查 [詢語言」概述](./overview.md)。

## 和

函式 `and` 用於建立邏輯連接。

**Format**

```sql
{QUERY} and {QUERY}
```

**範例**

以下PQL查詢將返回所有在加拿大和1985年出生的人。

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## 或

該 `or` 函式用於建立邏輯分離。

**Format**

```sql
{QUERY} or {QUERY}
```

**範例**

以下PQL查詢將返回所有在加拿大或1985年出生的人。

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## Not

( `not` 或 `!`)函式用來建立邏輯否定。

**Format**

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

函式 `if` 用於根據指定的條件是否為真來解析表達式。

**Format**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | 正在測試的布爾表達式。 |
| `{TRUE_EXPRESSION}` | 如果為true，則使用其值的運 `{TEST_EXPRESSION}` 算式。 |
| `{FALSE_EXPRESSION}` | 若為false，則使用其值的 `{TEST_EXPRESSION}` 運算式。 |

**範例**

以下PQL查詢將設定該值，如 `1` 果母國是加拿大， `2` 如果母國不是加拿大。

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## 後續步驟

現在，您已經瞭解了布爾函式，您可以在PQL查詢中使用它們。 有關其他PQL函式的詳細資訊，請閱讀配置式查 [詢語言概述](./overview.md)。
