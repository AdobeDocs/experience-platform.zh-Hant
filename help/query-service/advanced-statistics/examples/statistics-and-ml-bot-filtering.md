---
title: 使用統計和機器學習進行機器人篩選
description: 瞭解如何使用Data Distiller統計資料和機器學習來識別和篩選機器人活動，以確保準確分析並改善資料完整性。
source-git-commit: a8abbf61bdc646c0834c296a64b27c71c98ea1d3
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 0%

---

# 使用統計和機器學習進行機器人篩選

機器人過濾的實際應用跨越了不同的產業。 在電子商務中，它可改善轉換率量度的可靠性，新聞網站可藉由減少錯誤參與量度而獲益，而廣告網路則可確保公平計費。 為了維持精確分析並確保點按流或網站流量資料中的資料完整性，您必須處理機器人活動。 您可以使用Data Distiller實作有效的機器人篩選並消除不想要的流量，以確保高品質的分析資料。

本檔案提供使用SQL和機器學習技術來識別和篩選機器人活動的完整指南。 它代表一系列互補方法，從基本篩選開始，然後進展到機器學習型偵測和評估。 採用此健全的架構以增強您的機器人偵測並維護您的資料完整性。

## 瞭解機器人活動 {#understand-bot-activity}

可透過偵測特定時間間隔內使用者動作的尖峰來識別機器人活動。 例如，單一使用者在短時間內執行過多點按可能表示機器人行為。 機器人篩選使用的兩個關鍵屬性為：

- **ECID (Experience Cloud訪客識別碼)：**&#x200B;可識別訪客的通用、永續性識別碼。
- **時間戳記：**&#x200B;網站上發生活動的時間和日期。

以下範例示範如何使用SQL和機器學習技術來識別、調整及預測機器人活動。 使用這些方法可改善資料完整性並確保分析可操作性。

## SQL型機器人篩選 {#sql-based-bot-filtering}

此以SQL為基礎的機器人篩選範例示範如何使用SQL查詢來定義臨界值，以及根據預先定義的規則偵測機器人活動。 此基本方法可移除異常活動，有助於識別網站流量中的異常。 透過使用定義的臨界值和間隔來自訂偵測規則，您可以有效地量身打造機器人篩選以符合您的特定流量模式。

### 定義機器人活動的臨界值 {#define-thresholds}

從分析您的資料集開始，以識別並分類使用者行為。 專注於ECID、時間戳記和`webPageDetails.name` （所造訪網頁的名稱）等屬性，將使用者動作分組，並偵測表示機器人活動的模式。

下列SQL查詢示範如何套用一分鐘內超過60次點按的臨界值，以識別可疑活動：

```sql
SELECT *
FROM analytics_events_table
WHERE enduserids._experience.ecid NOT IN (
    SELECT enduserids._experience.ecid
    FROM analytics_events_table
    GROUP BY Unix_timestamp(timestamp) / 60, enduserids._experience.ecid
    HAVING Count(*) > 60
);
```

### 展開至多個間隔 {#expand-to-multiple-intervals}

接著，定義臨界值的不同時間間隔。 這些間隔可能包括：

- **1分鐘間隔：**&#x200B;最多60次點按。
- **5分鐘間隔：**&#x200B;最多300次點按。
- **30分鐘間隔：**&#x200B;最多1800次點按。

下列SQL查詢會建立名為`analytics_events_clicks_count_criteria`的檢視，以處理多個間隔的臨界值。 陳述式會將1分鐘、5分鐘和30分鐘間隔的點選計數合併為結構化資料集，並根據預先定義的臨界值標示潛在的機器人活動。

