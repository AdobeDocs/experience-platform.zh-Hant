---
title: 使用高階函式管理陣列和對應資料型別
description: 瞭解如何在Query Service中使用高階函式來管理陣列和對應資料型別。 提供常見使用案例的實用範例。
exl-id: dec4e4f6-ad6b-4482-ae8c-f10cc939a634
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 0%

---

# 使用高階函式管理陣列和對應資料型別

使用本指南瞭解高階函式如何處理複雜的資料型別，例如陣列和地圖。 這些函式會移除爆炸陣列、執行函式，然後合併結果的需要。 高階函式在分析或處理時間序列資料集和分析時特別有用，這些資料集和分析通常具有複雜的巢狀結構、陣列、地圖和各種使用案例。

下列使用案例清單包含高階陣列和地圖操作函式的範例。

## 使用轉換將總價調整為n {#adjust-price-total}

`transform(array<T>, function<T, U>): array<U>`

上述程式碼片段會將函式套用至陣列的每個元素，並傳迴轉換元素的新陣列。 具體來說，`transform`函式接受型別T的陣列，並將每個元素從型別T轉換為型別U。然後它會傳回U型別的陣列。實際型別T和U取決於轉換函式的特定用途。

`transform(array<T>, function<T, Int, U>): array<U>`

此陣列轉換函式與上一個範例類似，但函式有兩個引數。 此函式中的第二個引數除了會進行轉換之外，也會接收陣列中元素的索引。

**範例**

以下SQL範例示範此使用案例。 查詢會從指定的資料表中擷取有限的資料列集合，將每個專案的`priceTotal`屬性乘以73來轉換`productListItems`陣列。 結果包含`_id`、`productListItems`和轉換後的`price_in_inr`欄。 選取範圍是根據特定時間戳記範圍。

```sql
SELECT _id,
       productListItems,
       Transform(productListItems, value -> value.priceTotal * 73) AS
       price_in_inr
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  timestamp > To_timestamp('2017-11-01 00:00:00')
       AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**結果**

此SQL的結果看起來會類似於下面所示的結果。

```console
 productListItems | price_in_inr
-------------------+----------------
(8376, NULL, NULL) | 611448.0
{(Burbank Hills Jeans, NULL, NULL), (Thermomax Steel, NULL, NULL), (Bruin Point Shearling Boots, NULL, NULL), (Uintas Pro Ski Gloves, NULL, NULL), (Timberline Survival Knife, NULL, NULL), (Thermomax Steel, NULL, NULL), (Timpanogos Scarf, NULL, NULL), (Lost Prospector Beanie, NULL, NULL), (Timpanogos Scarf, NULL, NULL), (Uintas Pro Ski Gloves, NULL, NULL)} | {0.0,0.0.0.0,0,0,0,0,0,0,0,0,0,0,0,0,0.0}
(84763,NULL, NULL) | 6187699.0
(843765, NULL, NULL) | 6.1594845E7
(199684, NULL, NULL) | 1.4576932E7

(10 rows)
```

## 使用來探索具有特定SKU的產品是否存在 {#confirm-product-exists}

`exists(array<T>, function<T, boolean>): boolean`

在上述程式碼片段中，`exists`函式會套用至陣列的每個元素，並傳回布林值。 布林值會指出陣列中是否有一或多個元素符合指定的條件。 在此情況下，系統會確認是否存在具有特定SKU的產品。

**範例**

在以下SQL範例中，查詢會從`geometrixxx_999_xdm_pqs_1batch_10k_rows`資料表擷取`productListItems`，並評估`productListItems`陣列中SKU等於`123679`的元素是否存在。 然後它會根據特定時間戳記範圍篩選結果，並將最終結果限製為10列。

```sql
SELECT productListItems
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE EXISTS( productListItems, value -> value.sku == 123679)
AND timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')limit 10;
```

**結果**

此SQL的結果看起來會類似於下面所示的結果。

```console
productListItems
-----------------
{(123679, NULL,NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL,NULL)}
{(123679,NULL, NULL)}

