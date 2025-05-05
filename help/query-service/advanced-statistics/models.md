---
title: 模型
description: 使用Data Distiller SQL擴充功能建立生命週期管理的模型。 瞭解如何使用SQL建立、訓練和管理進階統計模型，包括模型版本設定、評估和預測等關鍵程式，以從資料中取得可行的深入分析。
role: Developer
exl-id: c609a55a-dbfd-4632-8405-55e99d1e0bd8
source-git-commit: 09129d9d19816b4d93b4979305f4ad532e5ffde4
workflow-type: tm+mt
source-wordcount: '1645'
ht-degree: 1%

---

# 模型

>[!AVAILABILITY]
>
>已購買Data Distiller附加元件的客戶可使用此功能。 如需詳細資訊，請聯絡您的 Adobe 代表。

查詢服務現在支援建置和部署模型的核心程式。 您可以使用SQL來使用您的資料訓練模型、評估其準確性，然後使用訓練好的模型來預測新資料。 然後，您可以使用模型來將過去資料歸納化，以針對真實世界的情境做出明智的決策。

模型生命週期中用於產生可操作深入分析的三個步驟如下：

1. **訓練**：模型會從提供的資料集中學習模式。 （建立或取代模型）
2. **測試/評估**：使用個別的資料集來評估模型的效能。(`model_evaluate`)
3. **預測**：已訓練的模型是用來預測新的、未見的資料。

使用模型SQL擴充功能（新增至現有的SQL文法），根據您的業務需求管理模型生命週期。 本文介紹建立或取代模型、訓練、評估、必要時重新訓練，以及預測深入分析所需的SQL。

## 模型建立與訓練 {#create-and-train}

瞭解如何使用SQL命令來定義、設定和訓練機器學習模型。 下列SQL示範如何建立模型、套用特徵工程轉換及啟動訓練程式，以確保模型已正確設定以供未來使用。 下列SQL命令詳細說明模型建立與管理的不同選項：

- **建立模型**：在指定的資料集上建立和訓練新模型。 如果已經存在相同名稱的模型，這個命令會傳回錯誤。
- **如果不存在則建立模型**：僅當指定資料集上不存在相同名稱的模型時，才建立及訓練新模型。
- **建立或取代模型**：建立並訓練模型，以指定資料集上相同名稱取代現有模型的最新版本。

```sql
CREATE MODEL | CREATE MODEL IF NOT EXISTS | CREATE OR REPLACE MODEL}
model_alias
[TRANSFORM (select_list)]
[OPTIONS(model_option_list)]
[AS {select_query}]
 
model_option_list:
    MODEL_TYPE = { 'LINEAR_REG' |
                   'LOGISTIC_REG' |
                   'KMEANS' }
  [, MAX_ITER = int64_value ]
 [, LABEL = string_array ]
[, REG_PARAM = float64_value ]
```

**範例**

```sql
CREATE MODEL churn_model
TRANSFORM (vector_assembler(array(current_customers, previous_customers)) features) 
OPTIONS(MODEL_TYPE='linear_reg', LABEL='churn_rate') 
AS
SELECT *
FROM churn_with_rate
ORDER BY period;
```

為了協助您瞭解模型建立和訓練流程中的關鍵元件和組態，下列附註會說明上述SQL範例中每個元素的用途和功能。

- `<model_alias>`：模型別名是指派給模型的可重複使用名稱，稍後可參考此名稱。 必須為模型命名。
- `transform`： transform子句是用來在訓練模型之前，將功能工程轉換（例如，單熱式編碼和字串索引）套用至資料集。 `TRANSFORM`陳述式的最後一個子句應該是一個含有欄清單的`vector_assembler`，這些欄會構成模型訓練的功能，或者是`vector_assembler`的衍生型別（例如`max_abs_scaler(feature)`、`standard_scaler(feature)`等）。 將只使用最後一個子句中提及的資料行來訓練；其他所有資料行，即使包含在`SELECT`查詢中，也會被排除。
- `label = <label-COLUMN>`：訓練資料集中的標籤欄，指定模型要預測的目標或結果。
- `training-dataset`：此語法會選取用來訓練模型的資料。
- `type = 'LogisticRegression'`：此語法指定要使用的機器學習演演算法型別。 選項包括`LinearRegression`、`LogisticRegression`和`KMeans`。
- `options`：此關鍵字提供一組彈性的機碼值組，可用來設定模型。
   - `Key model_type`： `model_type = '<supported algorithm>'`：指定要使用的機器學習演演算法型別。 支援的選項包括`LinearRegression`、`LogisticRegression`和`KMeans`。
   - `Key label`： `label = <label_COLUMN>`：定義訓練資料集中的標籤資料行，其指出模型要預測的目標或結果。

使用SQL來參照用於訓練的資料集。