```sql
CREATE VIEW analytics_events_clicks_count_criteria as  
SELECT struct (
        cast(count_1_min AS int) one_minute,
        cast(count_5_mins AS int) five_minute,
        cast(count_30_mins AS int) thirty_minute
       ) count_per_id,
       id,
      struct (
        struct (name) webpagedetails
      ) web,
      CASE
        WHEN count.one_minute > 50 THEN 1
        ELSE 0
      END AS isBot
FROM (
  SELECT table_count_1_min.mcid AS id,
         count_1_min,
         count_5_mins,
         count_30_mins,
         table_count_1_min.name AS name
  FROM (
      (SELECT mcid, Max(count_1_min) AS count_1_min, name
       FROM (SELECT enduserids._experience.mcid.id AS mcid,
                    Count(*) AS count_1_min,
                    web.webPageDetails.name AS name
             FROM delta_table
             WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                               AND TO_TIMESTAMP('2019-09-01 23:00:00')
             GROUP BY UNIX_TIMESTAMP(timestamp) / 60,
                      enduserids._experience.mcid.id,
                      web.webPageDetails.name)
       GROUP BY mcid, name) AS table_count_1_min
       LEFT JOIN
       (SELECT mcid, Max(count_5_mins) AS count_5_mins, name
        FROM (SELECT enduserids._experience.mcid.id AS mcid,
                     Count(*) AS count_5_mins,
                     web.webPageDetails.name AS name
              FROM delta_table
              WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                                AND TO_TIMESTAMP('2019-09-01 23:00:00')
              GROUP BY UNIX_TIMESTAMP(timestamp) / 300,
                       enduserids._experience.mcid.id,
                       web.webPageDetails.name)
        GROUP BY mcid, name) AS table_count_5_mins
       ON table_count_1_min.mcid = table_count_5_mins.mcid
       LEFT JOIN
       (SELECT mcid, Max(count_30_mins) AS count_30_mins, name
        FROM (SELECT enduserids._experience.mcid.id AS mcid,
                     Count(*) AS count_30_mins,
                     web.webPageDetails.name AS name
              FROM delta_table
              WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                                AND TO_TIMESTAMP('2019-09-01 23:00:00')
              GROUP BY UNIX_TIMESTAMP(timestamp) / 1800,
                       enduserids._experience.mcid.id,
                       web.webPageDetails.name)
        GROUP BY mcid, name) AS table_count_30_mins
       ON table_count_1_min.mcid = table_count_30_mins.mcid
  )
)
```

陳述式使用`mcid`值和網頁聯結來自`table_count_1_min`、`table_count_5_mins`和`table_count_30_mins`的資料。 然後它會合併多個時間間隔內每個使用者的點按計數，以提供使用者活動的完整檢視。 最後，標幟邏輯接著會識別一分鐘內超過50次點按的使用者，並將其標示為機器人(`isBot = 1`)。

### 輸出資料集結構

輸出資料集的結構包含平面和巢狀欄位。 此結構可讓您在偵測異常流量時具有彈性，並支援使用SQL和機器學習的進階篩選策略。 巢狀欄位包含`count`和`web`，它們封裝有關活動臨界值和網頁的詳細資訊。 擷取這些量度表示可輕鬆擷取特徵以用於訓練和預測工作。

下列結構描述圖概述結果資料集的結構，並著重說明巢狀和平坦欄位如何用於有效處理和機器人偵測。

```console
root
 |-- count: struct (nullable = false)
 |    |-- one_minute: integer (nullable = true)
 |    |-- five_minute: integer (nullable = true)
 |    |-- thirty_minute: integer (nullable = true)
 |-- id: string (nullable = true)
 |-- web: struct (nullable = false)
 |    |-- webpagedetails: struct (nullable = false)
 |    |    |-- name: string (nullable = true)
 |-- isBot: integer (nullable = false)
```

### 要用於訓練的輸出資料集

此運算式的結果可能類似於以下提供的表格。 在表格中，`isBot`欄當作區分機器人活動與非機器人活動的標籤。

```console
| `id`         | `count_per_id`                                      |`isBot`| `web`                                                                                                                    |
|--------------|-----------------------------------------------------|-------|------------------------------------------------------------------------------------------------------------------------|
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":99}| 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 1E+18        | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"KR+CC8TQzPyMOE/bk7EGgN3lSvP8OsxeI2aLaVrbaeLn8XK3y3zok2ryVyZoiBu3"}}                       |
| 1.00007E+18  | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"8DN0dM4rlvJxt4oByYLKZ/wuHyq/8CvsWNyXvGYnImytXn/bjUizfRSl86vmju7MFMXxnhTBoCWLHtyVSWro9LYg0MhN8jGbswLRLXoOIyh2wduVbc9XeN8yyQElkJm3AW3zcqC7iXNVv2eBS8vwGg=="}} |
| 1.00008E+18  | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"KR+CC8TQzPyMOE/bk7EGgN3lSvP8OsxeI2aLaVrbaeLn8XK3y3zok2ryVyZoiBu3"}}                       |
```

## 機器人篩選的進階統計函式 {#statistical-functions-for-bot-filtering}

第二個範例以基本的SQL篩選為基礎，結合機器學習技術來調整臨界值並改善篩選準確性。 透過使用進階統計函式（例如回歸分析或群集演演算法），此方法引進了預測功能，可用於開發模型以更精確的方式處理複雜的資料集。

### 建立訓練資料集 {#build-a-training-dataset}

首先，準備具有機器學習模型可使用的平面和巢狀結構的資料集（如上所述）。 若要進一步瞭解如何執行此動作，請參閱[使用巢狀資料結構檔案](../../key-concepts/nested-data-structures.md)。 依時間戳記、使用者ID和網頁名稱將資料分組，以識別機器人活動中的模式。

