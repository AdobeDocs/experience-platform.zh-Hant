---
title: 設定檔深入分析
description: 探索為您的設定檔深入分析提供支援的SQL，並使用這些查詢產生自訂深入分析，以進一步探索您的客戶及其消費者體驗。
exl-id: f3792076-3e01-4e26-8788-32927202a2e5
source-git-commit: 34eb9151cc6bb8551553b0a8427e58871acb4dbb
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 3%

---

# 設定檔深入分析

從資料模型分析衍生的深入解析可讓您的Adobe Real-time Customer Data Platform資料更易於存取、理解，並更能對決策產生影響。

存取提供個人資料的SQL來瞭解您的個人資料見解，然後產生您自己的見解，以進一步探索您的客戶及其構成個人資料的消費者體驗。 使用現有的Real-Time CDP資料模型SQL作為靈感，根據您獨特的業務需求建立查詢，將原始資料轉換為可採取行動的新見解。

請參閱[檢視SQL檔案](../view-sql.md)，以取得有關如何直接透過Platform UI調整您見解的SQL的詳細資訊。

下列見解全部都可供您用作[設定檔儀表板](../guides/profiles.md)或自訂[使用者定義儀表板](../user-defined-dashboards.md)的一部分。 請參閱[自訂總覽](../customize/overview.md)，瞭解如何自訂您的儀表板或[在Widget程式庫和[使用者定義儀表板](../user-defined-dashboards.md#create-widget)中建立及編輯新Widget](../customize/custom-widgets.md)的說明。

## 依合併原則區分的客群重疊 {#audience-overlap-by-merge-policy}

此深入分析所回答的問題：

- 哪些設定檔對兩個對象都是通用的？
- 重疊對參與或轉換率有何影響？
- 如何為重疊的區段量身打造行銷策略？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        Sum(overlap_count) Overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            sum(count_of_overlap)Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.date_key = '2024-01-10'
      AND ((qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=1333234510
            AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=1559754729)
            OR (qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=1559754729
                AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=1333234510))
    UNION ALL SELECT sum(count_of_profiles) overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    LEFT JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 1333234510
    UNION ALL SELECT 0 overlap_col1,
                      sum(count_of_profiles) overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 1559754729 ) a;
```

+++

如需此深入分析的外觀和功能的相關資訊，請參閱合併原則Widget檔案的[對象重疊](../guides/profiles.md#audience-overlap-by-merge-policy)。

## 客群重疊報告 {#audience-overlap-report}

此深入分析所回答的問題：

- 50個最重疊的對象是哪個？
- 50個最少的重疊受眾為何？
- 重疊模式會依合併原則而如何變更？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT source_segment_name,
        source_segment_id,
        overlap_segment_name,
        overlap_segment_id,
        max(source_segment_audience_count) source_segment_audience_count,
        max(overlap_segment_audience_count) overlap_segment_audience_count,
        max(overlap_audience_count) overlap_audience_count,
        CASE
            WHEN (max(source_segment_audience_count) + max(overlap_segment_audience_count) - max(overlap_audience_count)) > 0 THEN (cast(max(overlap_audience_count) AS DECIMAL(18, 2)) / cast((max(source_segment_audience_count) + max(overlap_segment_audience_count) - max(overlap_audience_count)) AS DECIMAL(18, 2))) * 100::DECIMAL(9, 2)
            ELSE 100.00
        END overlapping_percentage
  FROM
    (SELECT adwh_fact_profile_overlap_of_segments.Segment1 source_segment_id,
            adwh_fact_profile_overlap_of_segments.Segment2 overlap_segment_id,
            Sum(count_of_overlap) overlap_audience_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.date_key = '2024-01-10'
    GROUP BY qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.Segment2 ,
              qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.Segment1) a
  INNER JOIN
    (SELECT sum(count_of_profiles) source_segment_audience_count,
            adwh_dim_segments.segment_name source_segment_name,
            adwh_fact_profile_by_segment_trendlines.merge_policy_id,
            adwh_fact_profile_by_segment_trendlines.segment_Id segment1
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_dim_segments.segment_id = qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
    GROUP BY qsaccel.profile_agg.adwh_dim_segments.segment_name,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id) b ON a.source_segment_id = b.segment1
  INNER JOIN
    (SELECT sum(count_of_profiles) overlap_segment_audience_count,
            adwh_dim_segments.segment_name overlap_segment_name,
            adwh_fact_profile_by_segment_trendlines.merge_policy_id,
            adwh_fact_profile_by_segment_trendlines.segment_Id segment2
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON adwh_dim_segments.segment_id = adwh_fact_profile_by_segment_trendlines.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
    GROUP BY qsaccel.profile_agg.adwh_dim_segments.segment_name,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id) c ON a.overlap_segment_id = c.segment2
  GROUP BY source_segment_name,
          source_segment_id,
          overlap_segment_name,
          overlap_segment_id
  ORDER BY overlapping_percentage DESC
  LIMIT 5;
```

+++

如需此深入分析的外觀和功能的相關資訊，請參閱[對象重疊報表Widget檔案](../guides/profiles.md#audience-overlap-report)。

## 對象（計數） {#audiences}

此深入分析所回答的問題：

- 哪種合併原則主要用於分段？
- 對象在合併原則間的分佈情況如何？
- 特定合併政策的對象人數在一段時間內是否有任何重大變化？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT count(DISTINCT a.segment_id) count_of_segments
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines a
  JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) b ON a.merge_policy_id= b.merge_policy_id
  AND a.date_key = b.last_process_date
  WHERE a.merge_policy_id= 2027892989;
```

+++

如需此深入分析的外觀和功能的相關資訊，請參閱[對象Widget檔案](../guides/profiles.md#audiences)。

## 對應到目的地狀態的客群 {#audiences-mapped-to-destination-status}

此深入分析所回答的問題：

- 對應和未對應目的地之間的對象整體分佈情況如何？
- 哪些特定目的地的對應對象數量最高？
- 未對應的對象佔總對象比例為何？
- 在這些未對應的對象中，是否有模式或相關的趨勢？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT COUNT(DISTINCT (y.segment_id)) AS count_mapped_segments,
        COUNT(DISTINCT (x.segment_id)) - COUNT(DISTINCT (y.segment_id)) AS count_unmapped_segments,
        COUNT(DISTINCT (x.segment_id)) AS total_segments
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
  LEFT JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations y ON x.segment_id = y.segment_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) z ON x.merge_policy_id = z.merge_policy_id
  AND x.date_key = z.last_process_date
  WHERE x.merge_policy_id = 2027892989;
```

+++

如需此深入分析的外觀和功能的相關資訊，請參閱對應到目的地狀態Widget檔案的[對象](../guides/profiles.md#audiences-mapped-to-destination-status)。

## 客群人數 {#audiences-size}

此深入分析所回答的問題：

- 哪個受眾區段規模最大？
- 五大受眾為何？
- 排名在前的對象的對象人數分佈會隨著時間而如何變化？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key,
        qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
        qsaccel.profile_agg.adwh_dim_segments.segment,
        qsaccel.profile_agg.adwh_dim_segments.segment_name,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.count_of_profiles)count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id = qsaccel.profile_agg.adwh_dim_segments.segment_id
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id=adwh_dim_merge_policies.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id= 2027892989
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key,
          qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
          qsaccel.profile_agg.adwh_dim_segments.segment,
          qsaccel.profile_agg.adwh_dim_segments.segment_name
  ORDER BY count_of_profiles DESC
  LIMIT 20;
```

+++

如需此深入分析的外觀和功能的相關資訊，請參閱[對象大小Widget檔案](../guides/profiles.md#audiences-size)。

## Customer AI 分數的分佈 {#customer-ai-distribution-of-scores}

此深入分析所回答的問題：

- 我每個Customer AI模型各貯體中的分數分佈如何？
- 高、中、低分數的分數分佈情況如何？
- 依合併原則劃分評分分佈的資料為何？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT b.model_name,
     b.model_type,
     CASE
         WHEN score >= 0
              AND score < 25 THEN 'LOW'
         WHEN score >= 25
              AND score < 75 THEN 'MEDIUM'
         WHEN score >= 75
              AND score <= 100 THEN 'HIGH'
     END bucket_name,
     CASE
         WHEN score >= 0
              AND score < 5 THEN '02.50'
         WHEN score >= 5
              AND score < 10 THEN '07.50'
         WHEN score >= 10
              AND score < 15 THEN '12.50'
         WHEN score >= 15
              AND score < 20 THEN '17.50'
         WHEN score >= 20
              AND score < 25 THEN '22.50'
         WHEN score >= 25
              AND score < 30 THEN '27.50'
         WHEN score >= 30
              AND score < 35 THEN '32.50'
         WHEN score >= 35
              AND score < 40 THEN '37.50'
         WHEN score >= 40
              AND score < 45 THEN '42.50'
         WHEN score >= 45
              AND score < 50 THEN '47.50'
         WHEN score >= 50
              AND score < 55 THEN '52.50'
         WHEN score >= 55
              AND score < 60 THEN '57.50'
         WHEN score >= 60
              AND score < 65 THEN '62.50'
         WHEN score >= 65
              AND score < 70 THEN '67.50'
         WHEN score >= 70
              AND score < 75 THEN '72.50'
         WHEN score >= 75
              AND score < 80 THEN '77.50'
         WHEN score >= 80
              AND score < 85 THEN '82.50'
         WHEN score >= 85
              AND score < 90 THEN '87.50'
         WHEN score >= 90
              AND score < 95 THEN '92.50'
         WHEN score >= 95
              AND score <= 100 THEN '97.50'
     END score_bins,
     Sum(CASE
             WHEN score >= 0
                  AND score < 25 THEN count_of_profiles
             WHEN score >= 25
                  AND score < 75 THEN count_of_profiles
             WHEN score >= 75
                  AND score <= 100 THEN count_of_profiles
         END) count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_ai_models a
  JOIN qsaccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id = b.merge_policy_id
  AND a.model_id = b.model_id
  WHERE a.merge_policy_id = 2027892989
    AND a.model_id = 1829081696
    AND score_date =
      (SELECT Max(score_date)
       FROM qsaccel.profile_agg.adwh_fact_profile_ai_models d
       WHERE d.model_id = a.model_id) GROUP  BY b.model_name,
          model_type,
          CASE
              WHEN score >= 0
                   AND score < 25 THEN 'LOW'
              WHEN score >= 25
                   AND score < 75 THEN 'MEDIUM'
              WHEN score >= 75
                   AND score <= 100 THEN 'HIGH'
          END,
          CASE
              WHEN score >= 0
                   AND score < 5 THEN '02.50'
              WHEN score >= 5
                   AND score < 10 THEN '07.50'
              WHEN score >= 10
                   AND score < 15 THEN '12.50'
              WHEN score >= 15
                   AND score < 20 THEN '17.50'
              WHEN score >= 20
                   AND score < 25 THEN '22.50'
              WHEN score >= 25
                   AND score < 30 THEN '27.50'
              WHEN score >= 30
                   AND score < 35 THEN '32.50'
              WHEN score >= 35
                   AND score < 40 THEN '37.50'
              WHEN score >= 40
                   AND score < 45 THEN '42.50'
              WHEN score >= 45
                   AND score < 50 THEN '47.50'
              WHEN score >= 50
                   AND score < 55 THEN '52.50'
              WHEN score >= 55
                   AND score < 60 THEN '57.50'
              WHEN score >= 60
                   AND score < 65 THEN '62.50'
              WHEN score >= 65
                   AND score < 70 THEN '67.50'
              WHEN score >= 70
                   AND score < 75 THEN '72.50'
              WHEN score >= 75
                   AND score < 80 THEN '77.50'
              WHEN score >= 80
                   AND score < 85 THEN '82.50'
              WHEN score >= 85
                   AND score < 90 THEN '87.50'
              WHEN score >= 90
                   AND score < 95 THEN '92.50'
              WHEN score >= 95
                   AND score <= 100 THEN '97.50'
          END;
```

+++

如需此深入分析的外觀和功能的相關資訊，請參閱分數Widget檔案的[Customer AI分佈](../guides/profiles.md#customer-ai-distribution-of-scores)。

## Customer AI 評分摘要 {#customer-ai-scoring-summary}

此深入分析所回答的問題：

- 我的每個Customer AI模型的評分摘要為何？
- 我的Customer AI傾向分數如何隨著不同對象而改變？
- 與設定檔概述中的其他KPI相比，我的評分摘要有何變更？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT model_name,
         model_type,
         CASE
             WHEN score BETWEEN 0 AND 24 THEN 'LOW'
             WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
             WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
         END score_buckets,
         sum(count_of_profiles) count_of_profiles
  FROM QSAccel.profile_agg.adwh_fact_profile_ai_models a
  JOIN QSAccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id=b.merge_policy_id
  AND a.model_id=b.model_id
  WHERE a.merge_policy_id=2027892989
    AND a.model_id =1829081696
    AND score_date=
      (SELECT max(score_date)
       FROM QSAccel.profile_agg.adwh_fact_profile_ai_models d
       WHERE d.model_id=a.model_id)
  GROUP BY model_name,
           model_type,
           CASE
               WHEN score BETWEEN 0 AND 24 THEN 'LOW'
               WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
               WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
           END;
```

+++

如需此深入分析的外觀和功能的相關資訊，請參閱[Customer AI評分摘要Widget檔案](../guides/profiles.md#customer-ai-scoring-summary)。

## 身分識別覆蓋 {#identity-overlap}

此深入分析所回答的問題：

- [!UICONTROL 身分型別A]和[!UICONTROL 身分型別B]之間的共同交集是什麼？
- 我如何根據特定身分型別的重疊來調整客戶對象，以增強目標式行銷策略？
- 評估交集區域內的行銷活動績效能獲得哪些深入分析？
- 運用此行銷活動績效深入分析，如何最佳化未來的行銷工作？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        coalesce(Sum(overlap_count), 0) overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            Sum(count_of_profiles) overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.overlap_id IN
        (SELECT a.overlap_id
          FROM
            (SELECT qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id overlap_id,
                    count(*) cnt_num
            FROM qsaccel.profile_agg.adwh_dim_overlap_namespaces
            WHERE qsaccel.profile_agg.adwh_dim_overlap_namespaces.merge_policy_id = 2027892989
              AND qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_namespaces in ('avid',
                                                                                          'crmid')
            GROUP BY qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id)a
          WHERE a.cnt_num>1 )
    UNION ALL SELECT count_of_profiles overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'avid'
    UNION ALL SELECT 0 overlap_col1,
                      count_of_profiles overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'crmid' )a;
```

+++

如需此深入分析的外觀和功能的相關資訊，請參閱[身分重疊Widget檔案](../guides/profiles.md#identity-overlap)。

## 設定檔計數 {#profile-count}

此深入分析所回答的問題：

- Adobe Real-time Customer Data Platform中的整體設定檔計數為何？
- 如何根據合併原則分配設定檔？
- 哪個合併原則具有最高的設定檔計數？

產生這些深入分析的SQl如下：

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

您可以在[設定檔計數Widget指南](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#profile-count)中找到此深入分析外觀和功能的完整資訊。

如需此深入分析的外觀和功能的相關資訊，請參閱[設定檔計數Widget檔案](../guides/profiles.md#profile-count)。

## 設定檔計數變更 {#profile-count-change}

此深入分析所回答的問題：

- 整體設定檔計數變更的趨勢為何？
- 是什麼導致設定檔計數出現重大尖峰或下降？
- 是否有特定合併原則可推動設定檔計數變更？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT (sum(count_of_profiles) - sum(count_of_profiles_days_ago)) profiles_added
  FROM
    (SELECT sum(qsaccel.profile_agg.adwh_fact_profile.count_of_profiles) count_of_profiles,
            0 count_of_profiles_days_ago
    FROM qsaccel.profile_agg.adwh_fact_profile
    WHERE qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile.date_key = '2024-01-10'
    UNION ALL SELECT 0 count_of_profiles,
                      CASE
                          WHEN sum(cntondatediff) =0 THEN sum(cntmin)
                          ELSE sum(cntondatediff)
                      END AS count_of_profiles_days_ago
    FROM
      (SELECT coalesce(sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles), 0) cntondatediff,
              0 cntmin
        FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
        WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id =2027892989
          AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key =dateadd(DAY, - 30, '2024-01-10')
        UNION ALL SELECT 0 cntondatediff,
                        sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles) countMin
        FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
        WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id = 2027892989
          AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key =
            (SELECT min(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key) col
            FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
            WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id =2027892989
              AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key >= dateadd(DAY, - 30, '2024-01-10')
              AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles IS NOT NULL) )b) a;
```

+++

如需此深入分析的外觀和功能的相關資訊，請參閱[設定檔計數變更Widget檔案](../guides/profiles.md#profile-count-change)。

## 設定檔計數變更趨勢 {#profile-count-change-trend}

此深入分析所回答的問題：

- 根據合併原則，過去12個月設定檔計數變更的整體趨勢為何？
- 過去30天內設定檔計數是否有特定模式或波動需要注意？
- 與整體趨勢相比，過去90天的設定檔計數有何變更？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT date_key,
         profiles_count_change
  FROM
    (SELECT rn_num,
            date_key,
            (count_of_profiles-lag(count_of_profiles, 1, 0) over(
                                                            ORDER BY date_key))profiles_count_change
    FROM
      (SELECT qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key,
              sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles) count_of_profiles,
              row_number() OVER (
                              ORDER BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key) rn_num
      FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key >=dateadd(DAY, - 30 -1, '2024-01-10')
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key)a)b
  WHERE rn_num > 1;
```

+++

如需此深入分析的外觀和功能的相關資訊，請參閱[設定檔計數變更趨勢Widget檔案](../guides/profiles.md#profile-count-change-trend)。

## 輪廓計數趨勢 {#profile-count-trend}

此深入分析所回答的問題：

- 根據合併原則計算，過去30天的設定檔計數整體趨勢為何？
- 根據此趨勢，與長期趨勢（例如90天和12個月）有何不同？
- 在指定的時段（30天、90天和12個月）內，哪個合併原則對設定檔計數的增加或減少貢獻最大？
- 在30天的時間範圍內，是否有任何個人檔案計數的特定尖峰或下降與特定事件或期間相關聯？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT date_key,
       sum(count_of_profiles) AS count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines x
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL'
     GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
  WHERE date_key >= dateadd(DAY, -365, y.last_process_date)
    AND x.merge_policy_id = 2027892989
  GROUP BY date_key;
```

+++

如需此深入分析的外觀和功能的相關資訊，請參閱[設定檔計數趨勢Widget檔案](../guides/profiles.md#profile-count-trend)。

## 依身分識別劃分的設定檔 {#profiles-by-identity}

此深入分析所回答的問題：

- 在設定檔總數中，哪個身分型別所佔的比例較高？
- 身分型別之間是否有明顯的差異？
- 身分型別的整體分佈情況如何？
- 身分計數是否有任何重大差異或異常？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_profiles) count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
          qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id,
          qsaccel.profile_agg.adwh_dim_namespaces.namespace_description
  ORDER BY count_of_profiles DESC;
```

+++

如需此深入分析的外觀和功能的相關資訊，請參閱[依身分Widget的設定檔檔案](../guides/profiles.md#profiles-by-identity)。

## 設定檔計數變更趨勢 {#profiles-count-change-trend}

此深入分析所回答的問題：

- 根據合併原則，過去12個月期間設定檔計數變化的整體趨勢為何？
- 過去30天內設定檔計數變更是否有特定模式或波動需要注意？
- 與整體趨勢相比，過去90天內設定檔中的變更如何計算？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT date_key,
         profiles_count_change
  FROM
    (SELECT rn_num,
            date_key,
            (count_of_profiles-lag(count_of_profiles, 1, 0) over(
                                                            ORDER BY date_key))profiles_count_change
    FROM
      (SELECT qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key,
              sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles) count_of_profiles,
              row_number() OVER (
                              ORDER BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key) rn_num
      FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key >=dateadd(DAY, - 30 -1, '2024-01-10')
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key)a)b
  WHERE rn_num > 1;
```

+++

如需此深入分析的外觀和功能的相關資訊，請參閱[設定檔計數變更趨勢Widget檔案](../guides/profiles.md#profiles-count-change-trend)。

## 依身分列出的輪廓計數變更趨勢 {#profiles-count-change-trend-by-identity}

此深入分析所回答的問題：

- 過去12個月跨不同身分的設定檔計數變更的總體趨勢為何？
- 是否有任何特定身分趨勢會在過去30天內顯示重大變更？
- 比較特定身分的30天、90天和12個月趨勢時，設定檔計數的變更會有何不同？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT date_key,
        namespace_description,
        profiles_count_change
  FROM
    (SELECT rn_num,
            date_key,
            namespace_description,
            (count_of_profiles - lag(count_of_profiles, 1, 0) over(PARTITION BY namespace_description
                                                                  ORDER BY date_key)) profiles_count_change
    FROM
      (SELECT qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
              qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
              sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_profiles) count_of_profiles,
              row_number() OVER (PARTITION BY qsaccel.profile_agg.adwh_dim_namespaces.namespace_description
                                  ORDER BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key) rn_num
        FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
        LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
        AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
        WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
          AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id= -1042977439
          AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key >= dateadd(DAY, - 30 -1, '2024-01-10')
        GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
                adwh_dim_namespaces.namespace_description)a)b
  WHERE rn_num > 1;
```

+++

如需此深入分析的外觀和功能的相關資訊，請參閱身分識別介面工具檔案的[設定檔計數變更趨勢](../guides/profiles.md#profiles-count-change-trend-by-identity)。

## 單一身分識別設定檔 {#single-identity-profiles}

此深入分析所回答的問題：

- 我的客戶身分資料是否一致地以單一身分表示？
- 在我的使用者群中，僅有單一身分型別的設定檔佔多大百分比？
- 在只有單一身分型別的設定檔中，這會對設定檔完整性造成什麼影響？
- 最常見的身分型別與單一身分設定檔計數之間是否有關聯？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_Single_Identity_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

+++

如需此深入分析的外觀和功能的相關資訊，請參閱[單一身分設定檔Widget檔案](../guides/profiles.md#single-identity-profiles)。

## 依身分區分的單一身分輪廓 {#single-identity-profiles-by-identity}

此深入分析所回答的問題：

- 有多少不重複客戶以單一身分註冊（例如電子郵件或電話號碼）？
- 不同身分型別（例如電子郵件或電話號碼）之間的單一身分設定檔分佈情況如何？
- 單一身分設定檔中是否有新興的身分模式或轉變？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_Single_Identity_profiles) count_of_Single_Identity_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
          qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id,
          qsaccel.profile_agg.adwh_dim_namespaces.namespace_description;
```

+++

如需此深入分析的外觀和功能的相關資訊，請參閱[依身分識別的Widget檔案](../guides/profiles.md#single-identity-profiles-by-identity)。

## 無區段設定檔 {#unsegmented-profiles}

此深入分析所回答的問題：

- 有多少設定檔不屬於某個對象？
- 未分段的設定檔佔總對象的多少百分比？
- 任何合併原則是否都會對大量未分段的設定檔產生作用？

+++選取以顯示產生此深入分析的SQL

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_Orphan_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

+++

如需此深入分析的外觀和功能的相關資訊，請參閱[未分段的設定檔Widget檔案](../guides/profiles.md#unsegmented-profiles)。

## 後續步驟

閱讀本檔案後，您現在瞭解產生儀表板深入分析的SQL，以及此分析解決哪些常見問題。 您現在可以編輯並反複處理SQL，以產生您自己的深入分析。

如需有關如何直接透過PLatform UI調整您見解的SQL的詳細資訊，請參閱[檢視SQL檔案](../view-sql.md)。

您也可以閱讀並瞭解產生[對象](./audiences.md)、[帳戶設定檔](./account-profiles.md)和[目的地](./destinations.md)儀表板之深入分析的SQL。