(10 rows)
```

## 使用篩選器來尋找SKU > 100000的產品 {#find-specific-products}

`filter(array<T>, function<T, boolean>): array<T>`

此函式根據將每個元素評估為布林值的指定條件來篩選元素陣列。 然後它會傳回僅包含條件傳回true值的元素的新陣列。

**範例**

下列查詢會選取`productListItems`欄、套用篩選條件以僅包含SKU大於100000的元素，並將結果集限製為特定時間戳記範圍內的列。 然後，篩選的陣列會在輸出中別名為`_filter`。

```sql
SELECT productListItems,
    Filter(productListItems, value -> value.sku > 100000) AS _filter
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10; 
```

**結果**

此SQL的結果看起來會類似於下面所示的結果。

```console
productListItems | _filter
-----------------+---------
(123679, NULL, NULL) (123679, NULL, NULL)
(1346, NULL, NULL) |
(98347, NULL, NULL) |
(176015, NULL, NULL) | (176015, NULL, NULL)

(10 rows)
```

## 使用彙總來加總與特定ID相關聯之所有產品清單專案的SKU，並將結果總計加倍 {#sum-specific-skus-and-double-the-resulting-total}

`aggregate(array<T>, A, function<A, T, A>[, function<A, R>]): R`

此彙總運算會將二進位運運算元套用至初始狀態以及陣列中的所有元素。 它也會將多個值減少為單一狀態。 進行此縮減之後，會使用完成函式將最終狀態轉換為最終結果。 finish函式會取用在所有陣列元素套用二進位運運算元後所取得的最後一個狀態，並對它執行一些動作以產生最終結果。

**範例**

此查詢範例會計算指定時間戳記範圍內`productListItems`陣列的最大SKU值，並將結果加倍。 輸出包含原始`productListItems`陣列和計算的`max_value`。

```sql
SELECT productListItems,
aggregate(productListItems, 0, (acc, value) ->
case
WHEN (
value.sku > acc) THEN cast(value.sku AS int)
ELSE cast(acc AS int)
END, acc -> acc * 2) AS max_value
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
LIMIT 50;
```

**結果**

此SQL的結果看起來會類似於下面所示的結果。

```console
productListItems | max_value
-----------------+---------
(123679, NULL, NULL) | 247358
(1346,NULL, NULL) | 2692
(98347, NULL, NULL) | 196694
(176015, NULL, NULL) | 352030

(10 rows)
```

## 使用zip_with為產品清單中的所有專案指派序號 {#assign-a-sequence-number}

`zip_with(array<T>, array<U>, function<T, U, R>): array<R>`

此程式碼片段將兩個陣列的元素結合為單一新陣列。 該操作在陣列的每個元素上獨立執行，並產生值對。 如果一個陣列較短，則會新增null值以符合較長陣列的長度。 這會在套用函式之前發生。

**範例**

下列查詢使用`zip_with`函式從兩個陣列建立值組。 其做法是將來自`productListItems`陣列的SKU值新增至整數序列（使用`Sequence`函式產生）。 結果會與原始`productListItems`欄一起選取，而且會根據時間戳記範圍加以限制。

```sql
SELECT productListItems,
zip_with(Sequence(1,5), Transform(productListItems, p -> p.sku), (x,y) -> struct(x, y)) AS zip_with
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
limit 10;
```

**結果**

此SQL的結果看起來會類似於下面所示的結果。

```console
productListItems     | zip_with
---------------------+---------
                     | {(1,NULL), (2,NULL), (3,NULL),(4,NULL), (5,NULL)}
