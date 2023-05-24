---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；spark sql;Spark sql;spark sql函式；函式；
solution: Experience Platform
title: 查詢服務中的Spark SQL函式
description: 本文檔包含有關擴展SQL功能的Spark SQL函式的資訊。
exl-id: 59e6d82b-3317-456d-8c56-3efd5978433a
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '3866'
ht-degree: 0%

---

# [!DNL Spark] SQL函式

Adobe Experience Platform查詢服務提供多個內置的Spark SQL函式以擴展SQL功能。 此文檔列出查詢服務支援的Spark SQL函式。

有關函式（包括其語法、用法和示例）的詳細資訊，請閱讀 [Spark SQL函式文檔](https://spark.apache.org/docs/latest/api/sql/index.html)。

>[!NOTE]
>
>並非外部文檔中的所有功能都受支援。

## 數學和統計運算子及函式 {#math}

| 運算子/函式 | 說明 |
| ----------------- | ----------- |
| [`%`](https://spark.apache.org/docs/latest/api/sql/index.html#_3) | 返回兩個數字的剩餘部分 |
| [`*`](https://spark.apache.org/docs/latest/api/sql/index.html#_5) | 將兩個數字相乘 |
| [`+`](https://spark.apache.org/docs/latest/api/sql/index.html#_6) | 將這兩個數字相加 |
| [`-`](https://spark.apache.org/docs/latest/api/sql/index.html#_7) | 減去兩個數字 |
| [`/`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | 將這兩個數字除 |
| [`abs`](https://spark.apache.org/docs/latest/api/sql/index.html#abs) | 返回輸入的絕對值 |
| [`acos`](https://spark.apache.org/docs/latest/api/sql/index.html#acos) | 返回反余弦值 |
| [`approx_count_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_count_distinct) | 返回HyperLogLog++的估計基數 |
| [`approx_percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_percentile) | 返回給定百分比下的近似百分位值 |
| [`asin`](https://spark.apache.org/docs/latest/api/sql/index.html#asin) | 返回反正弦值 |
| [`atan`](https://spark.apache.org/docs/latest/api/sql/index.html#atan) | 返回反切值 |
| [`atan2`](https://spark.apache.org/docs/latest/api/sql/index.html#atan2) | 返回正x軸平面與坐標所給點之間的角度 |
| [`avg`](https://spark.apache.org/docs/latest/api/sql/index.html#avg) | 返回平均值 |
| [`cbrt`](https://spark.apache.org/docs/latest/api/sql/index.html#cbrt) | 返回多維資料集根 |
| [`ceil`](https://spark.apache.org/docs/latest/api/sql/index.html#ceil) 或 [`ceiling`](https://spark.apache.org/docs/latest/api/sql/index.html#ceiling) | 返回不大於輸入值的最小整數 |
| [`conv`](https://spark.apache.org/docs/latest/api/sql/index.html#conv) | 從一個基轉換到另一個基 |
| [`corr`](https://spark.apache.org/docs/latest/api/sql/index.html#corr) | 返回數字之間的Pearson系數 |
| [`cos`](https://spark.apache.org/docs/latest/api/sql/index.html#cos) | 返回余弦值 |
| [`cosh`](https://spark.apache.org/docs/latest/api/sql/index.html#cosh) | 返回雙曲余弦值 |
| [`cot`](https://spark.apache.org/docs/latest/api/sql/index.html#cot) | 返回餘切值 |
| [`dense_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#dense_rank) | 返回一組值中值的秩 |
| [`e`](https://spark.apache.org/docs/latest/api/sql/index.html#e) | 返回Euler數 |
| [`exp`](https://spark.apache.org/docs/latest/api/sql/index.html#exp) | 返回e到值的冪 |
| [`expm1`](https://spark.apache.org/docs/latest/api/sql/index.html#expm1) | 返回e到值減1的冪 |
| [`factorial`](https://spark.apache.org/docs/latest/api/sql/index.html#factorial) | 返回值的階乘 |
| [`floor`](https://spark.apache.org/docs/latest/api/sql/index.html#floor) | 返回不小於值的最大整數 |
| [`greatest`](https://spark.apache.org/docs/latest/api/sql/index.html#greatest) | 返回所有參數的最大值 |
| [`hypot`](https://spark.apache.org/docs/latest/api/sql/index.html#hypot) | 返回給定的兩個值的斜邊 |
| [`kurtosis`](https://spark.apache.org/docs/latest/api/sql/index.html#kurtosis) | 返回組的峭度值 |
| [`least`](https://spark.apache.org/docs/latest/api/sql/index.html#least) | 返回所有參數的最小值 |
| [`ln`](https://spark.apache.org/docs/latest/api/sql/index.html#ln) | 返回值的自然對數 |
| [`log`](https://spark.apache.org/docs/latest/api/sql/index.html#log) | 返回值的對數 |
| [`log10`](https://spark.apache.org/docs/latest/api/sql/index.html#log10) | 返回值的對數（以10為底） |
| [`log1p`](https://spark.apache.org/docs/latest/api/sql/index.html#log1p) | 返回值加1的對數 |
| [`log2`](https://spark.apache.org/docs/latest/api/sql/index.html#log2) | 返回值的以2為底的對數 |
| [`max`](https://spark.apache.org/docs/latest/api/sql/index.html#max) | 返回表達式的最大值 |
| [`mean`](https://spark.apache.org/docs/latest/api/sql/index.html#mean) | 返回根據值計算的平均值 |
| [`min`](https://spark.apache.org/docs/latest/api/sql/index.html#min) | 返回表達式的最小值 |
| [`monotonically_increasing_id`](https://spark.apache.org/docs/latest/api/sql/index.html#monotonically_increasing_id) | 返回單調增加的ID |
| [`negative`](https://spark.apache.org/docs/latest/api/sql/index.html#negative) | 返回否定值 |
| [`percent_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#percent_rank) | 返回值的百分比排序 |
| [`percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile) | 返回給定百分比的精確百分點 |
| [`percentile_approx`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile_approx) | 返回給定百分比的近似百分點 |
| [`pi`](https://spark.apache.org/docs/latest/api/sql/index.html#pi) | 返回pi |
| [`pmod`](https://spark.apache.org/docs/latest/api/sql/index.html#pmod) | 返回兩個值之間的正模 |
| [`positive`](https://spark.apache.org/docs/latest/api/sql/index.html#positive) | 返回正值 |
| [`pow`](https://spark.apache.org/docs/latest/api/sql/index.html#pow), [`power`](https://spark.apache.org/docs/latest/api/sql/index.html#power) | 返回第一個值到第二個值的冪 |
| [`radians`](https://spark.apache.org/docs/latest/api/sql/index.html#radians) | 將值轉換為弧度 |
| [`rand`](https://spark.apache.org/docs/latest/api/sql/index.html#rand) | 返回0到1之間的隨機數 |
| [`randn`](https://spark.apache.org/docs/latest/api/sql/index.html#randn) | 返回隨機值 |
| [`rint`](https://spark.apache.org/docs/latest/api/sql/index.html#rint) | 返回最接近的雙值 |
| [`round`](https://spark.apache.org/docs/latest/api/sql/index.html#round) | 返回最接近的捨入值 |
| [`sign`](https://spark.apache.org/docs/latest/api/sql/index.html#sign), [`signum`](https://spark.apache.org/docs/latest/api/sql/index.html#signum) | 返回數字元號 |
| [`sin`](https://spark.apache.org/docs/latest/api/sql/index.html#sin) | 返回值的正弦值 |
| [`sinh`](https://spark.apache.org/docs/latest/api/sql/index.html#sinh) | 返回值的雙曲正弦 |
| [`sqrt`](https://spark.apache.org/docs/latest/api/sql/index.html#sqrt) | 返回值的平方根 |
| [`stddev`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev) | 返回值的標準差 |
| [`sttdev_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#sttdev_pop) | 返回值的總體標準差 |
| [`stddev_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev_samp) | 返回值的標準偏差示例 |
| [`sum`](https://spark.apache.org/docs/latest/api/sql/index.html#sum) | 返回值之和 |
| [`tan`](https://spark.apache.org/docs/latest/api/sql/index.html#tan) | 返回值的切線 |
| [`tanh`](https://spark.apache.org/docs/latest/api/sql/index.html#tanh) | 返回值的雙曲正切 |
| [`var_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#var_pop) | 返回計算的總量差異 |
| [`var_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#var_samp), [`variance`](https://spark.apache.org/docs/latest/api/sql/index.html#variance) | 返回計算的樣本差異 |

### 邏輯運算子和函式 {#logical-operators}

| 運算子/函式 | 說明 |
| ----------------- | ----------- |
| [`!`](https://spark.apache.org/docs/latest/api/sql/index.html#_1) 或 [`not`](https://spark.apache.org/docs/latest/api/sql/index.html#not) | 邏輯不 |
| [`<`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | 少於 |
| [`<=`](https://spark.apache.org/docs/latest/api/sql/index.html#_9) | Less than or equal to |
| [`=`](https://spark.apache.org/docs/latest/api/sql/index.html#_12) | Equal to |
| [`>`](https://spark.apache.org/docs/latest/api/sql/index.html#_14) | Greater than |
| [`>=`](https://spark.apache.org/docs/latest/api/sql/index.html#_15) | 大於或等於 |
| [`^`](https://spark.apache.org/docs/latest/api/sql/index.html#_16) | 按位排除或 |
| [`\|`](https://spark.apache.org/docs/latest/api/sql/index.html#_17) | 按位或 |
| [`~`](https://spark.apache.org/docs/latest/api/sql/index.html#_19) | 按位不 |
| [`arrays_overlap`](https://spark.apache.org/docs/latest/api/sql/index.html#arrays_overlap) | 返回公用元素 |
| [`assert_true`](https://spark.apache.org/docs/latest/api/sql/index.html#assert_true) | 斷言如果表達式為true |
| [`if`](https://spark.apache.org/docs/latest/api/sql/index.html#if) | 如果表達式的計算結果為true，則返回第二個表達式。 否則，返回第三個表達式。 |
| [`ifnull`](https://spark.apache.org/docs/latest/api/sql/index.html#ifnull) | 如果表達式為null，則返回第二個表達式。 否則，它返回第一個表達式。 |
| [`in`](https://spark.apache.org/docs/latest/api/sql/index.html#in) | 如果第一個表達式位於任何後續表達式中，則返回true。 |
| [`isnan`](https://spark.apache.org/docs/latest/api/sql/index.html#isnan) | 如果值不是數字，則返回true |
| [`isnotnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnotnull) | 如果值不為null，則返回true |
| [`isnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnull) | 如果值為null，則返回true |
| [`nanvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nanvl) | 如果不是數字，則返回第一個表達式，否則返回第二個表達式 |
| [`or`](https://spark.apache.org/docs/latest/api/sql/index.html#or) | 邏輯或 |
| [`when`](https://spark.apache.org/docs/latest/api/sql/index.html#when) | 何時可用於建立分支條件以進行比較 |
| [`xpath_boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_boolean) | 如果XPath表達式的計算結果為true或找到匹配節點，則返回true |

### 日期/時間函式 {#datetime-functions}

| 函數 | 說明 |
| -------- | ----------- |
| [`add_months`](https://spark.apache.org/docs/latest/api/sql/index.html#add_months) | 添加至今的月份 |
| [`date_add`](https://spark.apache.org/docs/latest/api/sql/index.html#date_add) | 添加至今的天數 |
| [`date_format`](https://spark.apache.org/docs/latest/api/sql/index.html#date_format) | 修改日期格式 |
| [`date_sub`](https://spark.apache.org/docs/latest/api/sql/index.html#date_sub) | 從日期減去天數 |
| [`date_trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#date_trunc) | 返回截斷到指定單位的日期 |
| [`datediff`](https://spark.apache.org/docs/latest/api/sql/index.html#datediff) | 返回日期間的差值（以天為單位） |
| [`day`](https://spark.apache.org/docs/latest/api/sql/index.html#day), [`dayofmonth`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofmonth) | 返回月份的日期 |
| [`dayofweek`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofweek) | 返回星期(1-7) |
| [`dayofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofyear) | 返回年份的日期 |
| [`from_unixtime`](https://spark.apache.org/docs/latest/api/sql/index.html#from_unixtime) | 在Unix時間中返回日期 |
| [`from_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#from_utc_timestamp) | 以UTC時間表示的返回日期 |
| [`hour`](https://spark.apache.org/docs/latest/api/sql/index.html#hour) | 返回輸入小時 |
| [`last_day`](https://spark.apache.org/docs/latest/api/sql/index.html#last_day) | 返回日期所屬月份的最後一天 |
| [`minute`](https://spark.apache.org/docs/latest/api/sql/index.html#minute) | 返回輸入分鐘 |
| [`month`](https://spark.apache.org/docs/latest/api/sql/index.html#month) | 返回輸入的月份 |
| [`months_between`](https://spark.apache.org/docs/latest/api/sql/index.html#months_between) | 月數 |
| [`next_day`](https://spark.apache.org/docs/latest/api/sql/index.html#next_day) | 返回比輸入晚的第一天 |
| [`quarter`](https://spark.apache.org/docs/latest/api/sql/index.html#quarter) | 返回輸入的季度 |
| [`second`](https://spark.apache.org/docs/latest/api/sql/index.html#second) | 返回字串的第二個 |
| [`to_date`](https://spark.apache.org/docs/latest/api/sql/index.html#to_date) | 將字串轉換為日期。 **注：** 字串 **必須** 格式 `yyyy-mm-ddTHH24:MM:SS`。 |
| [`to_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_timestamp) | 將字串轉換為時間戳。 **注：** 字串 **必須** 格式 `yyyy-mm-ddTHH24:MM:SS`。 |
| [`to_unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_unix_timestamp) | 將字串轉換為Unix時間戳 |
| [`to_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_utc_timestamp) | 將字串轉換為UTC時間戳 |
| [`trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#trunc) | 截斷日期 |
| [`unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#unix_timestamp) | 返回Unix時間戳 |
| [`weekday`](https://spark.apache.org/docs/latest/api/sql/index.html#weekday) | 星期幾(0-6) |
| [`weekofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#weekofyear) | 返回給定日期的一年中的周 |
| [`year`](https://spark.apache.org/docs/latest/api/sql/index.html#year) | 返回字串的年份 |

### 陣列 {#arrays}

| 函數 | 說明 |
| -------- | ----------- |
| [`array`](https://spark.apache.org/docs/latest/api/sql/index.html#array) | 使用給定元素建立陣列 |
| [`array_contains`](https://spark.apache.org/docs/latest/api/sql/index.html#array_contains) | 檢查陣列是否包含值 |
| [`array_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#array_distinct) | 從陣列中刪除重複值 |
| [`array_except`](https://spark.apache.org/docs/latest/api/sql/index.html#array_except) | 返回第一個陣列中的元素陣列，但不返回第二個 |
| [`array_intersect`](https://spark.apache.org/docs/latest/api/sql/index.html#array_intersect) | 返回兩個陣列的交集 |
| [`array_join`](https://spark.apache.org/docs/latest/api/sql/index.html#array_join) | 將兩個陣列連接在一起 |
| [`array_max`](https://spark.apache.org/docs/latest/api/sql/index.html#array_max) | 返回陣列的最大值 |
| [`array_min`](https://spark.apache.org/docs/latest/api/sql/index.html#array_min) | 返回陣列的最小值 |
| [`array_position`](https://spark.apache.org/docs/latest/api/sql/index.html#array_position) | 返回元素的基於1的位置 |
| [`array_remove`](https://spark.apache.org/docs/latest/api/sql/index.html#array_remove) | 刪除與元素相等的所有元素 |
| [`array_repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#array_repeat) | 建立包含值計數次數的陣列 |
| [`array_sort`](https://spark.apache.org/docs/latest/api/sql/index.html#array_sort) | 對陣列排序 |
| [`array_union`](https://spark.apache.org/docs/latest/api/sql/index.html#array_union) | 將陣列連接在一起，不存在任何重複項 |
| [`arrays_zip`](https://spark.apache.org/docs/latest/api/sql/index.html#array_zip) | 將給定陣列的值與給定索引處原始集合的值組合 |
| [`cardinality`](https://spark.apache.org/docs/latest/api/sql/index.html#cardinality) | 返回陣列大小 |
| [`element_at`](https://spark.apache.org/docs/latest/api/sql/index.html#element_at) | 將元素返回位置 |
| [`explode`](https://spark.apache.org/docs/latest/api/sql/index.html#explode) | 將陣列的元素分隔成多行，不包括空 |
| [`explode_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#explode_outer) | 將陣列的元素分成多行，包括空值 |
| [`find_in_set`](https://spark.apache.org/docs/latest/api/sql/index.html#find_in_set) | 返回基於1的陣列位置 |
| [`flatten`](https://spark.apache.org/docs/latest/api/sql/index.html#flatten) | 拼合陣列 |
| [`inline`](https://spark.apache.org/docs/latest/api/sql/index.html#inline) | 將結構陣列分離到表中，不包括空 |
| [`inline_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#inline_outer) | 將結構陣列分離到表中，包括空值 |
| [`posexplode`](https://spark.apache.org/docs/latest/api/sql/index.html#posexplode) | 將陣列的元素分隔成多個具有位置的行，不包括空 |
| [`reverse`](https://spark.apache.org/docs/latest/api/sql/index.html#reverse) | 反向陣列元素 |
| [`shuffle`](https://spark.apache.org/docs/latest/api/sql/index.html#shuffle) | 返回陣列的隨機置換 |
| [`slice`](https://spark.apache.org/docs/latest/api/sql/index.html#slice) | 對陣列進行子集 |
| [`sort_array`](https://spark.apache.org/docs/latest/api/sql/index.html#sort_array) | 按順序對陣列排序 |
| [`zip_with`](https://spark.apache.org/docs/latest/api/sql/index.html#zip_with) | 在應用函式之前，將兩個陣列合併為單個陣列 |

### 資料類型轉換函式 {#datatype-casting}

| 函數 | 說明 |
| -------- | ----------- |
| [`bigint`](https://spark.apache.org/docs/latest/api/sql/index.html#bigint) | 將資料類型更改為bigint |
| [`binary`](https://spark.apache.org/docs/latest/api/sql/index.html#binary) | 將資料類型更改為二進位 |
| [`boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#boolean) | 將資料類型更改為布爾型 |
| [`type`](https://spark.apache.org/docs/latest/api/sql/index.html#type) | 將資料類型更改為指定類型 |
| [`date`](https://spark.apache.org/docs/latest/api/sql/index.html#date) | 將資料類型更改為日期 |
| [`decimal`](https://spark.apache.org/docs/latest/api/sql/index.html#decimal) | 將資料類型更改為十進位 |
| [`double`](https://spark.apache.org/docs/latest/api/sql/index.html#double) | 將資料類型更改為雙倍 |
| [`float`](https://spark.apache.org/docs/latest/api/sql/index.html#float) | 將資料類型更改為浮動 |
| [`int`](https://spark.apache.org/docs/latest/api/sql/index.html#int) | 將資料類型更改為int |
| [`smallint`](https://spark.apache.org/docs/latest/api/sql/index.html#smallint) | 將資料類型更改為smallint |
| [`str_to_map`](https://spark.apache.org/docs/latest/api/sql/index.html#str_to_map) | 從字串建立映射 |
| [`string`](https://spark.apache.org/docs/latest/api/sql/index.html#string) | 將資料類型更改為字串 |
| [`struct`](https://spark.apache.org/docs/latest/api/sql/index.html#struct) | 建立結構 |
| [`tinyint`](https://spark.apache.org/docs/latest/api/sql/index.html#tinyint) | 將資料類型更改為tinyint |

### 轉換和格式化函式 {#conversion}

| 函數 | 說明 |
| -------- | ----------- |
| [`ascii`](https://spark.apache.org/docs/latest/api/sql/index.html#ascii) | 返回數字(ASCII)值 |
| [`base64`](https://spark.apache.org/docs/latest/api/sql/index.html#base64) | 將參數更改為base64字串 |
| [`bin`](https://spark.apache.org/docs/latest/api/sql/index.html#bin) | 將參數更改為二進位值 |
| [`bit_length`](https://spark.apache.org/docs/latest/api/sql/index.html#bit_length) | 返回位長度 |
| [`char`](https://spark.apache.org/docs/latest/api/sql/index.html#char), [`chr`](https://spark.apache.org/docs/latest/api/sql/index.html#chr) | 返回ASCII字元 |
| [`char_length`](https://spark.apache.org/docs/latest/api/sql/index.html#char_length), [`character_length`](https://spark.apache.org/docs/latest/api/sql/index.html#character_length) | 返回字串長度 |
| [`crc32`](https://spark.apache.org/docs/latest/api/sql/index.html#crc32) | 返回循環冗餘校驗值 |
| [`degrees`](https://spark.apache.org/docs/latest/api/sql/index.html#degrees) | 將弧度轉換為度 |
| [`format_number`](https://spark.apache.org/docs/latest/api/sql/index.html#format_number) | 更改數字的格式 |
| [`from_json`](https://spark.apache.org/docs/latest/api/sql/index.html#from_json), [`get_json_object`](https://spark.apache.org/docs/latest/api/sql/index.html#get_json_object) | 從JSON獲取資料 |
| [`hash`](https://spark.apache.org/docs/latest/api/sql/index.html#hash) | 返回哈希值 |
| [`hex`](https://spark.apache.org/docs/latest/api/sql/index.html#hex) | 將參數轉換為十六進位值 |
| [`initcap`](https://spark.apache.org/docs/latest/api/sql/index.html#initcap) | 將字串更改為標題 |
| [`lcase`](https://spark.apache.org/docs/latest/api/sql/index.html#lcase), [`lower`](https://spark.apache.org/docs/latest/api/sql/index.html#lower) | 將字串更改為全小寫 |
| [`lpad`](https://spark.apache.org/docs/latest/api/sql/index.html#lpad) | 將字串的左側插入 |
| [`map`](https://spark.apache.org/docs/latest/api/sql/index.html#map) | 建立映射 |
| [`map_from_arrays`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_arrays) | 從陣列建立映射 |
| [`map_from_entries`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_entries) | 從結構陣列建立映射 |
| [`md5`](https://spark.apache.org/docs/latest/api/sql/index.html#md5) | 返回md5值 |
| [`rpad`](https://spark.apache.org/docs/latest/api/sql/index.html#rpad) | 將字串的右側插入 |
| [`rtrim`](https://spark.apache.org/docs/latest/api/sql/index.html#rtrim) | 刪除尾隨空格 |
| [`sha`](https://spark.apache.org/docs/latest/api/sql/index.html#sha), [`sha1`](https://spark.apache.org/docs/latest/api/sql/index.html#sha1) | 返回SHA1值 |
| [`sha2`](https://spark.apache.org/docs/latest/api/sql/index.html#sha2) | 返回SHA2值 |
| [`soundex`](https://spark.apache.org/docs/latest/api/sql/index.html#soundex) | 返回聲明代碼 |
| [`stack`](https://spark.apache.org/docs/latest/api/sql/index.html#stack) | 將值分隔為行 |
| [`substr`](https://spark.apache.org/docs/latest/api/sql/index.html#substr), [`substring`](https://spark.apache.org/docs/latest/api/sql/index.html#substring) | 返回子字串 |
| [`to_json`](https://spark.apache.org/docs/latest/api/sql/index.html#to_json) | 返回JSON字串 |
| [`translate`](https://spark.apache.org/docs/latest/api/sql/index.html#translate) | 替換字串中的值 |
| [`trim`](https://spark.apache.org/docs/latest/api/sql/index.html#trim) | 刪除前導字元和尾隨字元 |
| [`ucase`](https://spark.apache.org/docs/latest/api/sql/index.html#ucase), [`upper`](https://spark.apache.org/docs/latest/api/sql/index.html#upper) | 將字串更改為全大寫 |
| [`unbase64`](https://spark.apache.org/docs/latest/api/sql/index.html#unbase64) | 將base64字串轉換為二進位 |
| [`unhex`](https://spark.apache.org/docs/latest/api/sql/index.html#unhex) | 將十六進位轉換為二進位 |
| [`uuid`](https://spark.apache.org/docs/latest/api/sql/index.html#uuid) | 返回UUID |

### 資料評估 {#data-evaluation}

| 函數 | 說明 |
| -------- | ----------- |
| [`coalesce`](https://spark.apache.org/docs/latest/api/sql/index.html#coalesce) | 返回第一個非空參數 |
| [`collect_list`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_list) | 返回非唯一元素清單 |
| [`collect_set`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_set) | 返回一組唯一元素 |
| [`concat`](https://spark.apache.org/docs/latest/api/sql/index.html#concat) | 串聯 |
| [`concat_ws`](https://spark.apache.org/docs/latest/api/sql/index.html#concat_ws) | 帶分隔符的串聯 |
| [`count`](https://spark.apache.org/docs/latest/api/sql/index.html#count) | 返回行的總計數 |
| [`decode`](https://spark.apache.org/docs/latest/api/sql/index.html#decode) | 使用字元集進行解碼 |
| [`elt`](https://spark.apache.org/docs/latest/api/sql/index.html#elt) | 返回 [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n)輸入 |
| [`encode`](https://spark.apache.org/docs/latest/api/sql/index.html#encode) | 使用字元集進行編碼 |
| [`first`](https://spark.apache.org/docs/latest/api/sql/index.html#first), [`first_value`](https://spark.apache.org/docs/latest/api/sql/index.html#first_value) | 返回第一個值 |
| [`grouping`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping) | 指示列是否分組 |
| [`grouping_id`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping_id) | 返回分組級別 |
| [`instr`](https://spark.apache.org/docs/latest/api/sql/index.html#instr) | 返回基於1的字元出現率索引 |
| [`json_tuple`](https://spark.apache.org/docs/latest/api/sql/index.html#json_tuple) | 從JSON輸入返回元組 |
| [`lag`](https://spark.apache.org/docs/latest/api/sql/index.html#lag), [`lead`](https://spark.apache.org/docs/latest/api/sql/index.html#lead) | 返回偏移前的值 |
| [`last`](https://spark.apache.org/docs/latest/api/sql/index.html#last), [`last_value`](https://spark.apache.org/docs/latest/api/sql/index.html#last_value) | 返回最後一個值 |
| [`left`](https://spark.apache.org/docs/latest/api/sql/index.html#left) | 返回第一個 [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) 字元 |
| [`length`](https://spark.apache.org/docs/latest/api/sql/index.html#length) | 返回字串的長度 |
| [`levenshtein`](https://spark.apache.org/docs/latest/api/sql/index.html#levenshtein) | 返回字串之間的Levenstein距離 |
| [`locate`](https://spark.apache.org/docs/latest/api/sql/index.html#locate), [`position`](https://spark.apache.org/docs/latest/api/sql/index.html#position) | 返回子字串首次出現的位置 |
| [`map_concat`](https://spark.apache.org/docs/latest/api/sql/index.html#map_concat) | 連接映射 |
| [`map_keys`](https://spark.apache.org/docs/latest/api/sql/index.html#map_keys) | 返回地圖的鍵 |
| [`map_values`](https://spark.apache.org/docs/latest/api/sql/index.html#map_values) | 返回映射的值 |
| [`ntile`](https://spark.apache.org/docs/latest/api/sql/index.html#ntile) | 將行分為分區 |
| [`nullif`](https://spark.apache.org/docs/latest/api/sql/index.html#nullif) | 如果為true，則返回null |
| [`nvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl) | 返回值（如果為Null） |
| [`nvl2`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl2) | 如果不為null，則返回值 |
| [`parse_url`](https://spark.apache.org/docs/latest/api/sql/index.html#parse_url) | 提取URL的一部分 |
| [`rank`](https://spark.apache.org/docs/latest/api/sql/index.html#rank) | 計算值的秩 |
| [`regexp_extract`](https://spark.apache.org/docs/latest/api/sql/index.html#regexp_extract) | 提取與規則運算式匹配的內容 |
| [`regex_replace`](https://spark.apache.org/docs/latest/api/sql/index.html#regex_replace) | 替換與規則運算式匹配的內容 |
| [`repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#repeat) | 返回重複的字串 |
| [`replace`](https://spark.apache.org/docs/latest/api/sql/index.html#replace) | 替換字串的所有實例 |
| [`rollup`](https://spark.apache.org/docs/latest/api/sql/index.html#rollup) | 建立多維匯總 |
| [`row_number`](https://spark.apache.org/docs/latest/api/sql/index.html#row_number) | 分配唯一行號 |
| [`schema_of_json`](https://spark.apache.org/docs/latest/api/sql/index.html#schema_of_json) | 返回JSON的架構 |
| [`sentences`](https://spark.apache.org/docs/latest/api/sql/index.html#sentences) | 將字串拆分為一組單詞 |
| [`sequence`](https://spark.apache.org/docs/latest/api/sql/index.html#sequence) | 生成元素陣列 |
| [`shiftleft`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftleft) | 已簽名按位左移 |
| [`shiftright`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftright) | 簽名按位移右 |
| [`shiftrightunsigned`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftrightunsigned) | 無符號按位右移 |
| [`size`](https://spark.apache.org/docs/latest/api/sql/index.html#size) | 返回陣列大小 |
| [`space`](https://spark.apache.org/docs/latest/api/sql/index.html#space) | 返回字串 [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) 空間 |
| [`split`](https://spark.apache.org/docs/latest/api/sql/index.html#split) | 拆分字串 |
| [`substring_index`](https://spark.apache.org/docs/latest/api/sql/index.html#substring_index) | 返回子字串索引 |
| [`window`](https://spark.apache.org/docs/latest/api/sql/index.html#window) | 窗口 |
| [`xpath`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath) | 分析XML節點 |
| [`xpath_double`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_double), [`xpath_number`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_number) | 解析雙XML節點 |
| [`xpath_float`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_float) | 解析浮點的XML節點 |
| [`xpath_int`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_int) | 分析整數的XML節點 |
| [`xpath_long`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_long) | 解析XML節點長 |
| [`xpath_short`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_short) | 解析短整數的XML節點 |
| [`xpath_string`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_string) | 解析字串的XML節點 |

### 當前資訊 {#current-information}

| 函數 | 說明 |
| -------- | ----------- |
| [`current_database`](https://spark.apache.org/docs/latest/api/sql/index.html#current_database) | 返回當前資料庫 |
| [`current_date`](https://spark.apache.org/docs/latest/api/sql/index.html#current_date) | 返回當前日期 |
| [`current_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#current_timestamp), [`now`](https://spark.apache.org/docs/latest/api/sql/index.html#now) | 返回當前時間戳 |

### 高階函式 {#higher-order}

| 函數 | 說明 |
| -------- | ----------- |
| [`transform`](https://spark.apache.org/docs/latest/api/sql/index.html#transform) | 轉換陣列中的元素 |
| [`exists`](https://spark.apache.org/docs/latest/api/sql/index.html#exists) | 檢查元素是否存在 |
| [`filter`](https://spark.apache.org/docs/latest/api/sql/index.html#filter) | 篩選輸入陣列 |
| [`aggregate`](https://spark.apache.org/docs/latest/api/sql/index.html#aggregate) | 將二進位運算子應用於所有元素 |
