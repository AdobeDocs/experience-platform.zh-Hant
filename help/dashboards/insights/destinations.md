---
title: 目的地分析
description: 探索為您的目的地深入分析提供支援的SQL，並使用這些查詢產生自訂深入分析，以進一步探索Adobe Experience Platform中的資料啟用。
exl-id: 762a9960-e7a5-4796-80c7-ef745157cc04
source-git-commit: d4baf6cfaa772e5d46cef470fb35818c7af868b1
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 2%

---

# 目的地分析

從資料模型分析衍生的深入解析可讓您的Adobe Real-time Customer Data Platform資料更易於存取、理解，並更能對決策產生影響。

存取支援目的地深入分析的SQL，然後產生您自己的深入分析，進一步探索如何從Adobe Experience Platform啟用資料至您的目的地平台，藉此瞭解您的目的地深入分析。 使用現有的Real-Time CDP資料模型SQL作為靈感，根據您獨特的業務需求建立查詢，將原始資料轉換為可採取行動的新見解。

請參閱 [檢視SQL檔案](../view-sql.md) 有關如何直接透過Platform UI調整您見解的SQL的詳細資訊。

下列見解全部都可供您用作 [目的地儀表板](../guides/destinations.md) 或自訂 [使用者定義儀表板](../user-defined-dashboards.md). 請參閱 [自訂概述](../customize/overview.md) 以取得如何自訂儀表板的指示，或 [建立和編輯新Widget](../customize/custom-widgets.md) 在Widget資料庫和 [使用者定義儀表板](../user-defined-dashboards.md#create-widget).

## 啟用的對象 {#activated-audiences}

此深入分析所回答的問題：

- 依特定目的地篩選的已啟用對象總數是多少？
- 每個目的地啟用的對象人數是多少？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT
  COUNT(segment_id) AS Activated_Audiences_Count
FROM
  qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE
  (
    SELECT
      MAX(process_date)
    FROM
      qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE
      process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
  ) BETWEEN start_date AND end_date
  AND destination_id = 1458738325;
```

+++

請參閱 [啟用的對象Widget檔案](../guides/destinations.md#activated-audiences) 以取得此深入分析的外觀和功能相關資訊。

## 跨所有目的地的已啟用對象 {#activated-audiences-across-all-destinations}

此深入分析所回答的問題：

- 在所有目的地啟用多少對象？
- 啟用的對象總數是多少？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT count(segment_id) AS Activated_Audiences_Count
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE
    (SELECT MAX(process_date)
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL' ) BETWEEN start_date AND end_date;
```

+++

請參閱 [所有目的地Widget檔案中的啟用對象](../guides/destinations.md#activated-audiences-across-all-destinations) 以取得此深入分析的外觀和功能相關資訊。

## 依目的地平台區分的有效目的地 {#active-destinations-by-destination-platform}

此深入分析所回答的問題：

- 使用中的目的地有幾個？
- 依目的地平台區分的有效目的地為何？
- 依每個目的地平台劃分的作用中目的地數量是多少？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT destination_platform_name AS Destination_Platform_Name,
       COUNT(destination_id) AS Active_Destinations_Count
  FROM qsaccel.profile_agg.adwh_dim_destination a
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination_platform b ON a.destination_platform_id = b.destination_platform_id
  WHERE destination_status='enabled'
  GROUP BY destination_platform_name
  ORDER BY Active_Destinations_Count DESC
  LIMIT 20;
```

+++

請參閱 [依目的地平台Widget檔案區分的有效目的地](../guides/destinations.md#active-destinations-by-destination-platform) 以取得此深入分析的外觀和功能相關資訊。

## 對象規模趨勢 {#audience-size-trend}

此深入分析所回答的問題：

- 對象人數如何隨著時間改變，包括對應至目的地的對象出現異常？
- 如何在30天、90天和12個月的指定期間內，依目的地找到對象人數的整體趨勢？
- 對象的主要特性是什麼造成大小，例如任何電子郵件行銷活動的尖峰？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT d.destination_name,
        d.destination,
        d.destination_id,
        b.segment_name,
        b.segment,
        c.segment_id,
        a.date_key,
        sum(a.count_of_profiles) AS profile_count
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations c ON a.segment_id = c.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination d ON c.destination_id = d.destination_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) f ON a.merge_policy_id = f.merge_policy_id
  WHERE a.date_key >= dateadd(DAY, -30-1, f.last_process_date)
    AND d.destination_id = -1275507046
    AND c.segment_id = -1452100519
  GROUP BY d.destination_name,
          d.destination,
          d.destination_id,
          b.segment_name,
          b.segment,
          c.segment_id,
          a.date_key;
```

+++

請參閱 [對象人數趨勢Widget檔案](../guides/destinations.md#audience-size-trend) 以取得此深入分析的外觀和功能相關資訊。

## 常見對象 {#common-audiences}

此深入分析所回答的問題：

- 兩個不同目的地之間有哪些共同受眾？
- 兩個不同目的地之間的每個共同對象有多少個設定檔？
- 兩個目的地對應到的最大受眾是哪個？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT k.destination_name1,
       k.destination_1,
       k.destination_id1,
       k.destination_name2,
       k.destination_2,
       k.destination_id2,
       b.segment_name,
       b.segment,
       b.segment_id,
       sum(a.count_of_profiles) AS profile_count
  FROM
    (SELECT i.destination_name AS destination_name1,
            i.destination AS destination_1,
            i.destination_id AS destination_id1,
            j.destination_name AS destination_name2,
            j.destination AS destination_2,
            j.destination_id AS destination_id2,
            i.segment_id
     FROM
       (SELECT b.destination_name,
               b.destination,
               b.destination_id,
               a.segment_id
        FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
        INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id=b.destination_id
        WHERE b.destination_id=1458738325) AS i
     INNER JOIN
       (SELECT b.destination_name,
               b.destination,
               b.destination_id,
               a.segment_id
        FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
        INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id=b.destination_id
        WHERE b.destination_id=-635802802) AS j ON i.segment_id=j.segment_id) AS k
  INNER JOIN qsaccel.profile_agg.adwh_fact_profile_by_segment a ON a.segment_id = k.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON b.segment_id = k.segment_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL'
     GROUP BY merge_policy_id) c ON a.merge_policy_id = c.merge_policy_id
  WHERE a.date_key = c.last_process_date
  GROUP BY k.destination_name1,
           k.destination_1,
           k.destination_id1,
           k.destination_name2,
           k.destination_2,
           k.destination_id2,
           b.segment_name,
           b.segment,
           b.segment_id
  ORDER BY profile_count DESC
  LIMIT 20;
```

+++

請參閱 [常見受眾Widget檔案](../guides/destinations.md#common-audiences) 以取得此深入分析的外觀和功能相關資訊。

## 目的地狀態 {#destination-status}

此深入分析所回答的問題：

- 已啟用使用的目的地總數是多少？
- 已停用的目的地總數是多少？
- 已啟用和已停用目的地之間的百分比分割為何？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT COUNT(CASE
                 WHEN destination_status='enabled' THEN 1
             END) AS count_of_active_destinations,
       COUNT(CASE
                 WHEN destination_status='disabled' THEN 1
             END) AS count_of_inactive_destinations
FROM qsaccel.profile_agg.adwh_dim_destination;
```

+++

請參閱 [目的地狀態Widget檔案](../guides/destinations.md#destination-status) 以取得此深入分析的外觀和功能相關資訊。

## 目的地計數 {#destinations-count}

此深入分析所回答的問題：

- 目前設定了多少目的地？
- 目的地總數在一段時間內有何變更？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT count(destination_id) AS total_number_of_destinations
  FROM qsaccel.profile_agg.adwh_dim_destination;
```

+++

請參閱 [目的地計數Widget檔案](../guides/destinations.md#destinations-count) 以取得此深入分析的外觀和功能相關資訊。

## 已對應對象的健康情況 {#mapped-audience-health}

此深入分析所回答的問題：

- 哪些對應至目的地的對象在過去30天內有重大變化？
- 對應對象的最新大小為何，以及上個月是否有變更？
- 我如何根據上個月大小變化的嚴重性，列出對應到目的地的所有對象？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT destination_name,
        SEGMENT,
        segment_id,
        segment_name,
        avg_profile_count,
        latest_profile_count,
        stddev_profile_count,
        profile_count_z_factor
  FROM
    (SELECT b.destination_name,
            f.segment_id,
            c.segment_name,
            c.segment,
            f.avg_profile_count,
            f.latest_profile_count,
            f.stddev_profile_count,
            CASE
                WHEN stddev_profile_count = 0 THEN 0 ELSE(f.latest_profile_count - f.avg_profile_count)/f.stddev_profile_count
            END AS profile_count_z_factor
    FROM
      (SELECT segment_id,
              avg(profile_count) AS avg_profile_count,
              sum(CASE
                      WHEN last_process_date = date_key THEN profile_count
                      ELSE 0
                  END) AS latest_profile_count,
              stdevp(profile_count) AS stddev_profile_count
        FROM
          (SELECT x.date_key,
                  x.segment_id,
                  d.last_process_date,
                  sum(x.count_of_profiles) AS profile_count
          FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
          INNER JOIN
            (SELECT MAX(process_date) last_process_date,
                    merge_policy_id
              FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
              WHERE process_name = 'FACT_TABLES_PROCESSING'
                AND process_status = 'SUCCESSFUL'
              GROUP BY merge_policy_id) d ON x.merge_policy_id = d.merge_policy_id
          WHERE x.date_key >= dateadd (DAY, -30, d.last_process_date)
          GROUP BY x.date_key,
                    x.segment_id,
                    d.last_process_date) AS t
        GROUP BY segment_id) AS f
    INNER JOIN qsaccel.profile_agg.adwh_dim_segments c ON f.segment_id = c.segment_id
    INNER JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations a ON a.segment_id = c.segment_id
    INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id = b.destination_id
    WHERE b.destination_id = 1458738325) AS m
  WHERE abs(m.profile_count_z_factor) >= 1
  ORDER BY m.latest_profile_count DESC
  LIMIT 20;
```

+++

請參閱 [對應的對象健康狀況Widget檔案](../guides/destinations.md#mapped-audience-health) 以取得此深入分析的外觀和功能相關資訊。

## 對應的對象 {#mapped-audiences}

此深入分析所回答的問題：

- 有多少對象已對應至特定目的地？
- 對應對象的數量會隨著時間而如何變化？
- 我可以在哪裡比較兩個目的地，以檢視對應至每個目的地的對象重疊？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT COUNT(segment_id) AS mapped_audiences_count
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE destination_id = 1458738325;
```

+++

請參閱 [對應的對象Widget檔案](../guides/destinations.md#mapped-audiences) 以取得此深入分析的外觀和功能相關資訊。

<!-- Commented out until the Jan release as the SQL IS MISSING:
## Mapped audiences by identity {#mapped-audiences-by-identity}

Questions answered by this insight:

- How do I find a list of audiences that are mapped to a destination?
- What is the count of identities for audiences mapped to a destination?
- Which audiences have the highest count of identities mapped to a particular destination?

+++Select to reveal the SQL that generates this insight

```sql
```

+++

See the [Mapped audiences by identity widget documentation](../guides/destinations.md#mapped-audiences-by-identity) for information on the appearance and functionality of this insight.
-->

## 最常用的目的地 {#most-used-destinations}

此深入分析所回答的問題：

- 最常使用的目的地有哪些？
- 每個目的地對應了多少個對象，依最高到最低排序？
- 將對象對應至目的地如何從一個快照變更為另一個？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT qsaccel.profile_agg.adwh_dim_destination.destination_name,
       qsaccel.profile_agg.adwh_dim_destination.destination_id,
       qsaccel.profile_agg.adwh_dim_destination.destination,
       count(DISTINCT qsaccel.profile_agg.adwh_dim_br_segment_destinations.segment_id) segment_count
  FROM qsaccel.profile_agg.adwh_dim_destination
  JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations ON qsaccel.profile_agg.adwh_dim_destination.destination_id = qsaccel.profile_agg.adwh_dim_br_segment_destinations.destination_id
  WHERE qsaccel.profile_agg.adwh_dim_destination.destination_name IS NOT NULL
  GROUP BY qsaccel.profile_agg.adwh_dim_destination.destination_name,
           qsaccel.profile_agg.adwh_dim_destination.destination,
           qsaccel.profile_agg.adwh_dim_destination.destination_id
  ORDER BY segment_count DESC
  LIMIT 20;
```

+++

請參閱 [最常使用的目的地Widget檔案](../guides/destinations.md#most-used-destinations) 以取得此深入分析的外觀和功能相關資訊。

## 最近啟動的對象 {#recently-activated-audiences}

此深入分析所回答的問題：

- 對象最近啟用的目的地是哪個目的地？
- 如何找到依上次更新日期排序的所有目的地清單？
- 我如何根據最近的啟用比較兩個目的地？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT
  segment_name,
  segment,
  destination_name,
  a.create_time create_time
FROM
  qsaccel.profile_agg.adwh_dim_br_segment_destinations a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id = c.destination_id
ORDER BY
  create_time DESC,
  segment
LIMIT
  20;
```

+++

請參閱 [最近啟用的對象Widget檔案](../guides/destinations.md#recently-activated-audiences) 以取得此深入分析的外觀和功能相關資訊。

## 最近啟動的對象 (依目的地) {#recently-activated-audiences-by-destination}

此深入分析所回答的問題：

- 在特定目的地啟用的對象有哪些？
- 如何尋找由特定對象從最近到最近啟用的對象清單？
- 如何依據為特定目的地啟用的日期，找到對象清單？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT c.destination_name,
       c.destination,
       c.destination_id,
       b.segment_name,
       b.segment,
       b.segment_id,
       a.create_time activated
  FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id=b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id=c.destination_id
  WHERE c.destination_id=-1275507046
  ORDER BY a.create_time DESC,
           a.segment_id
  LIMIT 20;
```

+++

請參閱 [目的地Widget檔案最近啟用的對象](../guides/destinations.md#recently-activated-audiences-by-destination) 以取得此深入分析的外觀和功能相關資訊。

## 最近建立的目的地 {#recently-created-destinations}

此深入分析所回答的問題：

- 哪些是最近建立的目的地？
- 如何找到目的地清單及其建立日期？
- 最近建立的新目的地？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT DISTINCT
  destination,
  destination_name,
  create_time
FROM
  qsaccel.profile_agg.adwh_dim_destination
WHERE
  destination_status = 'enabled'
ORDER BY
  create_time DESC
LIMIT
  20;
```

+++

請參閱 [最近建立的目的地Widget檔案](../guides/destinations.md#recently-created-destinations) 以取得此深入分析的外觀和功能相關資訊。

<!-- Commented out until the Jan release as SQL MISSING FROM WIKI:

## Unmapped audiences by identity {#unmapped-audiences-by-identity}

Questions answered by this insight:

- How do I find a list of audiences that are not mapped to a destination?
- What is the count of identities for audiences that are not mapped to a destination?
- Which audiences have the highest count of identities not mapped to a particular destination?

+++Select to reveal the SQL that generates this insight

```sql
```

+++

See the [Unmapped audiences by identity widget documentation](../guides/destinations.md#unmapped-audiences-by-identity) for information on the appearance and functionality of this insight.

-->

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在瞭解產生儀表板深入分析的SQL，以及此分析解決哪些常見問題。 您現在可以編輯和疊代這些SQL查詢，以產生您自己的深入分析。

請參閱 [檢視SQL檔案](../view-sql.md) 有關如何直接透過Platform UI調整您見解的SQL的詳細資訊。

您也可以閱讀並瞭解為產生深入分析的SQL [設定檔](./profiles.md)， [帳戶設定檔](./account-profiles.md) 和 [受眾](./audiences.md) 控制面板。
