---
solution: Experience Platform
title: PQL日期和時間函式
description: 日期和時間函式用於對設定檔查詢語言(PQL)中的值執行日期和時間作業。
exl-id: 8cbffcb6-1c25-454f-8f02-eca602318e5e
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 4%

---

# 日期和時間函式

日期和時間函式用於對內的值執行日期和時間作業 [!DNL Profile Query Language] (PQL)。 如需其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md).

## 當月

此 `currentMonth` 函式以整數傳回目前月份。

**格式**

```sql
currentMonth()
```

**範例**

以下PQL查詢會檢查個人的出生月是否為當月。

```sql
person.birthMonth = currentMonth()
```

## 取得月份

此 `getMonth` 函式會根據指定的時間戳記，以整數傳回月份。

**格式**

```sql
{TIMESTAMP}.getMonth()
```

**範例**

以下PQL查詢會檢查個人的出生月份是否為六月。

```sql
person.birthdate.getMonth() = 6
```

## 目前年份

此 `currentYear` 函式以整數傳回目前年份。

**格式**

```sql
currentYear()
```

**範例**

下列PQL查詢會檢查產品是否在本年度內銷售。

```sql
product.saleYear = currentYear()
```

## 取得年份

此 `getYear` 函式會根據指定的時間戳記，以整數傳回年份。

**格式**

```sql
{TIMESTAMP}.getYear()
```

**範例**

下列PQL查詢會檢查個人的出生年份是1991、1992、1993、1994還是1995。

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## 當月日期

此 `currentDayOfMonth` 函式以整數傳回當月的目前日期。

**格式**

```sql
currentDayOfMonth()
```

**範例**

以下PQL查詢會檢查個人的出生日期是否與當月當天相符。

```sql
person.birthDay = currentDayOfMonth()
```

## 取得當月日期

此 `getDayOfMonth` 函式根據指定的時間戳記，以整數傳回日。

**格式**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**範例**

下列PQL查詢會檢查該專案是否在該月的前15天內售出。

```sql
product.sale.getDayOfMonth() <= 15
```

## 發生

此 `occurs` 函式比較指定的時間戳記函式與固定的時段。

**格式**

此 `occurs` 函式可使用下列任何格式來撰寫：

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| 引數 | 說明 |
| --------- | ----------- |
| `{COMPARISON}` | 比較運運算元。 可以是下列任一運運算元： `>`， `>=`， `<`， `<=`， `=`， `!=`. 有關比較函式的詳細資訊，請參閱 [比較函式檔案](./comparison-functions.md). |
| `{INTEGER}` | 非負整數。 |
| `{TIME_UNIT}` | 時間單位。 可以是下列任一字詞： `millisecond(s)`， `second(s)`， `minute(s)`， `hour(s)`， `day(s)`， `week(s)`， `month(s)`， `year(s)`， `decade(s)`， `century`， `centuries`， `millennium`， `millennia`. |
| `{DIRECTION}` | 說明何時將日期與進行比較的預置詞。 可以是下列任一字詞： `before`， `after`， `from`. |
| `{TIME}` | 可以是時間戳記常值(`today`， `now`， `yesterday`， `tomorrow`)，相對時間單位（以下其中之一） `this`， `last`，或 `next` 後跟時間單位)或時間戳記屬性。 |

>[!NOTE]
>
>單詞的用法 `on` 是選用專案。 它有助於改善某些組合的可讀性，例如 `timestamp occurs on date(2019,12,31)`.

**範例**

下列PQL查詢會檢查專案上週是否售出。

```sql
product.saleDate occurs last week
```

下列PQL查詢會檢查某個專案是否在2015年1月8日與2017年7月1日之間售出。

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## 現在

`now` 是代表PQL執行時間戳記的保留字。

**範例**

下列PQL查詢會檢查專案是否在三小時前剛好售出。

```sql
product.saleDate occurs = 3 hours before now
```

## 今天

`today` 是一個保留字，代表PQL執行當天開始的時間戳記。

**範例**

以下PQL查詢會檢查個人的生日是否為三天前。

```sql
person.birthday occurs = 3 days before today
```

## 後續步驟

現在您已瞭解日期和時間函式，可以在PQL查詢中使用它們。 如需其他PQL函式的詳細資訊，請參閱 [設定檔查詢語言概觀](./overview.md).
