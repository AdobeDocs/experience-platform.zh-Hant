---
title: 特徵轉換技術
description: 瞭解資料轉換、編碼和功能縮放等重要的預先處理技術，這些技術可為統計模型訓練準備資料。 它涵蓋處理遺失值和轉換分類資料以改善模型效能和正確性的重要性。
role: Developer
exl-id: ed7fa9b7-f74e-481b-afba-8690ce50c777
source-git-commit: e7bc30c153f67c59e9c04e8c8df60394f48871d0
workflow-type: tm+mt
source-wordcount: '3450'
ht-degree: 8%

---

# 特徵轉換技術

轉換是重要的預先處理步驟，可將資料轉換或調整為適合模型訓練與分析的格式，以確保最佳效能和準確性。 本檔案可用作補充語法資源，針對資料預先處理提供有關關鍵功能轉換技術的深入詳細資訊。

機器學習模型無法直接處理字串值或null值，因此必須預先處理資料。 本指南說明如何使用各種轉換來估算遺失的值、將分類資料轉換為數字格式，以及套用功能縮放技術，例如one-hot編碼和向量化。 這些方法可讓模型有效解讀資料並從中學習，最終提升其效能。

## 自動特徵轉換 {#automatic-transformations}

如果您選擇略過`CREATE MODEL`命令中的`TRANSFORM`子句，功能轉換會自動發生。 自動資料前置處理包括Null取代和標準特徵轉換（根據資料型別）。 會自動輸入數值和文字欄，然後進行特徵轉換，以確保資料採用適合機器學習模型訓練的格式。 此程式包括遺失資料推算及分類、數值和布林值轉換。

>[!IMPORTANT]
>
>在訓練時使用的特徵轉換也會在預測和評估時用於特徵轉換。

下表說明在`CREATE MODEL`命令期間省略`TRANSFORM`子句時，如何處理不同的資料型別。

### Null取代 {#automatic-null-replacement}

| 資料類型 | Null取代 |
|-----------------|-----------------------------------------------------|
| 數值 | 空值會取代為欄的平均值。 |
| 類別 | 以`ml_unknown`關鍵字取代Null。 |
| 布林值 | 以`FALSE`值取代Null。 |
| 時間戳記 | 這應為連續欄位。 |
| 巢狀/結構 | 取代取決於分葉節點的資料型別。 |

### 特徵轉換 {#automatic-feature-transformation}

| 資料類型 | 特徵轉換 |
|-----------------|-----------------------------------------------------|
| 數值 | 非必要 — 因為機器學習演演算法可瞭解此資料型別。 |
| 字串 | 發生字串索引。 |
| 布林值 | 發生字串索引。 |
| 時間戳記 | 沒有發生作業。 |
| 結構 | 值會展開至其葉節點。 轉換會根據分葉節點的資料型別進行。 |

**範例**

```sql
CREATE model modelname options(model_type='logistic_reg', label='rating') AS SELECT * FROM movie_rating;
```

## 手動特徵轉換 {#manual-transformations}

