---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；pql;PQL；配置檔案查詢語言；字串函式；字串；
solution: Experience Platform
title: PQL字串函式
description: 配置檔案查詢語言(PQL)提供使字串交互更簡單的函式。
exl-id: 9fd79d86-0802-4312-abce-f6ef5ba5bb34
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 6%

---

# 字串函式

[!DNL Profile Query Language] (PQL)提供使字串交互更簡單的函式。 有關其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md)。

## 像

的 `like` 函式用於確定字串是否與指定的模式匹配。

**格式**

```sql
{STRING_1} like {STRING_2}
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要與第一個字串匹配的表達式。 建立表達式時支援兩個特殊字元： `%` 和 `_`。 <ul><li>`%` 用於表示零個或多個字元。</li><li>`_` 只表示一個字元。</li></ul> |

**範例**

以下PQL查詢將檢索包含模式「es」的所有城市。

```sql
city like "%es%"
```

## 開始於

的 `startsWith` 函式用於確定字串是否以指定的子字串開頭。

**格式**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串內搜索的字串。 |
| `{BOOLEAN}` | 用於確定檢查是否區分大小寫的可選參數。 預設情況下，此值設定為true。 |

**範例**

以下PQL查詢以「Joe」開頭，並區分大小寫確定人員的姓名。

```sql
person.name.startsWith("Joe")
```

## 不以開頭

的 `doesNotStartWith` 函式用於確定字串是否不以指定的子字串開頭。

**格式**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串內搜索的字串。 |
| `{BOOLEAN}` | 用於確定檢查是否區分大小寫的可選參數。 預設情況下，此值設定為true。 |

**範例**

以下PQL查詢以區分大小寫的方式確定人員姓名不以「Joe」開頭。

```sql
person.name.doesNotStartWith("Joe")
```

## 終止於

的 `endsWith` 函式用於確定字串是否以指定的子字串結尾。

**格式**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串內搜索的字串。 |
| `{BOOLEAN}` | 用於確定檢查是否區分大小寫的可選參數。 預設情況下，此值設定為true。 |

**範例**

以下PQL查詢以「.com」結尾，並區分大小寫。

```sql
person.emailAddress.endsWith(".com")
```

## 不以

的 `doesNotEndWith` 函式用於確定字串是否以指定的子字串結尾。

**格式**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串內搜索的字串。 |
| `{BOOLEAN}` | 用於確定檢查是否區分大小寫的可選參數。 預設情況下，此值設定為true。 |

**範例**

以下PQL查詢以區分大小寫的方式確定人員的電子郵件地址不以&quot;。com&quot;結尾。

```sql
person.emailAddress.doesNotEndWith(".com")
```

## 包含

的 `contains` 函式用於確定字串是否包含指定的子字串。

**格式**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串內搜索的字串。 |
| `{BOOLEAN}` | 用於確定檢查是否區分大小寫的可選參數。 預設情況下，此值設定為true。 |

**範例**

以下PQL查詢以區分大小寫的方式確定人員的電子郵件地址是否包含字串&quot;2010@gm&quot;。

```sql
person.emailAddress.contains("2010@gm")
```

## 不包含

的 `doesNotContain` 函式用於確定字串是否不包含指定的子字串。

**格式**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串內搜索的字串。 |
| `{BOOLEAN}` | 用於確定檢查是否區分大小寫的可選參數。 預設情況下，此值設定為true。 |

**範例**

以下PQL查詢以區分大小寫的方式確定人員的電子郵件地址不包含字串「2010@gm」。

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## 等於

的 `equals` 函式用於確定字串是否等於指定的字串。

**格式**

```sql
{STRING_1}.equals({STRING_2})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要與第一個字串進行比較的字串。 |

**範例**

以下PQL查詢以區分大小寫的方式確定人員的姓名是「John」。

```sql
person.name.equals("John")
```

## 不等於

的 `notEqualTo` 函式用於確定字串是否不等於指定的字串。

**格式**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要與第一個字串進行比較的字串。 |

**範例**

以下PQL查詢以區分大小寫的方式確定人員的姓名不是「John」。

```sql
person.name.notEqualTo("John")
```

## 符合

的 `matches` 函式用於確定字串是否與特定規則運算式匹配。 請參閱 [此文檔](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) 的子菜單。

**格式**

```sql
{STRING_1}.matches(STRING_2})
```

**範例**

以下PQL查詢確定人員姓名以「John」開頭（不區分大小寫）。

```sql
person.name.matches("(?i)^John")
```

>[!NOTE]
>
>如果使用規則運算式函式，如 `\w`, **必須** 轉義反斜線字元。 所以，不要只寫 `\w`，必須包含額外的反斜線並寫入 `\\w`。

## 規則運算式組

的 `regexGroup` 函式用於根據所提供的規則運算式提取特定資訊。

**格式**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**範例**

以下PQL查詢用於從電子郵件地址中提取域名。

```sql
emailAddress.regexGroup("@(\\w+)", 1)
```

>[!NOTE]
>
>如果使用規則運算式函式，如 `\w`, **必須** 轉義反斜線字元。 所以，不要只寫 `\w`，必須包含額外的反斜線並寫入 `\\w`。

## 後續步驟

現在您已學習了字串函式，可以在PQL查詢中使用它們。 有關其他PQL功能的詳細資訊，請閱讀 [配置檔案查詢語言概述](./overview.md)。
