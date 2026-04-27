---
title: Engineer Features for Machine Learning
description: Learn how to transform data in Adobe Experience Platform into features or variables that can be consumed by a machine learning model. Use Data Distiller to compute ML features at scale and share those features with your machine learning environment.
exl-id: 7fe017c9-ec46-42af-ac8f-734c4c6e24b5
source-git-commit: f2d81f05c8c19c6f28849fc4dbe9bfa26be64645
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 18%

---

# Engineer features for machine learning

This document demonstrates how you can transform data in Adobe Experience Platform into **features**, or variables, that can be consumed by a machine learning model. This process is referred to as **feature engineering**. Use Data Distiller to compute ML features at scale and share those features to your machine learning environment. This involves the following:

1. Create a query template to define the target labels and features you want to compute for your model
2. Execute the query and store the results in a training dataset

## Define your training data {#define-training-data}

The following example illustrates a query to derive training data from an Experience Events dataset for a model to predict the propensity of a user to subscribe to a newsletter. Subscription events are represented by the event type `web.formFilledOut`, and other behavioral events in the dataset are used to derive profile-level features to predict subscriptions.

### Query positive and negative labels {#query-positive-and-negative-labels}

A complete dataset for training a (supervised) machine learning model includes target variable or label that represents the outcome to be predicted, and a set of features or explanatory variables used to describe the example profiles used to train the model.

In this case, the label is a variable called `subscriptionOccurred` which equals 1 if the user profile has an event with type `web.formFilledOut` , and 0 otherwise. The following query returns a set of 50,000 users from the events dataset, including all users with positive labels (`subscriptionOccurred = 1`) plus a set randomly selected user with negative labels to complete the 50,000 user sample size. This ensures that the training data includes both positive and negative examples for the model to learn from.

```python
from aepp import queryservice

dd_conn = queryservice.QueryService().connection()
dd_cursor = queryservice.InteractiveQuery2(dd_conn)

query_labels = f"""
SELECT *
FROM (
    SELECT
        eventType,
        _{tenant_id}.user_id as userId,
        SUM(CASE WHEN eventType='web.formFilledOut' THEN 1 ELSE 0 END) 
            OVER (PARTITION BY _{tenant_id}.user_id) 
            AS "subscriptionOccurred",
        row_number() OVER (PARTITION BY _{tenant_id}.user_id ORDER BY randn()) AS random_row_number_for_user
    FROM {table_name}
)
WHERE (subscriptionOccurred = 1 AND eventType = 'web.formFilledOut') OR (subscriptionOccurred = 0 AND random_row_number_for_user = 1)
"""

df_labels = dd_cursor.query(query_labels, output="dataframe")
print(f"Number of classes: {len(df_labels)}")
df_labels.head()
```

**Sample output**

Number of classes: 50000

|   | eventType | userId | subscriptionOccurred | random_row_number_for_user |
| ---  |   ---  |   ---  |   ---  |   --- |
| 0 | directMarketing.emailClicked | 01027994177972439148069092698714414382 | 0 | 1 |
| 1 | directMarketing.emailOpened | 01054714817856066632264746967668888198 | 0 | 1 |
| 2 | web.formFilledOut | 01117296890525140996735553609305695042 | 1 | 15 |
| 3 | directMarketing.emailClicked | 01149554820363915324573708359099551093 | 0 | 1 |
| 4 | directMarketing.emailClicked | 01172121447143590196349410086995740317 | 0 | 1 |

{style="table-layout:auto"}

### Aggregate events to define features for ML {#define-features}

With an appropriate query you can gather the events in the dataset into meaningful, numerical features that can be used to train a propensity model. Example events are seen below:

- **Number of emails** that were sent for marketing purposes and received by the user.
- Portion of these emails that were **opened**.
- Portion of these emails where the user **selected** the link.
- **Number of products** that were viewed.
- Number of **propositions that were interacted with**.
- Number of **propositions that were dismissed**.
- Number of **links that were selected**.
- Number of minutes between two consecutive emails received.
- Number of minutes between two consecutive emails opened.
- Number of minutes between two consecutive emails where the user actually selected the link.
- Number of minutes between two consecutive product views.
- Number of minutes between two propositions that were interacted with.
- Number of minutes between two propositions that were dismissed.
- Number of minutes between two links that were selected.

The following query aggregates these events:

+++Select to view example query

```python
query_features = f"""
SELECT
    _{tenant_id}.user_id as userId,
    SUM(CASE WHEN eventType='directMarketing.emailSent' THEN 1 ELSE 0 END) 
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "emailsReceived",
    SUM(CASE WHEN eventType='directMarketing.emailOpened' THEN 1 ELSE 0 END) 
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "emailsOpened",       
    SUM(CASE WHEN eventType='directMarketing.emailClicked' THEN 1 ELSE 0 END) 
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "emailsClicked",       
    SUM(CASE WHEN eventType='commerce.productViews' THEN 1 ELSE 0 END) 
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "productsViewed",       
    SUM(CASE WHEN eventType='decisioning.propositionInteract' THEN 1 ELSE 0 END) 
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "propositionInteracts",       
    SUM(CASE WHEN eventType='decisioning.propositionDismiss' THEN 1 ELSE 0 END) 
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "propositionDismissed",
    SUM(CASE WHEN eventType='web.webinteraction.linkClicks' THEN 1 ELSE 0 END) 
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "webLinkClicks" ,
    TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailSent', 'minutes')
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "minutes_since_emailSent",
    TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailOpened', 'minutes')
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "minutes_since_emailOpened",
    TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailClicked', 'minutes')
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "minutes_since_emailClick",
    TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'commerce.productViews', 'minutes')
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "minutes_since_productView",
    TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'decisioning.propositionInteract', 'minutes')
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "minutes_since_propositionInteract",
    TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'propositionDismiss', 'minutes')
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "minutes_since_propositionDismiss",
    TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'web.webinteraction.linkClicks', 'minutes')
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "minutes_since_linkClick"
FROM {table_name}
"""

df_features = dd_cursor.query(query_features, output="dataframe")
df_features.head()
```

+++

**Sample output**

|   | userId | emailsReceived | 電子郵件已開啟 | 電子郵件已點按 | 已檢視的產品 | propositionInteracts | propositionMissed | webLinkClicks | minutes_since_emailSent | minutes_since_emailOpen | minutes_since_emailClick | minutes_since_productView | minutes_since_propositionInteract | minutes_since_propositionDiscisse | minutes_since_linkClick |
| --- |    --- |    ---   |  ---  |   ---  |   ---  |  ---  |  ---  |   ---  |   ---  |   ---  |   ---  |   ---  |   ---  |   ---  |   --- |
| 0 | 01102546977582484968046916668339306826 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0.0 | NaN | NaN | NaN | NaN | None | NaN |
| 1 | 01102546977582484968046916668339306826 | 2 | 0 | 0 | 0 | 0 | 0 | 0 | 0.0 | NaN | NaN | NaN | NaN | None | NaN |
| 2 | 01102546977582484968046916668339306826 | 3 | 0 | 0 | 0 | 0 | 0 | 0 | 0.0 | NaN | NaN | NaN | NaN | None | NaN |
| 3 | 01102546977582484968046916668339306826 | 3 | 1 | 0 | 0 | 0 | 0 | 0 | 540.0 | 0.0 | NaN | NaN | NaN | None | NaN |
| 4 | 01102546977582484968046916668339306826 | 3 | 2 | 0 | 0 | 0 | 0 | 0 | 588.0 | 0.0 | NaN | NaN | NaN | None | NaN |

{style="table-layout:auto"}

#### 結合標籤和功能查詢 {#combine-queries}

最後，標籤查詢和功能查詢可以合併到單一查詢中，以傳回標籤和功能的訓練資料集：

+++選取以檢視範例查詢