若要在您的`CREATE MODEL`陳述式中定義自訂資料前置處理，請將`TRANSFORM`子句與任何數目的可用轉換函式結合使用。 這些手動前置處理函式也可以在`TRANSFORM`子句之外使用。 在](#available-transformations)下方的[轉換器區段中討論的所有轉換，都可以用來手動預先處理資料。

### 主要特性 {#key-characteristics}

下列是定義前置處理函式時要考慮的特徵轉換主要特性：

- **語法**： `TRANSFORM(functionName(colName, parameters) <aliasNAME>)`
   - 在語法中，別名是強制的。 您必須提供別名，否則查詢將會失敗。

- **引數**：引數是位置引數。 也就是說，如果有自訂值，每個引數只能取用某些值，且需要指定所有先前的引數。 請參閱相關檔案，以取得關於哪個函式接受哪個引數的詳細資訊。

- **鏈結轉換器**：一個轉換器的輸出可以成為另一個轉換器的輸入。

- **功能使用狀況**：上次的功能轉換已作為機器學習模型的功能使用。

**範例**

```sql
CREATE MODEL modelname 
TRANSFORM(
  string_imputer(language, 'adding_null') AS imp_language, 
  numeric_imputer(users_count, 'mode') AS imp_users_count, 
  string_indexer(imp_language) AS si_lang,  
  vector_assembler(array(imp_users_count, si_lang, watch_minutes)) AS features
)  
OPTIONS(MODEL_TYPE='logistic_reg', LABEL='rating') 
AS SELECT * FROM df;
```

## 可用的轉換 {#available-transformations}

有19種可用的轉換。 這些轉換分為[一般轉換](#general-transformations)、[數值轉換](#numeric-transformations)、[分類轉換](#categorical-transformations)和[文字轉換](#textual-transformations)。

### 一般轉換 {#general-transformations}

請閱讀本節，瞭解用於各種資料型別的轉換器的詳細資訊。 如果您需要套用非特定於分類或文字資料的轉換，此資訊至關重要。

>[!NOTE]
>
>輸入資料型別是指套用推算的欄。 輸出資料型別是指轉換生效後作為輸出產生的欄。

#### 數值輸入器 {#numeric-imputer}

**數值輸入器**&#x200B;轉換器完成資料集中遺漏的值。 這會使用遺失值所在欄的平均值、中間值或模式。 輸入資料行應為`DoubleType`或`FloatType`。 如需詳細資訊和範例，請參閱[Spark演演算法檔案](https://spark.apache.org/docs/2.2.0/ml-features.html#imputer)。

>[!NOTE]
>
>所有輸入資料行中的null值都會被視為遺失，因此也會被推算。

**資料類型**

- 輸入資料型別：數值
- 輸出資料型別：數值

**定義**

```sql
transformer(numeric_imputer(hour, 'mean') hour_imputed)
```

**參數**

| 參數 | 說明 | 類型 | 預設 | 選填 |
| -------- | ------------ | ----- | -------- | -------- |
| `STRATEGY` | 推算策略。 可用的值為： [`mean`、`median`、`mode`]。 | 字串 | 平均值 | 可選 |

{style="table-layout:auto"}

**在推算前的範例**

| ID | 小時 |
|---|---|
| 0 | 18.0 |
| 1 | Null |
| 2 | 8.0 |

**在推算之後的範例（使用平均策略）**

| ID | 小時 |
|---|---|
| 0 | 18.0 |
| 1 | 13.0 |
| 2 | 8.0 |

#### 字串輸入器 {#string-imputer}

**字串輸入器**&#x200B;轉換器會使用使用者提供的字串做為函式引數來完成資料集中的遺漏值。 輸入和輸出資料行應為`string`資料型別。

>[!NOTE]
>
>所有輸入資料行中的null值都會視為遺失，並由指定的字串取代。

**資料類型**

- 輸入資料型別：字串
- 輸出資料型別：字串

**定義**

```sql
transform(string_imputer(name, 'unknown_name') as name_imputed)
```

**參數**

| 參數 | 說明 | 類型 | 預設 | 選填 |
| -------- | ------------ | ----- | -------- | -------- |
| `NULL_REPLACEMENT` | 取代null的值。 | 字串 | ml_unknown | 可選 |

{style="table-layout:auto"}

**在推算前的範例**

| ID | 名稱 |
|---|---|
| 0 | John |
| 1 | Null |
| 2 | Alice |

**在推算後的範例（使用&#39;ml_unknown&#39;做為取代）**

| ID | 名稱 |
|---|---|
| 0 | John |
| 1 | ml_unknown |
| 2 | Alice |

#### 布林值輸入器 {#boolean-imputer}

**布林值輸入器**&#x200B;轉換器完成布林值資料行資料集中遺漏的值。 輸入和輸出資料行應該是`Boolean`型別。

>[!NOTE]
>
>所有輸入資料行中的null值都會視為遺失，並由指定的布林值取代。

**資料類型**

- 輸入資料型別：布林值
- 輸出資料型別：布林值

**定義**

```sql
transform(boolean_imputer(name, true) as name_imputed)
```

**參數**

| 參數 | 說明 | 類型 | 預設 | 選填 |
| -------- | ------------ | ----- | -------- | -------- |
| `NULL_REPLACEMENT` | 布林值輸入器。 允許的值： [`true`， `false`]。 | 布林值 | false | 可選 |

**在推算前的範例**

| ID | 標幟 |
|---|---|
| 0 | true |
| 1 | Null |
| 2 | false |

**在推算後的範例（使用&#39;true&#39;做為取代）**

| ID | 標幟 |
|---|---|
| 0 | true |
| 1 | true |
| 2 | false |

#### 向量組合器 {#vector-assembler}

`VectorAssembler`轉換器將指定的輸入欄清單結合為單一向量欄，讓您更輕鬆地管理機器學習模型中的多個功能。 這對於將原始特徵和由不同特徵轉換器產生的特徵合併到一個統一特徵向量特別有用。 `VectorAssembler`接受數值、布林值和向量型別的輸入資料行。 在每個列中，輸入欄的值會以指定順序串連到向量中。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#vectorassembler) -->

**資料類型**

- 輸入資料型別： `array[string]` （具有數值/陣列[數值]值的資料行名稱）
- 輸出資料型別： `Vector[double]`

**定義**

```sql
transform(vector_assembler(id, hour, mobile, userFeatures) as features)
```

**參數**

| 參數 | 說明 | 類型 | 預設 | 選填 |
| -------- | ------------ | ----- | -------- | -------- |
| 不適用 | 此轉換器不需要其他引數。 | 不適用 | 不適用 | 不適用 |

{style="table-layout:auto"}

**轉換前的範例**

| ID | 小時 | 行動 | userFeatures | 已點按 |
|---|-------|--------|------------------|---------|
| 0 | 18 | 1.0 | [0.0， 10.0， 0.5] | 1.0 |

{style="table-layout:auto"}

轉換後的&#x200B;**範例**

| ID | 小時 | 行動 | userFeatures | 已點按 | 功能 |
|---|------|--------|------------------|---------|-------------------------------|
| 0 | 18 | 1.0 | [0.0， 10.0， 0.5] | 1.0 | [18.0， 1.0， 0.0， 10.0， 0.5] |

{style="table-layout:auto"}

### 數值轉換 {#numeric-transformations}

請閱讀本小節，瞭解用於處理和縮放數值資料的可用轉換器。 這些轉換器是處理及最佳化資料集中的數值功能所必需的。

#### 二進位器 {#binarizer}

`Binarizer`轉換器會透過稱為二進位的程式將數值特徵轉換為二進位(0/1)特徵。 大於指定臨界值的特徵值會轉換為1.0，而等於或小於臨界值的值會轉換為0.0。`Binarizer`同時支援輸入資料行的`Vector`和`Double`型別。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#binarizer). -->

**資料類型**

- 輸入資料型別：數值欄
- 輸出資料型別：數值

**定義**

```sql
transform(numeric_imputer(rating, 'mode') rating_imp, binarizer(rating_imp) rating_binarizer)
```

**參數**

| 參數 | 說明 | 類型 | 預設 | 選填 |
|------------|----------------------------------------------------------------------------------------------------------|----------|----------|----------|
| `THRESHOLD` | 用來二進位化連續特徵的臨界值引數。 大於臨界值的功能會二進位為1.0，而等於或小於臨界值的功能會二進位為0.0。 | int/double | 0.0 | 可選 |

{style="table-layout:auto"}

**二進位前的輸入範例**

| ID | 評等 |
|---|---------|
| 0 | -18.0 |
| 1 | 13.0 |
| 2 | 8.0 |

**二進位後的輸出範例（預設臨界值為0.0）**

| ID | 評等 |
|---|---------|
| 0 | 0.0 |
| 1 | 1.0 |
| 2 | 1.0 |

**具有自訂臨界值的定義**

```sql
transform(numeric_imputer(age, 'mode') age_imp, binarizer(age_imp, 14.0) age_binarizer)
```

**二進位後的輸出範例（臨界值為14.0）**

| ID | 年齡 |
|---|-------|
| 0 | 0.0 |
| 1 | 0.0 |
| 2 | 1.0 |

#### 分段 {#bucketizer}

`Bucketizer`轉換器會根據使用者指定的臨界值，將連續功能欄轉換為功能值區欄。 此程式對於將連續資料分割成個別回收桶或貯體非常有用。 `Bucketizer`需要`splits`引數，這個引數定義值區的邊界。

**資料類型**

- 輸入資料型別：數值欄
- 輸出資料型別：數值（繫結值）

**定義**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

**參數**

| 參數 | 說明 | 類型 | 預設 | 選填 |
|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|----------|----------|
| `splits` | 用於將連續特徵對映到貯體的引數。 有`n+1`個分割，有`n`個貯體。 分割順序必須嚴格遞增，每個值區都會使用範圍(x，y)，最後一個值區除外，也就是y。 | 陣列（雙倍） | 不適用 | 可選 |

{style="table-layout:auto"}

**分割範例**

- 陣列(Double.NegativeInfinity， 0.0， 1.0， Double.PositiveInfinity)
- 陣列(0.0、1.0、2.0)

分割應該涵蓋整個Double值範圍；否則，指定分割之外的值將被視為錯誤。

**轉換範例**

此範例取一欄連續功能(`course_duration`)，根據提供的`splits`將其量化，然後將產生的貯體與其他功能組合。

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MinmaxScaler {#minmaxscaler}

`MinMaxScaler`轉換器會將向量列資料集中的每個功能重新調整為指定的範圍，通常是[0、1]。 這可確保所有特徵對模型的貢獻都是相同的。 這對於對特徵縮放敏感的模型特別有用，例如以漸層下降為基礎的演演算法。 `MinMaxScaler`對下列引數執行操作：

- **分鐘**：轉換的下限，由所有功能共用。 預設值為`0.0`。
- **max**：轉換的上限，由所有功能共用。 預設值為`1.0`。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#minmaxscaler).  -->

**資料類型**

- 輸入資料型別： `Array[Double]`
- 輸出資料型別： `Array[Double]`

**定義**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

**參數**

| 參數 | 說明 | 類型 | 預設 | 選填 |
|-----------|--------------------------------------------------------------------------------------------------|------|---------|----------|
| `min` | 轉換後的下限，由所有特徵共用。 | 雙精度浮點數 | 0.0 | 可選 |
| `max` | 轉換後的上限，由所有特徵共用。 | 雙精度浮點數 | 1.0 | 可選 |

**轉換範例**

此範例會轉換一組特徵，在套用其他幾個轉換之後，使用MinMaxScaler將它們重新縮放到指定的範圍。

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MaxAbsScaler {#maxabsscaler}

`MaxAbsScaler`轉換器會將向量列資料集中的每個功能重新調整為範圍[-1， 1]，方法是除以每個功能的最大絕對值。 此轉換非常適合用於保留同時具有正值和負值的資料集中的稀疏性，因為它不會移動或置中資料。 這讓`MaxAbsScaler`特別適合對輸入特徵比例敏感的模型，例如涉及距離計算的模型。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#maxabsscaler). -->

**資料類型**

- 輸入資料型別： `Array[Double]`
- 輸出資料型別： `Array[Double]`

**定義**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling)
```

**參數**

| 參數 | 說明 | 類型 | 預設 | 選填 |
|-----------|---------------------------------------------------------------------------------------------------------|------|---------|----------|
| 不適用 | MaxAbsScaler不需要任何額外的引數來進行操作。 | 不適用 | 不適用 | 不適用 |

**轉換範例**

此範例套用數個轉換（包括`MaxAbsScaler`），將功能重新縮放至範圍[-1、1]。

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling)
```

#### 標準化程式 {#normalizer}

`Normalizer`是轉換器，可將向量列資料集中的每個向量標準化，以具有單位標準。 此程式可確保一致的縮放而不改變向量的方向。 在依賴距離測量或其他向量式計算的機器學習模型中，這種轉換特別有用，尤其是在向量量值差別很大的情況下。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#normalizer) -->

**資料類型**

- 輸入資料型別： `array[double]` / `vector[double]`
- 輸出資料型別： `vector[double]`

**定義**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, normalizer(vec_assembler, 3) as normalized)
```

**參數**

| 參數 | 說明 | 類型 | 預設 | 選填 |
|-----------|----------------------------------------------------------------------------------------|---------|---------|----------|
| `p` | 指定用於正規化的`p-norm` （例如，`1-norm`、`2-norm`等）。 | 整數 | 2 | 可選 |

**轉換範例**

此範例示範如何套用數個轉換（包括`Normalizer`），以使用指定的`p-norm`標準化一組功能。

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, normalizer(vec_assembler, 3) as normalized)
```

#### QuantileDiscretizer {#quantilediscretizer}

`QuantileDiscretizer`是將具有連續功能的資料行轉換為繫結分類功能的轉換器，其值由`numBuckets`引數決定。 在某些情況下，如果相異值太少，無法建立足夠的數量，則實際值數可能會小於該指定數字。

此轉換對於簡化連續資料的表示或準備更適合用於分類輸入的演演算法特別有用。

**資料類型**

- 輸入資料型別：數值欄
- 輸出資料型別：數值欄（類別）

**定義**

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**參數**

| 參數 | 說明 | 類型 | 預設 | 選填 |
|--------------|--------------------------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `NUM_BUCKETS` | 資料點分組的貯體數量（數量單位或類別）。 此數字必須大於或等於2。 | 整數 | 2 | 可選 |

**轉換範例**

此範例示範`QuantileDiscretizer`如何將一欄連續功能(`hour`)整合到三個分類值區。

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**離散化前後範例**

| ID | 小時 | 結果 |
|---|------|--------|
| 0 | 18.0 | 2.0 |
| 1 | 19.0 | 2.0 |
| 2 | 8.0 | 1.0 |
| 3 | 5.0 | 1.0 |
| 4 | 2.2 | 0.0 |

#### StandardScale {#standardscaler}

`StandardScaler`是一種轉換器，可將向量列資料集中的每個功能標準化，以具有單位標準差和/或平均數零。 此程式可讓資料更適合用於假設特徵以一致的比例置中於零周圍的演演算法。 此轉換對於SVM、Logistic回歸和神經網路等機器學習模型尤其重要，在這些模型中，未標準化的資料可能會導致收斂問題或降低準確性。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#standardscaler).  -->

**資料類型**

- 輸入資料型別：向量
- 輸出資料型別： Vector

**定義**

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

**參數**

| 參數 | 說明 | 類型 | 預設 | 選填 |
|------------|------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `withStd` | 縮放資料以取得單位標準差。 | 布林值 | True | 可選 |
| `withMean` | 在縮放之前，以平均值將資料置中。 此選項會產生密集輸出，因此請謹慎使用稀疏輸入。 | 布林值 | False | 可選 |

**轉換範例**

此範例示範如何將StandardScaler套用至一組特徵，並以單位標準差和零平均值標準化它們。

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

### 類別轉換 {#categorical-transformations}

請參閱本節，概略瞭解可用於轉換及預先處理機器學習模型分類資料的轉換器。 這些轉換是針對代表不同類別或標籤的資料點而設計，而非數值。

#### StringIndexer {#stringindexer}

`StringIndexer`是將標籤的字串資料行編碼為數值索引資料行的轉換器。 索引範圍從0到`numLabels`，並依標籤頻率排序（最常見的標籤會收到0的索引）。 如果輸入欄是數字，則會先將其轉換為字串，然後再編制索引。 如果使用者指定，則可將未見的標籤指派給索引`numLabels`。

此轉換對於將分類字串資料轉換為數字形式特別有用，因此適用於需要數值輸入的機器學習模型。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stringindexer) -->

**資料類型**

- 輸入資料型別：字串
- 輸出資料型別：數值

**定義**

```sql
TRANSFORM(string_indexer(category) as si_category)
```

**參數**

| 參數 | 說明 | 類型 | 預設 | 選填 |
|-----------|-------------|------|---------|----------|
| 不適用 | `StringIndexer`不需要任何額外的引數才能執行作業。 | 不適用 | 不適用 | 不適用 |

**轉換範例**

此範例示範如何將`StringIndexer`套用至分類功能，並將其轉換為數值索引。

```sql
TRANSFORM(string_indexer(category) as si_category)
```

#### OneHotEncoder {#onehotencoder}

`OneHotEncoder`是將標籤索引資料行轉換為稀疏二進位向量資料行的轉換器，每個向量最多只有一個單一值。 這種編碼方式對於允許需要數值輸入的演演算法（例如Logistic回歸）有效地合併分類資料特別有用。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#onehotencoder).  -->

**資料類型**

- 輸入資料型別：數值
- 輸出資料型別： Vector[Int]

**定義**

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

**參數**

| 參數 | 說明 | 類型 | 預設 | 選填 |
|-----------|-------------|------|---------|----------|
| 不適用 | OneHotEncoder不需要任何額外的引數即可執行作業。 | 不適用 | 不適用 | 不適用 |

**轉換範例**

此範例示範如何先將`StringIndexer`套用至分類功能，然後使用`OneHotEncoder`將索引值轉換為二進位向量。

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

### 文字轉換 {#textual-transformations}

本節提供可用於處理和轉換文字資料為機器學習模型所用格式的轉換器的詳細資訊。 本節對於使用自然語言資料和文字分析的開發人員而言至關重要。

#### CountVectorizer {#countvectorizer}

`CountVectorizer`是一種轉換器，可將文字檔案的集合轉換為權杖計數的向量，根據從語料庫擷取的辭彙產生稀疏表示。 若要將文字資料轉換為機器學習演演算法(例如LDA (Latent Dirichlet Allocation))可使用的數值格式，這項轉換至關重要，因為它可代表每個檔案中權杖的頻率。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#countvectorizer). -->

**資料類型**

- 輸入資料型別： Array[String]
- 輸出資料型別：密集向量

**定義**

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**參數**

| 參數 | 說明 | 類型 | 預設 | 選填 |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|---------|----------|
| `VOCAB_SIZE` | 辭彙的最大尺寸。 CountVectorizer建置的辭彙只考慮在語料庫中按照辭彙頻率排序的前`vocabSize`個辭彙。 | 整數 | 218 | 可選 |
| `MIN_DOC_FREQ` | 指定某個辭彙必須出現在中才能包含在辭彙表內的不同檔案數目下限。 可以是絕對數字或檔案的分數（若為雙精度型）。 | 雙精度 | 1.0 | 可選 |
| `MAX_DOC_FREQ` | 指定字詞可出現在辭彙中的不同檔案數目上限。 可以是絕對數字或檔案的分數（若為雙精度型）。 | 雙精度 | (263)-1 | 可選 |
| `MIN_TERM_FREQ` | 篩選掉檔案中罕見的字詞。 頻率/計數小於給定臨界值的字詞會被忽略。 可以是絕對數字或檔案權杖計數的分數。 | 雙精度 | 1.0 | 可選 |

{style="table-layout:auto"}

**轉換範例**

此範例示範CountVectorizer如何將文字陣列集合轉換為權杖計數的向量，以產生稀疏表示。

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**向量化之前和之後的範例**

| ID | 文字 | cv_output |
|----|---------------------------------|-----------------------------------|
| 0 | 陣列(「a」、「b」、「c」) | (3，[0,1，2]，[1.0,1.0,1.0]) |
| 1 | 陣列(「a」、「b」、「b」、「c」、「a」) | (3，[0,1，2]，[2.0,2.0,1.0]) |

{style="table-layout:auto"}

#### NGram {#ngram}

`NGram`是產生n元格序列的轉換器，其中n元格是某些整數(`𝑛`)的(&#39;??&#39;)權杖序列（通常是字）。 輸出由以空格分隔的「??」連續字串組成，可用作機器學習模型（尤其是專注於自然語言處理的模型）中的功能。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#n-gram). -->

**資料類型**

- 輸入資料型別： Array[String]
- 輸出資料型別： Array[String]

**定義**

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**參數**

| 參數 | 說明 | 類型 | 預設 | 選填 |
|-----------|-----------------------------------------------------------------------------------------------|---------|-------------------|----------|
| `N` | 最小n元組長度，必須大於或等於1。 | 整數 | 2 （bigram功能） | 可選 |

{style="table-layout:auto"}

**轉換範例**

此範例示範NGram轉換器如何從衍生自文字資料的Token清單建立3克數序列。

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**n字元轉換之前和之後的範例**

| ID | 文字 | n_tokens |
|----|-------------------------------------------------------|-------------------------------------------------------|
| 0 | [&quot;this&quot;、&quot;was&quot;、&quot;an&quot;、&quot;entering&quot;、&quot;movie&quot;] | [「這是」、「是一個娛樂」、「一個娛樂電影」] |

{style="table-layout:auto"}

#### StopWordsRemover {#stopwordsremover}

`StopWordsRemover`是一種轉換器，可從字串序列中移除停用字詞，篩選掉沒有重要意義的一般字詞。 它以一連串字串作為輸入（例如Tokenizer的輸出），並移除`stopWords`引數所指定的所有停用詞。

此轉換有助於預先處理文字資料，藉由消除對整體意義貢獻不大的字詞來增強下游機器學習模型的效能。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stopwordsremover) -->

**資料類型**

- 輸入資料型別： Array[String]
- 輸出資料型別： Array[String]

**定義**

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**參數**

| 參數 | 說明 | 類型 | 預設 | 選填 |
|--------------------|--------------------------------------------------------------------------------------------------|---------------|-------------------------|----------|
| `stopWords` | 要篩選掉的字詞。 | 陣列[字串] | 預設：英文停用詞 | 可選 |

{style="table-layout:auto"}

<!-- Q) should this be the `CUSTOM_STOP_WORDS` parameter or the `stopWords` parameter?  -->

