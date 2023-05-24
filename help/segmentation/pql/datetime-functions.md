---
keywords: Experience Platform；主題；熱門主題；分段；分段；分段服務；pql;PQL；配置檔案查詢語言；日期和時間函式；日期時間函式；日期時間；時間；
solution: Experience Platform
title: PQL日期和時間函式
description: 日期和時間函式用於對配置檔案查詢語言(PQL)中的值執行日期和時間操作。
exl-id: 8cbffcb6-1c25-454f-8f02-eca602318e5e
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 3%

---

# 日期和時間函式

日期和時間函式用於對內的值執行日期和時間操作 [!DNL Profile Query Language] (PQL)。 有關其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md)。

## 當月

的 `currentMonth` 函式以整數形式返回當前月份。

**格式**

```sql
currentMonth()
```

**範例**

以下PQL查詢檢查人員的出生月份是否為當前月份。

```sql
person.birthMonth = currentMonth()
```

## 獲取月份

的 `getMonth` 函式根據給定時間戳以整數形式返回該月。

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

的 `currentYear` 函式以整數形式返回當前年份。

**格式**

```sql
currentYear()
```

**範例**

以下PQL查詢將檢查產品是否在當年銷售。

```sql
product.saleYear = currentYear()
```

## 獲取年份

的 `getYear` 函式根據給定時間戳以整數形式返回年。

**格式**

```sql
{TIMESTAMP}.getYear()
```

**範例**

以下PQL查詢將檢查人員的出生年度是否在1991、1992、1993、1994或1995年。

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## 當月的當天

的 `currentDayOfMonth` 函式以整數形式返回當月的當前日。

**格式**

```sql
currentDayOfMonth()
```

**範例**

以下PQL查詢將檢查人員的出生日是否與當月的當前日匹配。

```sql
person.birthDay = currentDayOfMonth()
```

## 獲取月中的某天

的 `getDayOfMonth` 函式根據給定時間戳以整數形式返回該日。

**格式**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**範例**

以下PQL查詢將檢查該物料是否在當月的前15天內售出。

```sql
product.sale.getDayOfMonth() <= 15
```

## 發生

的 `occurs` 函式將給定的時間戳函式與固定的時間段進行比較。

**格式**

的 `occurs` 函式可以使用以下任何格式編寫：

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| 引數 | 說明 |
| --------- | ----------- |
| `{COMPARISON}` | 比較運算子。 可以是下列任何運算子： `>`。 `>=`。 `<`。 `<=`。 `=`。 `!=`。 有關比較函式的詳細資訊，請參閱 [比較函式文檔](./comparison-functions.md)。 |
| `{INTEGER}` | 非負整數。 |
| `{TIME_UNIT}` | 時間單位。 可以是下列任一詞： `millisecond(s)`。 `second(s)`。 `minute(s)`。 `hour(s)`。 `day(s)`。 `week(s)`。 `month(s)`。 `year(s)`。 `decade(s)`。 `century`。 `centuries`。 `millennium`。 `millennia`。 |
| `{DIRECTION}` | 描述將日期比較到的時間的介詞。 可以是下列任一詞： `before`。 `after`。 `from`。 |
| `{TIME}` | 可以是時間戳文本(`today`。 `now`。 `yesterday`。 `tomorrow`)，相對時間單位(其中 `this`。 `last`或 `next` 後跟時間單位)或時間戳屬性。 |

>[!NOTE]
>
>單詞的用法 `on` 為可選項。 它可提高某些組合的可讀性，例如 `timestamp occurs on date(2019,12,31)`。

**範例**

以下PQL查詢將檢查該物料是否於上週售出。

```sql
product.saleDate occurs last week
```

以下PQL查詢檢查在2015年1月8日到2017年7月1日之間是否銷售了項目。

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## 現在

`now` 是表示PQL執行的時間戳的保留字。

**範例**

以下PQL查詢將檢查項目是否在三小時前銷售。

```sql
product.saleDate occurs = 3 hours before now
```

## 今天

`today` 是一個保留字，表示PQL執行日期開始的時間戳。

**範例**

以下PQL查詢檢查人員的生日是否在三天前。

```sql
person.birthday occurs = 3 days before today
```

## 後續步驟

現在您已經瞭解了日期和時間函式，可以在PQL查詢中使用它們。 有關其他PQL功能的詳細資訊，請閱讀 [配置檔案查詢語言概述](./overview.md)。