>[!TIP]
>
>如需`TRANSFORM`子句的完整參考，包括`CREATE MODEL`與`CREATE TABLE`中支援的函式與使用方式，請參閱SQL語法檔案[&#128279;](../sql/syntax.md#transform)中的`TRANSFORM`子句。

## 更新模型 {#update}

瞭解如何套用新功能工程轉換並設定演演算法型別和標籤欄等選項，以更新現有的機器學習模型。 每次更新都會建立模型的新版本，從上一個版本增加。 這樣可確保追蹤變更，且模型可在未來的評估或預測步驟中重複使用。

下列範例示範使用新的轉換和選項來更新模型：

```sql
UPDATE MODEL <model_alias> TRANSFORM (vector_assembler(array(current_customers, previous_customers)) features)  OPTIONS(MODEL_TYPE='logistic_reg', LABEL='churn_rate')  AS SELECT * FROM churn_with_rate ORDER BY period;
```

**範例**

為了幫助您瞭解版本設定過程，請考慮下列指令：

```sql
UPDATE MODEL model_vdqbrja OPTIONS(MODEL_TYPE='logistic_reg', LABEL='Survived') AS SELECT * FROM titanic_e2e_dnd;
```

執行此指令後，模型會有新版本，如下表所示：

| 已更新模型ID | 已更新模型 | 新版本 |
|--------------------------------------------|---------------|-------------|
| a8f6a254-8f28-42ec-8b26-94edeb4698e8 | model_vdqbrja | 2 |

下列附註說明模型更新工作流程中的關鍵元件和選項。

- `UPDATE model <model_alias>`：更新命令會處理版本設定並建立從上一個版本增加的新模型版本。
- `version`：僅在更新期間使用的選擇性關鍵字，用來明確指定應建立新版本。 如果省略，系統會自動增加版本。

### 預覽和保留轉換後的功能 {#preview-transform-output}

使用`CREATE TABLE`和`CREATE TEMP TABLE`陳述式中的`TRANSFORM`子句，在模型訓練之前預覽及保留功能轉換的輸出。 此增強功能可讓您檢視如何將轉換函式（例如編碼、代碼化和向量組合器）套用至您的資料集。

透過將轉換後的資料具體化成獨立表格，您可以在建立模型之前檢查中間特徵、驗證處理邏輯並確保特徵品質。 這麼做可改善整個機器學習管道的透明度，並支援在模型開發期間做出更明智的決策。

#### 語法 {#syntax}

在`CREATE TABLE`或`CREATE TEMP TABLE`陳述式中使用`TRANSFORM`子句，如下所示：

```sql
CREATE TABLE [IF NOT EXISTS] table_name
[WITH (tableProperties)]
TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)
AS SELECT * FROM source_table;
```

或：

```sql
CREATE TEMP TABLE [IF NOT EXISTS] table_name
[WITH (tableProperties)]
TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)
AS SELECT * FROM source_table;
```

**範例**

使用基本轉換建立表格：

```sql
CREATE TABLE ctas_transform_table
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments
)
AS SELECT * FROM movie_review;
```

使用其他特徵工程步驟建立臨時表格：

```sql
CREATE TEMP TABLE ctas_transform_table
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments,
  stop_words_remover(token_comments, array('and','very','much')) stp_token,
  ngram(stp_token, 3) ngram_token,
  tf_idf(ngram_token, 20) ngram_idf,
  count_vectorizer(stp_token, 13) cnt_vec_comments,
  tf_idf(token_comments, 10, 1) as cmts_idf
)
AS SELECT * FROM movie_review;
```

然後查詢輸出：

```sql
SELECT * FROM ctas_transform_table LIMIT 1;
```

#### 重要考量 {#considerations}

雖然此功能可增強透明度並支援功能驗證，但在模型建立之外使用`TRANSFORM`子句時，有一些重要的限制需要考量。

- **向量輸出**：如果轉換產生向量型別輸出，它們會自動轉換為陣列。
- **批次重複使用限制**：以`TRANSFORM`建立的資料表只能在資料表建立期間套用轉換。 以`INSERT INTO`插入的新資料批次&#x200B;**未自動轉換**。 若要將相同的轉換邏輯套用至新資料，您必須使用新的`CREATE TABLE AS SELECT` (CTAS)陳述式重新建立表格。
- **模型重複使用限制**：使用`TRANSFORM`建立的資料表不能直接用於`CREATE MODEL`陳述式。 您必須在模型建立期間重新定義`TRANSFORM`邏輯。 模型訓練期間不支援產生向量型別輸出的轉換。 如需詳細資訊，請參閱[功能轉換輸出資料型別](./feature-transformation.md#available-transformations)。

>[!NOTE]
>
>此功能是專為檢查和驗證所設計。 它無法取代可重複使用的管道邏輯。 任何用於模型輸入的轉換必須在模型建立步驟中明確重新定義。

## 評估模型 {#evaluate-model}

為了確保可靠的結果，請使用`model_evaluate`關鍵字將模型部署為預測之前，先評估模型的正確性和有效性。 下列SQL陳述式會指定測試資料集、特定欄及模型的版本，以評估模型的效能，藉以測試模型。

```sql
SELECT *
FROM   model_evaluate(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   test_dataset)
```

`model_evaluate`函式將`model-alias`當作第一個引數，並將彈性的`SELECT`陳述式當作第二個引數。 查詢服務會先執行`SELECT`陳述式，並將結果對應至`model_evaluate` Adobe定義函式(ADF)。 系統期望`SELECT`陳述式結果中的資料行名稱和資料型別符合訓練步驟中所使用的名稱。 這些欄名稱和資料型別會視為測試資料和標籤資料進行評估。

>[!IMPORTANT]
>
>評估(`model_evaluate`)和預測(`model_predict`)時，會使用訓練時執行的轉換。

## 預測 {#predict}

>[!IMPORTANT]
>
>`model_predict`的增強欄選擇和別名是由功能標幟所控制。 依預設，預測輸出中不包含中繼欄位，例如`probability`和`rawPrediction`。\
>若要啟用對這些中間欄位的存取權，請在執行`model_predict`之前執行下列命令：
>
>`set advanced_statistics_show_hidden_fields=true;`

使用`model_predict`關鍵字將指定的模型和版本套用至資料集並產生預測。 您可以選取所有輸出欄、選擇特定欄或指派別名以提高輸出清晰度。

依預設，除非啟用功能標幟，否則僅傳回基礎欄和最終預測。

```sql
SELECT * FROM model_predict(model-alias, version-number, SELECT col1, col2 FROM dataset);
```

### 選取特定輸出欄位 {#select-specific-output-fields}

啟用功能標幟時，您可以從`model_predict`輸出擷取欄位子集。 使用此項可擷取中繼結果，例如預測機率、原始預測分數，以及輸入查詢中的基礎欄。

**案例1：傳回所有可用的輸出欄位**

```sql
SELECT * FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

**案例2：傳回選取的資料行**

```sql
SELECT a, b, c, probability, predictionCol FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

**案例3：傳回選取的具有別名的資料行**

```sql
SELECT a, b, c, probability AS p1, predictionCol AS pdc FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

在每種情況下，外部`SELECT`會控制傳回哪些結果欄位。 這些包括來自輸入查詢的基礎欄位，以及預測輸出，例如`probability`、`rawPrediction`和`predictionCol`。

### 使用CREATE TABLE或INSERT INTO保留預測

您可以使用「以選取方式建立表格」或「插入至選取專案」來儲存預測，包括預測輸出（如有需要）。

**範例：建立包含所有預測輸出欄位的資料表**

```sql
CREATE TABLE scored_data AS SELECT * FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

**範例：插入選取的輸出欄位（含別名**）

```sql
INSERT INTO scored_data SELECT a, b, c, probability AS p1, predictionCol AS pdc FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

如此可讓您靈活地選取並僅保留相關的預測輸出欄位和基礎欄，以用於下游分析或報告。

## 評估和管理您的模型

使用`SHOW MODELS`命令列出您建立的所有可用模型。 用它來檢視經過訓練的模型，並可用於評估或預測。 在查詢時，會從模型存放庫中擷取資訊，在建立模型期間會更新該資訊。 傳回的詳細資料包括：模型ID、模型名稱、版本、來源資料集、演演算法詳細資訊、選項/引數、建立/更新時間以及建立模型的使用者。

```sql
SHOW MODELS;
```

結果會顯示在類似於以下所示的表格中：

| model-id | model-name | 版本 | source-data | 類型 | 選項 | 轉換 | 欄位 | 已建立 | 已更新 | 建立者 |
|--------------------|---------------|---------|------------------|-----------------------|------------------------------|---------------------------------------------------------------------------|----------------------|---------------------|---------------------|------------|
| `model-84362-mdunj` | `SalesModel` | 1.0 | `sales_data_2023` | `LogisticRegression` | `{"label": "label-field"}` | `one_hot_encoder(name)`、`ohe_name`、`string_indexer(gender)`、`genderSI` | \[&quot;name&quot;， &quot;gender&quot;\] | 2024-08-14 10:30 AM | 2024-08-14 11:00 AM | `JohnSnow@adobe.com` |

## 清理和維護您的模型

使用`DROP MODELS`命令刪除您從模型登入建立的模型。 您可以使用它來移除過時、未使用或不想要的模型。 這樣可以釋放資源，並確保只維護相關的模型。 您也可以加入選用模型名稱，以改善專一性。 這只會捨棄具有所提供模型版本的模型。

```sql
DROP MODEL IF EXISTS modelName
DROP MODEL IF EXISTS modelName modelVersion ;
```

## 後續步驟

閱讀本檔案後，您現在瞭解使用Data Distiller建立、訓練和管理受信任模型所需的基本SQL語法。 接下來，請探索[實作進階統計模型檔案](./implement-models/implement-models.md)，瞭解各種可用的信任模型，以及如何在SQL工作流程中有效實作這些模型。 若尚未完成，請務必檢閱[功能工程](./feature-engineering.md)檔案，以確保您的資料已準備好接受模型訓練。
