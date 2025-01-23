---
title: 使用SQL型Logistic回歸預測客戶流失
description: 瞭解如何使用SQL型Logistic回歸預測客戶流失。 本指南涵蓋從模型建立到評估和預測的整個過程。 從客戶購買行為中獲得可操作的見解，以實施主動的保留策略並最佳化業務決策。
source-git-commit: 95c7ad3f8eb86cacd42077008824eea9e25b4db0
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 1%

---

# 使用SQL型Logistic回歸預測客戶流失

預測客戶流失可透過可操作的深入分析提高滿意度和忠誠度，協助企業保留客戶、最佳化資源及提高盈利能力。

探索如何使用SQL型Logistic回歸來預測客戶流失。 使用本全方位的SQL指南，根據關鍵行為量度（例如購買頻率、平均訂購值和上次購買間隔時間），將原始電子商務資料轉換為有意義的客戶深入分析。 本檔案涵蓋從資料準備和特徵工程到模型建立、評估和預測的整個過程。

使用本指南建立強大的流失預測模型，用於識別高風險客戶、改良保留策略，以及推動更好的業務決策。 其中包含逐步指示、SQL查詢和詳細解釋，協助您在資料環境中自信地套用機器學習技術。

## 快速入門

在建立流失模型之前，請務必探索關鍵客戶功能和資料需求。 以下各節概述精確模型訓練所需的基本客戶屬性和必要資料欄位。

### 定義客戶功能 {#define-customer-features}

為了準確地分類流失率，此模型會分析購買習慣和趨勢。 下表概述模型中使用的主要客戶行為功能：

| 功能 | 說明 |
|---------------------------|-------------------------------------------------------|
| `total_purchases` | 客戶進行的購買總數。 |
| `total_revenue` | 從客戶購買產生的總收入。 |
| `avg_order_value` | 客戶購買的平均值。 |
| `customer_lifetime` | 客戶首次和上次購買之間的天數。 |
| `days_since_last_purchase` | 自客戶上次購買以來的天數。 |
| `purchase_frequency` | 客戶購買的不同月份數。 |

### 假設和必填欄位 {#assumptions-required-fields}

若要產生客戶流失預測，此模型依賴`webevents`表格中擷取客戶交易詳細資料的主要欄位。 您的資料集必須包括下列欄位：

| 欄位 | 說明 |
|--------------------------------|----------------------------------------------------|
| `identityMap['ECID'][0].id` | 用於跨工作階段追蹤客戶的唯一識別碼。 |
| `productListItems.priceTotal[0]` | 每筆交易的外購專案總成本。 |
| `productListItems.quantity[0]` | 購買中的專案總數。 |
| `timestamp` | 每個購買事件的確切日期和時間。 |
| `commerce.order.purchaseID` | 確認完成購買的必要值。 |

資料集必須包含結構化歷史客戶交易記錄，每一列代表購買事件。 每個事件都必須包含與SQL `DATEDIFF`函式相容之適當日期 — 時間格式的時間戳記（例如YYYY-MM-DD HH:MI:SS）。 此外，每個記錄都必須在`identityMap`欄位中包含有效的Experience Cloud識別碼(`ECID`)，才能唯一識別客戶。

>[!TIP]
>
>處理包含數百萬筆記錄的大型資料集可能會大幅影響效能。 若要最佳化查詢執行，請依時間戳記分割體驗資料集、使用快照執行增量處理，並視需要套用有效的彙總函式。 此外，在彙總之前篩選資料，以減少處理額外負荷。

## 建立模型 {#create-a-model}

若要預測客戶流失，您必須建立以SQL為基礎的Logistic回歸模型，分析客戶購買記錄和行為量度。 模型會判斷客戶在過去90天內是否購買，以將其分類為`churned`或`not churned`。

### 使用SQL建立流失預測模型 {#sql-create-model}

SQL型模型會處理`webevents`資料，方法是彙總關鍵量度，並根據90天非使用狀態規則指派流失標籤。 此方法可區分活躍客戶與高風險客戶。 SQL查詢還會執行功能工程來增強模型準確性並改善流失分類。 這些見解讓您的企業能夠實施針對性的保留策略、減少流失並最大化客戶期限價值。

