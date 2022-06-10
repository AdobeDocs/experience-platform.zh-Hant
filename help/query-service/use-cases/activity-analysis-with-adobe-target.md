---
title: 活動分析與Adobe Target
description: 本文檔介紹如何使用查詢服務從使用您的Adobe Target資料建立的資料集中建立可操作的洞見。
source-git-commit: 870626f25b1aabdcb5739bbb1ab85bdad44df195
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 3%

---

# Adobe Target活動分析

Adobe Experience Platform允許您使用「體驗資料模型」(XDM)欄位從Adobe Target接收資料，以建立資料集，以便與查詢服務一起使用。 由於Adobe Target旨在定制內容並個性化用戶體驗，因此運行在這些資料集上的查詢通過通過SQL分析用戶活動，可提供高度個性化和集中的見解。

本文檔提供了各種SQL查詢示例，這些示例查詢基於客戶的行為和特徵演示了常見的使用案例。

## 快速入門

對於以下每種使用情形，都會提供一個參數化SQL查詢示例作為模板供您自定義。 無論您看到什麼位置都提供參數 `{ }` 在您感興趣的SQL示例中。

## 高級部分XDM欄位映射

下表列出了常用目標欄位及其映射到的相應XDM欄位。

>[!NOTE]
>
>使用 `[ ]` 在XDM欄位中表示一個陣列。

| 目標欄位名 | XDM欄位名 | 附註 |
|---|---|---|
| `mboxName` | `_experience.target.mboxname` | 不適用 |
| 活動 ID | `_experience.target.activities.activityID` | 不適用 |
| 體驗 ID | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID` | 不適用 |
| 段ID | `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id` | 不適用 |
| 事件範圍 | `_experience.target.activities[].activityEvents[].eventScope` | 這個領域跟蹤新的訪問者和訪問者。 |
| 步驟ID | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID` | 此欄位是Adobe Campaign的自定義步驟ID。 |
| 價格合計 | commerce.order.priceTotal | 不適用 |

>[!IMPORTANT]
>
>使用目標資料自動建立的資料集的名稱是「Adobe Target體驗事件」。 將此資料集與查詢一起使用時，請使用名稱 `adobe_target_experience_events`。

## 目標

通過分析用戶活動，您可以個性化特定受眾的內容，並為單個實體test不同版本的內容。 此外，通過分析給定時間段內的特定活動或針對單個用戶的特定活動，可以更清楚地瞭解每個單個活動的效能。 此組合分析的結果可用於瞭解每個單獨活動的效能。

以下個性化使用案例是使用Adobe Target資料建立的，並側重於用戶活動，以便對客戶在業務應用程式上的行為進行有價值的洞見。

本指南通過用例示例說明了以下主要概念：

* 瞭解給定日的活動ID的效能，如計數、詳細資訊和關聯的體驗ID。
* 確定活動的訪問者和事件範圍。
* 要收集「體驗ID」、「段ID」和「活動ID」的訪問者數、訪問次數和印象資訊。

### 生成給定日的每小時活動計數

```sql
SELECT
  Hour,
  ActivityID,
  COUNT(ActivityID) AS Instances
FROM
(
  SELECT
    date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
    EXPLODE(_experience.target.activities.activityID) AS ActivityID
  FROM adobe_target_experience_events
  WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, ActivityID
ORDER BY Hour DESC, Instances DESC
LIMIT 24
```

### 為特定生成小時詳細資訊

```sql
SELECT
  date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
  _experience.target.activities.activityID AS ActivityID,
  COUNT(ActivityID) AS Instances
FROM adobe_target_experience_events
WHERE
  array_contains( _experience.target.activities.activityID, {Activity ID} ) AND
    TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
  _experience.target.activities IS NOT NULL
GROUP BY Hour, ActivityID
ORDER BY Hour DESC
LIMIT 24
```

### 確定給定日的特定活動的體驗ID清單

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  COUNT(ExperienceID) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents._experience.target.activity.activityevent.context.experienceID) AS ExperienceID
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

### 按每個活動ID的實例返回給定日期的事件範圍（訪問者、訪問者、印象）清單

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  COUNT(ExperienceID) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents._experience.target.activity.activityevent.context.experienceID) AS ExperienceID
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

### 確定給定一天內每個活動的訪問者、訪問次數和觀感數

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  COUNT(ExperienceID) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents._experience.target.activity.activityevent.context.experienceID) AS ExperienceID
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

### 確定給定日期的體驗ID、段ID和EventScope的訪問者、訪問和印象

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  SegmentID._id,
  SUM(CASE WHEN ActivityEvent.eventScope = 'visitor' THEN 1 END) as Visitors,
  SUM(CASE WHEN ActivityEvent.eventScope = 'visit' THEN 1 END) as Visits,
  SUM(CASE WHEN ActivityEvent.eventScope = 'impression' THEN 1 END) as Impressions
FROM
(
  SELECT
    Day,
    Activities,
    ActivityEvent,
    ActivityEvent._experience.target.activity.activityevent.context.experienceID AS ExperienceID,
    EXPLODE(ActivityEvent.segmentEvents.segmentID) AS SegmentID
  FROM
  (
    SELECT
      Day,
      Activities,
      EXPLODE(Activities.activityEvents) AS ActivityEvent
    FROM
    (
      SELECT
        date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
        EXPLODE(_experience.target.activities) AS Activities
      FROM adobe_target_experience_events
      WHERE
        TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
        _experience.target.activities IS NOT NULL
      LIMIT 1000000
    )
    LIMIT 1000000
  )
  LIMIT 1000000
)
GROUP BY Day, Activities.activityID, ExperienceID, SegmentID._id
ORDER BY Day DESC, Activities.activityID, ExperienceID ASC, SegmentID._id ASC, Visitors DESC
LIMIT 20
```

### 返回給定日期的框名稱和記錄計數

```sql
SELECT
  _experience.target.mboxname,
  COUNT(timestamp) AS records
FROM
  adobe_target_experience_events
WHERE
  TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
  GROUP BY _experience.target.mboxname ORDER BY records DESC
LIMIT 100
```
