---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 範例查詢
topic: queries
translation-type: tm+mt
source-git-commit: 33282b1c8ab1129344bd4d7054e86fed75e7b899

---


# Adobe Target資料的範例查詢

來自Adobe Target的資料會轉換為Experience Event XDM架構，並以資料集的形式匯入Experience Platform。 Query Service使用此資料的使用案例很多，下列範例查詢應與您的Adobe Target資料集搭配使用。

>[!NOTE]
>在以下範例中，您需要編輯SQL，以根據您想要評估的資料集、變數或時間範圍，填寫您查詢的預期參數。 在SQL中查看的任何位 `{ }` 置都提供參數。

## 平台上Target資料來源的標準資料集名稱：

Adobe Target體驗事件（好記名稱） <br>`adobe_target_experience_events` （用於查詢的名稱）

## 高級部分XDM域映射

使用表 `[ ]` 示陣列

| 名稱 | XDM欄位 | 附註 |
| ---- | --------- | ----- |
| mboxName | `_experience.target.mboxname` |  |
| 活動 ID | `_experience.target.activities.activityID` |  |
| 體驗ID | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID` |  |
| 區段ID | `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id` |  |
| 事件範圍 | `_experience.target.activities[].activityEvents[].eventScope` | 追蹤新訪客和瀏覽 |
| 步驟ID | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID` | 促銷活動的自訂步驟ID |
| 總價 | `commerce.order.priceTotal` |  |

## 指定日的每小時活動計數

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
  WHERE
    _ACP_YEAR = {target_year} AND 
    _ACP_MONTH = {target_month} AND 
    _ACP_DAY = {target_day} AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, ActivityID
ORDER BY Hour DESC, Instances DESC
LIMIT 24
```

## 特定日期活動的每小時詳細資料

```sql
SELECT
  date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
  _experience.target.activities.activityID AS ActivityID,
  COUNT(ActivityID) AS Instances
FROM adobe_target_experience_events
WHERE
  array_contains( _experience.target.activities.activityID, {Activity ID} ) AND 
  _ACP_YEAR = {target_year} AND 
  _ACP_MONTH = {target_month} AND 
  _ACP_DAY = {target_day} AND 
  _experience.target.activities IS NOT NULL
GROUP BY Hour, ActivityID
ORDER BY Hour DESC
LIMIT 24
```

## 指定日期特定活動的體驗ID

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
      _ACP_YEAR = {target_year} AND 
      _ACP_MONTH = {target_month} AND 
      _ACP_DAY = {target_day} AND 
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

## 在指定的一天內，依每個活動ID的例項傳回事件範圍（訪客、瀏覽、曝光）清單

```sql
SELECT
  Day,
  Activities.activityID,
  EventScope,
  COUNT(EventScope) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents.eventScope) AS EventScope
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE 
      _ACP_YEAR = {target_year} AND 
      _ACP_MONTH = {target_month} AND 
      _ACP_DAY = {target_day} AND 
      _experience.target.activities IS NOT NULL
  )
)
GROUP BY Day, Activities.activityID, EventScope
ORDER BY Day DESC, Instances DESC
LIMIT 30
```

## 特定日期的訪客、瀏覽、每個活動的回訪計數

```sql
SELECT
  Hour,
  Activities.activityid,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'visitor' ) THEN 1 END) as Visitors,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'visit' ) THEN 1 END) as Visits,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'impression' ) THEN 1 END) as Impressions
FROM
(
  SELECT
    date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
    EXPLODE(_experience.target.activities) AS Activities
  FROM adobe_target_experience_events
  WHERE
    _ACP_YEAR = {target_year} AND 
    _ACP_MONTH = {target_month} AND 
    _ACP_DAY = {target_day} AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, Activities.activityid
ORDER BY Hour DESC, Visitors DESC
LIMIT 30
```

## 特定日期的回訪訪客、瀏覽、體驗ID、區段ID和EventScope的曝光數

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
        _ACP_YEAR = {target_year} AND
        _ACP_MONTH = {target_month} AND 
        _ACP_DAY = {target_day} AND 
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

## 傳回指定日期的mbox名稱和記錄計數

```sql
SELECT
  _experience.target.mboxname,
  COUNT(timestamp) AS records
FROM
  adobe_target_experience_events
WHERE
  _ACP_YEAR= {target_year} AND 
  _ACP_MONTH= {target_month} AND 
  _ACP_DAY= {target_day}
  GROUP BY _experience.target.mboxname ORDER BY records DESC
LIMIT 100
```
