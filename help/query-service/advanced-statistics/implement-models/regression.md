---
title: 回歸演演算法
description: 瞭解如何使用關鍵引數、說明和範常式式碼來設定和最佳化各種回歸演演算法，協助您實作進階統計模型。
role: Developer
exl-id: d38733bb-0420-40bf-a70b-19e0e0e58730
source-git-commit: 8b9cfb48a11701f0e4b358416c6b627bedf1db8b
workflow-type: tm+mt
source-wordcount: '2384'
ht-degree: 4%

---

# 回歸演演算法 {#regression-algorithms}

本檔案提供各種回歸演演算法的概觀，重點是它們的設定、關鍵引數，以及在進階統計模型中的實際使用。 回歸演演算法可用來建立相依變數和獨立變數之間的關係模型，根據觀察到的資料來預測連續結果。 每個區段都包含引數說明和範常式式碼，協助您針對如線性、隨機森林和生存回歸等工作，實作和最佳化這些演演算法。

## [!DNL Decision Tree]回歸 {#decision-tree-regression}

[!DNL Decision Tree]學習是一種監督學習方法，用於統計資料、資料採礦和機器學習。 在這個方法中，分類或回歸決策樹會作為預測模型來得出關於一組觀察結果的結論。

**參數**

下表概述用於設定和最佳化決策樹模型效能的關鍵引數。

