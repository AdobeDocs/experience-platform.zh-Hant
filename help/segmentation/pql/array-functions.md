---
solution: Experience Platform
title: 陣列、清單和設定PQL函式
description: Profile Query Language (PQL)提供的功能可讓您更輕鬆地與陣列、清單和字串互動。
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 4%

---

# 陣列、清單和設定函式

[!DNL Profile Query Language] (PQL)提供的功能可讓您更輕鬆地與陣列、清單和字串互動。 如需其他PQL函式的詳細資訊，請參閱[[!DNL Profile Query Language] 總覽](./overview.md)。

## 位於

`in`函式是用來判斷專案是陣列的成員，還是清單為布林值。

**格式**

```sql
{VALUE} in {ARRAY}
```

**範例**

以下PQL查詢定義三月、六月或九月有生日的人。

```sql
person.birthMonth in [3, 6, 9]
```

## 不在

`notIn`函式是用來判斷專案是否不是陣列的成員或清單做為布林值。

>[!NOTE]
>
>`notIn`函式&#x200B;*也*&#x200B;可確保這兩個值都不等於null。 因此，結果不是`in`函式的完全否定。

**格式**

```sql
{VALUE} notIn {ARRAY}
```

**範例**

下列PQL查詢會定義非三月、六月或九月的人員生日。

```sql
person.birthMonth notIn [3, 6, 9]
```

## 相交

`intersects`函式用來判斷兩個陣列或清單是否至少有一個通用成員做為布林值。

**格式**

```sql
{ARRAY}.intersects({ARRAY})
```

**範例**

以下PQL查詢定義哪些人最喜愛的顏色至少包括紅色、藍色或綠色之一。

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## 交集

`intersection`函式是用來決定兩個陣列或清單的共同成員。

**格式**

```sql
{ARRAY}.intersection({ARRAY})
```

**範例**

以下PQL查詢定義人員1和人員2是否同時具有最喜愛的紅色、藍色和綠色顏色。

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## 子集: 

`subsetOf`函式是用來判斷特定陣列（陣列A）是否是另一個陣列（陣列B）的子集。 換言之，陣列A中的所有元素都是陣列B的元素做為布林值。

**格式**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**範例**

以下PQL查詢會定義已造訪過其所有最喜愛城市的人。

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## 超集: 

`supersetOf`函式是用來判斷特定陣列（陣列A）是否是另一個陣列（陣列B）的超集。 換言之，該陣列A包含陣列B中的所有元素作為布林值。

**格式**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**範例**

以下PQL查詢會定義至少吃過一次壽司和比薩的人。

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## 包括

`includes`函式是用來判斷陣列或清單是否包含指定專案做為布林值。

**格式**

```sql
{ARRAY}.includes({ITEM})
```

**範例**

以下PQL查詢定義哪些人最喜愛的顏色包括紅色。

```sql
person.favoriteColors.includes("red")
```

## 相異

`distinct`函式用於從陣列或清單中移除重複值，以作為陣列。

**格式**

```sql
{ARRAY}.distinct()
```

**範例**

下列PQL查詢會指定在多個商店下訂單的人。

```sql
person.orders.storeId.distinct().count() > 1
```

## 分組依據

`groupBy`函式用來根據運算式的值，將陣列或清單的值分割成群組，從群組運算式的唯一值，到陣列運算式的值分割，做為對應。

**格式**

```sql
{ARRAY}.groupBy({EXPRESSION})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{ARRAY}` | 要分組的陣列或清單。 |
| `{EXPRESSION}` | 對應傳回陣列或清單中每個專案的運算式。 |

**範例**

下列PQL查詢會將下訂單所依據的所有訂單分組。

```sql
xEvent[type="order"].groupBy(storeId)
```

## 篩選器

`filter`函式是用來根據運算式篩選陣列或清單，做為陣列或清單（視輸入而定）。

**格式**

```sql
{ARRAY}.filter({EXPRESSION})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{ARRAY}` | 要篩選的陣列或清單。 |
| `{EXPRESSION}` | 篩選依據的運算式。 |

**範例**

以下PQL查詢會定義所有21歲或以上的人。

```sql
person.filter(age >= 21)
```

## 地圖

`map`函式是用來建立新陣列，方法是將運算式套用至指定陣列中的每個專案，做為陣列。

**格式**

```sql
array.map(expression)
```

**範例**

以下PQL查詢會建立新的數字陣列，並對原始數字的值進行平方。

```sql
numbers.map(square)
```

## 陣列中的前`n` {#first-n}

當根據作為陣列的給定數值運算式依遞增順序排序時，`topN`函式用於傳回陣列中的前`N`個專案。

**格式**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| 引數 | 說明 |
| --------- | ----------- |
| `{ARRAY}` | 要排序的陣列或清單。 |
| `{VALUE}` | 要排序陣列或清單的屬性。 |
| `{AMOUNT}` | 要傳回的專案數。 |

**範例**

下列PQL查詢會傳回價格最高的前五個訂單。

```sql
orders.topN(price, 5)
```

## 陣列中的最後`n`

當根據作為陣列的給定數值運算式依遞增順序排序時，`bottomN`函式用於傳回陣列中的最後`N`個專案。

**格式**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| 引數 | 說明 |
| --------- | ----------- | 
| `{ARRAY}` | 要排序的陣列或清單。 |
| `{VALUE}` | 要排序陣列或清單的屬性。 |
| `{AMOUNT}` | 要傳回的專案數。 |

**範例**

下列PQL查詢會傳回價格最低的前五個訂單。

```sql
orders.bottomN(price, 5)
```

## 第一個項目

`head`函式用來傳回陣列或清單中的第一個專案做為物件。

**格式**

```sql
{ARRAY}.head()
```

**範例**

下列PQL查詢會傳回價格最高的前五個訂單中的第一個。 有關`topN`函式的詳細資訊可在陣列](#first-n)區段的[第一個`n`中找到。

```sql
orders.topN(price, 5).head()
```

## 後續步驟

現在您已瞭解陣列、清單和設定函式，可以在PQL查詢中使用它們。 如需其他PQL功能的詳細資訊，請參閱[Profile Query Language概觀](./overview.md)。
