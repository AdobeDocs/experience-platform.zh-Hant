---
title: 分類演演算法
description: 瞭解如何使用關鍵引數、說明和範常式式碼來設定和最佳化各種分類演演算法，協助您實作進階統計模型。
role: Developer
exl-id: 9105ab04-b480-48a0-b8f7-cf0ed5e5399d
source-git-commit: 489063fcd003e20f233a9c9d85d8cb6c22708d88
workflow-type: tm+mt
source-wordcount: '2449'
ht-degree: 4%

---

# 分類演演算法 {#classification-algorithms}

本檔案提供各種分類演演算法的概觀，重點是它們的設定、關鍵引數，以及在進階統計模型中的實際使用。 分類演演算法可用來根據輸入功能將類別指派給資料點。 每個區段都包含引數說明和範常式式碼，協助您針對決策樹、隨機森林和樸素貝葉斯分類等工作實作和最佳化這些演演算法。

## [!DNL Decision Tree Classifier] {#decision-tree-classifier}

[!DNL Decision Tree Classifier]是一種監督學習方法，用於統計資料、資料採礦和機器學習。 在這個方法中，決策樹是用來作為分類任務的預測模型，從一組觀察結果中得出結論。

**參數**

下表概述設定及最佳化[!DNL Decision Tree Classifier]效能的關鍵引數。