```python
query_training_set = f"""
SELECT *
FROM (
    SELECT _{tenant_id}.user_id as userId, 
       eventType,
       timestamp,
       SUM(CASE WHEN eventType='web.formFilledOut' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id) 
           AS "subscriptionOccurred",
       SUM(CASE WHEN eventType='directMarketing.emailSent' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsReceived",
       SUM(CASE WHEN eventType='directMarketing.emailOpened' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsOpened",       
       SUM(CASE WHEN eventType='directMarketing.emailClicked' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsClicked",       
       SUM(CASE WHEN eventType='commerce.productViews' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "productsViewed",       
       SUM(CASE WHEN eventType='decisioning.propositionInteract' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "propositionInteracts",       
       SUM(CASE WHEN eventType='decisioning.propositionDismiss' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "propositionDismissed",
       SUM(CASE WHEN eventType='web.webinteraction.linkClicks' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "webLinkClicks" ,
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailSent', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailSent",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailOpened', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailOpened",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailClicked', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailClick",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'commerce.productViews', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_productView",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'decisioning.propositionInteract', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_propositionInteract",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'propositionDismiss', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_propositionDismiss",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'web.webinteraction.linkClicks', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_linkClick",
        row_number() OVER (PARTITION BY _{tenant_id}.user_id ORDER BY randn()) AS random_row_number_for_user
    FROM {table_name} LIMIT 1000
)
WHERE (subscriptionOccurred = 1 AND eventType = 'web.formFilledOut') OR (subscriptionOccurred = 0 AND random_row_number_for_user = 1)
ORDER BY timestamp
"""

df_training_set = dd_cursor.query(query_training_set, output="dataframe")
df_training_set.head()
```

+++

**範例輸出**

|  | userId | eventType | 時間戳記 | subscriptionOcked | 電子郵件已接收 | 電子郵件已開啟 | 電子郵件已點按 | 已檢視的產品 | propositionInteracts | propositionMissed | webLinkClicks | minutes_since_emailSent | minutes_since_emailOpen | minutes_since_emailClick | minutes_since_productView | minutes_since_propositionInteract | minutes_since_propositionDiscisse | minutes_since_linkClick | random_row_number_for_user |
| ---  |  --- |   ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---   | ---  |  ---  |  ---  |  --- |
| 0 | 02554909162592418347780983091131567290 | directMarketing.emailSent | 2023-06-17 13:44:59.086 | 0 | 2 | 0 | 0 | 0 | 0 | 0 | 0 | 0.0 | NaN | NaN | NaN | NaN | None | NaN | 1 |
| 1 | 01130334080340815140184601481559659945 | directMarketing.emailOpen | 2023-06-19 06:01:55.366 | 0 | 1 | 3 | 0 | 1 | 0 | 0 | 0 | 1921.0 | 0.0 | NaN | 1703.0 | NaN | None | NaN | 1 |
| 2 | 01708961660028351393477273586554010192 | web.formFilledOut | 2023-06-19 18:36:49.083 | 1 | 1 | 2 | 2 | 0 | 0 | 0 | 0 | 2365.0 | 26.0 | 1.0 | NaN | NaN | None | NaN | 7 |
| 3 | 01809182902320674899156240602124740853 | directMarketing.emailSent | 2023-06-21 19:17:12.535 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0.0 | NaN | NaN | NaN | NaN | None | NaN | 1 |
| 4 | 03441761949943678951106193028739001197 | directMarketing.emailSent | 2023-06-21 21:58:29.482 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0.0 | NaN | NaN | NaN | NaN | None | NaN | 1 |

{style="table-layout:auto"}

## 建立查詢範本以逐步計算培訓資料

通常使用更新的訓練資料定期重新訓練模型，以隨著時間保持模型的準確性。 為了有效更新您的訓練資料集，最佳實務是透過訓練集查詢建立範本，以增量方式計算新的訓練資料。 這可讓您僅從上次更新訓練資料以來新增至原始體驗事件資料集的資料計算標籤和功能，並將新標籤和功能插入現有訓練資料集。