>[!NOTE]
>
>流失預測模型使用90天的預設臨界值，將客戶分類為已流失。 若要調整此臨界值以符合您的業務目標和保留策略，請修改SQL查詢中的`DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90`條件。

使用下列SQL陳述式來建立具有指定功能和標籤的`retention_model_logistic_reg`模型：

```sql
CREATE MODEL retention_model_logistic_reg
TRANSFORM (
  vector_assembler(array(total_purchases, total_revenue, avg_order_value, customer_lifetime, days_since_last_purchase, purchase_frequency)) features
  -- Combines selected customer metrics into a feature vector for model training
)
OPTIONS (
  MODEL_TYPE = 'logistic_reg',  -- Specifies logistic regression as the model type
  LABEL = 'churned'             -- Defines the target label for churn classification
)
AS
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,  -- Extract the unique customer ID from identityMap
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,  -- Calculates the average order value, and handles null values with COALESCE
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue, -- The sum of all purchase values per customer
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases,  -- The total number of items purchased by the customer
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,  -- The days between first and last recorded purchase
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,  -- The days since the last purchase event
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency  -- The count of unique months with purchases
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  -- Filters transactions with valid total price
      AND commerce.`order`.purchaseID <> ''  -- Ensures the order has a valid purchase ID
    GROUP BY customer_id 
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,  -- Extract the unique customer ID for labeling
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1  -- Marks the customer as churned if no purchase occurred in the last 90 days
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0) 
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id  
)
SELECT
    f.customer_id,
    f.total_purchases,
    f.total_revenue,
    f.avg_order_value,
    f.customer_lifetime,
    f.days_since_last_purchase,
    f.purchase_frequency,
    l.churned
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id  -- Join features with churn labels
ORDER BY RANDOM()  -- Shuffles rows randomly for training
LIMIT 500000;  -- Limit the dataset to 500,000 rows for model training
```

### 模型輸出 {#model-output}

輸出資料集包含客戶相關量度及其流失狀態。 每一列代表客戶、其功能值及其流失狀態。 您可以使用此輸出來分析客戶行為、訓練預測模型並開發目標性的保留策略以保留有風險的客戶。 輸出表範例如下所示：

```console
 customer_id  | total_purchases | total_revenue | avg_order_value  | customer_lifetime | days_since_last_purchase | purchase_frequency | churned |
--------------+-----------------+---------------+------------------+-------------------+--------------------------+--------------------+----------
  100001      | 25              | 1250.00       | 50.00            | 540               | 20                       | 10                 | 0       
  100002      | 3               | 90.00         | 30.00            | 120               | 95                       | 1                  | 1       
  100003      | 60              | 7200.00       | 120.00           | 800               | 5                        | 24                 | 0       
  100004      | 15              | 750.00        | 50.00            | 365               | 60                       | 8                  | 0       
  100005      | 1               | 25.00         | 25.00            | 60                | 180                      | 1                  | 1       
```

| 欄 | 說明 |
|-----------|------------------------------------------------------------------------------------|
| `churned` | 此值會指出客戶是否在過去90天內進行購買（0 =未流失，1 =流失）。 |

## 使用SQL評估模型 {#model-evaluation}

接下來，評估流失預測模型，以判斷其在識別風險客戶方面的有效性。 使用測量精確度和可靠性的關鍵量度來評估模型效能。

若要測量`retention_model_logistic_reg`模型預測客戶流失的準確度，請使用`model_evaluate`函式。 以下SQL範例會使用如訓練資料結構化的資料集來評估模型：

```sql
SELECT * 
FROM model_evaluate(retention_model_logistic_reg, 1,
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue,
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases, 
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency 
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)
      AND commerce.`order`.purchaseID <> ''
    GROUP BY customer_id
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1 
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0) 
      AND commerce.`order`.purchaseID <> '' 
    GROUP BY customer_id
)
SELECT
    f.customer_id,
    f.total_purchases,
    f.total_revenue,
    f.avg_order_value,
    f.customer_lifetime,
    f.days_since_last_purchase,
    f.purchase_frequency,
    l.churned
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id); -- Joins customer features with churn labels
```

### 模型評估輸出