**轉換範例**

此範例顯示`StopWordsRemover`如何從權杖清單中篩選出常見的英文停用詞。

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**移除停用字之前和之後的範例**

| ID | 原始 | 已篩選 |
|----|------------------------------|--------------------------|
| 0 | [我，看見，紅色，氣球] | [鋸，紅色，氣球] |
| 1 | [Mary， had， a， little， lamb] | [Mary， little， lamb] |

**包含自訂停用字的範例**

此範例示範如何使用停用字的自訂清單，從輸入序列中篩選掉特定字詞。

```sql
TRANSFORM(stop_words_remover(raw, array("red", "I", "had")) as filtered)
```

**移除自訂停用字之前和之後的範例**

| ID | 原始 | 已篩選 |
|----|------------------------------|--------------------------|
| 0 | [我，看見，紅色，氣球] | [已看見，氣球] |
| 1 | [Mary， had， a， little， lamb] | [Mary， a， little， lamb] |

#### TF-IDF {#tf-idf}

`TF-IDF` （詞語頻率 — 反轉檔案頻率）是用來測量檔案中字詞相對於語料庫的重要性的轉換器。 字詞頻率(TF)是指字詞\(t\)出現在檔案\(d\)中的次數，而檔案頻率(DF)則是測量語料庫中有多少檔案\(D\)包含字詞\(t\)。 此方法廣泛應用於文字採礦中，以降低常見字詞（例如&quot;a&quot;、&quot;the&quot;及&quot;of&quot;）的影響，這些字詞幾乎沒有唯一資訊。

