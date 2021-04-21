---
keywords: Experience Platform;home；熱門主題；分段；分段；分段服務；pql;PQL；配置檔案查詢語言；日期和時間函式；日期時間函式；日期時間；時間；
solution: Experience Platform
title: PQL日期和時間函式
topic-legacy: developer guide
description: 日期和時間函式用於對配置檔案查詢語言(PQL)中的值執行日期和時間操作。
exl-id: 8cbffcb6-1c25-454f-8f02-eca602318e5e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 3%

---

# 日期和時間函式

日期和時間函式用於對[!DNL Profile Query Language](PQL)內的值執行日期和時間操作。 有關其他PQL函式的詳細資訊，請參閱[[!DNL Profile Query Language] overview](./overview.md)。

## 當月

`currentMonth`函式會以整數傳回目前月份。

**格式**

```sql
currentMonth()
```

**範例**

以下PQL查詢會檢查人員的出生月份是否為當月。

```sql
person.birthMonth = currentMonth()
```

## 取得月份

`getMonth`函式會根據指定的時間戳記，以整數形式傳回月份。

**格式**

```sql
{TIMESTAMP}.getMonth()
```

**範例**

以下PQL查詢檢查人員的出生月份是否在6月。

```sql
person.birthdate.getMonth() = 6
```

## 本年度

`currentYear`函式將當前年返回整數。

**格式**

```sql
currentYear()
```

**範例**

以下PQL查詢會檢查產品是否在當年售出。

```sql
product.saleYear = currentYear()
```

## 取得年份

`getYear`函式會根據指定的時間戳記，以整數形式傳回年份。

**格式**

```sql
{TIMESTAMP}.getYear()
```

**範例**

以下PQL查詢檢查人員的出生年數是否在1991、1992、1993、1994或1995年。

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## 當月當天

`currentDayOfMonth`函式會以整數傳回當月的當天。

**格式**

```sql
currentDayOfMonth()
```

**範例**

以下PQL查詢檢查人員的出生日是否與當月的當天匹配。

```sql
person.birthDay = currentDayOfMonth()
```

## 取得每月的某天

`getDayOfMonth`函式會根據指定的時間戳記，以整數形式傳回日。

**格式**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**範例**

以下PQL查詢會檢查該項目是否在當月的前15天內售出。

```sql
product.sale.getDayOfMonth() <= 15
```

## 發生

`occurs`函式將給定時間戳函式與固定時段進行比較。

**格式**

`occurs`函式可使用下列任一格式編寫：

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| 引數 | 說明 |
| --------- | ----------- |
| `{COMPARISON}` | 比較運算子。 可以是下列任何運算子：`>`、`>=`、`<`、`<=`、`=`、`!=`。 有關比較函式的詳細資訊，請參閱[比較函式文檔](./comparison-functions.md)。 |
| `{INTEGER}` | 非負整數。 |
| `{TIME_UNIT}` | 時間單位。 可以是下列任何字詞：`millisecond(s)`、`second(s)`、`minute(s)`、`hour(s)`、`week(s)`、`month(s)`、`year(s)`、`decade(s)`、`century`、`centuries`、`millennium`、`millennia`。`day(s)` |
| `{DIRECTION}` | 描述日期比較時機的前置詞。 可以是下列任何字詞：`before`、`after`、`from`。 |
| `{TIME}` | 可以是時間戳記常值(`today`、`now`、`yesterday`、`tomorrow`)、相對時間單位（`this`、`last`或`next`之一，後面接著時間單位）或時間戳記屬性。 |

>[!NOTE]
>
>單字`on`的使用是選擇性的。 它可改善某些組合的可讀性，例如`timestamp occurs on date(2019,12,31)`。

**範例**

以下PQL查詢會檢查該項目是否上週售出。

```sql
product.saleDate occurs last week
```

下列PQL查詢會檢查2015年1月8日到2017年7月1日之間是否售出項目。

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## 現在

`now` 是表示PQL執行時間戳的保留字。

**範例**

以下PQL查詢會檢查項目是否在前三小時才售出。

```sql
product.saleDate occurs = 3 hours before now
```

## 今天

`today` 是表示PQL執行日期開始的時間戳記的保留字。

**範例**

以下PQL查詢會檢查某人的生日是否在三天前。

```sql
person.birthday occurs = 3 days before today
```

## 後續步驟

現在您已經瞭解了日期和時間函式，可以在PQL查詢中使用它們。 有關其他PQL函式的詳細資訊，請閱讀[配置檔案查詢語言概述](./overview.md)。