### 使用TRANSFORM和OPTIONS子句建立模型 {#transform-and-preprocess}

若要轉換資料集並有效設定機器學習模型，請遵循下列步驟。 這些步驟詳細說明了如何處理Null值、準備特徵以及定義模型引數以獲得最佳效能。

>[!TIP]
>
>若要進一步瞭解使用轉換及預先處理資料，請參閱[功能轉換技術檔案](../feature-transformation.md)。

1. 若要在數值、字串及布林資料行中填入Null值，請分別使用`numeric_imputer`、`string_imputer`及`boolean_imputer`函式。 此步驟可確保機器學習演演算法處理資料時不會發生錯誤。
2. 套用特徵轉換來準備要建模的資料。 套用`binarized`、`quantile_discretizer`或`string_indexer`以分類或標準化資料行。 接著，將輸入程式（`numeric_imputer`和`string_imputer`）的輸出輸入到後續的轉換器，如`string_indexer`或`quantile_discretizer`，以建立有意義的功能。
3. 使用`vector_assembler`函式將轉換的資料行合併成單一功能資料行。 然後使用`min_max_scaler`來縮放功能，將值標準化以獲得更好的模型效能。 注意：在SQL範例中，TRANSFORM子句中提及的最後一個轉換會變成機器學習模型所使用的特徵資料行。
4. 在OPTIONS子句中指定模型型別和任何其他超引數。 例如，在此選擇`decision_tree_classifier`，因為這是分類問題。 已調整(`MAX_DEPTH=4`)其他引數（例如`max_depth`）以調整模型，以獲得更好的效能。
5. 結合特徵並標籤輸出資料。 使用SELECT子句指定要訓練的資料集。 此子句應包含功能資料行(`count_per_id`、`web`、`id`)和標籤資料行(`isBot`)，以指出動作是否可能是機器人。

您的陳述式可能如下列範例所示。

```sql
CREATE MODEL bot_filtering_model
TRANSFORM (
  numeric_imputer(count_per_id.one_minute, 'mean') imputed_one_minute,
  numeric_imputer(count_per_id.five_minute, 'mode') imputed_five_minute,
  numeric_imputer(count_per_id.thirty_minute) imputed_thirty_minute,
  string_imputer(id, 'unknown') imputed_id,
  string_indexer(imputed_id) si_id,
  quantile_discretizer(imputed_five_minute) buckets_five,
  string_indexer(web.webpagedetails.NAME) si_name,
  quantile_discretizer(imputed_thirty_minute) buckets_thirty,
  vector_assembler(array(si_id, imputed_one_minute, buckets_five, si_name, buckets_thirty)) features,
  min_max_scaler(features) scaled_features
)
OPTIONS (model_type='decision_tree_classifier', max_depth=4, label='isBot')
AS
SELECT count_per_id, isBot, web, id FROM analytics_events_clicks_count_criteria;
```

**結果**

在下方顯示的結果中，模型`bot_filtering_model`已成功以唯一識別碼、名稱和版本建立。 此輸出可作為追蹤和管理模型的參考。 使用這些參考資料來識別預測或評估所需的確切設定和版本。

```console
           Created Model ID           |       Created Model       | Version
--------------------------------------+---------------------------+---------
 2fb4b49e-d35c-44cf-af19-cc210e7dc72c | bot_filtering_model       |       1
```

### 評估經過訓練的模型 {#evaluate-trained-model}

建立模型之後，請使用`MODEL_EVALUATE`命令來評估其效能。 此步驟可確保模型符合偵測機器人活動的精確度和效能需求。

在SQL命令中使用下列引數來評估模型：

1. 指定模型名稱(`bot_filtering_model`)以指示要評估的模型。 此名稱必須符合您先前使用`CREATE MODEL`命令建立的名稱。
2. 在第二個引數中提供模型版本(`1`)，以指定您要評估的模型版本。 如果存在多個版本，這可確保使用正確的版本。
3. 加入評估資料集，以定義要評估的資料集。 請確定資料集包含訓練期間使用的相同功能資料行(`count_per_id`、`web`、`id`)和標籤資料行(`isBot`)。

>[!NOTE]
>
>在模型訓練期間套用的轉換會在評估期間自動套用。

```sql
SELECT *
FROM   model_evaluate(bot_filtering_model, 1,
                      SELECT count_per_id, isBot, web, id
                      FROM   analytics_events_clicks_count_criteria);
```

**結果**

回應包括準確度、精確度、召回率和AUC-ROC等量度。 結果會確認模型是否執行良好。

>[!NOTE]
>
>0至1範圍內的值表示比例或機率，1.0表示完美效能。

