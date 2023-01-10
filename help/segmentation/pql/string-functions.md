---
keywords: Experience Platform；首頁；熱門主題；分段；分段服務；PQL;PQL；設定檔查詢語言；字串函式；字串；
solution: Experience Platform
title: PQL字串函式
description: 設定檔查詢語言(PQL)提供函式，讓與字串的互動更簡單。
exl-id: 9fd79d86-0802-4312-abce-f6ef5ba5bb34
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 6%

---

# 字串函式

[!DNL Profile Query Language] (PQL)提供的函式可讓與字串的互動更簡單。 有關其他PQL函式的詳細資訊，請參見 [[!DNL Profile Query Language] 概述](./overview.md).

## 贊

此 `like` 函式來判斷字串是否符合指定的模式。

**格式**

```sql
{STRING_1} like {STRING_2}
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 比對第一個字串的運算式。 建立運算式時有兩個支援的特殊字元： `%` 和 `_`. <ul><li>`%` 用於表示零個或多個字元。</li><li>`_` 僅代表一個字元。</li></ul> |

**範例**

以下PQL查詢會擷取包含「es」模式的所有城市。

```sql
city like "%es%"
```

## 開始於

此 `startsWith` 函式可用來判斷字串是否以指定的子字串開頭。

**格式**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串內搜尋的字串。 |
| `{BOOLEAN}` | 可選參數，用於確定檢查是否區分大小寫。 預設情況下，此值會設為true。 |

**範例**

以下PQL查詢將區分大小寫確定人員的名稱以「Joe」開頭。

```sql
person.name.startsWith("Joe")
```

## 開頭非為

此 `doesNotStartWith` 函式來判斷字串是否未以指定的子字串開頭。

**格式**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串內搜尋的字串。 |
| `{BOOLEAN}` | 可選參數，用於確定檢查是否區分大小寫。 預設情況下，此值會設為true。 |

**範例**

如果人員名稱的開頭不是「Joe」，則以下PQL查詢將區分大小寫地確定為。

```sql
person.name.doesNotStartWith("Joe")
```

## 終止於

此 `endsWith` 函式可用來判斷字串結尾是否為指定的子字串。

**格式**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串內搜尋的字串。 |
| `{BOOLEAN}` | 可選參數，用於確定檢查是否區分大小寫。 預設情況下，此值會設為true。 |

**範例**

以下PQL查詢會區分大小寫地確定人員的電子郵件地址結尾是「.com」。

```sql
person.emailAddress.endsWith(".com")
```

## 結尾並非為

此 `doesNotEndWith` 函式來判斷字串是否未以指定的子字串結尾。

**格式**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串內搜尋的字串。 |
| `{BOOLEAN}` | 可選參數，用於確定檢查是否區分大小寫。 預設情況下，此值會設為true。 |

**範例**

以下PQL查詢會區分大小寫地確定人員的電子郵件地址結尾不是「.com」。

```sql
person.emailAddress.doesNotEndWith(".com")
```

## 包含

此 `contains` 函式來判斷字串是否包含指定的子字串。

**格式**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串內搜尋的字串。 |
| `{BOOLEAN}` | 可選參數，用於確定檢查是否區分大小寫。 預設情況下，此值會設為true。 |

**範例**

以下PQL查詢將區分大小寫地確定人員的電子郵件地址是否包含字串「2010@gm」。

```sql
person.emailAddress.contains("2010@gm")
```

## 不包含

此 `doesNotContain` 函式來判斷字串是否不包含指定的子字串。

**格式**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串內搜尋的字串。 |
| `{BOOLEAN}` | 可選參數，用於確定檢查是否區分大小寫。 預設情況下，此值會設為true。 |

**範例**

以下PQL查詢將區分大小寫確定人員的電子郵件地址中不包含字串「2010@gm」。

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## 等於

此 `equals` 函式來判斷字串是否等於指定的字串。

**格式**

```sql
{STRING_1}.equals({STRING_2})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要與第一個字串比較的字串。 |

**範例**

以下PQL查詢將區分大小寫確定人員的名稱為「John」。

```sql
person.name.equals("John")
```

## 不等於

此 `notEqualTo` 函式來判斷字串是否不等於指定的字串。

**格式**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 要執行檢查的字串。 |
| `{STRING_2}` | 要與第一個字串比較的字串。 |

**範例**

如果人員的名稱不是「John」，則以下PQL查詢會區分大小寫地確定該人員。

```sql
person.name.notEqualTo("John")
```

## 符合

此 `matches` 函式來判斷字串是否符合特定的規則運算式。 請參閱 [此文檔](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) ，以取得規則運算式中比對模式的詳細資訊。

**格式**

```sql
{STRING_1}.matches(STRING_2})
```

**範例**

以下PQL查詢將不區分大小寫地確定人員的名稱以「John」開頭。

```sql
person.name.matches("(?i)^John")
```

>[!NOTE]
>
>如果您使用規則運算式函式，例如 `\w`，您 **必須** 逸出反斜線字元。 所以，不要寫 `\w`，您必須包含額外的反斜線和寫入 `\\w`.

## 規則運算式群組

此 `regexGroup` 函式用於根據提供的規則運算式來擷取特定資訊。

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
>如果您使用規則運算式函式，例如 `\w`，您 **必須** 逸出反斜線字元。 所以，不要寫 `\w`，您必須包含額外的反斜線和寫入 `\\w`.

## 後續步驟

現在您已了解字串函式，可以在PQL查詢中使用這些函式。 有關其他PQL功能的詳細資訊，請閱讀 [設定檔查詢語言概觀](./overview.md).
