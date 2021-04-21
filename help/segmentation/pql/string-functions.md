---
keywords: Experience Platform;home；熱門主題；分段；分段；分段服務；pql;PQL；配置檔案查詢語言；字串函式；字串；
solution: Experience Platform
title: PQL字串函式
topic-legacy: developer guide
description: 描述檔查詢語言(PQL)提供函式，讓字串互動更簡單。
exl-id: 9fd79d86-0802-4312-abce-f6ef5ba5bb34
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 6%

---

# 字串函式

[!DNL Profile Query Language] (PQL)提供函式，讓字串互動更簡單。有關其他PQL函式的詳細資訊，請參閱[[!DNL Profile Query Language] overview](./overview.md)。

## 贊

`like`函式用於確定字串是否與指定的模式匹配。

**格式**

```sql
{STRING_1} like {STRING_2}
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 與第一個字串相符的運算式。 建立表達式時有兩個支援的特殊字元：`%`和`_`。 <ul><li>`%` 用於表示零或多個字元。</li><li>`_` 僅代表一個字元。</li></ul> |

**範例**

以下PQL查詢檢索包含模式&quot;es&quot;的所有城市。

```sql
city like "%es%"
```

## 開始於

`startsWith`函式用於確定字串是否以指定的子字串開頭。

**格式**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串內搜索的字串。 |
| `{BOOLEAN}` | 可選參數，用於確定檢查是否區分大小寫。 依預設，此值會設為true。 |

**範例**

以下PQL查詢以區分大小寫的方式確定人員名稱是否以&quot;Joe&quot;開頭。

```sql
person.name.startsWith("Joe")
```

## 不以

`doesNotStartWith`函式用於確定字串是否不以指定的子字串開頭。

**格式**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串內搜索的字串。 |
| `{BOOLEAN}` | 可選參數，用於確定檢查是否區分大小寫。 依預設，此值會設為true。 |

**範例**

以下PQL查詢會區分大小寫確定人員的姓名不是以&quot;Joe&quot;開頭。

```sql
person.name.doesNotStartWith("Joe")
```

## 終止於

`endsWith`函式用於確定字串是否以指定的子字串結尾。

**格式**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串內搜索的字串。 |
| `{BOOLEAN}` | 可選參數，用於確定檢查是否區分大小寫。 依預設，此值會設為true。 |

**範例**

以下PQL查詢會區分大小寫確定人員的電子郵件地址是否以&quot;。com&quot;結尾。

```sql
person.emailAddress.endsWith(".com")
```

## 不以

`doesNotEndWith`函式用於確定字串是否不以指定的子字串結尾。

**格式**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串內搜索的字串。 |
| `{BOOLEAN}` | 可選參數，用於確定檢查是否區分大小寫。 依預設，此值會設為true。 |

**範例**

以下PQL查詢會區分大小寫確定人員的電子郵件地址未以&quot;。com&quot;結尾。

```sql
person.emailAddress.doesNotEndWith(".com")
```

## 包含

`contains`函式用於確定字串是否包含指定的子字串。

**格式**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串內搜索的字串。 |
| `{BOOLEAN}` | 可選參數，用於確定檢查是否區分大小寫。 依預設，此值會設為true。 |

**範例**

以下PQL查詢會區分大小寫確定人員的電子郵件地址是否包含字串&quot;2010@gm&quot;。

```sql
person.emailAddress.contains("2010@gm")
```

## 不包含

`doesNotContain`函式用於確定字串是否不包含指定的子字串。

**格式**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串內搜索的字串。 |
| `{BOOLEAN}` | 可選參數，用於確定檢查是否區分大小寫。 依預設，此值會設為true。 |

**範例**

以下PQL查詢會區分大小寫確定人員的電子郵件地址中是否不包含字串&quot;2010@gm&quot;。

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## 等於

`equals`函式用於確定字串是否等於指定字串。

**格式**

```sql
{STRING_1}.equals({STRING_2})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要與第一個字串比較的字串。 |

**範例**

以下PQL查詢會區分大小寫確定人員的名稱是否為&quot;John&quot;。

```sql
person.name.equals("John")
```

## 不等於

`notEqualTo`函式用於確定字串是否不等於指定字串。

**格式**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要與第一個字串比較的字串。 |

**範例**

以下PQL查詢會區分大小寫確定人員的名稱不是&quot;John&quot;。

```sql
person.name.notEqualTo("John")
```

## 符合

`matches`函式用於確定字串是否與特定規則運算式匹配。 有關規則運算式中的匹配模式的詳細資訊，請參閱[本檔案](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html)。

**格式**

```sql
{STRING_1}.matches(STRING_2})
```

**範例**

以下PQL查詢可確定人員的名稱是否以&quot;John&quot;開頭，而不區分大小寫。

```sql
person.name.matches("(?i)^John")
```

## 規則運算式群組

`regexGroup`函式用於根據提供的規則運算式提取特定資訊。

**格式**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**範例**

以下PQL查詢用於從電子郵件地址中抽取域名。

```sql
emailAddress.regexGroup("@(\w+)", 1)
```

## 後續步驟

現在您已瞭解字串函式，可在PQL查詢中使用它們。 有關其他PQL函式的詳細資訊，請閱讀[配置檔案查詢語言概述](./overview.md)。
