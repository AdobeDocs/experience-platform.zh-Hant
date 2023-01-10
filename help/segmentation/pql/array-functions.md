---
keywords: Experience Platform；首頁；熱門主題；細分；細分；細分服務；PQL;PQL；設定檔查詢語言；陣列函式；陣列；
solution: Experience Platform
title: 陣列、清單和設定PQL函式
description: 設定檔查詢語言(PQL)提供的功能可讓您更輕鬆地與陣列、清單和字串進行互動。
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 5%

---

# 陣列、清單和設定函式

[!DNL Profile Query Language] (PQL)提供的功能可讓您更輕鬆地與陣列、清單和字串進行交互。 有關其他PQL函式的詳細資訊，請參見 [[!DNL Profile Query Language] 概述](./overview.md).

## 在

此 `in` 函式用於確定項是否為陣列或清單的成員。

**格式**

```sql
{VALUE} in {ARRAY}
```

**範例**

以下PQL查詢會使用生日來定義3月、6月或9月的人。

```sql
person.birthMonth in [3, 6, 9]
```

## 不在

此 `notIn` 函式用於確定項目是否不是陣列或清單的成員。

>[!NOTE]
>
>此 `notIn` 函式 *an* 確保兩個值均不等於null。 因此，結果並非對 `in` 函式。

**格式**

```sql
{VALUE} notIn {ARRAY}
```

**範例**

以下PQL查詢會使用不在3月、6月或9月的生日來定義人員。

```sql
person.birthMonth notIn [3, 6, 9]
```

## 相交

此 `intersects` 函式用於確定兩個陣列或清單是否具有至少一個公共成員。

**格式**

```sql
{ARRAY}.intersects({ARRAY})
```

**範例**

以下PQL查詢定義了喜愛的顏色至少包括紅色、藍色或綠色之一的人。

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## 交集

此 `intersection` 函式用於確定兩個陣列或清單的公共成員。

**格式**

```sql
{ARRAY}.intersection({ARRAY})
```

**範例**

以下PQL查詢定義人員1和人員2是否均具有紅色、藍色和綠色的收藏夾顏色。

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## 子集

此 `subsetOf` 函式用於確定特定陣列（陣列A）是否是另一陣列（陣列B）的子集。 換句話說，陣列A中的所有元素都是陣列B的元素。

**格式**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**範例**

以下PQL查詢定義了已訪問其所有最喜愛城市的人。

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## 超集

此 `supersetOf` 函式用於確定特定陣列（陣列A）是否是另一陣列（陣列B）的超集。 換句話說，陣列A包含陣列B中的所有元素。

**格式**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**範例**

以下PQL查詢定義了至少吃過壽司和披薩的人。

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## 包含

此 `includes` 函式來判斷陣列或清單是否包含指定項目。

**格式**

```sql
{ARRAY}.includes({ITEM})
```

**範例**

以下PQL查詢定義最喜愛的顏色為紅色的人。

```sql
person.favoriteColors.includes("red")
```

## 不重複

此 `distinct` 函式可用來從陣列或清單中移除重複值。

**格式**

```sql
{ARRAY}.distinct()
```

**範例**

以下PQL查詢指定在多個儲存中下過訂單的人員。

```sql
person.orders.storeId.distinct().count() > 1
```

## 分組依據

此 `groupBy` 函式用於根據表達式的值將陣列或清單的值分割到組中。

**格式**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| 引數 | 說明 |
| --------- | ----------- |
| `{ARRAY}` | 要分組的陣列或清單。 |
| `{EXPRESSION}` | 映射陣列或返回清單中每個項的表達式。 |

**範例**

以下PQL查詢將儲存訂單的所有訂單分組。

```sql
orders.groupBy(storeId)
```

## 篩選

此 `filter` 函式來根據運算式來篩選陣列或清單。

**格式**

```sql
{ARRAY}.filter({EXPRESSION})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{ARRAY}` | 要篩選的陣列或清單。 |
| `{EXPRESSION}` | 要篩選的運算式。 |

**範例**

以下PQL查詢定義所有21歲或21歲以上的人。

```sql
person.filter(age >= 21)
```

## 地圖

此 `map` 函式可用來建立新陣列，方法是將運算式套用至指定陣列中的每個項目。

**格式**

```sql
array.map(expression)
```

**範例**

以下PQL查詢將建立一個新的數字陣列，並將原始數字的值平方。

```sql
numbers.map(square)
```

## 第一個 `n` 陣列 {#first-n}

此 `topN` 函式來傳回第一個 `N` 陣列中的項目，根據指定的數值運算式以升序排序。

**格式**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{ARRAY}` | 要排序的陣列或清單。 |
| `{VALUE}` | 排序陣列或清單的屬性。 |
| `{AMOUNT}` | 要傳回的項目數。 |

**範例**

以下PQL查詢返回價格最高的前5個訂單。

```sql
orders.topN(price, 5)
```

## 上次 `n` 陣列

此 `bottomN` 函式來傳回最後一個 `N` 陣列中的項目，根據指定的數值運算式以升序排序。

**格式**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| 引數 | 說明 |
| --------- | ----------- | 
| `{ARRAY}` | 要排序的陣列或清單。 |
| `{VALUE}` | 排序陣列或清單的屬性。 |
| `{AMOUNT}` | 要傳回的項目數。 |

**範例**

以下PQL查詢返回價格最低的前5個訂單。

```sql
orders.bottomN(price, 5)
```

## 第一項

此 `head` 函式可用來傳回陣列或清單中的第一個項目。

**格式**

```sql
{ARRAY}.head()
```

**範例**

以下PQL查詢返回價格最高的前5個訂單中的第一個。 有關 `topN` 函式 [first `n` 陣列](#first-n) 區段。

```sql
orders.topN(price, 5).head()
```

## 後續步驟

現在您已了解陣列、清單和設定函式，可以在PQL查詢中使用這些函式。 有關其他PQL功能的詳細資訊，請閱讀 [設定檔查詢語言概觀](./overview.md).