若要這麼做，需要對訓練集查詢進行一些修改：

- 新增邏輯以建立不存在的新訓練資料集，否則請將新標籤和功能插入現有訓練資料集中。 這需要訓練集查詢的一系列兩個版本：
   - 首先，使用`CREATE TABLE IF NOT EXISTS {table_name} AS`陳述式
   - 接著，針對訓練資料集已存在的情況使用`INSERT INTO {table_name}`陳述式
- 新增`SNAPSHOT BETWEEN $from_snapshot_id AND $to_snapshot_id`陳述式，將查詢限制在指定間隔內新增的事件資料。 快照ID上的`$`首碼表示它們是在執行查詢範本時要傳入的變數。

套用這些變更會導致下列查詢：

+++選取以檢視範例查詢

```python
ctas_table_name = "propensity_training_set"

query_training_set_template = f"""
$$ BEGIN

SET @my_table_exists = SELECT table_exists('{ctas_table_name}');

CREATE TABLE IF NOT EXISTS {ctas_table_name} AS
SELECT *
FROM (
    SELECT _{tenant_id}.user_id as userId, 
       eventType,
       timestamp,
       SUM(CASE WHEN eventType='web.formFilledOut' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id) 
           AS "subscriptionOccurred",
       SUM(CASE WHEN eventType='directMarketing.emailSent' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsReceived",
       SUM(CASE WHEN eventType='directMarketing.emailOpened' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsOpened",       
       SUM(CASE WHEN eventType='directMarketing.emailClicked' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsClicked",       
       SUM(CASE WHEN eventType='commerce.productViews' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "productsViewed",       
       SUM(CASE WHEN eventType='decisioning.propositionInteract' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "propositionInteracts",       
       SUM(CASE WHEN eventType='decisioning.propositionDismiss' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "propositionDismissed",
       SUM(CASE WHEN eventType='web.webinteraction.linkClicks' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "webLinkClicks" ,
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailSent', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailSent",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailOpened', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailOpened",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailClicked', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailClick",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'commerce.productViews', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_productView",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'decisioning.propositionInteract', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_propositionInteract",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'propositionDismiss', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_propositionDismiss",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'web.webinteraction.linkClicks', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_linkClick",
        row_number() OVER (PARTITION BY _{tenant_id}.user_id ORDER BY randn()) AS random_row_number_for_user
    FROM {table_name}
    SNAPSHOT BETWEEN $from_snapshot_id AND $to_snapshot_id
)
WHERE (subscriptionOccurred = 1 AND eventType = 'web.formFilledOut') OR (subscriptionOccurred = 0 AND random_row_number_for_user = 1)
ORDER BY timestamp;

INSERT INTO {ctas_table_name}
SELECT *
FROM (
    SELECT _{tenant_id}.user_id as userId, 
       eventType,
       timestamp,
       SUM(CASE WHEN eventType='web.formFilledOut' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id) 
           AS "subscriptionOccurred",
       SUM(CASE WHEN eventType='directMarketing.emailSent' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsReceived",
       SUM(CASE WHEN eventType='directMarketing.emailOpened' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsOpened",       
       SUM(CASE WHEN eventType='directMarketing.emailClicked' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsClicked",       
       SUM(CASE WHEN eventType='commerce.productViews' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "productsViewed",       
       SUM(CASE WHEN eventType='decisioning.propositionInteract' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "propositionInteracts",       
       SUM(CASE WHEN eventType='decisioning.propositionDismiss' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "propositionDismissed",
       SUM(CASE WHEN eventType='web.webinteraction.linkClicks' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "webLinkClicks" ,
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailSent', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailSent",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailOpened', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailOpened",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailClicked', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailClick",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'commerce.productViews', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_productView",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'decisioning.propositionInteract', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_propositionInteract",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'propositionDismiss', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_propositionDismiss",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'web.webinteraction.linkClicks', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_linkClick",
        row_number() OVER (PARTITION BY _{tenant_id}.user_id ORDER BY randn()) AS random_row_number_for_user
    FROM {table_name}
    SNAPSHOT BETWEEN $from_snapshot_id AND $to_snapshot_id
)
WHERE 
    @my_table_exists = 't' AND
    ((subscriptionOccurred = 1 AND eventType = 'web.formFilledOut') OR (subscriptionOccurred = 0 AND random_row_number_for_user = 1))
ORDER BY timestamp;

EXCEPTION
  WHEN OTHERS THEN
    SELECT 'ERROR';

END $$;
"""
```