```console
auc_roc | accuracy | precision | recall
---------+----------+-----------+--------
     1.0 |      1.0 |       1.0 |    1.0
```

| **量度** | **說明** |
|--------------|-----------------------------------------------------------------------------------------------------|
| `auc_roc` | 此量度會指出模型分類機器人與非機器人的效率。 它廣泛用於評估分類模型。 |
| `accuracy` | 模型所做的正確預測的百分比。 |
| `precision` | 所有預測機器人中的真實機器人預測比例。 |
| `recall` | 在所有實際機器人中偵測到的真實機器人比例。 |

>[!TIP]
>
>若要用於生產沙箱，請考慮在測試資料集上評估模型，以確保它有效地泛化。

### 預測機器人活動 {#predict-bot-activity}

將`MODEL_PREDICT`命令與訓練好的模型搭配使用，以識別哪些使用者(`id`)是機器人。 請依照下列步驟產生識別機器人活動的預測：

1. 在第一個引數中使用模型名稱(`bot_filtering_model`)來指定要用於預測的模型。
2. 在第二個引數中指定模型版本(`1`)，以確保使用正確的模型版本。
3. 若要為預測提供正確的資料，請使用SELECT陳述式來指定功能資料行(`count_per_id`、`web`、`id`)。 不要包含標籤欄(`isBot`)，因為模型將會產生此欄位的預測。

```sql
SELECT *
FROM model_predict(bot_filtering_model, 1,
    SELECT count_per_id, web, id FROM analytics_events_clicks_count_criteria
);
```

**結果**

回應包括每個使用者(`id`)的預測，以及有關其活動和模型分類結果的詳細資訊。 此輸出可讓您詳細檢查使用者行為以及模型的機器人活動分類。

<!-- Q) Anil, why is there no ID in the first two rows? Can we get that info? Or should it be the same as the other IDs? -->

```console
         id          | count.one_minute | count.five_minute | count.thirty_minute |                                                                  web.webpagedetails.name                                                                  | prediction
---------------------+------------------+-------------------+---------------------+-------+----------------------------------------------------------------------------------------------------------------------------------------------------+------------
                     |              110 |                   |                     |   4UNDilcY5VAgu2pRmX4/gtVnj+YxDDQaJd1G8p8WX46//wYcrHy+APUN0I556E80j1gIzFmilA6DV4s0Zcs4ruiP36gLgC7bj4TH0q6LU0E=                                             |        1.0  
                     |              105 |                   |                     |   lrSaZk04Yq+5P9+6l4BohwXik0s0/XeW9X28ZgWt1yj1QQztiAt9Qgt2WYrWcAeoGZChAJw/l8e4ojZDT5WHCjteSt35S01Vv1JzDGPAg+IyhIzMTsVyLpW8WWpXjJoMCt6Tv7fFdF73EIH+IrK5fA== |        1.0
 2553215812530219515 |               99 |                 1 |                   1 |   KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg==                                                                 |        1.0
 2553215812530219515 |               99 |                 1 |                   1 |   KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg==                                                                 |        1.0
```

下表說明每個量度：

| 欄名稱 | 說明 |
|---------------------------|----------------------------------------------------------------------------------------------------------|
| `id` | 每個使用者的唯一識別碼。 |
| `count.one_minute` | 1分鐘間隔的彙總點按計數。 |
| `count.five_minute` | 5分鐘間隔的彙總點按計數。 |
| `count.thirty_minute` | 30分鐘間隔的彙總點按計數。 |
| `web.webpagedetails.name` | 造訪的網頁名稱。 這會提供使用者活動的內容。 |
| `prediction` | 模型的預測。 `1.0`結果表示使用者根據其活動模式標示為機器人。 |

## 管理您的模型 {#manage-models}

若要管理您的機器學習模型，請使用下節中列出的SQL關鍵字。

### 列出可用的模型 {#list-available-models}

使用`SHOW MODELS;`命令有效地管理和檢閱模型。 這個指令會列出已在目前工作區中建立的所有機器學習模型。 輸出提供可用模型的概覽，並包括其名稱、版本和其他中繼資料。

```sql
SHOW MODELS;
```

### 刪除模型 {#delete-models}

若要釋放資源並確保只保留相關的模型，請使用`DROP MODEL`命令移除過時或不必要的模型。 這個命令會刪除在關鍵字之後指定的任何機器學習模型。 在下列範例中，`bot_filtering_model`已從系統中移除。

```sql
DROP MODEL bot_filtering_model;
```

## 後續步驟

閱讀本檔案後，您已瞭解如何使用SQL和機器學習技術(使用Data Distiller方法)來識別和篩選機器人活動。 接下來，將這些概念套用至您的資料集，並自動化模型重新訓練，以持續改進。