| 參數 | 說明 | 預設值 | 可能的值 |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------|
| `MAX_BINS` | 最大回收桶數決定如何將連續特徵分割成離散間隔。 這會影響每個決策樹節點上的功能分割方式。 更多的回收桶可提供更高的精細度。 | 32 | 必須至少為2且至少等於任何分類功能中的類別數。 |
| `CACHE_NODE_IDS` | 如果`false`，演演算法會將樹狀結構傳遞給執行程式，以比對執行個體與節點。 如果是`true`，演演算法會快取每個執行個體的節點ID，以加速更深層的樹狀結構的訓練。 | `false` | `true`、`false` |
| `CHECKPOINT_INTERVAL` | 指定對快取節點ID進行查核點的頻率。 例如，`10`表示每10次反複檢查一次快取。 | 10 | (>= 1) |
| `IMPURITY` | 用於資訊增益計算的准則（不區分大小寫）。 | 「基尼」 | `entropy`、`gini` |
| `MAX_DEPTH` | 樹狀結構的最大深度（非負值）。 例如，深度`0`表示1個分葉節點，深度`1`表示1個內部節點和2個分葉節點。 | 5 | (>= 0) （範圍： [0,30]） |
| `MIN_INFO_GAIN` | 要在樹狀結構節點考慮的分割所需的最小資訊增益。 | 0.0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | 每個子系在分割後必須擁有的最小加權樣本計數。 如果分割導致任一子系中總重量的比例小於此值，則會捨棄此分割。 | 0.0 | (>= 0.0， &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | 分割後每個子系必須具有的最小例項數目。 如果分割產生的例項少於此值，則會捨棄分割。 | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | 配置給長條圖彙總的最大記憶體（以MB為單位）。 如果此值太小，每個疊代只會分割1個節點，而且其彙總可能會超過此大小。 | 256 | (>= 0) |
| `PREDICTION_COL` | 預測輸出的欄名稱。 | &quot;prediction&quot; | 任何字串 |
| `SEED` | 隨機種子。 | 不適用 | 任何64位元數字 |
| `WEIGHT_COL` | 欄名稱，例如，權重。 如果未設定或空白，則所有執行個體權重都會視為`1.0`。 | 未設定 | 任何字串 |
| `ONE_VS_REST` | 啟用或停用使用One-vs-Rest將此演演算法包裝起來，以用於多類別分類問題。 | `false` | `true`、`false` |

{style="table-layout:auto"}

**範例**

```sql
Create MODEL modelname OPTIONS(
  type = 'decision_tree_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Factorization Machine Classifier] {#factorization-machine-classifier}

[!DNL Factorization Machine Classifier]是支援一般漸層下降和AdamW求解器的分類演演算法。 分解機器分類模型使用Logistic損失，其可透過梯度下降進行最佳化，通常包括如L2等規則化辭彙，以防止過度擬合。

**參數**

下表概述設定和最佳化[!DNL Factorization Machine Classifier]效能的關鍵引數。

| 參數 | 說明 | 預設值 | 可能的值 |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------------------------------------|
| `TOL` | 收斂公差，控制最佳化的精確度。 | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | 因子的維度。 | 8 | (>= 0) |
| `FIT_INTERCEPT` | 指定是否配合擷取詞語。 | `true` | `true`、`false` |
| `FIT_LINEAR` | 指定是否要符合線性字詞（也稱為單向字詞）。 | `true` | `true`、`false` |
| `INIT_STD` | 初始化係數的標準差。 | 0.01 | (>= 0) |
| `MAX_ITER` | 演演算法要執行的最大迭代次數。 | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | 在訓練期間用於小型批次的資料比例。 必須在`(0, 1]`範圍內。 | 1.0 | 0 &lt;值&lt;= 1 |
| `REG_PARAM` | 規則化引數，可協助控制模型複雜度並防止過度擬合。 | 0.0 | (>= 0) |
| `SEED` | 控制演演算法中隨機處理程式的隨機種子。 | 不適用 | 任何64位元數字 |
| `SOLVER` | 用於最佳化的求解器演演算法。 支援的選項為`gd` （漸層下降）和`adamW`。 | &quot;adamW&quot; | `gd`、`adamW` |
| `STEP_SIZE` | 最佳化的初始步驟大小，通常解譯為學習率。 | 1.0 | > 0 |
| `PROBABILITY_COL` | 預測類別條件概率的資料行名稱。 注意：並非所有模型都會輸出經過良好校正的機率；這些機率應被視為信賴分數，而非確切的機率。 | &quot;probability&quot; | 任何字串 |
| `PREDICTION_COL` | 預測類別標籤的欄名稱。 | &quot;prediction&quot; | 任何字串 |
| `RAW_PREDICTION_COL` | 原始預測值的欄名稱（也稱為信賴度）。 | &quot;rawPrediction&quot; | 任何字串 |
| `ONE_VS_REST` | 指定是否啟用多重類別分類的One-vs-Rest。 | 假 | `true`、`false` |

{style="table-layout:auto"}

**範例**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'factorization_machines_classifier'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Gradient Boosted Tree Classifier] {#gradient-boosted-tree-classifier}

[!DNL Gradient Boosted Tree Classifier]使用決策樹集合來改善分類工作的正確性，結合多個樹狀結構來提升模型效能。

**參數**

下表概述設定和最佳化[!DNL Gradient Boosted Tree Classifier]效能的關鍵引數。

| 參數 | 說明 | 預設值 | 可能的值 |
|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | 最大回收桶數決定如何將連續特徵分割成離散間隔。 這會影響每個決策樹節點上的功能分割方式。 更多的回收桶可提供更高的精細度。 | 32 | 任何分類功能中的類別數至少必須是2，並等於或大於。 |
| `CACHE_NODE_IDS` | 如果`false`，演演算法會將樹狀結構傳遞給執行程式，以比對執行個體與節點。 如果是`true`，演演算法會快取每個執行個體的節點ID，以加速更深層的樹狀結構的訓練。 | `false` | `true`、`false` |
| `CHECKPOINT_INTERVAL` | 指定對快取節點ID進行查核點的頻率。 例如，`10`表示每10次反複檢查一次快取。 | 10 | (>= 1) |
| `MAX_DEPTH` | 樹狀結構的最大深度（非負值）。 例如，深度`0`表示1個分葉節點，深度`1`表示1個內部節點和2個分葉節點。 | 5 | (>= 0) |
| `MIN_INFO_GAIN` | 要在樹狀結構節點考慮的分割所需的最小資訊增益。 | 0.0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | 每個子系在分割後必須擁有的最小加權樣本計數。 如果分割導致任一子系中總重量的比例小於此值，則會捨棄此分割。 | 0.0 | (>= 0.0， &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | 分割後每個子系必須具有的最小例項數目。 如果分割產生的例項少於此值，則會捨棄分割。 | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | 配置給長條圖彙總的最大記憶體（以MB為單位）。 如果此值太小，每個疊代只會分割1個節點，而且其彙總可能會超過此大小。 | 256 | (>= 0) |
| `PREDICTION_COL` | 預測輸出的欄名稱。 | &quot;prediction&quot; | 任何字串 |
| `VALIDATION_INDICATOR_COL` | 欄名稱會指出每一列是否用於訓練或驗證。 值`false`表示訓練，而`true`表示驗證。 如果未設定值，預設值為`None`。 | &quot;無&quot; | 任何字串 |
| `RAW_PREDICTION_COL` | 原始預測值的欄名稱（也稱為信賴度）。 | &quot;rawPrediction&quot; | 任何字串 |
| `LEAF_COL` | 葉索引的欄名稱，是每個樹狀結構中每個執行個體的預測葉索引，由預先排序周遊產生。 | 「」 | 任何字串 |
| `FEATURE_SUBSET_STRATEGY` | 每個樹節點中要分割的特徵數目。 支援的選項： `auto` （根據工作自動決定）、`all` （使用所有功能）、`onethird` （使用三分之一的功能）、`sqrt` （使用功能數目的平方根）、`log2` （使用功能數目以2為底的對數）以及`n` (其中n是功能的一小部分（如果是在範圍`(0, 1]`），或是特定數目的功能（如果是在範圍`[1, total number of features]`）。 | &quot;auto&quot; | `auto`，`all`，`onethird`，`sqrt`，`log2`，`n` |
| `WEIGHT_COL` | 欄名稱，例如，權重。 如果未設定或空白，則所有執行個體權重都會視為`1.0`。 | 未設定 | 任何字串 |
| `LOSS_TYPE` | [!DNL Gradient Boosted Tree]模型嘗試最小化的損失函式。 | &quot;logistic&quot; | `logistic` （不區分大小寫） |
| `STEP_SIZE` | 範圍在`(0, 1]`中的步長大小（也稱為學習率），用來縮小每個估算器的貢獻。 | 0.1 | (>= 0.0， &lt;= 1) |
| `MAX_ITER` | 演演算法的最大迭代次數。 | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | 用於訓練每個決策樹的訓練資料比例。 值必須在0 &lt;值&lt;= 1的範圍內。 | 1.0 | `(0, 1]` |
| `PROBABILITY_COL` | 預測類別條件概率的資料行名稱。 注意：並非所有模型都會輸出經過良好校正的機率；這些機率應被視為信賴分數，而非確切的機率。 | &quot;probability&quot; | 任何字串 |
| `ONE_VS_REST` | 針對多類別分類，啟用或停用以One-vs-Rest包裝此演演算法。 | `false` | `true`、`false` |

{style="table-layout:auto"}

**範例**

```sql
Create MODEL modelname OPTIONS(
  type = 'gradient_boosted_tree_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Linear Support Vector Classifier] (LinearSVC) {#linear-support-vector-classifier}

[!DNL Linear Support Vector Classifier] (LinearSVC)會建構超平面，以分類高維度空間中的資料。 您可以使用它來最大化類別之間的利潤，以最小化分類錯誤。

**參數**

下表概述設定和最佳化[!DNL Linear Support Vector Classifier (LinearSVC)]效能的關鍵引數。

| 參數 | 說明 | 預設值 | 可能的值 |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_ITER` | 演演算法要執行的最大迭代次數。 | 100 | (>= 0) |
| `AGGREGATION_DEPTH` | 樹狀結構彙總的深度。 此引數是用來減少網路通訊的額外負荷。 | 2 | 任何正整數 |
| `FIT_INTERCEPT` | 是否適合擷取詞語。 | `true` | `true`、`false` |
| `TOL` | 此引數決定停止反複專案的臨界值。 | 1E-6 | (>= 0) |
| `MAX_BLOCK_SIZE_IN_MB` | 將輸入資料棧疊成區塊的最大記憶體（以MB為單位）。 如果引數設為`0`，則會自動選擇最佳值（通常約為1 MB）。 | 0.0 | (>= 0) |
| `REG_PARAM` | 規則化引數，可協助控制模型複雜度並防止過度擬合。 | 0.0 | (>= 0) |
| `STANDARDIZATION` | 此引數指示在配合模型之前是否標準化訓練特徵。 | `true` | `true`、`false` |
| `PREDICTION_COL` | 預測輸出的欄名稱。 | &quot;prediction&quot; | 任何字串 |
| `RAW_PREDICTION_COL` | 原始預測值的欄名稱（也稱為信賴度）。 | &quot;rawPrediction&quot; | 任何字串 |
| `ONE_VS_REST` | 針對多類別分類，啟用或停用以One-vs-Rest包裝此演演算法。 | `false` | `true`、`false` |

{style="table-layout:auto"}

**範例**

```sql
Create MODEL modelname OPTIONS(
  type = 'linear_svc_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Logistic Regression] {#logistic-regression}

[!DNL Logistic Regression]是用於二進位分類工作的監督演演算法。 它會使用Logistic函式來模擬執行個體屬於某個類別的機率，並將執行個體指派給機率較高的類別。 這使其適用於目標為將資料分離成兩個類別之一的問題。

**參數**

下表概述設定和最佳化[!DNL Logistic Regression]效能的關鍵引數。

| 參數 | 說明 | 預設值 | 可能的值 |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|----------------|
| `MAX_ITER` | 演演算法執行的最大迭代次數。 | 100 | (>= 0) |
| `REGPARAM` | 規則化引數可用來控制模型的複雜性。 | 0.0 | (>= 0) |
| `ELASTICNETPARAM` | `ElasticNet`混合引數可控制L1 （套索）與L2 （脊狀）懲罰之間的平衡。 值為0會套用L2懲罰（Ridge，會減少係數的大小），而值為1則會套用L1懲罰（Lasso，將某些係數設定為零，鼓勵稀疏性）。 | 0.0 | (>= 0， &lt;= 1) |

{style="table-layout:auto"}

**範例**

```sql
Create MODEL modelname OPTIONS(
  type = 'logistic_reg'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Multilayer Perceptron Classifier] {#multilayer-perceptron-classifier}

[!DNL Multilayer Perceptron Classifier] (MLPC)是前向人工神經網路分類器。 它由多個完全連線的節點層組成，每個節點會套用加權的線性輸入組合，接著會套用啟動函式。 MLPC適用於需要非線性決策界限的複雜分類工作。

**參數**

| 參數 | 說明 | 預設值 | 可能的值 |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | 演演算法要執行的最大迭代次數。 | 100 | (>= 0) |
| `BLOCK_SIZE` | 在分割區內以矩陣棧疊輸入資料的區塊大小。 如果區塊大小超過分割區中的剩餘資料，則會據此調整。 | 128 | (>= 0) |
| `STEP_SIZE` | 用於每個最佳化反複運算的步驟大小（僅適用於求解器`gd`）。 | 0.03 | (> 0) |
| `TOL` | 最佳化的收斂公差。 | `1E-6` | (>= 0) |
| `PREDICTION_COL` | 預測輸出的欄名稱。 | &quot;prediction&quot; | 任何字串 |
| `SEED` | 控制演演算法中隨機處理程式的隨機種子。 | 未設定 | 任何64位元數字 |
| `PROBABILITY_COL` | 預測類別條件概率的資料行名稱。 這些應被視為信賴分數，而非確切概率。 | &quot;probability&quot; | 任何字串 |
| `RAW_PREDICTION_COL` | 原始預測值的欄名稱（也稱為信賴度）。 | &quot;rawPrediction&quot; | 任何字串 |
| `ONE_VS_REST` | 針對多類別分類，啟用或停用以One-vs-Rest包裝此演演算法。 | `false` | `true`、`false` |

{style="table-layout:auto"}

**範例**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'multilayer_perceptron_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Naive Bayes Classifier] {#naive-bayes-classifier}

[!DNL Naive Bayes Classifier]是一個簡單的機率、多類別分類器，它以貝葉斯定理為基礎，特徵之間具有強（天真）獨立性假設。 它透過在訓練資料的單次傳遞中計算條件機率來有效地訓練，以計算給定每個標籤的每個特徵的條件機率分佈。 對於預測，它使用Bayes定理來計算每個已觀察標籤的條件機率分佈。

**參數**

| 參數 | 說明 | 預設值 | 可能的值 |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MODEL_TYPE` | 指定模型型別。 支援的選項為`"multinomial"`、`"complement"`、`"bernoulli"`和`"gaussian"`。 模型型別區分大小寫。 | &quot;多項式&quot; | `"multinomial"`、`"complement"`、`"bernoulli"`、`"gaussian"` |
| `SMOOTHING` | 平滑引數是用來處理分類資料中的零頻率問題。 | 1.0 | (>= 0) |
| `PROBABILITY_COL` | 此引數指定預測類別條件概率的資料行名稱。 注意：並非所有模型都提供精確校準的機率預估；請將這些值視為機密而非精確機率。 | &quot;probability&quot; | 任何字串 |
| `WEIGHT_COL` | 執行個體權重的欄名稱。 如果未設定或空白，則所有執行個體權重都會視為`1.0`。 | 未設定 | 任何字串 |
| `PREDICTION_COL` | 預測輸出的欄名稱。 | &quot;prediction&quot; | 任何字串 |
| `RAW_PREDICTION_COL` | 原始預測值的欄名稱（也稱為信賴度）。 | &quot;rawPrediction&quot; | 任何字串 |
| `ONE_VS_REST` | 指定是否啟用多重類別分類的One-vs-Rest。 | `false` | `true`、`false` |

{style="table-layout:auto"}

**範例**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'naive_bayes_classifier'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Random Forest Classifier] {#random-forest-classifier}

[!DNL Random Forest Classifier]是一種整體學習演演算法，可在訓練期間建立多個決策樹。 它透過平均預測並選取大多數樹狀結構為分類任務選擇的類別來緩解過度擬合。

**參數**

| 參數 | 說明 | 預設值 | 可能的值 |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | 最大回收桶數決定如何將連續特徵分割成離散間隔。 這會影響每個決策樹節點上的功能分割方式。 更多的回收桶可提供更高的精細度。 | 32 | 任何分類功能中的類別數至少必須是2，並等於或大於。 |
| `CACHE_NODE_IDS` | 如果`false`，演演算法會將樹狀結構傳遞給執行程式，以比對執行個體與節點。 如果為`true`，演演算法會快取每個執行個體的節點ID，以加速訓練。 | `false` | `true`、`false` |
| `CHECKPOINT_INTERVAL` | 指定對快取節點ID進行查核點的頻率。 例如，`10`表示每10次反複檢查一次快取。 | 10 | (>= 1) |
| `IMPURITY` | 用於資訊增益計算的准則（不區分大小寫）。 | 「基尼」 | `entropy`、`gini` |
| `MAX_DEPTH` | 樹狀結構的最大深度（非負值）。 例如，深度`0`表示1個分葉節點，深度`1`表示1個內部節點和2個分葉節點。 | 5 | (>= 0) |
| `MIN_INFO_GAIN` | 要在樹狀結構節點考慮的分割所需的最小資訊增益。 | 0.0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | 每個子系在分割後必須擁有的最小加權樣本計數。 如果分割導致任一子系中總重量的比例小於此值，則會捨棄此分割。 | 0.0 | (>= 0.0， &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | 分割後每個子系必須具有的最小例項數目。 如果分割產生的例項少於此值，則會捨棄分割。 | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | 配置給長條圖彙總的最大記憶體（以MB為單位）。 如果此值太小，每個疊代只會分割1個節點，而且其彙總可能會超過此大小。 | 256 | (>= 1) |
| `PREDICTION_COL` | 預測輸出的欄名稱。 | &quot;prediction&quot; | 任何字串 |
| `WEIGHT_COL` | 欄名稱，例如，權重。 如果未設定或空白，則所有執行個體權重都會視為`1.0`。 | 未設定 | 任何有效的欄名稱或空白 |
| `SEED` | 用來控制演演算法中隨機程式的隨機種子。 | -1689246527 | 任何64位元數字 |
| `BOOTSTRAP` | 建置樹狀結構時是否使用啟動程式範例。 | `true` | `true`、`false` |
| `NUM_TREES` | 要訓練的樹狀結構數目。 若為`1`，則不會使用任何啟動裝載。 如果大於`1`，則套用啟動程式。 | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | 用於學習每個決策樹的訓練資料部份。 | 1.0 | (> 0， &lt;= 1) |
| `LEAF_COL` | 分葉索引的欄名稱，包含每個樹狀結構中每個執行處理的預測分葉索引（依預排序）。 | 「」 | 任何字串 |
| `PROBABILITY_COL` | 預測類別條件概率的資料行名稱。 這些應被視為信賴分數，而非確切概率。 | 未設定 | 任何字串 |
| `RAW_PREDICTION_COL` | 原始預測值的欄名稱（也稱為信賴度）。 | &quot;rawPrediction&quot; | 任何字串 |
| `ONE_VS_REST` | 指定是否啟用多重類別分類的One-vs-Rest。 | `false` | `true`、`false` |

{style="table-layout:auto"}

**範例**

```sql
Create MODEL modelname OPTIONS(
  type = 'random_forest_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## 後續步驟

閱讀本檔案後，您現在瞭解如何設定和使用各種分類演演算法。 接著，參閱[回歸](./regression.md)與[叢集](./clustering.md)上的檔案，瞭解其他型別的進階統計模型。