此轉換在文字採礦和自然語言處理任務中特別有用，因為它會為檔案內和整個語料庫中的每個字的重要程度指定一個數值。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tf-idf) -->

**資料類型**

- 輸入資料型別： Array[String]
- 輸出資料型別： Vector[Int]

**定義**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**參數**

| 參數 | 說明 | 類型 | 預設 | 選填 |
|-----------------|----------------------------------------------------------------------------------------|------|---------|----------|
| `NUM_FEATURES` | 要產生的功能數目。 必須大於 0。 | 整數 | 262144 | 可選 |
| `MIN_DOC_FREQ` | 模型中必須包含字詞的最小檔案數。 | 整數 | 0 | 可選 |

{style="table-layout:auto"}

**轉換範例**

此範例示範如何使用TF-IDF將標籤化的句子轉換為特徵向量，該向量代表每個辭彙在整個語料庫內容中的重要性。

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Tokenizer {#tokenizer}

`Tokenizer`是將文字（例如句子）劃分為個別詞語（通常是單字）的轉換程式。 它會將句子轉換為權杖陣列，提供文字前置處理的基本步驟，為進一步的文字分析或模型化程式準備資料。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tokenizer) -->

**資料類型**

- 輸入資料型別：文字句子
- 輸出資料型別： Array[String]

