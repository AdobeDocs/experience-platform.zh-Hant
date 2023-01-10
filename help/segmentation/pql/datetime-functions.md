---
keywords: Experience Platform；首頁；熱門主題；分段；分段服務；PQL;PQL；設定檔查詢語言；日期和時間函式；日期時間函式；日期時間；日期；時間；時間；
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

日期和時間函式用於對內的值執行日期和時間操作 [!DNL Profile Query Language] (PQL)。 有關其他PQL函式的詳細資訊，請參見 [[!DNL Profile Query Language] 概述](./overview.md).

## 當月

此 `currentMonth` 函式會以整數傳回目前的月份。

**格式**

```sql
currentMonth()
```

**範例**

以下PQL查詢將檢查人員的出生月份是否為當月。

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

以下PQL查詢會檢查人員的出生月份是否為6月。

```sql
person.birthdate.getMonth() = 6
```

## 當年

此 `currentYear` 函式會以整數傳回目前的年份。

**格式**

```sql
currentYear()
```

**範例**

以下PQL查詢會檢查產品是否在當年銷售。

```sql
product.saleYear = currentYear()
```

## 獲取年

此 `getYear` 函式會根據指定的時間戳記，以整數傳回年份。

**格式**

```sql
{TIMESTAMP}.getYear()
```

**範例**

以下PQL查詢會檢查該人的出生年數是否在1991、1992、1993、1994或1995年下降。

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## 當月的當天

此 `currentDayOfMonth` 函式會以整數傳回當月的當天。

**格式**

```sql
currentDayOfMonth()
```

**範例**

以下PQL查詢會檢查人員的出生日期是否與當月的當天相符。

```sql
person.birthDay = currentDayOfMonth()
```

## 取得每月的某天

此 `getDayOfMonth` 函式會根據指定的時間戳記，以整數傳回日。

**格式**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**範例**

以下PQL查詢會檢查該物料是否在當月的前15天內銷售。

```sql
product.sale.getDayOfMonth() <= 15
```

## 發生

此 `occurs` 函式會將指定的時間戳記函式與固定的時段比較。

**格式**

此 `occurs` 函式可使用下列任何格式撰寫：

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| 引數 | 說明 |
| --------- | ----------- |
| `{COMPARISON}` | 比較運算子。 可以是下列任一運算子： `>`, `>=`, `<`, `<=`, `=`, `!=`. 如需比較函式的詳細資訊，請參閱 [比較函式文檔](./comparison-functions.md). |
| `{INTEGER}` | 非負整數。 |
| `{TIME_UNIT}` | 時間單位。 可以是下列任一字： `millisecond(s)`, `second(s)`, `minute(s)`, `hour(s)`, `day(s)`, `week(s)`, `month(s)`, `year(s)`, `decade(s)`, `century`, `centuries`, `millennium`, `millennia`. |
| `{DIRECTION}` | 說明比較日期的時間的前置詞。 可以是下列任一字： `before`, `after`, `from`. |
| `{TIME}` | 可以是時間戳記常值(`today`, `now`, `yesterday`, `tomorrow`)，相對時間單位( `this`, `last`，或 `next` 後接時間單位)或時間戳記屬性。 |

>[!NOTE]
>
>字詞用法 `on` 為選用。 可改善某些組合的可讀性，例如 `timestamp occurs on date(2019,12,31)`.

**範例**

以下PQL查詢會檢查物料是否在上週銷售。

```sql
product.saleDate occurs last week
```

以下PQL查詢會檢查2015年1月8日至2017年7月1日之間是否銷售了某個項目。

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## 現在

`now` 是代表PQL執行時間戳的保留字。

**範例**

以下PQL查詢會檢查項目是否在三小時前才售出。

```sql
product.saleDate occurs = 3 hours before now
```

## 今天

`today` 是保留字，表示PQL執行當天開始的時間戳。

**範例**

以下PQL查詢會檢查某人的生日是否在三天前。

```sql
person.birthday occurs = 3 days before today
```

## 後續步驟

現在您已了解日期和時間函式，可以在PQL查詢中使用這些函式。 有關其他PQL功能的詳細資訊，請閱讀 [設定檔查詢語言概觀](./overview.md).
