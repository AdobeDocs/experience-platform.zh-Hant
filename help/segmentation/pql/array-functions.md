---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 陣列、清單和設定函式
topic: developer guide
translation-type: tm+mt
source-git-commit: 0fc356b67af4d34e35cd9329385ec284d9336953
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 5%

---


# 陣列、清單和設定函式

[!DNL Profile Query Language] (PQL)提供的功能可讓與陣列、清單和字串的交互更輕鬆。 有關其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md)。

## 在

此函 `in` 數用於確定項目是否是陣列或清單的成員。

**Format**

```sql
{VALUE} in {ARRAY}
```

**範例**

以下PQL查詢定義了3月、6月或9月的生日。

```sql
person.birthMonth in [3, 6, 9]
```

## 不在

此函 `notIn` 數用於確定項目是否不是陣列或清單的成員。

>[!NOTE]
>
>此函 `notIn` 數 *也可確保* ，兩個值均不等於null。 因此，結果不是函式的完全否 `in` 定。

**Format**

```sql
{VALUE} notIn {ARRAY}
```

**範例**

以下PQL查詢定義人們的生日不是在3月、6月或9月。

```sql
person.birthMonth notIn [3, 6, 9]
```

## Intercests

該函 `intersects` 數用於確定兩個陣列或清單是否具有至少一個公共成員。

**Format**

```sql
{ARRAY}.intersects({ARRAY})
```

**範例**

以下PQL查詢定義了喜愛的顏色至少包含紅色、藍色或綠色之一的人。

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## 交集

函式 `intersection` 用於確定兩個陣列或清單的公共成員。

**Format**

```sql
{ARRAY}.intersection({ARRAY})
```

**範例**

以下PQL查詢定義人員1和人員2是否都具有紅色、藍色和綠色的收藏夾顏色。

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## 子集

該函 `subsetOf` 數用於確定特定陣列（陣列A）是否是另一陣列（陣列B）的子集。 換言之，陣列A中的所有元素都是陣列B的元素。

**Format**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**範例**

以下PQL查詢定義已訪問其所有最愛城市的訪客。

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## 超集

該函 `supersetOf` 數用於確定特定陣列（陣列A）是否是另一陣列（陣列B）的超集。 換言之，陣列A包含陣列B中的所有元素。

**Format**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**範例**

以下PQL查詢定義至少吃過壽司和披薩的人。

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## 包含

函 `includes` 數用於確定陣列或清單是否包含給定項。

**Format**

```sql
{ARRAY}.includes({ITEM})
```

**範例**

以下PQL查詢定義其收藏夾顏色包含紅色的人。

```sql
person.favoriteColors.includes("red")
```

## Distinct

此函 `distinct` 數用於從陣列或清單中刪除重複值。

**Format**

```sql
{ARRAY}.distinct()
```

**範例**

以下PQL查詢指定在多個儲存中下了訂單的人員。

```sql
person.orders.storeId.distinct().count() > 1
```

## 分組依據

該 `groupBy` 函式用於根據表達式的值將陣列或清單的值分成組。

**Format**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| 引數 | 說明 |
| --------- | ----------- |
| `{ARRAY}` | 要分組的陣列或清單。 |
| `{EXPRESSION}` | 映射陣列或清單中返回的每個項的表達式。 |

**範例**

以下PQL查詢將儲存訂單的所有訂單分組到。

```sql
orders.groupBy(storeId)
```

## 篩選器

該函 `filter` 數用於根據表達式過濾陣列或清單。

**Format**

```sql
{ARRAY}.filter({EXPRESSION})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{ARRAY}` | 要篩選的陣列或清單。 |
| `{EXPRESSION}` | 篩選依據的運算式。 |

**範例**

以下PQL查詢定義所有21歲或以上的人。

```sql
person.filter(age >= 21)
```

## 地圖

此函 `map` 數可用來透過將運算式套用至指定陣列中的每個項目來建立新陣列。

**Format**

```sql
array.map(expression)
```

**範例**

以下PQL查詢將建立一個新的數字陣列，並將原始數字的值平方。

```sql
numbers.map(square)
```

## 陣列 `n` 中的第一個 {#first-n}

當根 `topN` 據給定的數值表達式按升 `N` 序排序時，該函式用於返回陣列中的第一個項。

**Format**

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

## 陣列中 `n` 的最後一個

當根 `bottomN` 據給定的數值表達式按升 `N` 序排序時，該函式用於返回陣列中的最後一個項。

**Format**

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

函 `head` 數用於返回陣列或清單中的第一個項。

**Format**

```sql
{ARRAY}.head()
```

**範例**

以下PQL查詢返回價格最高的前5個訂單中的第一個。 有關函式的 `topN` 詳細資訊，請參 [閱 `n` array一節](#first-n) 。

```sql
orders.topN(price, 5).head()
```

## 後續步驟

現在您已經瞭解了陣列、清單和設定函式，可以在PQL查詢中使用這些函式。 有關其他PQL函式的詳細資訊，請閱讀配置式查 [詢語言概述](./overview.md)。
