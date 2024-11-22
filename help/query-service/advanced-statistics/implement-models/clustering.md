---
title: 叢集演演算法
description: 瞭解如何使用關鍵引數、說明和範常式式碼來設定和最佳化各種叢集演演算法，協助您實作進階統計模型。
role: Developer
exl-id: 273853c6-85d2-43e5-b51a-aa9d20b313ae
source-git-commit: 69c08f688d355e689e78426dd4b0ed1f4934965c
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 4%

---

# 叢集演演算法 {#clustering-algorithms}

叢集演演算法會根據相似性，將資料點分組為不同的叢集，讓不受監督的學習能夠揭示資料中的模式。 若要建立叢集演演算法，請使用`OPTIONS`子句中的`type`引數，指定您要用於模型訓練的演演算法。 接著，將相關引數定義為鍵值配對，以微調模型。

>[!NOTE]
>
>請確定您瞭解所選演演算法的引數需求。 如果您選擇不自訂某些引數，系統會套用預設設定。 請參閱相關檔案，瞭解每個引數的函式和預設值。

## [!DNL K-Means] {#kmeans}

`K-Means`是一種叢集演演算法，可將資料點分割成預先定義的叢集數目(k)。 由於其簡單性和效率，這是最常用於叢集的演演算法之一。

**參數**

使用`K-Means`時，可在`OPTIONS`子句中設定下列引數：

| 參數 | 說明 | 預設值 | 可能的值 |
|---------------------|---------------------------------------------------------------------------------------------------------------|-----------------|----------------------------------|
| `MAX_ITER` | 演演算法應執行的迭代次數。 | `20` | (>= 0) |
| `TOL` | 收斂公差等級。 | `0.0001` | (>= 0) |
| `NUM_CLUSTERS` | 要建立的叢集數目(`k`)。 | `2` | (>1) |
| `DISTANCE_TYPE` | 用來計算兩點之間距離的演演算法。 值區分大小寫。 | `euclidean` | `euclidean`、`cosine` |
| `KMEANS_INIT_METHOD` | 叢集中心的初始化演演算法。 | `k-means\|\|` | `random`， `k-means\|\|` (平行版本的k-means++) |
| `INIT_STEPS` | `k-means\|\|`初始化模式的步驟數（僅適用於`KMEANS_INIT_METHOD`為`k-means\|\|`時）。 | `2` | (>0) |
| `PREDICTION_COL` | 將儲存預測的欄名稱。 | `prediction` | 任何字串 |
| `SEED` | 可重現性的隨機種子。 | `-1689246527` | 任何64位元數字 |
| `WEIGHT_COL` | 用於實體權重的欄名稱。 如果未設定，則所有例項都會平均加權。 | `not set` | 不適用 |

{style="table-layout:auto"}

**範例**

```sql
CREATE MODEL modelname 
OPTIONS(
  type = 'kmeans',
  MAX_ITERATIONS = 30,
  NUM_CLUSTERS = 4
) 
AS SELECT col1, col2, col3 FROM training-dataset;
```

## [!DNL Bisecting K-means] {#bisecting-kmeans}

[!DNL Bisecting K-means]是階層式叢集演演算法，使用分裂式（或「由上而下」）方法。 所有觀察從單一叢集開始，並在建立階層時遞回執行分割。 [!DNL Bisecting K-means]通常可以比一般的K-means更快，但它通常會產生不同的叢集結果。

**參數**