評估輸出包括關鍵效能量度，例如AUC-ROC、精確度、精確度和召回率。 這些量度可讓您深入瞭解模型有效性，以便用於調整保留策略及制定資料導向式決策。

>[!NOTE]
>
>效能值的範圍從0到1，其中1.0表示完美效能。

```console
 auc_roc | accuracy | precision | recall 
---------+----------+-----------+--------
1        | 0.99998  |  1        |  1      
```

| 量度 | 說明 |
|------------|-------------------------------------------------------------------------|
| `auc_roc` | 此量度表示模型區分流失與非流失客戶的能力。 值越接近1表示效能越好。 |
| `accuracy` | 準確性量度代表正確預測的比例，提供模型績效的整體測量。 |
| `precision` | 精確度會顯示正確識別的流失客戶比例，並指出流失預測中的可靠性。 高值表示誤報較少。 |
| `recall` | 召回率會衡量模型識別所有實際流失客戶的能力。 高召回率表示遺漏的流失客戶較少。 |

>[!NOTE]
>
>此範例中的近乎完美分數僅供展示之用。 實際上，由於雜訊和變異性，真實世界的資料可能會產生較低的值。

## 模型預測 {#model-prediction}

評估模型後，使用`model_predict`將其套用至新資料集並預測客戶流失。 您可以使用這些預測來識別有風險的客戶，並實作目標性的保留策略。

### 使用SQL產生流失預測 {#sql-model-predict}

下列SQL查詢使用`retention_model_logistic_reg`模型，透過如訓練資料結構化的資料集來預測客戶流失：

```sql
SELECT * 
FROM model_predict(retention_model_logistic_reg, 1,  -- Applies the trained model for churn prediction
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,  
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue, 
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases,  
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,  
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,  
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency  
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  -- Ensures only valid purchase data is considered
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,  
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1  -- Identify customers who have not purchased in the last 90 days
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id
)
SELECT
    f.customer_id,  
    f.total_purchases,  
    f.total_revenue,  
    f.avg_order_value,  
    f.customer_lifetime,  
    f.days_since_last_purchase,  
    f.purchase_frequency,  
    l.churned  
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id);  -- Matches features with their churn labels for prediction
```

### 模型預測輸出 {#prediction-output}

輸出資料集包含關鍵客戶功能及其預測的客戶流失狀態，可指出客戶是否可能流失。 運用這些見解實施主動式保留策略並減少客戶流失。

```console
 total_purchases | total_revenue | avg_order_value | customer_lifetime | days_since_last_purchase | purchase_frequency | churned | prediction
-----------------+---------------+-----------------+-------------------+--------------------------+--------------------+---------+------------
 2               | 299           | 149.5           | 0                 | 13                        | 1                  | 0       | 0
 1               | 710           | 710.00          | 0                 | 149                       | 1                  | 1       | 1
 1               | 19.99         | 19.99           | 0                 | 30                        | 1                  | 0       | 0
 1               | 4528          | 4528.00         | 0                 | 26                        | 1                  | 0       | 0
 1               | 21.84         | 21.84           | 0                 | 90                        | 1                  | 0       | 0
 1               | 16.64         | 16.64           | 0                 | 268                       | 1                  | 1       | 1
```

| 欄 | 說明 |
|---------------|-------------------------------------------------------------------------------|
| `prediction` | 根據模型預測的客戶流失狀態（0 =未流失，1 =流失）。 |

## 後續步驟

您現在已經瞭解如何建立、評估及使用以SQL為基礎的模型來預測客戶流失。 有了這個基礎，您就可以分析客戶行為、識別有風險的客戶，並實作主動保留策略以改善客戶保留率。 若要進一步增強並套用流失預測模型，請考慮下列步驟：

- 自動化流程：將模型整合至資料管道，以進行持續監控和即時分析。 [探索如何使用SQL](../../../dashboards/query.md)驗證及處理資料集。
- 監控模型效能：持續使用新資料評估模型，以維護準確性和相關性。  在Adobe Experience Platform UI中使用[AI助理](../../../ai-assistant/landing.md)來監視關鍵效能變更和[預測對象趨勢](../../../ai-assistant/new-features/audience-forecasting.md)。