**定義**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**參數**

| 參數 | 說明 | 類型 | 預設 | 選填 |
|-----------|-------------|------|---------|----------|
| 不適用 | `Tokenizer`的作業不需要任何額外的引數。 | 不適用 | 不適用 | 不適用 |

**轉換範例**

此範例示範`Tokenizer`在文書處理管道中，如何將句子劃分為個別單字（代號）。

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Word2Vec {#word2vec}

`Word2Vec`是處理代表檔案的字序列並訓練`Word2VecModel`的估計器。 此模型會將每個字對應至唯一的固定大小向量，並透過平均檔案中所有字的向量將每個檔案轉換為向量。 `Word2Vec`廣泛使用於自然語言處理工作，可建立擷取語意的文字內嵌，將文字資料轉換成代表文字間關係的數值向量，並啟用更有效的文字分析和機器學習模型。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#word2vec) -->

**資料類型**

- 輸入資料型別： Array[String]
- 輸出資料型別： Vector[Double]

**定義**

```sql
TRANSFORM(tokenizer(review) as tokenized, word2Vec(tokenized, 10, 1) as word2Vec)
```

**參數**

| 參數 | 說明 | 類型 | 預設 | 選填 |
|--------------|-----------------------------------------------------------------------------------------------------|---------|---------|----------|
| `VECTOR_SIZE` | 每個字轉換成的向量尺寸。 | 整數 | 100 | 可選 |
| `MIN_COUNT` | 在`Word2Vec`模型的辭彙表中必須包含權杖的最小次數。 | 整數 | 5 | 可選 |

{style="table-layout:auto"}

**轉換範例**

此範例顯示`Word2Vec`如何將代碼化稽核轉換為代表檔案中字向量平均值的固定大小向量。

```sql
TRANSFORM(tokenizer(review) as tokenized, word2Vec(tokenized, 10, 1) as word2Vec)
```

**Word2Vec轉換之前和之後的範例**

| 評論 | 代碼化 | word2Vec |
|-------------------------------|--------------------------------------|---------------------------------|
| 這是部娛樂電影 | [這個，曾經是，娛樂，電影] | [-0.025713888928294182、0.00818799751577899、0.0092235435731709、-0.01515385233797133、0.012175946310162545、3.1129065901041035E-4、0.0025145105042611252、0.005757019785232843、-0.021328244300093502、0.009335877187550069] |

{style="table-layout:auto"}
