---
title: 使用Adobe Target進行活動分析
description: 本檔案說明如何使用Query Service從以Adobe Target資料建立的資料集中建立可操作的深入分析。
exl-id: a5181ee2-1e1c-405d-8dfe-5a32c28ac9f1
source-git-commit: d573c01a0aa9989f581796a0be4aec6904ffc569
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 3%

---

# 使用Adobe Target進行活動分析

Adobe Experience Platform可讓您使用Experience Data Model(XDM)欄位從Adobe Target內嵌資料，以建立資料集以搭配Query Service使用。 由於Adobe Target的設計目的是自訂內容並個人化使用者體驗，因此透過SQL分析使用者活動，在這些資料集上執行查詢可提供高度個人化且專注的深入分析。

本文檔提供了各種示例SQL查詢，這些查詢基於客戶的行為和特性演示常見的使用案例。

## 快速入門

對於以下每個使用案例，都將提供參數化SQL查詢示例作為模板，供您自定義。 無論您在哪裡看到，都提供參數 `{ }` 在您想要評估的SQL示例中。

## 高階部分XDM欄位對應

下表列出常見的Target欄位及其對應的對應XDM欄位。

>[!NOTE]
>
>使用 `[ ]` 在「XDM」欄位內表示陣列。

| 目標欄位名稱 | XDM欄位名稱 | 附註 |
|---|---|---|
| `mboxName` | `_experience.target.mboxname` | 不適用 |
| 活動 ID | `_experience.target.activities.activityID` | 不適用 |
| 體驗 ID | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID` | 不適用 |
| 區段ID | `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id` | 不適用 |
| 事件範圍 | `_experience.target.activities[].activityEvents[].eventScope` | 此欄位會追蹤新訪客和造訪。 |
| 步驟ID | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID` | 此欄位是Adobe Campaign的自訂步驟ID。 |
| 價格總計 | commerce.order.priceTotal | 不適用 |

>[!IMPORTANT]
>
>使用Target資料自動建立的資料集名稱為「Adobe Target Experience Events」。 使用此資料集進行查詢時，請使用名稱 `adobe_target_experience_events`.

## 目標

透過分析使用者活動，您可以個人化特定對象的內容，並測試個別實體的不同版本內容。 此外，通過分析指定時段內或針對個別使用者的特定活動，可更清楚地了解每個個別活動的效能。 這種組合分析的結果可以用來了解每個活動的效能。

下列個人化使用案例是使用Adobe Target資料建立，並著重於使用者活動，以針對客戶在業務應用程式上的行為建立有價值的深入分析。

本指南透過使用案例範例說明下列重要概念：

* 了解指定日期的活動ID效能，例如計數、詳細資料和相關的體驗ID。
* 決定活動的訪客和事件範圍。
* 收集體驗ID、區段ID和活動ID的訪客數、造訪次數和曝光資訊。

### 產生指定日的每小時活動計數

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

### 生成特定的每小時詳細資訊

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

### 決定指定日期特定活動的體驗ID清單

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

### 傳回指定日內每個活動ID的事件範圍（訪客、造訪、曝光）例項清單

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

### 決定指定日內每個活動的訪客數、造訪次數和曝光數

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

### 決定指定日期的體驗ID、區段ID和EventScope的訪客、造訪和曝光數

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

### 傳回指定日期的mbox名稱和記錄計數

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
