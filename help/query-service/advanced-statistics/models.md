---
title: 模型
description: 使用Data Distiller SQL擴充功能建立生命週期管理的模型。 瞭解如何使用SQL建立、訓練和管理進階統計模型，包括模型版本設定、評估和預測等關鍵程式，以從資料中取得可行的深入分析。
role: Developer
source-git-commit: b248e8f8420b617a117d36aabad615e5bbf66b58
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 1%

---

# 模型

>[!AVAILABILITY]
>
>已購買Data Distiller附加元件的客戶可使用此功能。 如需詳細資訊，請聯絡您的 Adobe 代表。

查詢服務現在支援建置和部署模型的核心程式。 您可以使用SQL來使用您的資料訓練模型、評估其準確性，然後套用訓練模型來預測新資料。 然後，您可以使用模型來將過去資料歸納化，以針對真實世界的情境做出明智的決策。

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

## 更新模型 {#update}

瞭解如何套用新功能工程轉換並設定演演算法型別和標籤欄等選項，以更新現有的機器學習模型。 以下SQL示範如何在每次更新時增加模型的版本編號，並確保追蹤變更，以便在未來的評估或預測步驟中可重複使用模型。

```sql
UPDATE model <model_alias> transform( one_hot_encoder(NAME) ohe_name, string_indexer(gender) gendersi) options ( type = 'LogisticRegression', label = <label-COLUMN>, ) ASSELECT col1,
       col2,
       col3
FROM   training-dataset.
```

為了協助您瞭解如何管理模型版本並有效地套用轉換，下列附註將說明模型更新工作流程中的關鍵元件和選項。

- `UPDATE model <model_alias>`：更新命令會處理版本設定，並隨著每次更新而增加模型的版本號碼。
- `version`：選擇性關鍵字，只在更新時用於建立模型的新版本。

## 評估模型 {#evaluate-model}

為了確保可靠的結果，請使用`model_evaluate`關鍵字將模型部署為預測之前，先評估模型的正確性和有效性。 下列SQL陳述式會指定測試資料集、特定欄及模型的版本，以評估模型的效能，藉以測試模型。

```sql
SELECT *
FROM   model_evaluate(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   test -dataset)
```

`model_evaluate`函式將`model-alias`當作第一個引數，並將彈性的`SELECT`陳述式當作第二個引數。 查詢服務會先執行`SELECT`陳述式，並將結果對應到`model_evaluate`Adobe定義函式(ADF)。 系統期望`SELECT`陳述式結果中的資料行名稱和資料型別符合訓練步驟中所使用的名稱。 這些欄名稱和資料型別會視為測試資料和標籤資料進行評估。

>[!IMPORTANT]
>
>評估(`model_evaluate`)和預測(`model_predict`)時，會使用訓練時執行的轉換。

## 預測 {#predict}

接下來，使用`model_predict`關鍵字將指定的模型與版本套用至資料集，並針對選取的欄產生預測。 下列SQL會示範此程式，說明如何使用模型的別名和版本來預測結果。

```sql
SELECT *
FROM   model_predict(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   dataset)
```

`model_predict`接受模型別名做為第一個引數，彈性的`SELECT`陳述式做為第二個引數。 查詢服務會先執行`SELECT`陳述式，並將結果對應至`model_predict` ADF。 系統期望`SELECT`陳述式結果中的資料行名稱和資料型別符合訓練步驟中的資料行名稱和資料型別。 然後，此資料會用於評分和產生預測。

>[!IMPORTANT]
>
>評估(`model_evaluate`)和預測(`model_predict`)時，會使用訓練時執行的轉換。

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
