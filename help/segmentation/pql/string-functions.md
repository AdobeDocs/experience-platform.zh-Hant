---
solution: Experience Platform
title: PQL字串函式
description: Profile Query Language (PQL)提供的函式可讓您更輕鬆與字串互動。
exl-id: 9fd79d86-0802-4312-abce-f6ef5ba5bb34
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 5%

---

# 字串函式

[!DNL Profile Query Language] (PQL)提供可簡化與字串互動的函式。 如需其他PQL函式的詳細資訊，請參閱[[!DNL Profile Query Language] 總覽](./overview.md)。

## 讚

`like`函式是用來判斷字串是否符合指定的布林值模式。

**格式**

```sql
{STRING_1} like {STRING_2}
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 執行檢查的字串。 |
| `{STRING_2}` | 比對第一個字串的運算式。 建立運算式有兩個支援的特殊字元： `%`和`_`。 <ul><li>`%`用於表示零個或多個字元。</li><li>`_`只代表一個字元。</li></ul> |

**範例**

下列PQL查詢會擷取包含「es」模式的所有城市。

```sql
city like "%es%"
```

## 開頭為

`startsWith`函式是用來判斷字串的開頭是否為指定的子字串做為布林值。

**格式**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串中搜尋的字串。 |
| `{BOOLEAN}` | 選擇性引數，用來判斷檢查是否區分大小寫。 依預設，此設定為true。 |

**範例**

下列PQL查詢會區分大小寫，判斷人員名稱是否以「Joe」開頭。

```sql
person.name.startsWith("Joe")
```

## 開頭不是

`doesNotStartWith`函式是用來判斷字串的開頭是否不是以指定的子字串做為布林值。

**格式**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串中搜尋的字串。 |
| `{BOOLEAN}` | 選擇性引數，用來判斷檢查是否區分大小寫。 依預設，此設定為true。 |

**範例**

下列PQL查詢會區分大小寫，判斷人員名稱是否以「Joe」開頭。

```sql
person.name.doesNotStartWith("Joe")
```

## 結尾為

`endsWith`函式是用來判斷字串的結尾是否為指定的子字串做為布林值。

**格式**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串中搜尋的字串。 |
| `{BOOLEAN}` | 選擇性引數，用來判斷檢查是否區分大小寫。 依預設，此設定為true。 |

**範例**

下列PQL查詢會區分大小寫，判斷此人的電子郵件地址是否以「.com」結尾。

```sql
person.emailAddress.endsWith(".com")
```

## 結尾不是

`doesNotEndWith`函式是用來判斷字串的結尾是否不是指定的子字串做為布林值。

**格式**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串中搜尋的字串。 |
| `{BOOLEAN}` | 選擇性引數，用來判斷檢查是否區分大小寫。 依預設，此設定為true。 |

**範例**

下列PQL查詢會區分大小寫，判斷個人的電子郵件地址是否以「.com」結尾。

```sql
person.emailAddress.doesNotEndWith(".com")
```

## 包含

`contains`函式是用來判斷字串是否包含指定的子字串做為布林值。

**格式**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串中搜尋的字串。 |
| `{BOOLEAN}` | 選擇性引數，用來判斷檢查是否區分大小寫。 依預設，此設定為true。 |

**範例**

下列PQL查詢會區分大小寫，判斷個人的電子郵件地址是否包含「2010@gm」字串。

```sql
person.emailAddress.contains("2010@gm")
```

## 不包含

`doesNotContain`函式是用來判斷字串是否不包含指定的子字串做為布林值。

**格式**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串中搜尋的字串。 |
| `{BOOLEAN}` | 選擇性引數，用來判斷檢查是否區分大小寫。 依預設，此設定為true。 |

**範例**

下列PQL查詢會區分大小寫，判斷個人的電子郵件地址是否不包含字串「2010@gm」。

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## 等於

`equals`函式是用來判斷字串是否等於指定的布林字串。

**格式**

```sql
{STRING_1}.equals({STRING_2})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 執行檢查的字串。 |
| `{STRING_2}` | 要與第一個字串進行比較的字串。 |

**範例**

下列PQL查詢會區分大小寫判斷此人的姓名是否為「John」。

```sql
person.name.equals("John")
```

## 不等於

`notEqualTo`函式是用來判斷字串是否不等於指定的布林值字串。

**格式**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{STRING_1}` | 執行檢查的字串。 |
| `{STRING_2}` | 要與第一個字串進行比較的字串。 |

**範例**

下列PQL查詢會區分大小寫判斷此人的姓名是否為「John」。

```sql
person.name.notEqualTo("John")
```

## 符合

`matches`函式是用來判斷字串是否符合特定的規則運算式。 請參考[此檔案](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html)以取得規則運算式做為布林值比對模式的詳細資訊。

**格式**

```sql
{STRING_1}.matches(STRING_2})
```

**範例**

下列PQL查詢會在不區分大小寫的情況下，判斷使用者的名稱是否以「John」開頭。

```sql
person.name.matches("(?i)^John")
```

>[!NOTE]
>
>如果您使用規則運算式函式（例如`\w`），則&#x200B;**必須**&#x200B;逸出反斜線字元。 因此，您必須加入額外的反斜線並寫入`\\w`，而不要只寫入`\w`。

## 規則運算式群組

`regexGroup`函式是用來根據作為字串提供的規則運算式擷取特定資訊。

**格式**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**範例**

以下PQL查詢用於從電子郵件地址中擷取網域名稱。

```sql
emailAddress.regexGroup("@(\\w+)", 1)
```

>[!NOTE]
>
>如果您使用規則運算式函式（例如`\w`），則&#x200B;**必須**&#x200B;逸出反斜線字元。 因此，您必須加入額外的反斜線並寫入`\\w`，而不要只寫入`\w`。

## 後續步驟

現在您已瞭解字串函式，可以在PQL查詢中使用它們。 如需其他PQL功能的詳細資訊，請參閱[Profile Query Language概觀](./overview.md)。