(123679, NULL, NULL) | {(1,123679), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL),(3,NULL),(4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3, NULL),(4,NULL), (5,NULL)}
(1346,NULL, NULL)    | {(1,1346), (2,NULL),(3,NULL),(4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL),(4,NULL), (5,NULL)}
(98347, NULL, NULL)  | {(1,98347), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
(176015, NULL, NULL) | {(1,176015),(2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}

(10 rows)
```

## 使用map_from_entries為產品清單中的每個料號指定序號，並取得最終結果作為對映 {#assign-a-sequence-number-return-result-as-map}

`map_from_entries(array<struct<K, V>>): map<K, V>`

此程式碼片段將索引鍵/值組的陣列轉換為對應。 在處理機碼值組資料時，此方法相當實用，因為此資料可受益於更具組織性和更有效率的結構。

**範例**

下列查詢會從序列和productListItems陣列建立值對，使用map_from_entries將這些值對轉換成對應，然後選取原始的productListItems欄以及新建立的map_from_entries欄。 系統會根據指定的時間戳記範圍，篩選及限制結果。

```sql
SELECT productListItems,      map_from_entries(zip_with(Sequence(1,Size(productListItems)), productListItems, (x,y) -> struct(x, y))) AS map_from_entries
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  timestamp > to_timestamp('2017-11-01 00:00:00')
AND    timestamp < to_timestamp('2017-11-02 00:00:00')
LIMIT 10;
```

**結果**

此SQL的結果看起來會類似於下面所示的結果。

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## 使用map_form_arrays將序號指定給產品清單中的專案，並傳回對應結果 {#assign-sequence-numbers-to-items-return-the-result-as-a-map}

`map_form_arrays(array<K>, array<V>): map<K, V>`

`map_form_arrays`函式使用兩個陣列中的配對值來建立對應。

>[!IMPORTANT]
>
>索引鍵中應該沒有空元素。

**範例**

下列SQL會建立對應，其中的索引鍵是使用`Sequence`函式產生的循序數字，而值是來自`productListItems`陣列的元素。 查詢會選取`productListItems`資料行，並使用`Map_from_arrays`函式，根據產生的數字順序和陣列元素建立對應。 結果限製為10列，並根據時間戳記範圍進行篩選。

```sql
SELECT productListItems,
       Map_from_arrays(Sequence(1, Size(productListItems)), productListItems) AS
       map_from_arrays
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  Size(productListItems) > 0
       AND timestamp > To_timestamp('2017-11-01 00:00:00')
       AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**結果**

此SQL的結果看起來會類似於下面所示的結果。

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## 使用map_concat將兩個地圖串連成單一地圖 {#concatenate-two-maps-into-as-single-map}

`map_concat(map<K, V>, ...): map<K, V>`

上述程式碼片段中的`map_concat`函式以多個對應作為引數，並傳回結合來自輸入對應的所有機碼值組的新對應。 函式會將多個對應串連到單一對應中，而產生的對應會包含輸入對應中的所有機碼值組。

**範例**

以下SQL會建立對應，其中`productListItems`中的每個專案都與序號相關聯，然後與另一個對應串連，其中索引鍵是在特定序列範圍中產生。

```sql
SELECT productListItems,
      map_concat(           
         map_from_entries(zip_with(Sequence(1,Size(productListItems)), productListItems, (x,y) -> struct(x, y))),
         map_from_arrays(sequence(size(productListItems) + 1, size(productListItems) + size(productListItems)), productListItems) )
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE size(productListItems) > 0
AND timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
limit 10;
```

**結果**

此SQL的結果看起來會類似於下面所示的結果。

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)",2 -> "(123679, NULL, NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)",2 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)",2 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)",2 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)",2 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)",2 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)",2 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)",2 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)",2 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)",2 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## 使用element_at在身分對應中擷取與「AAID」對應的值以進行進一步計算 {#retrieve-a-corresponding-value}

`element_at(array<T>, Int): T / element_at(map<K, V>, K): V`

針對陣列，此程式碼片段會傳回指定（1型）索引處的元素，或與對應中索引鍵相關的值。 如果索引小於0，則會存取從最後一個到第一個的元素，如果索引超過陣列的長度，則會傳回null。

對於對應，它會傳回給定索引鍵的值，如果索引鍵未包含在對應中，則傳回null。

**範例**

查詢從資料表`geometrixxx_999_xdm_pqs_1batch_10k_rows`選取`identitymap`資料行，並擷取與每個資料列的索引鍵`AAID`相關的值。 結果限製為指定時間戳記範圍內的列，而查詢將輸出限製為10列。

```sql
SELECT identitymap,
              Element_at(identitymap, 'AAID')
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10; 
```

**結果**

此SQL的結果看起來會類似於下面所示的結果。