+++

最後，下列程式碼會將查詢範本儲存在Data Distiller中：

```python
template_res = dd.createQueryTemplate({
  "sql": query_training_set_template,
  "queryParameters": {},
  "name": "Template for propensity training data"
})
template_id = template_res["id"]

print(f"Template for propensity training data created as ID {template_id}")
```

**範例輸出**

`Template for propensity training data created as ID f3d1ec6b-40c2-4d13-93b6-734c1b3c7235`

在儲存範本後，您可以透過參考範本ID來隨時執行查詢，並指定應包含在查詢中的快照ID範圍。 下列查詢會擷取原始Experience Events資料集的快照：

```python
query_snapshots = f"""
SELECT snapshot_id 
FROM (
    SELECT history_meta('{table_name}')
) 
WHERE is_current = true OR snapshot_generation = 0 
ORDER BY snapshot_generation ASC
"""

df_snapshots = dd_cursor.query(query_snapshots, output="dataframe")
```

下列程式碼會示範如何使用第一個和最後一個快照來查詢整個資料集，進而執行查詢範本：

```python
snapshot_start_id = str(df_snapshots["snapshot_id"].iloc[0])
snapshot_end_id = str(df_snapshots["snapshot_id"].iloc[1])

query_final_res = qs.postQueries(
    name=f"[CMLE][Week2] Query to generate training data created by {username}",
    templateId=template_id,
    queryParameters={
        "from_snapshot_id": snapshot_start_id,
        "to_snapshot_id": snapshot_end_id,
    },
    dbname=f"{cat_conn.sandbox}:all"
)
query_final_id = query_final_res["id"]
print(f"Query started successfully and got assigned ID {query_final_id} - it will take some time to execute")
```

**範例輸出**

`Query started successfully and got assigned ID c6ea5009-1315-4839-b072-089ae01e74fd - it will take some time to execute`

您可以定義以下函式以定期檢查查詢的狀態：

```python
def wait_for_query_completion(query_id):
    while True:
        query_info = qs.getQuery(query_id)
        query_state = query_info["state"]
        if query_state in ["SUCCESS", "FAILED"]:
            break
        print("Query is still in progress, sleeping…")
        time.sleep(60)

    duration_secs = query_info["elapsedTime"] / 1000
    if query_state == "SUCCESS":
        print(f"Query completed successfully in {duration_secs} seconds")
    else:
        print(f"Query failed with the following errors:", file=sys.stderr)
        for error in query_info["errors"]:
            print(f"Error code {error['code']}: {error['message']}", file=sys.stderr)

wait_for_query_completion(query_final_id)
```

**範例輸出**

```console
Query is still in progress, sleeping…
Query is still in progress, sleeping…
Query is still in progress, sleeping…
Query is still in progress, sleeping…
Query is still in progress, sleeping…
Query is still in progress, sleeping…
Query is still in progress, sleeping…
Query is still in progress, sleeping…
Query completed successfully in 473.8 seconds
```

## 後續步驟：

閱讀本檔案後，您已瞭解如何將Adobe Experience Platform中的資料轉換為機器學習模型可以使用的功能或變數。 從Experience Platform建立功能管道以饋送機器學習環境中的自訂模型時，下一個步驟是[匯出功能資料集](./export-data.md)。
