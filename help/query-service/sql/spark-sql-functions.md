---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Spark SQL函式
topic: spark sql functions
translation-type: tm+mt
source-git-commit: a98e31f57c6ff4fc49d8d8f64441a6e1e18d89da
workflow-type: tm+mt
source-wordcount: '4900'
ht-degree: 5%

---


# [!DNL Spark] SQL函式

SQL [!DNL Spark] 幫助器提供內置的 [!DNL Spark] SQL函式以擴展SQL功能。

參考： [Spark SQL函式檔案](https://spark.apache.org/docs/2.4.0/api/sql/index.html)

>[!NOTE]
>
>並非外部文檔中的所有功能都受支援。

## 類別

- [數學和統計運算子與函式](#math-and-statistical-operators-and-functions)
- [邏輯運算子](#logical-operators)
- [日期／時間函式](#date/time-functions)
- [集合函式](#aggregate-functions)
- [陣列](#arrays)
- [資料類型轉換函式](#datatype-casting-functions)
- [轉換和格式化功能](#conversion-and-formatting-functions)
- [資料評估](#data-evaluation)
- [目前資訊](#current-information)

### 數學和統計運算子與函式

#### 模數

`expr1 % expr2`: 在／後返回剩餘 `expr1`值`expr2`。

範例：

```
> SELECT 2 % 1.8;
 0.2
> SELECT MOD(2, 1.8);
 0.2
```

#### 乘

`expr1 * expr2`: 傳回 `expr1`*`expr2`.

範例：

```
> SELECT 2 * 3;
 6
```

#### 新增

`expr1 + expr2`: 傳回 `expr1`+`expr2`.

範例：

```
> SELECT 1 + 2;
 3
```

#### 去除

`expr1 - expr2`: 傳回 `expr1`-`expr2`.

範例：

```
> SELECT 2 - 1;
 1
```

#### 除法

`expr1 / expr2`: 傳回 `expr1`/`expr2`. 它總是執行浮點除法。

範例：

```
> SELECT 3 / 2;
 1.5
> SELECT 2L / 2L;
 1.0
```

#### abs

`abs(expr)`: 傳回數值的絕對值。

範例：

```
> SELECT abs(-1);
  1
```

#### acos

`acos(expr)`: 傳回的反余弦（又稱為反余弦） `expr`，如同由計算 `java.lang.Math.acos`。

範例：

```
> SELECT acos(1);
 0.0
> SELECT acos(2);
 NaN
```

#### approx_percentile

`approx_percentile(col, percentage [, accuracy])`: 傳回數值欄的指定百分比 `col` 的近似百分位值。 百分比的值必須介於0.0和1.0之間。 參 `accuracy` 數(預設值： 10000)是正數值常值，以記憶體的成本控制近似精度。 結果表明，高 `accuracy` 精度是近 `1.0/accuracy` 似的相對誤差。 當 `percentage` 是陣列時，百分比陣列的每個值必須介於0.0和1.0之間。 在此情況下，會傳回指定百分比數 `col` 組的列的近似百分位陣列。

範例：

```
> SELECT approx_percentile(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT approx_percentile(10.0, 0.5, 100);
 10.0
```

#### asin

`asin(expr)`: 傳回反正弦（也稱為反正弦），即反正弦， `expr`如同由計算 `java.lang.Math.asin`。

範例：

```
> SELECT asin(0);
 0.0
> SELECT asin(2);
 NaN
```

#### atan

`atan(expr)`: 傳回的反相切（又稱為反相切） `expr`，如同 `java.lang.Math.atan`

範例：

```
> SELECT atan(0);
 0.0
```

#### atan2

`atan2(exprY, exprX)`: 傳回平面的正x軸與坐標(`exprX`, `exprY`)所給點之間的弧度角，如同由計算 `java.lang.Math.atan2`。

引數：

`exprY`: Y軸坐標`exprX`: X軸上的坐標

範例：

```
> SELECT atan2(0, 0);
 0.0
```

#### avg

`avg(expr)`: 傳回根據群組值計算的平均值。

#### 基數

`cardinality(expr)`: 返回陣列或映射的大小。 如果函式的輸入為null且設定為true(缺 `spark.sql.legacy.sizeOfNull` 省)，則返回-1。 如果 `spark.sql.legacy.sizeOfNull` 設定為false，則函式會為空輸入返回null。

範例：

```
> SELECT cardinality(array('b', 'd', 'c', 'a'));
 4
> SELECT cardinality(map('a', 1, 'b', 2));
 2
> SELECT cardinality(NULL);
 -1
```

#### cbrt

`cbrt(expr)`: 返回的立方根 `expr`。

範例：

```
> Select cbrt(27.0);
 3.0
```

#### ceil

`ceil(expr)`: 傳回不小於的最小整數 `expr`。

範例：

```
> SELECT ceil(-0.1);
 0
> SELECT ceil(5);
 5
```

#### 天花板

`ceiling(expr)`: 傳回不小於的最小整數 `expr`。

範例：

```
> SELECT ceiling(-0.1);
 0
> SELECT ceiling(5);
 5
```

#### conv

`conv(num, from_base, to_base)`: 從 `num` 轉換 `from_base` 為 `to_base`

範例：

```
> SELECT conv('100', 2, 10);
 4
> SELECT conv(-10, 16, -10);
 -16
```

#### cor

`corr(expr1, expr2)`: 傳回一組數字對之間的相關的Pearson系數。

#### cos

`cos(expr)`: 傳回的余弦 `expr`，如同由計算 `java.lang.Math.cos`。

範例：

```
> SELECT cos(0);
 1.0
```

#### cosh

`cosh(expr)`: 傳回的雙曲余弦 `expr`，如同計算者 `java.lang.Math.cosh`。

引數：
- `expr`: 雙曲角

範例：

```
> SELECT cosh(0);
 1.0
```

#### cot

`cot(expr)`: 傳回的餘切 `expr`，如同由計算 `1/java.lang.Math.cot`。

引數：
- `expr`: 角度（以弧度為單位）

範例：

```
> SELECT cot(1);
 0.6420926159343306
```

#### dense_rank

`dense_rank()`: 計算值組中值的排名。 結果是加上先前指派的排名值。 與函式不 `rank`同， `dense_rank` 在排名順序中不會產生間隙。

#### e

`e()`: 傳回Euler的數字，e。

範例：

```
> SELECT e();
 2.718281828459045
```

#### exp

`exp(expr)`: 返回e的權 `expr`。

範例：

```
> SELECT exp(0);
 1.0
```

#### expml

`expm1(expr)`: 返回exp(`expr`)- 1。

範例：

```
> SELECT expm1(0);
 0.0
```

#### 因子

`factorial(expr)`: 返回的工廠 `expr`。 `expr` 是 [0..20]。 否則，為null。

範例：

```
> SELECT factorial(5);
 120
```

#### 地板

`floor(expr)`: 傳回不大於的最大整數 `expr`。

範例：

```
> SELECT floor(-0.1);
 -1
> SELECT floor(5);
 5
```

#### 最偉大的

`greatest(expr, ...)`: 傳回所有參數的最大值，並略過null值。

範例：

```
> SELECT greatest(10, 9, 2, 4, 3);
 10
```

#### 缺口

`hypot(expr1, expr2)`: 傳回sqrt(`expr1`<sup>2</sup> + `expr2`<sup>2</sup>)。

範例：

```
> SELECT hypot(3, 4);
 5.0
```

#### 峭度

`kurtosis(expr)`: 傳回根據群組值計算的峰度值。


#### 至少

`least(expr, ...)`: 傳回所有參數的最小值，並跳過空值。

範例：

```
> SELECT least(10, 9, 2, 4, 3);
 2
```

#### 萊文施泰因

`levenshtein(str1, str2)`: 傳回兩個指定字串之間的Levenstein距離。

範例：

```
> SELECT levenshtein('kitten', 'sitting');
 3
```

#### ln

`ln(expr)`: 傳回的自然對數（以e為底） `expr`。

範例：

```
> SELECT ln(1);
 0.0
```

#### 日誌

`log(base, expr)`: 傳回的對 `expr` 數 `base`。

範例：

```
> SELECT log(10, 100);
 2.0
```

#### log10

`log10(expr)`: 傳回以10為底 `expr` 數的對數。

範例：

```
> SELECT log10(10);
 1.0
```

#### log1p

`log1p(expr)`: 傳回 `log(1 + expr)`.

範例：

```
> SELECT log1p(0);
 0.0
```

#### log2

`log2(expr)`: 傳回以2為底 `expr` 數的對數。

範例：

```
> SELECT log2(2);
 1.0
```

#### max

`max(expr)`: 返回最大值 `expr`。

#### mean

`mean(expr)`: 傳回根據群組值計算的平均值。

#### min

`min(expr)`: 傳回最小值 `expr`。

#### monotonically_ingrading_id

`monotonically_increasing_id()`: 傳回單調遞增的64位元整數。 所生成的ID被保證單調地增加且唯一，但不連續。 當前實現將分區ID放在上部31位中，而下部33位代表每個分區中的記錄數。 假設資料幀的分區數少於10億個，而每個分區的記錄數少於80億個。 函式是非確定性的，因為其結果取決於分區ID。

#### 負

`negative(expr)`: 傳回否定值 `expr`。

範例：

```
> SELECT negative(1);
 -1
```

#### 百分比排名

`percent_rank()`: 計算值組中值的百分比排名。

#### 百分位數

`percentile(col, percentage [, frequency])`: 傳回指定百分比的數值欄 `col` 的精確百分位值。 值必 `percentage` 須介於0.0和1.0之間。 值應 `frequency` 為正積分。

`percentile(col, array(percentage1 [, percentage2]...) [, frequency])`: 傳回指定百分比的數值欄的精 `col` 確百分位數值陣列。 百分比陣列的每個值必須介於0.0和1.0之間。 值應 `frequency` 為正積分。

#### percentile_approx

`percentile_approx(col, percentage [, accuracy])`: 傳回數值欄的指定百分比 `col` 的近似百分位值。 值必 `percentage` 須介於0.0和1.0之間。 參 `accuracy` 數(預設值： 10000)是正數值常值，以記憶體的成本控制近似精度。 結果表明，高 `accuracy` 精度是近 `1.0/accuracy` 似的相對誤差。 當 `percentage` 是陣列時，百分比陣列的每個值必須介於0.0和1.0之間。 在此情況下，返回給定百分比陣列的列 `col` 的近似百分位陣列。

範例：

```
> SELECT percentile_approx(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT percentile_approx(10.0, 0.5, 100);
 10.0
```

#### pi

`pi()`: 傳回pi。

範例：

```
> SELECT pi();
 3.141592653589793
```

#### pmod

`pmod(expr1, expr2)`: 傳回mod的正 `expr1` 值 `expr2`。

範例：

```
> SELECT pmod(10, 3);
 1
> SELECT pmod(-10, 3);
 2
```

#### 正

`positive(expr)`: 傳回的正值 `expr`

#### pow

`pow(expr1, expr2)`: 提 `expr1` 升力量 `expr2`。

範例：

```
> SELECT pow(2, 3);
 8.0
```

#### 功率

`power(expr1, expr2)`: 提 `expr1` 升力量 `expr2`。

範例：

```
> SELECT power(2, 3);
 8.0
```

#### 弧度

`radians(expr)`: 將度轉換為弧度。

引數：

- `expr`: 角度（度）

範例：

```
> SELECT radians(180);
 3.141592653589793
```

#### 蘭德

`rand([seed])`: 傳回隨機值，其中具有獨立且相同分佈(i.i.d.)的一致分佈值(在(0,1)中)。

範例：

```
> SELECT rand();
 0.9629742951434543
> SELECT rand(0);
 0.8446490682263027
> SELECT rand(null);
 0.8446490682263027
```

>[!NOTE]
>
>在一般情況下，此函式是非確定性的。

#### randn

`randn([seed])`: 傳回從標準常態分佈抽取的具有獨立且相同分佈（即i.d.）值的隨機值。

範例：

```
> SELECT randn();
 -0.3254147983080288
> SELECT randn(0);
 1.1164209726833079
> SELECT randn(null);
 1.1164209726833079
```

>[!NOTE]
>
>在一般情況下，此函式是非確定性的。

#### rint

`rint(expr)`: 傳回值最接近引數且等於數學整數的雙重值。

範例：

```
> SELECT rint(12.3456);
 12.0
```

#### round

`round(expr, d)`: 使用 `expr` HALF_UP `d` 捨入模式返回四捨五入到小數位。

範例：

```
> SELECT round(2.5, 0);
 3.0
```

#### 簽署

`sign(expr)`: 傳回-1.0、0.0或1.0, `expr` 為負數、0或正數。

範例：

```
> SELECT sign(40);
 1.0
```

#### signum

`signum(expr)`: 傳回-1.0、0.0或1.0, `expr` 為負數、0或正數。

範例：

```
> SELECT signum(40);
 1.0
```

#### sin

`sin(expr)`: 傳回的正弦 `expr`，如同由計算 `java.lang.Math.sin`。

引數：

- `expr`: 角度（以弧度為單位）

範例：

```
> SELECT sin(0);
 0.0
```

#### sinh

`sinh(expr)`: 傳回雙曲正 `expr`弦，如同由計算 `java.lang.Math.sinh`。

引數：

- `expr`: 雙曲角

範例：

```
> SELECT sinh(0);
 0.0
```

#### sqrt

`sqrt(expr)`: 傳回的平方根 `expr`。

範例：

```
> SELECT sqrt(4);
 2.0
```

#### stddev

`stddev(expr)`: 傳回根據群組值計算的範例標準差。

#### stddev_pop

`sttdev_pop(expr)`: 返回根據組值計算的人口標準差。

#### stddev_samp

`stddev_samp(expr)`: 傳回根據群組值計算的範例標準差。

#### sum

`sum(expr)`: 傳回根據群組值計算的總和。

#### 陳

`tan(expr)`: 傳回的正切 `expr`，如同由計算 `java.lang.Math.tan`。

引數：

- `expr`: 角度（以弧度為單位）

範例：

```
> SELECT tan(0);
 0.0
```

#### 坦赫

`tanh(expr)`: 傳回的雙曲正切 `expr`，如同由計算 `java.lang.Math.tanh`。

引數：

- `expr`: 雙曲角

範例：

```
> SELECT tanh(0);
 0.0
```

#### Var_pop

`var_pop(expr)`: 傳回根據群組值計算的人口差異。

#### Var_samp

`var_samp(expr)`: 傳回根據群組值計算的範例變數。

#### 方差

`variance(expr)`: 傳回根據群組值計算的範例變數。

### 邏輯運算子

#### 邏輯非

`! expr`: 邏輯上不是。

#### 小於

`expr1 < expr2`: 如果小於， `expr1` 則返回true `expr2`。

引數：

- `expr1, expr2`: 這兩個表達式必須是相同的類型，或者它們可以轉換為公用類型，並且必須是可排序的類型。 例如，映射類型不可排序，因此不受支援。 對於複雜類型（如陣列／結構），欄位的資料類型必須可以排序。

範例：

```
> SELECT 1 < 2;
 true
> SELECT 1.1 < '1';
 false
> SELECT to_date('2009-07-30 04:17:52') < to_date('2009-07-30 04:17:52');
 false
> SELECT to_date('2009-07-30 04:17:52') < to_date('2009-08-01 04:17:52');
 true
> SELECT 1 < NULL;
 NULL
```

#### 小於或等於

`expr1 <= expr2`: 若小於或等於， `expr1` 則傳回true `expr2`。

引數：

- `expr1, expr2`: 這兩個表達式必須是相同類型，或可以轉換為公用類型，並且必須是可排序的類型。 例如，映射類型不可排序，因此不受支援。 對於複雜類型（如陣列／結構），欄位的資料類型必須可以排序。

範例：

```
> SELECT 2 <= 2;
 true
> SELECT 1.0 <= '1';
 true
> SELECT to_date('2009-07-30 04:17:52') <= to_date('2009-07-30 04:17:52');
 true
> SELECT to_date('2009-07-30 04:17:52') <= to_date('2009-08-01 04:17:52');
 true
> SELECT 1 <= NULL;
 NULL
```

#### 等於

`expr1 = expr2`: 若等於則傳 `expr1` 回 `expr2`true，否則傳回false。

引數：

- `expr1, expr2`: 這兩個表達式必須是相同的類型，或者它們可以轉換為公共類型，並且必須是可用於等式比較的類型。 不支援地圖類型。 對於複雜類型（如陣列／結構），欄位的資料類型必須可以排序。

範例：

```
> SELECT 2 = 2;
 true
> SELECT 1 = '1';
 true
> SELECT true = NULL;
 NULL
> SELECT NULL = NULL;
 NULL
```

#### 大於

`expr1 > expr2`: 若大於， `expr1` 則傳回true `expr2`。

引數：

- `expr1, expr2`: 這兩個表達式必須是相同的類型，或者它們可以轉換為公用類型，並且必須是可排序的類型。 例如，映射類型不可排序，因此不受支援。 對於複雜類型（如陣列／結構），欄位的資料類型必須可以排序。

範例：

```
> SELECT 2 > 1;
 true
> SELECT 2 > '1.1';
 true
> SELECT to_date('2009-07-30 04:17:52') > to_date('2009-07-30 04:17:52');
 false
> SELECT to_date('2009-07-30 04:17:52') > to_date('2009-08-01 04:17:52');
 false
> SELECT 1 > NULL;
 NULL
```

#### 大於或等於

`expr1 >= expr2`: 若大於或等於 `expr1` ，則傳回true `expr2`。

引數：

- `expr1, expr2`: 這兩個表達式必須是相同的類型，或者它們可以轉換為公用類型，並且必須是可排序的類型。 例如，映射類型不可排序，因此不受支援。 對於複雜類型（如陣列／結構），欄位的資料類型必須可以排序。

範例：

```
> SELECT 2 >= 1;
 true
> SELECT 2.0 >= '2.1';
 false
> SELECT to_date('2009-07-30 04:17:52') >= to_date('2009-07-30 04:17:52');
 true
> SELECT to_date('2009-07-30 04:17:52') >= to_date('2009-08-01 04:17:52');
 false
> SELECT 1 >= NULL;
 NULL
```

#### Bitwise獨佔或

`expr1 ^ expr2`: 傳回位排它OR的結 `expr1` 果 `expr2`。

範例：

```
> SELECT 3 ^ 5;
 2
```

#### 和

`expr1 and expr2`: 邏輯和。

#### arrays_overlap

`arrays_overlap(a1, a2)`: 如果a1至少包含同樣存在於a2中的非空元素，則返回true。 如果陣列沒有公共元素，並且它們都是非空的，且其中一個包含空元素，則返回空值。 否則，返回false。

範例：

```
> SELECT arrays_overlap(array(1, 2, 3), array(3, 4, 5));
 true
```

自： 2.4.0

#### assert_true

`assert_true(expr)`: 如果不是true，則 `expr` 拋出異常。

範例：

```
> SELECT assert_true(0 < 1);
 NULL
```

#### if

`if(expr1, expr2, expr3)`: 若 `expr1` 評估為true，則傳回 `expr2`; 否則，將返 `expr3`回。

範例：

```
> SELECT if(1 < 2, 'a', 'b');
 a
```

#### ifnull

`ifnull(expr1, expr2)`: 如果 `expr2` 為 `expr1` null，則返回，否則 `expr1` 返回。

範例：

```
> SELECT ifnull(NULL, array('2'));
 ["2"]
```

#### in

`expr1 in(expr2, expr3, ...)`: 如果等於任何 `expr` valN，則返回true。

引數：
- `expr1, expr2, expr3, ...`: 引數類型必須相同。

範例：

```
> SELECT 1 in(1, 2, 3);
 true
> SELECT 1 in(2, 3, 4);
 false
> SELECT named_struct('a', 1, 'b', 2) in(named_struct('a', 1, 'b', 1), named_struct('a', 1, 'b', 3));
 false
> SELECT named_struct('a', 1, 'b', 2) in(named_struct('a', 1, 'b', 2), named_struct('a', 1, 'b', 3));
 true
```

#### isnan

`isnan(expr)`: 如果為NaN則傳 `expr` 回true，否則傳回false。

範例：

```
> SELECT isnan(cast('NaN' as double));
 true
```

#### isnotnull

`isnotnull(expr)`: 若非null，則 `expr` 傳回true，否則傳回false。

範例：

```
> SELECT isnotnull(1);
 true
```

#### isnull

`isnull(expr)`: 若為null，則傳 `expr` 回true，否則傳回false。

範例：

```
> SELECT isnull(1);
 false
```

#### 納維

`nanvl(expr1, expr2)`: 如果 `expr1` 不是NaN或其他情況，則傳回 `expr2` 此選項。

範例：

```
> SELECT nanvl(cast('NaN' as double), 123);
 123.0
```

#### not

`not expr`: 邏輯上不是。

#### 或

`expr1 or expr2`: 邏輯或。

#### xpath_boolean

`xpath_boolean(xml, xpath)`: 如果XPath表達式評估為true或找到匹配節點，則返回true。

範例：

```
> SELECT xpath_boolean('<a><b>1</b></a>','a/b');
 true
```

### 日期／時間函式

#### add_months

`add_months(start_date, num_months)`: 傳回晚於的 `num_months` 日期 `start_date`。

範例：

```
> SELECT add_months('2016-08-31', 1);
 2016-09-30
```

自： 1.5.0

#### date_add

`date_add(start_date, num_days)`: 傳回晚於的 `num_days` 日期 `start_date`。

範例：

```
> SELECT date_add('2016-07-30', 1);
 2016-07-31
```

自： 1.5.0

#### date_format

`date_format(timestamp, fmt)`: 轉 `timestamp` 換為日期格式指定格式的字串值 `fmt`。

範例：

```
> SELECT date_format('2016-04-08', 'y');
 2016
```

自： 1.5.0

#### date_sub

`date_sub(start_date, num_days)`: 傳回先前的 `num_days` 日期 `start_date`。

範例：

```
> SELECT date_sub('2016-07-30', 1);
 2016-07-29
```

自： 1.5.0

#### date_trunc

`date_trunc(fmt, ts)`: 傳回截斷為格式模型所指定單位的時間戳記 `fmt`。 `fmt` 應為 [&quot;YEAR&quot;、&quot;YYY&quot;、&quot;YY&quot;、&quot;MON&quot;、&quot;MONTH&quot;、&quot;MM&quot;、&quot;DAY&quot;、&quot;DD&quot;、&quot;HOUR&quot;、&quot;MINUTE&quot;、&quot;SECOND&quot;、&quot;WEEK、&quot;QUARTER&quot;之一者]

範例：

```
> SELECT date_trunc('YEAR', '2015-03-05T09:32:05.359');
 2015-01-01 00:00:00
> SELECT date_trunc('MM', '2015-03-05T09:32:05.359');
 2015-03-01 00:00:00
> SELECT date_trunc('DD', '2015-03-05T09:32:05.359');
 2015-03-05 00:00:00
> SELECT date_trunc('HOUR', '2015-03-05T09:32:05.359');
 2015-03-05 09:00:00
```

自： 2.3.0

#### datediff

`datediff(endDate, startDate)`: 返回從到的天 `startDate` 數 `endDate`。

範例：

```
> SELECT datediff('2009-07-31', '2009-07-30');
 1

> SELECT datediff('2009-07-30', '2009-07-31');
 -1
```

自： 1.5.0

#### 天

`day(date)`: 傳回日期／時間戳記的月份日。

範例：

```
> SELECT day('2009-07-30');
 30
```

自： 1.5.0

#### dayofmonth

`dayofmonth(date)`: 傳回日期／時間戳記的月份日。

範例：

```
> SELECT dayofmonth('2009-07-30');
 30
```

自： 1.5.0

#### dayofweek

`dayofweek(date)`: 傳回日期／時間戳記的星期幾（1 =星期日，2 =星期一， ..., 7 =星期六）。

範例：

```
> SELECT dayofweek('2009-07-30');
 5
```

自： 2.3.0

#### dayofyer

`dayofyear(date)`: 傳回日期／時間戳記的年份日。

範例：

```
> SELECT dayofyear('2016-04-09');
 100
```

自： 1.5.0

#### from_unixtime

`from_unixtime(unix_time, format)`: 在指 `unix_time` 定中返回 `format`。

範例：

```
> SELECT from_unixtime(0, 'yyyy-MM-dd HH:mm:ss');
 1970-01-01 00:00:00
```

自： 1.5.0

#### from_utc_timestamp

`from_utc_timestamp(timestamp, timezone)`: 將&#39;2017-07-14 02:40:00.0&#39;等時間戳記解譯為UTC的時間，並將該時間轉換為指定時區的時間戳記。 例如，&#39;GMT+1&#39;會產生&#39;2017-07-14 03:40:00.0&#39;。

範例：

```
> SELECT from_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-31 09:00:00
```

自： 1.5.0

#### 小時

`hour(timestamp)`: 傳回字串／時間戳記的hour元件。

範例：

```
> SELECT hour('2009-07-30 12:58:59');
 12
```

自： 1.5.0

#### last_day

`last_day(date):` 傳回日期所屬月份的最後一天。

範例：

```
> SELECT last_day('2009-01-12');
 2009-01-31
```

自： 1.5.0

#### 分鐘

`minute(timestamp)`: 傳回字串／時間戳記的分鐘元件。

範例：

```
> SELECT minute('2009-07-30 12:58:59');
 58
```

自： 1.5.0

#### 個月

`month(date)` 傳回日期／時間戳記的月份元件。

範例：

```
> SELECT month('2016-07-30');
 7
```

自： 1.5.0

#### months_between

`months_between(timestamp1, timestamp2[, roundOff])`: 如果 `timestamp1` 晚於 `timestamp2`，則結果為正面。 如 `timestamp1` 果 `timestamp2` 和是在當月的同一天，或兩者皆是當月的最後一天，則會忽略一天中的時間。 否則，差額會根據每月31天計算，並四捨五入至8位數（除非如此） `roundOff=false`。

範例：

```
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30');
 3.94959677
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30', false);
 3.9495967741935485
```

自： 1.5.0

#### next_day

`next_day(start_date, day_of_week)`: 傳回遲於並指定的 `start_date` 第一個日期。

範例：

```
> SELECT next_day('2015-01-14', 'TU');
 2015-01-20
```

自： 1.5.0

#### 季

`quarter(date)`: 傳回日期的年份季度，範圍為1到4。

範例：

```
> SELECT quarter('2016-08-31');
 3
```

自： 1.5.0

#### 秒

`second(timestamp)`: 傳回字串／時間戳記的第二個元件。

範例：

```
> SELECT second('2009-07-30 12:58:59');
 59
```

自： 1.5.0

#### to_date

`to_date(date_str[, fmt])`: 將運算 `date_str` 式剖析為 `fmt` 日期。 傳回輸入無效的null。 依預設，若省略，則會遵循傳送規則至 `fmt` 日期。

範例：

```
> SELECT to_date('2009-07-30 04:17:52');
 2009-07-30
> SELECT to_date('2016-12-31', 'yyyy-MM-dd');
 2016-12-31
```

自： 1.5.0

#### to_timestamp

`to_timestamp(timestamp[, fmt])`: 使用運算 `timestamp` 式剖析運算式 `fmt` 至時間戳記。 傳回輸入無效的null。 依預設，如果省略，則會將轉存規則遵循至 `fmt` 時間戳記。

範例：

```
> SELECT to_timestamp('2016-12-31 00:12:00');
 2016-12-31 00:12:00
> SELECT to_timestamp('2016-12-31', 'yyyy-MM-dd');
 2016-12-31 00:00:00
```

自： 2.2.0

#### to_unix_timestamp

`to_unix_timestamp(expr[, pattern])`: 返回給定時間的UNIX時間戳。

範例：

```
> SELECT to_unix_timestamp('2016-04-08', 'yyyy-MM-dd');
 1460041200
```

自： 1.6.0

#### to_utc_timestamp

`to_utc_timestamp(timestamp, timezone)`: 將&#39;2017-07-14 02:40:00.0&#39;等時間戳記解譯為指定時區中的時間，並將該時間呈現為UTC中的時間戳記。 例如，&#39;GMT+1&#39;會產生&#39;2017-07-14 01:40:00.0&#39;。

範例：

```
> SELECT to_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-30 15:00:00
```

自： 1.5.0

#### trunc

`trunc(date, fmt)`: 將日期的時間部分截斷為格式模型指定的單位，返回日期 `fmt`。 `fmt` 是&quot;year&quot;、 [&quot;yyyy&quot;、&quot;yy&quot;、&quot;mon&quot;、&quot;month&quot;、&quot;mm&quot;的其中一個]

範例：

```
> SELECT trunc('2009-02-12', 'MM');
 2009-02-01
> SELECT trunc('2015-10-27', 'YEAR');
 2015-01-01
```

自： 1.5.0

#### unix_timestamp

`unix_timestamp([expr[, pattern]])`: 傳回目前或指定時間的UNIX時間戳記。

範例：

```
> SELECT unix_timestamp();
 1476884637
> SELECT unix_timestamp('2016-04-08', 'yyyy-MM-dd');
 1460041200
```

自： 1.5.0

#### 工作日

`weekday(date)`: 傳回日期／時間戳記的星期幾（0 =星期一， 1 =星期二， ..., 6 =星期日）。

範例：

```
> SELECT weekday('2009-07-30');
 3
```

自： 2.4.0

#### week_of_year

`weekofyear(date)`: 傳回指定日期當年的一週。 周被認為是星期一開始，第1週是超過3天的第一週。

範例：

```
> SELECT weekofyear('2008-02-20');
 8
```

自： 1.5.0

#### when

`CASE WHEN expr1 THEN expr2 [WHEN expr3 THEN expr4]* [ELSE expr5] END`: 當 `expr1` = true時，返回 `expr2`; else when `expr3` = true, returns `expr4`; else傳回 `expr5`。

引數：

- `expr1`, `expr3`: 分支條件表達式應全部為布爾類型。
- `expr2`、 `expr4`、 `expr5`: 分支值表達式和else值表達式都應為相同類型或可強制為公共類型。

範例：

```
> SELECT CASE WHEN 1 > 0 THEN 1 WHEN 2 > 0 THEN 2.0 ELSE 1.2 END;
 1
> SELECT CASE WHEN 1 < 0 THEN 1 WHEN 2 > 0 THEN 2.0 ELSE 1.2 END;
 2
> SELECT CASE WHEN 1 < 0 THEN 1 WHEN 2 < 0 THEN 2.0 END;
 NULL
```

#### 年

`year(date)`: 傳回日期／時間戳記的年份元件。

範例：

```
> SELECT year('2016-07-30');
 2016
```

自： 1.5.0

### 集合函式

#### 約_count_distinct

`approx_count_distinct(expr[, relativeSD])`: 返回由HyperLogLog++提供的估計基數。 `relativeSD` 定義允許的最大估計錯誤。

### 陣列

#### 陣列

`array(expr, ...)`: 傳回具有給定元素的陣列。

範例：

```
> SELECT array(1, 2, 3);
 [1,2,3]
```

#### array_contains

`array_contains(array, value)`: 如果陣列包含值，則返回true。

範例：

```
> SELECT array_contains(array(1, 2, 3), 2);
 true
```

#### array_distinct

`array_distinct(array)`: 從陣列中刪除重複值。

範例：

```
> SELECT array_distinct(array(1, 2, 3, null, 3));
 [1,2,3,null]
```

自： 2.4.0

#### array_except

`array_except(array1, array2)`: 傳回中（但不是中）的元 `array1` 素陣列，而 `array2`且不複製。

範例：

```
> SELECT array_except(array(1, 2, 3), array(1, 3, 5));
 [2]
```

自： 2.4.0

#### array_intersect

`array_intersect(array1, array2)`: 傳回和交集中的元素陣列， `array1` 不 `array2`複製。

範例：

```
> SELECT array_intersect(array(1, 2, 3), array(1, 3, 5));
 [1,3]
```

自： 2.4.0

#### array_join

`array_join(array, delimiter[, nullReplacement])`: 使用分隔字元和選用字串串連指定陣列的元素以取代空值。 如果未設定值，則 `nullReplacement`會篩選任何空值。

範例：

```
> SELECT array_join(array('hello', 'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ', ',');
 hello , world
```

自： 2.4.0

#### array_max

`array_max(array)`: 返回陣列中的最大值。 會跳過Null元素。

範例：

```
> SELECT array_max(array(1, 20, null, 3));
 20
```

自： 2.4.0

#### array_min

`array_min(array)`: 傳回陣列中的最小值。 會跳過Null元素。

範例：

```
> SELECT array_min(array(1, 20, null, 3));
 1
```

自： 2.4.0

#### array_position

`array_position(array, element)`: 返回陣列第一個元素（基於1）的索引，只要長。

範例：

```
> SELECT array_position(array(3, 2, 1), 1);
 3
```

自： 2.4.0

#### array_remove

`array_remove(array, element)`: 從陣列中移除所有等於元素的元素。

範例：

```
> SELECT array_remove(array(1, 2, 3, null, 3), 3);
 [1,2,null]
```

自： 2.4.0

#### array_repeat

`array_repeat(element, count)`: 傳回包含元素計數時間的陣列。

範例：

```
> SELECT array_repeat('123', 2);
 ["123","123"]
```

自： 2.4.0

#### array_sort

`array_sort(array)`: 按升序排序輸入陣列。 輸入陣列的元素必須可以排序。 空元素放置在返回陣列的末尾。

範例：

```
> SELECT array_sort(array('b', 'd', null, 'c', 'a'));
 ["a","b","c","d",null]
```

自： 2.4.0

#### array_union

`array_union(array1, array2)`: 傳回和（不含重複項）並合中 `array1` 的元 `array2`素陣列。

範例：

```
> SELECT array_union(array(1, 2, 3), array(1, 3, 5));
 [1,2,3,5]
```

自： 2.4.0

#### array_zip

`arrays_zip(a1, a2, ...)`: 傳回結合的結構陣列，其中第N個結構包含輸入陣列的所有第N個值。

範例：

```
> SELECT arrays_zip(array(1, 2, 3), array(2, 3, 4));
 [{"0":1,"1":2},{"0":2,"1":3},{"0":3,"1":4}]
> SELECT arrays_zip(array(1, 2), array(2, 3), array(3, 4));
 [{"0":1,"1":2,"2":3},{"0":2,"1":3,"2":4}]
```

自： 2.4.0

#### element_at

`element_at(array, index)`: 在給定（基於1）索引處返回陣列元素。 若 `index < 0`是，存取從最後一個到第一個的元素。 如果索引超過陣列的長度，則返回NULL。

`element_at(map, key)`: 傳回指定金鑰的值，若金鑰未包含在映射中，則傳回NULL

範例：

```
> SELECT element_at(array(1, 2, 3), 2);
 2
> SELECT element_at(map(1, 'a', 2, 'b'), 2);
 b
```

自： 2.4.0

#### 爆炸

`explode(expr)`: 將陣列的元素分 `expr` 成多行，或將映射的元素分 `expr` 成多行和多列。

範例：

```
> SELECT explode(array(10, 20));
 10
 20
```

#### explode_outer

`explode_outer(expr)`: 將陣列的元素分 `expr` 成多行，或將映射的元素分 `expr` 成多行和多列。

範例：

```
> SELECT explode_outer(array(10, 20));
 10
 20
```

#### find_in_set

`find_in_set(str, str_array)`: 傳回逗號分隔清單(`str`)中指定字串()的索引(以1為基`str_array`礎)。 如果找不到字串或指定字串(`str`)包含逗號，則傳回0。

範例：

```
> SELECT find_in_set('ab','abc,b,ab,c,def');
 3
```

#### 平面化

`flatten(arrayOfArrays)`: 將陣列轉換為單個陣列。

範例：

```
> SELECT flatten(array(array(1, 2), array(3, 4)));
 [1,2,3,4]
```

自： 2.4.0

#### 內嵌

`inline(expr)`: 將一系列結構分解成一個表格。

範例：

```
> SELECT inline(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### inilne_outer

`inline_outer(expr)`: 將一系列結構分解成一個表格。

範例：

```
> SELECT inline_outer(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### 波塞普洛德

`posexplode(expr)`: 將陣列的元素分 `expr` 成多個具有位置的行，或將映射的元素分 `expr` 成多個具有位置的行和列。

範例：

```
> SELECT posexplode(array(10,20));
 0  10
 1  20
```

#### posexplode_outer

`posexplode_outer(expr)`: 將陣列的元素分 `expr` 成多個具有位置的行，或將映射的元素分 `expr` 成多個具有位置的行和列。

範例：

```
> SELECT posexplode_outer(array(10,20));
 0  10
 1  20
```

#### 逆

`reverse(array)`: 傳回元素順序相反的字串或陣列。

範例：

```
> SELECT reverse('Spark SQL');
 LQS krapS
> SELECT reverse(array(2, 1, 4, 3));
 [3,4,1,2]
```

自： 1.5.0
>[!NOTE]
>
>自2.4.0以來，陣列的rse邏輯可用。

#### 洗牌

`shuffle(array)`: 傳回給定陣列的隨機置換。

範例：

```
> SELECT shuffle(array(1, 20, 3, 5));
 [3,1,5,20]
> SELECT shuffle(array(1, 20, null, 3));
 [20,null,3,1]
```

自： 2.4.0
>[!NOTE]
>
>函式是非確定性的。

#### 切片

`slice(x, start, length)`: 子集陣列x從索引開始(或從結束開始（如果開始為負），以指定的長度開始。

範例：

```
> SELECT slice(array(1, 2, 3, 4), 2, 2);
 [2,3]
> SELECT slice(array(1, 2, 3, 4), -2, 2);
 [3,4]
```

自： 2.4.0

#### sort_array

`sort_array(array[, ascendingOrder])`: 根據陣列元素的自然順序，按遞增或遞減順序對輸入陣列進行排序。 Null元素會以遞增順序放置在傳回陣列的開頭，或以遞減順序放置在傳回陣列的結尾。

範例：

```
> SELECT sort_array(array('b', 'd', null, 'c', 'a'), true);
 [null,"a","b","c","d"]
```

#### zip_with

`zip_with(left, right, func)`: 使用函式將兩個給定的陣列（按元素劃分）合併為單個陣列。 如果一個陣列較短，則在應用函式之前，會在末尾附加空值以匹配較長陣列的長度。

範例：

```
> SELECT zip_with(array(1, 2, 3), array('a', 'b', 'c'), (x, y) -> (y, x));
 [{"y":"a","x":1},{"y":"b","x":2},{"y":"c","x":3}]
> SELECT zip_with(array(1, 2), array(3, 4), (x, y) -> x + y);
 [4,6]
> SELECT zip_with(array('a', 'b', 'c'), array('d', 'e', 'f'), (x, y) -> concat(x, y));
 ["ad","be","cf"]
```

自： 2.4.0

### 資料類型轉換函式

#### bigint

`bigint(expr)`: 將值轉 `expr` 換為目標資料類型 `bigint`。

#### 二進位

`binary(expr)`: 將值轉 `expr` 換為目標資料類型 `binary`。

#### 布林值

`boolean(expr)`: 將值轉 `expr` 換為目標資料類型 `boolean`。

#### cast

`cast(expr AS type)`: 將值轉 `expr` 換為目標資料類型 `type`。

範例：

```
> SELECT cast('10' as int);
 10
```

#### 日期

`date(expr)`: 將值轉 `expr` 換為目標資料類型 `date`。

#### 小數點

`decimal(expr)`: 將值轉 `expr` 換為目標資料類型 `decimal`。

#### 雙倍

`double(expr)`: 將值轉 `expr` 換為目標資料類型 `double`。

#### 浮水

`float(expr)`: 將值轉 `expr` 換為目標資料類型 `float`。

#### int

`int(expr)`: 將值轉 `expr` 換為目標資料類型 `int`。

#### 地圖

`map(key0, value0, key1, value1, ...)`: 建立具有給定鍵／值對的映射。

範例：

```
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### smallint

`smallint(expr)`: 將值轉 `expr` 換為目標資料類型 `smallint`。

#### str_to_map

`str_to_map(text[, pairDelim[, keyValueDelim]])`: 使用分隔字元將文字分割為索引鍵／值對後，建立對應。 預設分隔字元為&#39;,&#39;（代表） `pairDelim` 和&#39;:&#39;（代表） `keyValueDelim`。

範例：

```
> SELECT str_to_map('a:1,b:2,c:3', ',', ':');
 map("a":"1","b":"2","c":"3")
> SELECT str_to_map('a');
 map("a":null)
```

#### 字串

`string(expr)`: 將值轉 `expr` 換為目標資料類型 `string`。

#### 結構

`struct(col1, col2, col3, ...)`: 建立具有給定欄位值的結構。

#### tinyint

`tinyint(expr)`: 將值轉 `expr` 換為目標資料類型 `tinyint`。

### 轉換和格式化功能

#### ascii

`ascii(str)`: 傳回第一個字元的數值 `str`。

範例：

```
> SELECT ascii('222');
 50
> SELECT ascii(2);
 50
```

#### base64

`base64(bin)`: 將引數從二進位轉 `bin` 換為基64字串。

範例：

```
> SELECT base64('Spark SQL');
 U3BhcmsgU1FM
```

#### 賓

`bin(expr)`: 傳回長值的字串表示法(以二進 `expr` 位格式表示)。

範例：

```
> SELECT bin(13);
 1101
> SELECT bin(-13);
 1111111111111111111111111111111111111111111111111111111111110011
> SELECT bin(13.3);
 1101
```

#### bit_length

`bit_length(expr)`: 傳回字串資料的位元長度或二進位資料的位元數。

範例：

```
> SELECT bit_length('Spark SQL');
 72
```

#### char

`char(expr)`: 傳回二進位等效為的ASCII字元 `expr`。 如果n大於256，則結果等於 `chr(n % 256)`。

範例：

```
> SELECT char(65);
 A
```

#### char_length

`char_length(expr)`: 傳回字串資料的字元長度或二進位資料的位元組數。 字串資料的長度包含尾隨空格。 二進位資料的長度包含二進位零。

範例：

```
> SELECT char_length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### character_length

`character_length(expr)`: 傳回字串資料的字元長度或二進位資料的位元組數。 字串資料的長度包含尾隨空格。 二進位資料的長度包含二進位零。

範例：

```
> SELECT character_length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### chr

`chr(expr)`: 傳回二進位等效為expr的ASCII字元。 若n大於256，則結果等同於 `chr(n % 256)`

範例：

```
> SELECT chr(65);
 A
```

#### 度

`degrees(expr)`: 將弧度轉換為度。

引數：
- `expr`: 角度（以弧度為單位）

範例：

```
> SELECT degrees(3.141592653589793);
 180.0
```

#### format_number

`format_number(expr1, expr2)`: 格式化 `expr1` 數字，例如&#39;#、###、###。##&#39;，四捨五入至小 `expr2` 數位。 如果 `expr2` 為0，則結果沒有小數點或小數部分。 `expr2` 也接受使用者指定的格式。 此功能與MySQL的功能類似 `FORMAT`。

範例：

```
> SELECT format_number(12332.123456, 4);
 12,332.1235
> SELECT format_number(12332.123456, '##################.###');
 12332.123
```

#### from_json

`from_json(jsonStr, schema[, options])`: 傳回具有給定和的結構 `jsonStr` 值 `schema`。

範例：

```
> SELECT from_json('{"a":1, "b":0.8}', 'a INT, b DOUBLE');
 {"a":1, "b":0.8}
> SELECT from_json('{"time":"26/08/2015"}', 'time Timestamp', map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"2015-08-26 00:00:00.0"}
```

自： 2.2.0

#### 雜湊

`hash(expr1, expr2, ...)`: 傳回引數的雜湊值。

範例：

```
> SELECT hash('Spark', array(123), 2);
 -1321691492
```

#### 十六進位

`hex(expr)`: 轉換為 `expr` 十六進位。

範例：

```
> SELECT hex(17);
 11
> SELECT hex('Spark SQL');
 537061726B2053514C
```

#### initcap

`initcap(str)`: 傳 `str` 回每個單字的首字母大寫。 所有其它字母都用小寫表示。 字詞以空格分隔。

範例：

```
> SELECT initcap('sPark sql');
 Spark Sql
```

#### lcase

`lcase(str)`: 傳回 `str` 所有字元皆變更為小寫。

範例：

```
> SELECT lcase('SparkSql');
 sparksql
```

#### lower

`lower(str)`: 傳回 `str` 所有字元皆變更為小寫。

範例：

```
> SELECT lower('SparkSql');
 sparksql
```

#### lpad

`lpad(str, len, pad)`: 傳 `str`回左邊填 `pad` 入長度的檔 `len`案 如果 `str` 長度大於 `len`，則返回值會縮短為字 `len` 元。

範例：

```
> SELECT lpad('hi', 5, '??');
 ???hi
> SELECT lpad('hi', 1, '??');
 h
```

#### 地圖

`map(key0, value0, key1, value1, ...)`: 建立具有給定鍵／值對的映射。

範例：

```
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### map_from_arrays

`map_from_arrays(keys, values)`: 建立具有一對給定鍵／值陣列的映射。 鍵中的元素不能為null。

範例：

```
> SELECT map_from_arrays(array(1.0, 3.0), array('2', '4'));
 {1.0:"2",3.0:"4"}
```

自： 2.4.0

#### map_from_entries

`map_from_entries(arrayOfEntries)`: 返回從給定條目陣列建立的映射。

範例：

```
> SELECT map_from_entries(array(struct(1, 'a'), struct(2, 'b')));
 {1:"a",2:"b"}
```

自： 2.4.0

#### md5

`md5(expr)`: 返回MD5 128位校驗和作為十六進位字串 `expr`。

範例：

```
> SELECT md5('Spark');
 8cde774d6f7333752ed72cacddb05126
```

#### rpad

`rpad(str, len, pad)`: 傳 `str`回，加上右邊填充 `pad` 的長度 `len`。 如果 `str` 長度大於 `len`，則返回值會縮短為字 `len` 元。

範例：

```
> SELECT rpad('hi', 5, '??');
 hi???
> SELECT rpad('hi', 1, '??');
 h
```

#### rtrim

`rtrim(str)`: 從中刪除尾隨空格字元 `str`。

`rtrim(trimStr, str)`: 移除尾隨字串，該字串從中包含修剪字串中的字元 `str`。

引數：
- `str`: 字串運算式
- `trimStr`: 要修剪的修剪字串字元。 預設值為單個空格

範例：

```
> SELECT rtrim('    SparkSQL   ');
 SparkSQL
> SELECT rtrim('LQSa', 'SSparkSQLS');
 SSpark
```

#### sha

`sha(expr)`: 傳回 `sha1` 雜湊值作為的十六進位字串 `expr`。

範例：

```
> SELECT sha('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha1

`sha1(expr)`: 傳回 `sha1` 雜湊值作為的十六進位字串 `expr`。

範例：

```
> SELECT sha1('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha2

`sha2(expr, bitLength)`: 將SHA-2系列的校驗和作為十六進位字串返回 `expr`。 支援SHA-224、SHA-256、SHA-384和SHA-512。 位長度0等於256。

範例：

```
> SELECT sha2('Spark', 256);
 529bc3b07127ecb7e53a4dcf1991d9152c24537d919178022b2c42657f79a26b
```

#### soundex

`soundex(str)`: 傳回字串的Soundex程式碼。

範例：

```
> SELECT soundex('Miller');
 M460
```

#### 堆疊

`stack(n, expr1, ..., exprk)`: 分 `expr1`成幾 `exprk` 行 `n` 。

範例：

```
> SELECT stack(2, 1, 2, 3);
 1  2
 3  NULL
```

#### substr

`substr(str, pos[, len])`: 傳回以開 `str` 頭為和 `pos` 為長度的子字串，或以開頭為和為長度的位元組數 `len`組片段 `pos``len`。

範例：

```
> SELECT substr('Spark SQL', 5);
 k SQL
> SELECT substr('Spark SQL', -3);
 SQL
> SELECT substr('Spark SQL', 5, 1);
 k
```

#### 子字串

`substring(str, pos[, len])`: 傳回以開 `str` 頭為和 `pos` 為長度的子字串，或以開頭為和為長度的位元組數 `len`組片段 `pos``len`。

範例：

```
> SELECT substring('Spark SQL', 5);
 k SQL
> SELECT substring('Spark SQL', -3);
 SQL
> SELECT substring('Spark SQL', 5, 1);
 k
```

#### to_json

`to_json(expr[, options])`: 傳回具有指定結構值的JSON字串。

範例：

```
> SELECT to_json(named_struct('a', 1, 'b', 2));
 {"a":1,"b":2}
> SELECT to_json(named_struct('time', to_timestamp('2015-08-26', 'yyyy-MM-dd')), map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"26/08/2015"}
> SELECT to_json(array(named_struct('a', 1, 'b', 2)));
 [{"a":1,"b":2}]
> SELECT to_json(map('a', named_struct('b', 1)));
 {"a":{"b":1}}
> SELECT to_json(map(named_struct('a', 1),named_struct('b', 2)));
 {"[1]":{"b":2}}
> SELECT to_json(map('a', 1));
 {"a":1}
> SELECT to_json(array((map('a', 1))));
 [{"a":1}]
```

自： 2.2.0

#### 翻譯

`translate(input, from, to)`: 將字 `input` 串中的字元取代為字串中 `from` 的對應字元，以轉譯字 `to` 串。

範例：

```
> SELECT translate('AaBbCc', 'abc', '123');
 A1B2C3
```

#### trim

`trim(str)`: 從中刪除前導和尾隨空格字元 `str`。

`trim(BOTH trimStr FROM str)`: 從中刪除前導和尾隨 `trimStr` 字元 `str`。

`trim(LEADING trimStr FROM str)`: 從中刪除 `trimStr` 前導字 `str`符。

`trim(TRAILING trimStr FROM str)`: 從中刪除尾 `trimStr` 隨字元 `str`。

引數：
- `str`: 字串運算式
- `trimStr`: 要修剪的修剪字串字元，預設值為單一空格
- `BOTH`, `FROM`: 這些關鍵字用於指定字串兩端的修剪字串字元
- `LEADING`, `FROM`: 這些是從字串左側指定修剪字串字元的關鍵字
- `TRAILING`, `FROM`: 這些是從字串右側指定修剪字串字元的關鍵字

範例：

```
> SELECT trim('    SparkSQL   ');
 SparkSQL
> SELECT trim('SL', 'SSparkSQLS');
 parkSQ
> SELECT trim(BOTH 'SL' FROM 'SSparkSQLS');
 parkSQ
> SELECT trim(LEADING 'SL' FROM 'SSparkSQLS');
 parkSQLS
> SELECT trim(TRAILING 'SL' FROM 'SSparkSQLS');
 SSparkSQ
```

#### ucase

`ucase(str)`: 傳回 `str` 所有字元皆變更為大寫。

範例：

```
> SELECT ucase('SparkSql');
 SPARKSQL
```

#### unbase64

`unbase64(str)`: 將引數從基64字串轉 `str` 換為二進位。

範例：

```
> SELECT unbase64('U3BhcmsgU1FM');
 Spark SQL
```

#### 未十六進位

`unhex(expr)`: 將十六進位 `expr` 轉換為二進位。

範例：

```
> SELECT decode(unhex('537061726B2053514C'), 'UTF-8');
 Spark SQL
```

#### upper

`upper(str)`: 傳回 `str` 所有字元皆變更為大寫。

範例：

```
> SELECT upper('SparkSql');
 SPARKSQL
```

#### uid

`uuid()`: 傳回通用唯一識別碼(UUID)字串。 值會傳回為標準UUID 36字元字串。

範例：

```
> SELECT uuid();
 46707d92-02f4-4817-8116-a4c3b23e6266
```

>[!NOTE]
>
>函式是非確定性的。

### 資料評估

#### 聚結

`coalesce(expr1, expr2, ...)`: 傳回第一個非空值引數（如果存在）。 否則，為null。

範例：

```
> SELECT coalesce(NULL, 1, NULL);
 1
```

#### collect_list

`collect_list(expr)`: 收集並傳回非唯一元素的清單。

#### collect_set

`collect_set(expr)`: 收集並傳回一組獨特元素。

#### concat

`concat(col1, col2, ..., colN)`: 返回col1、col2、...、colN的串連。

範例：

```
> SELECT concat('Spark', 'SQL');
 SparkSQL
> SELECT concat(array(1, 2, 3), array(4, 5), array(6));
 [1,2,3,4,5,6]
```

>[!NOTE]
>
>`concat` 自2.4.0以來，陣列的邏輯可用。

#### concat_ws

`concat_ws(sep, [str | array(str)]+)`: 傳回以分隔的字串串串連 `sep`。

範例：

```
> SELECT concat_ws(' ', 'Spark', 'SQL');
  Spark SQL
```

#### count

`count(*)`: 傳回擷取的列總數，包括包含null的列。

`count(expr[, expr...])`: 返回所提供表達式均為非空值的行數。

`count(DISTINCT expr[, expr...])`: 傳回所提供運算式為唯一且非null的列數。

#### crc32

`crc32(expr)`: 傳回的循環冗餘校驗值 `expr` 為bigint。

範例：

```
> SELECT crc32('Spark');
 1557323817
```

#### 解碼

`decode(bin, charset)`: 使用第二個引數字元集解碼第一個引數。

範例：

```
> SELECT decode(encode('abc', 'utf-8'), 'utf-8');
 abc
```

#### 跪

`elt(n, input1, input2, ...)`: 傳回 `n`第個輸入，例如，在 `input2` 為 `n` 2時傳回。

範例：

```
> SELECT elt(1, 'scala', 'java');
 scala
```

#### 編碼

`encode(str, charset)`: 使用第二個引數字元集來編碼第一個引數。

範例：

```
> SELECT encode('abc', 'utf-8');
 abc
```

#### first

`first(expr[, isIgnoreNull])`: 傳回一組列 `expr` 的第一個值。 如果 `isIgnoreNull` 為true，則僅傳回非null值。

#### first_value

`first_value(expr[, isIgnoreNull])`: 傳回一組列 `expr` 的第一個值。 如果 `isIgnoreNull` 為true，則僅傳回非null值。

#### get_json_object

`get_json_object(json_txt, path)`: 從擷取json物件 `path`。

範例：

```
> SELECT get_json_object('{"a":"b"}', '$.a');
 b
```

#### 分組

<!-- was blank --->

#### grouping_id

<!-- was blank --->

#### instr

`instr(str, substr)`: 返回（基於1）的索引，該索引是第一個出現 `substr` 的 `str`。

範例：

```
> SELECT instr('SparkSQL', 'SQL');
 6
```

#### json_tuple

`json_tuple(jsonStr, p1, p2, ..., pn)`: 傳回與函式類似的元 `get_json_object`組，但會使用多個名稱。 所有輸入參數和輸出列類型都是字串。

範例：

```
> SELECT json_tuple('{"a":1, "b":2}', 'a', 'b');
 1  2
```

#### 滯後

`lag(input[, offset[, default]])`: 返回窗口 `input` 中當 `offset`前行前面第一行的值。 預設值為 `offset` 1，預設值 `default` 為null。 如果行中 `input` 的 `offset`值為null，則返回null。 如果沒有此類偏移行（例如，當偏移為1時，窗口的第一行沒有任何前一行），並返回 `default` 該行。

#### last

`last(expr[, isIgnoreNull])`: 傳回一組列 `expr` 的最後一個值。 如果 `isIgnoreNull` 為true，則僅傳回非null值。

#### last_value

`last_value(expr[, isIgnoreNull])`: 傳回一組列 `expr` 的最後一個值。 如果 `isIgnoreNull` 為true，則僅傳回非null值。

#### 鉛

`lead(input[, offset[, default]])`: 返回窗口 `input` 中當 `offset`前行後面第一行的值。 預設值為 `offset` 1，預設值 `default` 為null。 如果行中 `input` 的 `offset`值為null，則返回null。 如果沒有這樣的偏移行（例如，當偏移為1時，窗口的最後一行沒有任何後續行），則返回 `default` 該行。


#### left

`left(str, len)`: 從字串傳 `len` 回最`len` 左側（可以是字串類型）的字元 `str`。 如 `len` 果小於或等於0，則結果為空字串。

範例：

> SELECT left(&#39;Spark SQL&#39;, 3);
Spa


#### length

`length(expr)`: 傳回字串資料的字元長度或二進位資料的位元組數。 字串資料的長度包含尾隨空格。 二進位資料的長度包含二進位零。

範例：

```
> SELECT length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### 定位

`locate(substr, str[, pos])`: 傳回第一個出現位置 `substr` 的 `str` 位置 `pos`。 給定 `pos` 和返回值基於1。

範例：

```
> SELECT locate('bar', 'foobarbar');
 4
> SELECT locate('bar', 'foobarbar', 5);
 7
> SELECT POSITION('bar' IN 'foobarbar');
 4
```

#### map_concat

`map_concat(map, ...)`: 傳回所有指定地圖的合併。

範例：

```
> SELECT map_concat(map(1, 'a', 2, 'b'), map(2, 'c', 3, 'd'));
 {1:"a",2:"c",3:"d"}
```

自： 2.4.0

#### map_keys

`map_keys(map)`: 返回包含映射鍵的無序陣列。

範例：

```
> SELECT map_keys(map(1, 'a', 2, 'b'));
 [1,2]
```

#### map_values

`map_values(map)`: 返回包含映射值的無序陣列。

範例：

```
> SELECT map_values(map(1, 'a', 2, 'b'));
 ["a","b"]
```

#### ntile

`ntile(n)`: 將每個窗口分區的行分 `n` 成最多1到1的桶 `n`。

#### nullify

`nullif(expr1, expr2)`: 如果等於， `expr1` 則傳回 `expr2`null，否則 `expr1` 傳回。

範例：

```
> SELECT nullif(2, 2);
 NULL
```

#### nvl

`nvl(expr1, expr2)`: 如果 `expr2` 為 `expr1` null，則返回，否則 `expr1` 返回。

範例：

```
> SELECT nvl(NULL, array('2'));
 ["2"]
```

#### nvl2

`nvl2(expr1, expr2, expr3)`: 如果 `expr2` 不是 `expr1` null，則返回，否則 `expr3` 返回。

範例：

```
> SELECT nvl2(NULL, 2, 1);
 1
```

#### parse_url

`parse_url(url, partToExtract[, key])`: 從URL中提取部件。

範例：

```
> SELECT parse_url('http://spark.apache.org/path?query=1', 'HOST')
 spark.apache.org
> SELECT parse_url('http://spark.apache.org/path?query=1', 'QUERY')
 query=1
> SELECT parse_url('http://spark.apache.org/path?query=1', 'QUERY', 'query')
 1
```

#### position

`position(substr, str[, pos])`: 傳回第一個出現位置 `substr` 的 `str` 位置 `pos`。 給定 `pos` 和返回值基於1。

範例：

```
> SELECT position('bar', 'foobarbar');
 4
> SELECT position('bar', 'foobarbar', 5);
 7
> SELECT POSITION('bar' IN 'foobarbar');
 4
```

#### 排名

`rank()`: 計算值組中值的排名。 結果為分區排序中當前行前面或等於當前行的行數加一。 這些值會在序列中產生間隙。

#### regexp_extract

`regexp_extract(str, regexp[, idx])`: 擷取符合的群組 `regexp`。

範例：

```
> SELECT regexp_extract('100-200', '(\\d+)-(\\d+)', 1);
 100
```

#### regex_replace

`regexp_replace(str, regexp, rep)`: 取代與相符的 `str` 所有子字 `regexp` 串 `rep`。

範例：

```
> SELECT regexp_replace('100-200', '(\\d+)', 'num');
 num-num
```

#### 重複

`repeat(str, n)`: 傳回重複指定字串值n次的字串。

範例：

```
> SELECT repeat('123', 2);
 123123
```

#### replace

`replace(str, search[, replace])`: 將所有出現的 `search` 項目替換 `replace`為。

引數：
- `str`: 字串運算式
- `search`: 字串運算式。 如果 `search` 未在中找到， `str`則 `str` 會傳回不變。
- `replace`: 字串運算式。 如果 `replace` 未指定或是空字串，則不會替換從中刪除的字串 `str`。

範例：

```
> SELECT replace('ABCabc', 'abc', 'DEF');
 ABCDEF
```

#### 統計

<!-- was blank -->

#### row_number

`row_number()`: 根據窗口分區內行的順序，為每個行指派一個唯一的連續編號，從一個開始。

#### schema_of_json

`schema_of_json(json[, options])`: 傳回JSON字串的DDL格式結構。

範例：

```
> SELECT schema_of_json('[{"col":0}]');
 array<struct<col:int>>
```

自： 2.4.0

#### 句子

`sentences(str[, lang, country])`: 分 `str` 割成一組字詞。

範例：

```
> SELECT sentences('Hi there! Good morning.');
 [["Hi","there"],["Good","morning"]]
```

#### 序列

`sequence(start, stop, step)`: 從開始到停止（包括）生成元素陣列，逐步遞增。 傳回的元素類型與參數運算式類型相同。

支援的類型包括： 位元組、短、整數、長、日期、時間戳。

和 `start` 表達 `stop` 式必須解析為相同類型。 如果 `start` 和 `stop` 表達式解析為「日期」或「時間戳」類型，則表達 `step` 式必須解析為「間隔」類型； 否則，它會解析為與和表達式相 `start` 同的類 `stop` 型。

引數：
- `start`: 表達式。 範圍的開始。
- `stop`: 表達式。 範圍（含）結尾。
- `step`: 可選運算式。 範圍的步驟。 如果小 `step` 於或等於， `start` 則預設為1，否 `stop`則為-1。 對於時序，分別為1天和-1天。 如果 `start` 大於 `stop`，則 `step` 必須為負值，反之亦然。

範例：

```
> SELECT sequence(1, 5);
 [1,2,3,4,5]
> SELECT sequence(5, 1);
 [5,4,3,2,1]
> SELECT sequence(to_date('2018-01-01'), to_date('2018-03-01'), interval 1 month);
 [2018-01-01,2018-02-01,2018-03-01]
```

自： 2.4.0

#### shiftleft

`shiftleft(base, expr)`: 按位左班。

範例：

```
> SELECT shiftleft(2, 1);
 4
```

#### shiftright

`shiftright(base, expr)`: 按位（已簽署）右移。

範例：

```
> SELECT shiftright(4, 1);
 2
```

#### shittrightunged

`shiftrightunsigned(base, expr)`: 按位無號的右移。

範例：

```
> SELECT shiftrightunsigned(4, 1);
 2
```

#### 大小

`size(expr)`: 返回陣列或映射的大小。 如果函式的輸入為null且設定為true，則 `spark.sql.legacy.sizeOfNull` 返回-1。 如果 `spark.sql.legacy.sizeOfNull` 設定為false，則函式會為空輸入返回null。 依預設， `spark.sql.legacy.sizeOfNull` 參數會設為true。

範例：

```
> SELECT size(array('b', 'd', 'c', 'a'));
 4
> SELECT size(map('a', 1, 'b', 2));
 2
> SELECT size(NULL);
 -1
```

#### 空間

`space(n)`: 傳回由空格組成的 `n` 字串。

範例：

```
> SELECT concat(space(2), '1');
   1
```

#### split

`split(str, regex)`: 將符合 `str` 的發生次數分割 `regex`。

範例：

```
> SELECT split('oneAtwoBthreeC', '[ABC]');
 ["one","two","three",""]
```

#### substring_index

`substring_index(str, delim, count)`: 傳回分隔字元 `str` 出現 `count` 前的子字串 `delim`。 如 `count` 果為正數，則會傳回最終分隔字元左側的所有項目（從左側計算）。 如果 `count` 為負數，則會傳回最終分隔字元右側的所有項目（從右側計算）。 函式在 `substring_index` 搜索時執行區分大小寫匹配 `delim`。

範例：

```
> SELECT substring_index('www.apache.org', '.', 2);
 www.apache
```

#### window

<!-- was blank -->

#### xpath

`xpath(xml, xpath)`: 傳回xml節點中與XPath運算式相符的值字串陣列。

範例：

```
> SELECT xpath('<a><b>b1</b><b>b2</b><b>b3</b><c>c1</c><c>c2</c></a>','a/b/text()');
 ['b1','b2','b3']
```

#### xpath_double

`xpath_double(xml, xpath)`: 傳回雙重值、如果找不到相符項目，則返回零值，如果找到相符項目，則傳回NaN，但該值為非數值。

範例：

```
> SELECT xpath_double('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_float

`xpath_float(xml, xpath)`: 傳回浮點值、如果找不到相符項目則返回零值，如果找到相符項目，則傳回NaN，但該值為非數值。

範例：

```
> SELECT xpath_float('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_int

`xpath_int(xml, xpath)`: 傳回整數值，若找不到相符項目，則傳回零值，或找到相符項目，但該值為非數值。

範例：

```
> SELECT xpath_int('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_long

`xpath_long(xml, xpath)`: 傳回長整數值，若找不到相符項目，則傳回零值，或找到相符項目，但該值為非數值。

範例：

```
> SELECT xpath_long('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_number

`xpath_number(xml, xpath)`: 傳回雙重值、如果找不到相符項目，則返回零值，如果找到相符項目，則傳回NaN，但該值為非數值。

範例：

```
> SELECT xpath_number('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_short

`xpath_short(xml, xpath)`: 傳回短整數值，若找不到相符項目，則傳回零值，或找到相符項目，但該值為非數值。

範例：

```
> SELECT xpath_short('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_string

`xpath_string(xml, xpath)`: 傳回第一個與XPath運算式相符的xml節點的文字內容。

範例：

```
> SELECT xpath_string('<a><b>b</b><c>cc</c></a>','a/c');
 cc
```

### 目前資訊

#### current_database

`current_database()`: 返回當前資料庫。

範例：

```
> SELECT current_database();
 default
```

#### current_date

`current_date()`: 返回查詢評估開始時的當前日期。

自： 1.5.0

#### current_timestamp

`current_timestamp()`: 傳回查詢評估開始時的目前時間戳記。

自： 1.5.0

#### now

`now()`: 傳回查詢評估開始時的目前時間戳記。

自： 1.5.0