| 參數 | 說明 | 預設值 | 可能的值 |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MAX_ITER` | 演演算法執行的最大迭代次數。 | 20 | (>= 0) |
| `WEIGHT_COL` | 執行個體權重的欄名稱。 如果未設定或空白，則所有執行個體權重都會視為`1.0`。 | 未設定 | 任何字串 |
| `NUM_CLUSTERS` | 所需的葉叢集數目。 如果沒有可分割的叢集，實際數字可能會比較小。 | 4 | (> 1) |
| `SEED` | 用來控制演演算法中隨機程式的隨機種子。 | 未設定 | 任何64位元數字 |
| `DISTANCE_MEASURE` | 用來計算點之間相似度的距離測量。 | &quot;euclidean&quot; | `euclidean`、`cosine` |
| `MIN_DIVISIBLE_CLUSTER_SIZE` | 叢集可分割的最小點數（如果>= 1.0）或最小點比例（如果&lt; 1.0）。 | 1.0 | (>= 0) |
| `PREDICTION_COL` | 預測輸出的欄名稱。 | &quot;prediction&quot; | 任何字串 |

{style="table-layout:auto"}

**範例**

```sql
Create MODEL modelname OPTIONS(
  type = 'bisecting_kmeans',
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Gaussian Mixture Model] {#gaussian-mixture-model}

[!DNL Gaussian Mixture Model]代表複合分佈，其中資料點從k個高斯子分佈之一繪製，每個子分佈都有自己的機率。 它用來模型化假設是從數個高斯分佈的混合產生的資料集。

**參數**

| 參數 | 說明 | 預設值 | 可能的值 |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | 演演算法要執行的最大迭代次數。 | 100 | (>= 0) |
| `WEIGHT_COL` | 欄名稱，例如，權重。 如果未設定或空白，則所有執行個體權重都會視為`1.0`。 | 未設定 | 任何有效的欄名稱或空白 |
| `NUM_CLUSTERS` | 混合模型中獨立高斯分佈的數量。 | 2 | (> 1) |
| `SEED` | 用來控制演演算法中隨機程式的隨機種子。 | 未設定 | 任何64位元數字 |
| `AGGREGATION_DEPTH` | 此引數控制計算期間使用的彙總樹狀結構的深度。 | 2 | (>= 1) |
| `PROBABILITY_COL` | 預測類別條件概率的資料行名稱。 這些應被視為信賴分數，而非確切概率。 | &quot;probability&quot; | 任何字串 |
| `TOL` | 迭代演演算法的收斂公差。 | 0.01 | (>= 0) |
| `PREDICTION_COL` | 預測輸出的欄名稱。 | &quot;prediction&quot; | 任何字串 |

{style="table-layout:auto"}

**範例**

```sql
Create MODEL modelname OPTIONS(
  type = 'gaussian_mixture',
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Latent Dirichlet Allocation] (LDA) {#latent-dirichlet-allocation}

[!DNL Latent Dirichlet Allocation] (LDA)是一種機率模型，可從檔案集合中擷取基礎主題結構。 這是具有文字、主題和檔案層的三層階層Bayesian模型。 LDA會使用這些圖層以及觀察到的檔案來建置潛在的主題結構。

**參數**

| 參數 | 說明 | 預設值 | 可能的值 |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | 演演算法執行的最大迭代次數。 | 20 | (>= 0) |
| `OPTIMIZER` | 用於估計LDA模型的最佳化或推斷演演算法。 支援的選項為`"online"` （線上變數貝葉斯）和`"em"` （期望 — 最大化）。 | &quot;online&quot; | `online`， `em` （不區分大小寫） |
| `NUM_CLUSTERS` | 要建立的叢集數目(k)。 | 10 | (> 1) |
| `CHECKPOINT_INTERVAL` | 指定對快取節點ID進行查核點的頻率。 | 10 | (>= 1) |
| `DOC_CONCENTRATION` | 集中引數(「alpha」)決定有關跨檔案主題分佈的先前假設。 預設行為由最佳化處理程式決定。 對於`EM`最佳化程式，Alpha值應大於1.0 (預設：均勻分佈為(50/k) + 1)，確保對稱主題分佈。 對於`online`最佳化程式，Alpha值可以為0或更大（預設：均勻分佈為1.0/k），允許更靈活的主題初始化。 | 自動 | 長度k的任何單一值或向量，其中EM的值> 1 |
| `KEEP_LAST_CHECKPOINT` | 指示在使用`em`最佳化處理程式時是否保留最後一個查核點。 如果資料分割遺失，刪除檢查點可能會導致失敗。 當不再需要查核點時，就會根據參考計數自動將查核點從儲存空間中移除。 | `true` | `true`、`false` |
| `LEARNING_DECAY` | `online`最佳化程式的學習率，設定為介於`(0.5, 1.0]`之間的指數衰減率。 | 0.51 | `(0.5, 1.0]` |
| `LEARNING_OFFSET` | `online`最佳化程式的學習引數，可減低早期反複專案的權重，以降低早期反複專案的計數。 | 1024 | (> 0) |
| `SEED` | 控制演演算法中隨機處理程式的隨機種子。 | 未設定 | 任何64位元數字 |
| `OPTIMIZE_DOC_CONCENTRATION` | 針對`online`最佳化工具：是否在訓練期間最佳化`docConcentration` （檔案主題散發的Dirichlet引數）。 | `false` | `true`、`false` |
| `SUBSAMPLING_RATE` | 針對`online`最佳化程式：取樣並用於每個小型批次漸層下降反複專案中的語料片段，範圍為`(0, 1]`。 | 0.05 | `(0, 1]` |
| `TOPIC_CONCENTRATION` | 集中度引數（「beta」或「eta」）會定義在主題分佈上各字詞的先前假設。 預設值由最佳化處理程式決定：對於`EM`，值> 1.0 （預設= 0.1 + 1）。 對於`online`，值≥0 （預設值= 1.0/k）。 | 自動 | 長度k的任何單一值或向量，其中EM的值> 1 |
| `TOPIC_DISTRIBUTION_COL` | 此引數會輸出每個檔案的預估主題混合分佈，在文獻中通常稱為「theta」。 對於空白檔案，它會傳回零向量。 估計值是使用變分近似（「伽馬」）所衍生。 | 未設定 | 任何字串 |

{style="table-layout:auto"}

**範例**

```sql
Create MODEL modelname OPTIONS(
  type = 'lda',
) AS
  select col1, col2, col3 from training-dataset
```

## 後續步驟

閱讀本檔案後，您現在瞭解如何設定和使用各種叢集演演算法。 接著，參閱[分類](./classification.md)和[回歸](./regression.md)上的檔案，瞭解其他型別的進階統計模型。