| 參數 | 說明 | 預設值 | 可能的值 |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|--------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | 此引數指定用來離散化連續特徵的最大桶數，並決定每個節點的分割。 更多的回收桶可提供更精細的詳細資訊和細節。 | 32 | 在任何分類功能中必須至少為2且至少為類別數。 |
| `CACHE_NODE_IDS` | 此引數決定是否快取每個執行個體的節點ID。 如果`false`，演演算法會將樹狀結構傳遞給執行程式，以比對執行個體與節點。 如果`true`，演演算法會快取每個執行個體的節點ID，這會加快更深入樹狀結構的訓練。 使用者可以設定`CHECKPOINT_INTERVAL`來設定快取檢查點或停用的頻率。 | false | `true`或`false` |
| `CHECKPOINT_INTERVAL` | 此引數會指定快取節點ID被檢查的頻率。 例如，將其設定為`10`表示快取將每10次反複檢查一次。 這僅適用於`CACHE_NODE_IDS`設定為`true`且在`org.apache.spark.SparkContext`中設定查核點目錄的情況。 | 10 | (>=1) |
| `IMPURITY` | 此引數指定用於計算資訊增益的標準。 支援的值為`entropy`和`gini`。 | `gini` | `entropy`、`gini` |
| `MAX_DEPTH` | 此引數指定樹狀結構的最大深度。 例如，深度`0`表示1個分葉節點，而深度`1`表示1個內部節點和2個分葉節點。 深度必須在範圍`[0, 30]`內。 | 5 | [0， 30] |
| `MIN_INFO_GAIN` | 此引數設定分割所需的最小資訊增益，以便在樹狀節點視為有效。 | 0.0 | (>=0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | 此引數會指定每個子節點在分割後所必須擁有之加權樣本計數的最小分數。 如果任一子節點的片段小於此值，則會捨棄分割。 | 0.0 | [0.0， 0.5] |
| `MIN_INSTANCES_PER_NODE` | 此引數設定分割後每個子節點必須擁有的最小例證數目。 如果分割產生的例項少於此值，則會捨棄分割為無效。 | 1 | (>=1) |
| `MAX_MEMORY_IN_MB` | 此引數會指定配置給長條圖彙總的最大記憶體(MB)。 如果記憶體太小，每個疊代只會分割一個節點，其彙總可能會超過此大小。 | 256 | 任何正整數值 |
| `PREDICTION_COL` | 此引數會指定用來儲存預測的資料行名稱。 | &quot;prediction&quot; | 任何字串 |
| `SEED` | 此引數設定模型中使用的隨機種子。 | None | 任何64位元數字 |
| `WEIGHT_COL` | 此引數指定權重資料行的名稱。 如果此引數未設定或空白，則所有執行個體權重都會視為`1.0`。 | 未設定 | 任何字串 |

{style="table-layout:auto"}

**範例**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'decision_tree_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Factorization Machines]回歸 {#factorization-machines-regression}

[!DNL Factorization Machines]是回歸學習演演算法，支援一般漸層下降和AdamW求解器。 演演算法是以S. Rendle (2010)的論文&quot;[!DNL Factorization Machines]&quot;為基礎。

**參數**

下表概述設定和最佳化[!DNL Factorization Machines]回歸效能的關鍵引數。

| 參數 | 說明 | 預設值 | 可能的值 |
|------------------------|-------------------------------------------------------------------------------------------------|---------------|-----------------------|
| `TOL` | 此引數指定演演算法的收斂公差。 值越高收斂速度越快，但精確度越低。 | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | 此引數定義因子的維度。 較高的值會增加模型的複雜性。 | 8 | (>= 0) |
| `FIT_INTERCEPT` | 此引數會指出模型是否應該包含攔截字詞。 | `true` | `true`、`false` |
| `FIT_LINEAR` | 此引數會指定是否在模型中包含線性字詞（也稱為單向字詞）。 | `true` | `true`、`false` |
| `INIT_STD` | 此引數定義模型中使用的初始係數的標準差。 | 0.01 | (>= 0) |
| `MAX_ITER` | 此引數會指定演演算法要執行的最大迭代次數。 | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | 此引數會設定迷你批次分數，這會決定每個批次中使用的資料部分。 它必須在`(0, 1]`範圍內。 | 1.0 | `(0, 1]` |
| `REG_PARAM` | 此引數設定規則化引數以防止過度擬合。 | 0.0 | (>= 0) |
| `SEED` | 此引數指定用於模型初始化的隨機種子。 | None | 任何64位元數字 |
| `SOLVER` | 此引數指定用於最佳化的求解器演演算法。 | &quot;adamW&quot; | `gd` （漸層下降），`adamW` |
| `STEP_SIZE` | 此引數指定第一個最佳化步驟的初始步驟大小（或學習速率）。 | 1.0 | 任何正值 |
| `PREDICTION_COL` | 此引數會指定儲存預測的欄名稱。 | &quot;prediction&quot; | 任何字串 |

{style="table-layout:auto"}

**範例**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'factorization_machines_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Generalized Linear]回歸 {#generalized-linear-regression}

與線性回歸(假設結果遵循正態（高斯）分佈)不同，[!DNL Generalized Linear]模型(GLM)允許結果遵循不同型別的分佈，例如[!DNL Poisson]或二項式，具體取決於資料的性質。

**參數**

下表概述設定和最佳化[!DNL Generalized Linear]回歸效能的關鍵引數。

| 參數 | 說明 | 預設值 | 可能的值 |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------|
| `MAX_ITER` | 設定迭代次數上限（適用於使用求解器`irls`）。 | 25 | (>= 0) |
| `REG_PARAM` | 規則化引數。 | 未設定 | (>= 0) |
| `TOL` | 收斂公差。 | `1E-6` | (>= 0) |
| `AGGREGATION_DEPTH` | `treeAggregate`的建議深度。 | 2 | (>= 2) |
| `FAMILY` | 族引數，說明模型中使用的誤差分佈。 支援的選項為`gaussian`、`binomial`、`poisson`、`gamma`和`tweedie`。 | &quot;gaussian&quot; | `gaussian`，`binomial`，`poisson`，`gamma`，`tweedie` |
| `FIT_INTERCEPT` | 是否適合擷取詞語。 | `true` | `true`、`false` |
| `LINK` | 連結函式，定義線性預測值與分佈函式平均值之間的關係。 支援的選項為`identity`、`log`、`inverse`、`logit`、`probit`、`cloglog`和`sqrt`。 | 未設定 | `identity`，`log`，`inverse`，`logit`，`probit`，`cloglog`，`sqrt` |
| `LINK_POWER` | 此引數指定電源連結函式中的索引。 引數僅適用於[!DNL Tweedie]系列。 如果未設定，則預設為`1 - variancePower`，這與R `statmod`封裝一致。 0、1、-1和0.5的特定連結冪分別對應至Log、Identity、Inverse和Sqrt連結。 | 1 | 任何數值 |
| `SOLVER` | 用於最佳化的求解器演演算法。 支援的選項： `irls` （反複重新加權的最小平方）。 | &quot;irls&quot; | `irls` |
| `VARIANCE_POWER` | 此引數指定[!DNL Tweedie]分佈之變異函式中的冪，定義變異數和平均數之間的關係。 支援的值為0和`[1, inf)`。 方差冪0、1和2分別對應於Gaussian、Poisson和Gamma系列。 | 0.0 | 0， `[1, inf)` |
| `LINK_PREDICTION_COL` | 連結預測（線性預測值）欄名稱。 | 未設定 | 任何字串 |
| `OFFSET_COL` | 位移欄名稱。 如果未設定，則所有執行個體位移都會視為0.0。位移特徵的常數係數為1.0。 | 未設定 | 任何字串 |
| `WEIGHT_COL` | 權重欄名稱。 如果未設定或空白，則所有執行個體權重都會視為`1.0`。 在「二項式」系列中，權重會對應試算次數，而非整數的權重會在AIC計算中四捨五入。 | 未設定 | 任何字串 |

{style="table-layout:auto"}

**範例**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'generalized_linear_reg'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Gradient Boosted Tree]回歸 {#gradient-boosted-tree-regression}

漸層提升樹(GBT)是分類和回歸的有效方法，結合多個決策樹的預測，以改進預測精確度和模型效能。

**參數**

下表概述設定和最佳化[!DNL Gradient Boosted Tree]回歸效能的關鍵引數。

| 參數 | 說明 | 預設值 | 可能的值 |
|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | 用來將連續特徵分割成離散間隔的桶數上限，這有助於決定每個決策樹節點上的特徵分割方式。 更多的回收桶可提供更高的精細度。 | 32 | 任何分類功能中的類別數至少必須是2，並等於或大於。 |
| `CACHE_NODE_IDS` | 如果`false`，演演算法會將樹狀結構傳遞給執行程式，以比對執行個體與節點。 若為`true`，演演算法會快取每個執行個體的節點ID。 快取可以加速更深入的樹狀結構的訓練。 | `false` | `true`、`false` |
| `CHECKPOINT_INTERVAL` | 指定對快取節點ID進行查核點的頻率。 例如，`10`表示每10次反複檢查一次快取。 | 10 | (>= 1) |
| `MAX_DEPTH` | 樹狀結構的最大深度（非負值）。 例如，深度`0`表示1個分葉節點，深度`1`表示1個內部節點和2個分葉節點。 | 5 | (>= 0) |
| `MIN_INFO_GAIN` | 要在樹狀結構節點考慮的分割所需的最小資訊增益。 | 0.0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | 每個子系在分割後必須擁有的最小加權樣本計數。 如果分割導致任一子系中總重量的比例小於此值，則會捨棄此分割。 | 0.0 | (>= 0.0， &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | 分割後每個子系必須具有的最小例項數目。 如果分割產生的例項少於此值，則會捨棄分割。 | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | 配置給長條圖彙總的最大記憶體（以MB為單位）。 如果此值太小，每個疊代只會分割1個節點，而且其彙總可能會超過此大小。 | 256 | 任何正整數值 |
| `PREDICTION_COL` | 預測輸出的欄名稱。 | &quot;prediction&quot; | 任何字串 |
| `VALIDATION_INDICATOR_COL` | 指示每一列是用於訓練或驗證的欄名稱。 `false`用於訓練，`true`用於驗證。 | 未設定 | 任何字串 |
| `LEAF_COL` | 分葉索引的欄名稱。 每個樹狀結構中每個執行個體的預測葉索引，由預先排序周遊所產生。 | 「」 | 任何字串 |
| `FEATURE_SUBSET_STRATEGY` | 此引數指定每個樹節點要考慮的分割特徵數目。 | &quot;auto&quot; | `auto`、`all`、`onethird`、`sqrt`、`log2`或介於0到1.0之間的分數 |
| `SEED` | 隨機種子。 | 未設定 | 任何64位元數字 |
| `WEIGHT_COL` | 欄名稱，例如，權重。 如果未設定或空白，則所有執行個體權重都會視為`1.0`。 | 未設定 | 任何字串 |
| `LOSS_TYPE` | 此引數指定[!DNL Gradient Boosted Tree]模型最小化的損失函式。 | &quot;方形&quot; | `squared` (L2)和`absolute` (L1)。 注意：值不區分大小寫。 |
| `STEP_SIZE` | 範圍在`(0, 1]`中的步長大小（也稱為學習率），用來縮小每個估算器的貢獻。 | 0.1 | `(0, 1]` |
| `MAX_ITER` | 演演算法的最大迭代次數。 | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | 用於學習每個決策樹狀結構的訓練資料小數，範圍在`(0, 1]`。 | 1.0 | `(0, 1]` |

{style="table-layout:auto"}

**範例**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'gradient_boosted_tree_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Isotonic]回歸 {#isotonic-regression}

[!DNL Isotonic Regression]是一種演演算法，用來反複調整距離，同時保留資料中的相對不相同順序。

**參數**

下表概述設定和最佳化[!DNL Isotonic Regression]效能的關鍵引數。

| 參數 | 說明 | 預設值 | 可能的值 |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `ISOTONIC` | 指定在`true`時輸出序列是等調（增加），或是在`false`時反調（減少）。 | `true` | `true`、`false` |
| `WEIGHT_COL` | 欄名稱，例如，權重。 如果未設定或空白，則所有執行個體權重都會視為`1.0`。 | 未設定 | 任何字串 |
| `PREDICTION_COL` | 預測輸出的欄名稱。 | &quot;prediction&quot; | 任何字串 |
| `FEATURE_INDEX` | 功能的索引，適用於`featuresCol`為向量資料行時。 如果未設定，預設值為`0`。 否則，就沒有效用。 | 0 | 任何非負整數 |

{style="table-layout:auto"}

**範例**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'isotonic_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Linear]回歸 {#linear-regression}

[!DNL Linear Regression]是一種監督的機器學習演演算法，可將線性方程式配合到資料，以模擬相依變數和獨立特徵之間的關係。

**參數**

下表概述設定和最佳化[!DNL Linear Regression]效能的關鍵引數。

| 參數 | 說明 | 預設值 | 可能的值 |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `MAX_ITER` | 迭代次數上限。 | 100 | (>= 0) |
| `REGPARAM` | 用來控制模型複雜性的規則化引數。 | 0.0 | (>= 0) |
| `ELASTICNETPARAM` | ElasticNet混合引數，可控制L1 （套索）與L2 （脊線）之間的平衡。 0值會套用L2懲罰，1值會套用L1懲罰。 | 0.0 | (>= 0， &lt;= 1) |

{style="table-layout:auto"}

**範例**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'linear_reg'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Random Forest Regression] {#random-forest-regression}

[!DNL Random Forest Regression]是一種整體演演算法，可在訓練期間建立多個決策樹，並傳回這些決策樹用於回歸任務的平均預測，有助於防止過度擬合。

**參數**

下表概述設定和最佳化[!DNL Random Forest Regression]效能的關鍵引數。

| 參數 | 說明 | 預設值 | 可能的值 |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | 用來離散化連續特徵並決定特徵在每個節點的分割方式的最大值區數。 更多的回收桶可提供更高的精細度。 | 32 | 必須至少為2且至少等於任何分類功能中的類別數。 |
| `CACHE_NODE_IDS` | 如果`false`，演演算法會將樹狀結構傳遞給執行程式，以比對執行個體與節點。 如果是`true`，演演算法會快取每個執行個體的節點ID，以加速更深層的樹狀結構的訓練。 | `false` | `true`、`false` |
| `CHECKPOINT_INTERVAL` | 指定對快取節點ID進行查核點的頻率。 例如，`10`表示每10次反複檢查一次快取。 | 10 | (>= 1) |
| `IMPURITY` | 用於資訊增益計算的准則（不區分大小寫）。 | &quot;entropy&quot; | `entropy`、`gini` |
| `MAX_DEPTH` | 樹狀結構的最大深度（非負值）。 例如，深度`0`表示1個分葉節點，深度`1`表示1個內部節點和2個分葉節點。 | 5 | 任何非負整數 |
| `MIN_INFO_GAIN` | 要在樹狀結構節點考慮的分割所需的最小資訊增益。 | 0.0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | 每個子系在分割後必須擁有的最小加權樣本計數。 如果分割導致任一子系中總重量的比例小於此值，則會捨棄此分割。 | 0.0 | (>= 0.0， &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | 分割後每個子系必須具有的最小例項數目。 如果分割產生的例項少於此值，則會捨棄分割。 | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | 配置給長條圖彙總的最大記憶體（以MB為單位）。 如果此值太小，每個疊代只會分割1個節點，而且其彙總可能會超過此大小。 | 256 | (>= 1) |
| `BOOTSTRAP` | 建置樹狀結構時是否使用啟動程式範例。 | TRUE | `true`、`false` |
| `NUM_TREES` | 要訓練的樹狀結構數目（至少1）。 如果`1`，則不會使用任何啟動程式。 如果大於`1`，則套用啟動程式。 | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | 用來訓練每個決策樹狀結構的訓練資料部份，範圍在`(0, 1]`。 | 1.0 | (>= 0.0， &lt;= 1) |
| `LEAF_COL` | 葉索引的欄名稱，是每個樹狀結構中每個執行個體的預測葉索引，由預先排序周遊產生。 | 「」 | 任何字串 |
| `PREDICTION_COL` | 預測輸出的欄名稱。 | &quot;prediction&quot; | 任何字串 |
| `SEED` | 隨機種子。 | 未設定 | 任何64位元數字 |
| `WEIGHT_COL` | 欄名稱，例如，權重。 如果未設定或空白，則所有執行個體權重都會視為`1.0`。 | 未設定 | 任何有效的欄名稱或留空。 |

{style="table-layout:auto"}

**範例**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'random_forest_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Survival Regression] {#survival-regression}

[!DNL Survival Regression]是用來根據[!DNL Weibull distribution]調整引數存活回歸模型，稱為[!DNL Accelerated Failure Time] (AFT)模型。 它可以將執行個體棧疊到區塊中以提高效能。

**參數**

下表概述設定和最佳化[!DNL Survival Regression]效能的關鍵引數。

| 參數 | 說明 | 預設值 | 可能的值 |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `MAX_ITER` | 演演算法應執行的最大迭代次數。 | 100 | (>= 0) |
| `TOL` | 收斂公差。 | `1E-6` | (>= 0) |
| `AGGREGATION_DEPTH` | `treeAggregate`的建議深度。 如果特徵尺寸或分割區數量很大，則可將此引數設定為較大的值。 | 2 | (>= 2) |
| `FIT_INTERCEPT` | 是否適合擷取詞語。 | TRUE | `true`、`false` |
| `PREDICTION_COL` | 預測輸出的欄名稱。 | &quot;prediction&quot; | 任何字串 |
| `CENSOR_COL` | 用於審查的欄名稱。 值`1`表示事件已發生（未審查），而`0`表示事件已審查。 | &quot;censor&quot; | 0， 1 |
| `MAX_BLOCK_SIZE_IN_MB` | 將輸入資料棧疊成區塊的最大記憶體（以MB為單位）。 如果分割區中的剩餘資料大小較小，則會相應地調整此值。 `0`的值允許自動調整。 | 0.0 | (>= 0) |

{style="table-layout:auto"}

**範例**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'survival_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## 後續步驟

閱讀本檔案後，您現在瞭解如何設定和使用各種回歸演演算法。 接著，參閱[分類](./classification.md)和[叢集](./clustering.md)上的檔案，瞭解其他型別的進階統計模型。
