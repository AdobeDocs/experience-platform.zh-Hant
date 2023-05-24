---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；PQL;PQL；配置式查詢語言；陣列函式；陣列；
solution: Experience Platform
title: 陣列、清單和設定PQL函式
description: 配置檔案查詢語言(PQL)提供了一些功能，使與陣列、清單和字串的交互更容易。
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 5%

---

# 陣列、清單和集函式

[!DNL Profile Query Language] (PQL)提供使與陣列、清單和字串交互更簡單的函式。 有關其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md)。

## 在

的 `in` 函式用於確定項目是否是陣列或清單的成員。

**格式**

```sql
{VALUE} in {ARRAY}
```

**範例**

以下PQL查詢定義3月、6月或9月的生日。

```sql
person.birthMonth in [3, 6, 9]
```

## 不在

的 `notIn` 函式用於確定項目是否不是陣列或清單的成員。

>[!NOTE]
>
>的 `notIn` 函式 *也* 確保兩個值均不等於null。 因此，結果不是對 `in` 的子菜單。

**格式**

```sql
{VALUE} notIn {ARRAY}
```

**範例**

以下PQL查詢定義生日不在三月、六月或九月的人。

```sql
person.birthMonth notIn [3, 6, 9]
```

## 交叉

的 `intersects` 函式用於確定兩個陣列或清單是否具有至少一個公共成員。

**格式**

```sql
{ARRAY}.intersects({ARRAY})
```

**範例**

以下PQL查詢定義其最喜愛的顏色至少包括紅色、藍色或綠色之一的人。

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## 交集

的 `intersection` 函式用於確定兩個陣列或清單的公用成員。

**格式**

```sql
{ARRAY}.intersection({ARRAY})
```

**範例**

以下PQL查詢定義人員1和人員2是否都具有紅色、藍色和綠色的最喜愛顏色。

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## 子集

的 `subsetOf` 函式用於確定特定陣列（陣列A）是否是另一陣列（陣列B）的子集。 換句話說，陣列A中的所有元素都是陣列B的元素。

**格式**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**範例**

以下PQL查詢定義訪問了所有其喜愛城市的人員。

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## 超集

的 `supersetOf` 函式用於確定特定陣列（陣列A）是否是另一陣列（陣列B）的超集。 換句話說，陣列A包含陣列B中的所有元素。

**格式**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**範例**

以下PQL查詢定義了至少吃過壽司和比薩餅的人。

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## 包括

的 `includes` 函式用於確定陣列或清單是否包含給定項。

**格式**

```sql
{ARRAY}.includes({ITEM})
```

**範例**

以下PQL查詢定義其最喜愛的顏色包括紅色的人。

```sql
person.favoriteColors.includes("red")
```

## 獨特

的 `distinct` 函式用於從陣列或清單中刪除重複值。

**格式**

```sql
{ARRAY}.distinct()
```

**範例**

以下PQL查詢指定在多個儲存中下訂單的人員。

```sql
person.orders.storeId.distinct().count() > 1
```

## 分組依據

的 `groupBy` 函式用於根據表達式的值將陣列或清單的值分區為組。

**格式**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| 引數 | 說明 |
| --------- | ----------- |
| `{ARRAY}` | 要分組的陣列或清單。 |
| `{EXPRESSION}` | 返回的表達式，用於映射陣列或清單中的每個項。 |

**範例**

以下PQL查詢將儲存訂單的所有訂單分組。

```sql
orders.groupBy(storeId)
```

## 篩選

的 `filter` 函式用於根據表達式篩選陣列或清單。

**格式**

```sql
{ARRAY}.filter({EXPRESSION})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{ARRAY}` | 要篩選的陣列或清單。 |
| `{EXPRESSION}` | 要篩選的表達式。 |

**範例**

以下PQL查詢定義所有21歲或21歲以上的人。

```sql
person.filter(age >= 21)
```

## 地圖

的 `map` 函式用於通過將表達式應用於給定陣列中的每個項來建立新陣列。

**格式**

```sql
array.map(expression)
```

**範例**

以下PQL查詢將建立一個新的數字陣列，並將原始數字的值平方。

```sql
numbers.map(square)
```

## 第一個 `n` 在陣列中 {#first-n}

的 `topN` 函式用於返回第一個 `N` 陣列中的項，根據給定的數值表達式按升序排序。

**格式**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{ARRAY}` | 要排序的陣列或清單。 |
| `{VALUE}` | 對陣列或清單進行排序的屬性。 |
| `{AMOUNT}` | 要返回的項數。 |

**範例**

以下PQL查詢返回價格最高的前五個訂單。

```sql
orders.topN(price, 5)
```

## 最後 `n` 在陣列中

的 `bottomN` 函式用於返回最後一個 `N` 陣列中的項，根據給定的數值表達式按升序排序。

**格式**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| 引數 | 說明 |
| --------- | ----------- | 
| `{ARRAY}` | 要排序的陣列或清單。 |
| `{VALUE}` | 對陣列或清單進行排序的屬性。 |
| `{AMOUNT}` | 要返回的項數。 |

**範例**

以下PQL查詢返回價格最低的前五個訂單。

```sql
orders.bottomN(price, 5)
```

## 第一項

的 `head` 函式用於返回陣列或清單中的第一項。

**格式**

```sql
{ARRAY}.head()
```

**範例**

以下PQL查詢返回價格最高的前五個訂單中的第一個。 有關 `topN` 函式 [第一 `n` 在陣列中](#first-n) 的子菜單。

```sql
orders.topN(price, 5).head()
```

## 後續步驟

現在您已經瞭解了陣列、清單和設定函式，可以在PQL查詢中使用它們。 有關其他PQL功能的詳細資訊，請閱讀 [配置檔案查詢語言概述](./overview.md)。
