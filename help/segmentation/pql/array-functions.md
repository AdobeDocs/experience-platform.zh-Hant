---
keywords: Experience Platform;home；熱門主題；分段；分段；分段服務；pql;PQL；配置檔案查詢語言；陣列函式；array;
solution: Experience Platform
title: 陣列、清單和設定PQL函式
topic-legacy: developer guide
description: 配置式查詢語言(PQL)提供一些功能，使與陣列、清單和字串的交互更加容易。
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 5%

---

# 陣列、清單和設定函式

[!DNL Profile Query Language] (PQL)提供的功能可讓與陣列、清單和字串的交互更輕鬆。有關其他PQL函式的詳細資訊，請參閱[[!DNL Profile Query Language] overview](./overview.md)。

## 在

`in`函式用於確定項目是否是陣列或清單的成員。

**格式**

```sql
{VALUE} in {ARRAY}
```

**範例**

以下PQL查詢定義了3月、6月或9月的生日。

```sql
person.birthMonth in [3, 6, 9]
```

## 不在

`notIn`函式用於確定項目是否不是陣列或清單的成員。

>[!NOTE]
>
>`notIn`函式&#x200B;*allo*&#x200B;可確保兩個值均不等於null。 因此，結果不是對`in`函式的完全否定。

**格式**

```sql
{VALUE} notIn {ARRAY}
```

**範例**

以下PQL查詢定義人們的生日不是在3月、6月或9月。

```sql
person.birthMonth notIn [3, 6, 9]
```

## Intercests

`intersects`函式用於確定兩個陣列或清單是否具有至少一個公共成員。

**格式**

```sql
{ARRAY}.intersects({ARRAY})
```

**範例**

以下PQL查詢定義了喜愛的顏色至少包含紅色、藍色或綠色之一的人。

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## 交集

`intersection`函式用於確定兩個陣列或清單的公共成員。

**格式**

```sql
{ARRAY}.intersection({ARRAY})
```

**範例**

以下PQL查詢定義人員1和人員2是否都具有紅色、藍色和綠色的收藏夾顏色。

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## 子集

`subsetOf`函式用於確定特定陣列（陣列A）是否是另一陣列（陣列B）的子集。 換言之，陣列A中的所有元素都是陣列B的元素。

**格式**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**範例**

以下PQL查詢定義已訪問其所有最愛城市的訪客。

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## 超集

`supersetOf`函式用於確定特定陣列（陣列A）是否是另一陣列（陣列B）的超集。 換言之，陣列A包含陣列B中的所有元素。

**格式**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**範例**

以下PQL查詢定義至少吃過壽司和披薩的人。

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## 包含

`includes`函式用於確定陣列或清單是否包含給定項。

**格式**

```sql
{ARRAY}.includes({ITEM})
```

**範例**

以下PQL查詢定義其收藏夾顏色包含紅色的人。

```sql
person.favoriteColors.includes("red")
```

## Distinct

`distinct`函式用於從陣列或清單中刪除重複值。

**格式**

```sql
{ARRAY}.distinct()
```

**範例**

以下PQL查詢指定在多個儲存中下了訂單的人員。

```sql
person.orders.storeId.distinct().count() > 1
```

## 分組依據

`groupBy`函式用於根據表達式的值將陣列或清單的值分成組。

**格式**

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

## 篩選

`filter`函式用於根據表達式過濾陣列或清單。

**格式**

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

`map`函式用於通過對給定陣列中的每個項應用表達式來建立新陣列。

**格式**

```sql
array.map(expression)
```

**範例**

以下PQL查詢將建立一個新的數字陣列，並將原始數字的值平方。

```sql
numbers.map(square)
```

## 陣列{#first-n}中第一個`n`

`topN`函式用於根據給定的數值表達式按升序排序時，返回陣列中的第一個`N`項。

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

## 陣列中最後一個`n`

`bottomN`函式用於根據給定的數值表達式按升序排序時，返回陣列中最後一個`N`項。

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

`head`函式用於返回陣列或清單中的第一個項目。

**格式**

```sql
{ARRAY}.head()
```

**範例**

以下PQL查詢返回價格最高的前5個訂單中的第一個。 有關`topN`函式的更多資訊，請參閱array](#first-n)部分的[first `n`。

```sql
orders.topN(price, 5).head()
```

## 後續步驟

現在您已經瞭解了陣列、清單和設定函式，可以在PQL查詢中使用這些函式。 有關其他PQL函式的詳細資訊，請閱讀[配置檔案查詢語言概述](./overview.md)。