```console
                                                                  identitymap                                            |  element_at(identitymap, AAID) 
-------------------------------------------------------------------------------------------------------------------------+-------------------------------------
[AAID -> "(3617FBB942466D79-5433F727AD6A0AD, false)",ECID -> "(67383754798169392543508586197135045866,true)"]            | (3617FBB942466D79-5433F727AD6A0AD, false) 
[AAID -> "[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"] | (533F56A682C059B1-396437F68879F61D, false) 
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            | (22E195F8A8ECCC6A-A39615C93B72A9F, false) 
[AAID -> "(6A60527B9D66CCB9-29638A632B45E9, false)",ECID -> "(50117234882064422833184021414056250576,true)"]             | (6A60527B9D66CCB9-29638A632B45E9, false) 
[AAID -> "(64FB4DC317E21B59-2A23602D234647E7, false)",ECID -> "(79785479785408621882908938960039330887,true)"]           | (64FB4DC317E21B59-2A23602D234647E7, false) 
[AAID -> "(2E70E8CF6DB1DE86-270E55BBBA58B9C1, false)",ECID -> "(80073674009951685326146914344189474476,true)"]           | (2E70E8CF6DB1DE86-270E55BBBA58B9C1, false) 
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            | (22E195F8A8ECCC6A-A39615C93B72A9F, false) 
[AAID -> "(1CFB3297C3146F2F-28D6902A610BA3B1, false)",ECID -> "(88251082790399360979074868101758236669,true)"]           | (1CFB3297C3146F2F-28D6902A610BA3B1, false) 
[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"]           | (533F56A682C059B1-396437F68879F61D, false) 
(10 rows)
```

## 使用基數來尋找身分對應中的身分數量 {#find-the-number-of-identities-in-the-identity-map}

`cardinality(array<T>): Int / cardinality(map<K, V>): Int`

此程式碼片段會傳回指定陣列或對應的大小，並提供別名。 若該值為空值，則會傳回–1。

**範例**

下列查詢會擷取`identitymap`欄，`Cardinality`函式會計算`identitymap`內每個對應中的元素數目。 結果限製為10列，並根據指定的時間戳記範圍進行篩選。

```sql
SELECT identitymap,
       Cardinality(identitymap)
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**結果**

此SQL的結果看起來會類似於下面所示的結果。

```console
                                                                  identitymap                                            |  size(identitymap) 
-------------------------------------------------------------------------------------------------------------------------+-------------------------------------
[AAID -> "(3617FBB942466D79-5433F727AD6A0AD, false)",ECID -> "(67383754798169392543508586197135045866,true)"]            |      2  
[AAID -> "[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"] |      2  
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            |      2  
[AAID -> "(6A60527B9D66CCB9-29638A632B45E9, false)",ECID -> "(50117234882064422833184021414056250576,true)"]             |      2  
[AAID -> "(64FB4DC317E21B59-2A23602D234647E7, false)",ECID -> "(79785479785408621882908938960039330887,true)"]           |      2  
[AAID -> "(2E70E8CF6DB1DE86-270E55BBBA58B9C1, false)",ECID -> "(80073674009951685326146914344189474476,true)"]           |      2  
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            |      2  
[AAID -> "(1CFB3297C3146F2F-28D6902A610BA3B1, false)",ECID -> "(88251082790399360979074868101758236669,true)"]           |      2  
[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"]           |      2  
(10 rows)
```

## 使用array_distinct尋找productListItems中的不重複元素 {#find-distinct-elements}

`array_distinct(array<T>): array<T>`

上述程式碼片段會從指定陣列中移除重複值。

**範例**

下列查詢會選取`productListItems`欄、從陣列中移除任何重複的專案，以及根據指定的時間戳記範圍將輸出限製為10列。

```sql
SELECT productListItems,
              Array_distinct(productListItems)
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10;
```

**結果**

此SQL的結果看起來會類似於下面所示的結果。

```console
productListItems     | array_distinct(productListItems)
---------------------+---------------------------------
                     |
(123679, NULL, NULL) | (123679, NULL, NULL)
                     |
                     |
(1346,NULL, NULL)    | (1346,NULL, NULL)
                     |
(98347, NULL, NULL)  | (98347, NULL, NULL)
                     |
(176015, NULL, NULL) | (176015, NULL, NULL)
                     |

(10 rows)
```

### 其他高階函式 {#additional-higher-order-functions}

以下高階函式的範例將說明為擷取類似記錄使用案例的一部分。 有關每個函式用途的範例和說明會提供在該檔案的個別區段中。

[`transform`函式範例](../use-cases/retrieve-similar-records.md#length-adjustment)涵蓋產品清單的代碼化。

[`filter`函式範例](../use-cases/retrieve-similar-records.md#filter-results)示範從文字資料更精細、更精確的相關資訊擷取。

[`reduce`函式](../use-cases/retrieve-similar-records.md#higher-order-function-solutions)提供衍生累積值或聚總的方法，這可以在各種分析和計畫處理中起到關鍵作用。
