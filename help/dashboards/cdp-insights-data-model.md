---
title: Customer Data Platform(CDP)Insights資料模型
description: 了解如何使用CDP Insights資料模型的SQL查詢，針對您的行銷和KPI使用案例自訂您自己的CDP報表。
exl-id: 61bc7f23-9f79-4c75-a515-85dd9dda2d02
source-git-commit: 2c96bfd2c1b541d30a72fcf2bac414ee06607456
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 0%

---

# Customer Data Platform(CDP)Insights資料模型

Customer Data Platform(CDP)Insights Data Model功能可公開資料模型和SQL，為各種設定檔、目的地和細分小工具提供深入分析。 您可以自訂這些SQL查詢範本，為您的行銷和關鍵績效指標(KPI)使用案例建立CDP報表。 然後，這些前瞻分析便可作為使用者定義控制面板的自訂小工具。

## 先決條件

本指南需要妥善了解 [使用者定義的控制面板功能](./user-defined-dashboards.md). 繼續閱讀本指南之前，請先閱讀本檔案。

## CDP分析報告和使用案例

CDP報告可深入分析您的設定檔資料及其與區段和目的地的關係。 開發各種星型架構模型以回應各種常見的行銷使用案例，而每個資料模型可支援數個使用案例。

>[!IMPORTANT]
>
>用於CDP報告的資料對於選定的合併策略和最近的每日快照是準確的。

### 輪廓模型 {#profile-model}

設定檔模型由三個資料集組成：

- `adwh_dim_date`
- `adwh_fact_profile`
- `adwh_dim_merge_policies`

下圖包含每個資料集中的相關資料欄位。

![描述檔模型的ERD。](./images/cdp-insights/profile-model.png)

#### 設定檔計數使用案例

用於設定檔計數Widget的邏輯會傳回建立快照時，設定檔存放區內合併的設定檔總數。 請參閱 [[!UICONTROL 設定檔計數] widget檔案](./guides/profiles.md#profile-count) 以取得更多資訊。

生成 [!UICONTROL 設定檔計數] 介面工具集會顯示在下方的可折疊區段。

+++SQL查詢

```sql
SELECT adwh_dim_merge_policies.merge_policy_name,
  sum(adwh_fact_profile.count_of_profiles) CNT
FROM qsaccel.profile_agg.adwh_fact_profile
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
WHERE adwh_fact_profile.date_key='${lastProcessDate}'
AND adwh_fact_profile.merge_policy_id=${mergePolicyId}
GROUP BY adwh_dim_merge_policies.merge_policy_name;
```

+++

#### 單一身分設定檔使用案例

用於 [!UICONTROL 單一身分設定檔] 介面工具集會提供貴組織的設定檔計數，這些設定檔只有一種可建立其身分的ID類型。 請參閱[[!UICONTROL 單一身分設定檔] widget檔案](./guides/profiles.md#single-identity-profiles) 以取得更多資訊。

生成 [!UICONTROL 單一身分設定檔] 介面工具集會顯示在下方的可折疊區段。

+++SQL查詢

```sql
SELECT adwh_dim_merge_policies.merge_policy_name,
  sum(adwh_fact_profile.count_of_Single_Identity_profiles) CNT
FROM QSAccel.profile_agg.adwh_fact_profile
LEFT OUTER JOIN QSAccel.profile_agg.adwh_dim_merge_policies ON adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
WHERE adwh_fact_profile.date_key='${lastProcessDate}'
  AND adwh_fact_profile.merge_policy_id =${mergePolicyId}
GROUP BY adwh_dim_merge_policies.merge_policy_name;
```

+++

### 命名空間模型 {#namespace-model}

命名空間模型由下列資料集組成：

- `adwh_fact_profile_by_namespace`
- `adwh_dim_date`
- `adwh_dim_namespaces`
- `adwh_dim_merge_policies`

下圖包含每個資料集中的相關資料欄位。

![命名空間模型的ERD。](./images/cdp-insights/namespace-model.png)

#### 依身分使用案例的設定檔

此 [!UICONTROL 依身分設定檔] 介面工具集會顯示您的個人資料存放區中所有合併設定檔的身分劃分。 請參閱 [[!UICONTROL 依身分設定檔] widget檔案](./guides/profiles.md#profiles-by-identity) 以取得更多資訊。

生成 [!UICONTROL 依身分設定檔] 介面工具集會顯示在下方的可折疊區段。

+++SQL查詢

```sql
SELECT adwh_dim_namespaces.namespace_description,
    sum(adwh_fact_profile_by_namespace.count_of_profiles) count_of_profiles
FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace
JOIN qsaccel.profile_agg.adwh_dim_namespaces ON adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
WHERE adwh_fact_profile_by_namespace.merge_policy_id =${mergePolicyId}
AND adwh_fact_profile_by_namespace.date_key = '${lastProcessDate}'
GROUP BY adwh_fact_profile_by_namespace.date_key,
        adwh_fact_profile_by_namespace.merge_policy_id,
        adwh_dim_namespaces.namespace_description
ORDER BY count_of_profiles DESC
LIMIT 5;
```

+++

#### 依身分使用案例劃分的單一身分設定檔

用於 [!UICONTROL 依身分的單一身分設定檔] 介面工具集說明了僅以單一唯一識別碼識別的設定檔總數。 請參閱 [依身分識別Widget檔案的單一身分識別設定檔](./guides/profiles.md#single-identity-profiles-by-identity) 以取得更多資訊。

生成 [!UICONTROL 依身分的單一身分設定檔] 介面工具集會顯示在下方的可折疊區段。

+++SQL查詢

```sql
SELECT
  adwh_dim_namespaces.namespace_description,
  sum(adwh_fact_profile_by_namespace.count_of_Single_Identity_profiles) count_of_Single_Identity_profiles
FROM
  qsaccel.profile_agg.adwh_fact_profile_by_namespace
  LEFT OUTER JOIN
    qsaccel.profile_agg.adwh_dim_namespaces
    ON adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
WHERE
  adwh_fact_profile_by_namespace.merge_policy_id=${mergePolicyId}
  AND adwh_fact_profile_by_namespace.date_key='${lastProcessDate}'
GROUP BY
  adwh_fact_profile_by_namespace.date_key,
  adwh_fact_profile_by_namespace.merge_policy_id,
  adwh_dim_namespaces.namespace_description;
```

+++

### 區段模型 {#segment-model}

區段模型由下列資料集組成：

- `adwh_dim_date`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_fact_profile_by_segment`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

下圖包含每個資料集中的相關資料欄位。

![區段模型的ERD。](./images/cdp-insights/segment-model.png)

#### 對象大小使用案例

用於 [!UICONTROL 對象大小] 介面工具集會傳回在最近快照時，所選區段內合併的設定檔總數。 請參閱 [[!UICONTROL 對象大小] widget檔案](./guides/segments.md#audience-size) 以取得更多資訊。

生成 [!UICONTROL 對象大小] 介面工具集會顯示在下方的可折疊區段。

+++SQL查詢

```sql
SELECT adwh_fact_profile_by_segment.date_key,
       adwh_dim_merge_policies.merge_policy_name,
       adwh_dim_segments.segment,
       adwh_dim_segments.segment_name,
       sum(adwh_fact_profile_by_segment.count_of_profiles)count_of_profiles
FROM qsaccel.profile_agg.adwh_fact_profile_by_segment
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_segments ON adwh_fact_profile_by_segment.segment_id = adwh_dim_segments.segment_id
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON adwh_fact_profile_by_segment.merge_policy_id=adwh_dim_merge_policies.merge_policy_id
WHERE adwh_fact_profile_by_segment.date_key ='${lastProcessDate}'
  AND adwh_fact_profile_by_segment.merge_policy_id=${mergePolicyId}
GROUP BY adwh_fact_profile_by_segment.date_key,
         adwh_dim_merge_policies.merge_policy_name,
         adwh_dim_segments.segment,
         adwh_dim_segments.segment_name
ORDER BY count_of_profiles DESC
LIMIT 20;
```

+++

#### 對象大小變更趨勢使用案例

用於 [!UICONTROL 對象大小變更趨勢] 介面工具集提供折線圖圖示，說明在最近的每日快照中符合指定區段資格的設定檔總數之間的差異。 請參閱 [[!UICONTROL 對象大小變更趨勢] widget檔案](./guides/segments.md#audience-size-change-trend) 以取得更多資訊。

生成 [!UICONTROL 對象大小變更趨勢] 介面工具集會顯示在下方的可折疊區段。

+++SQL查詢

```sql
SELECT DISTINCT cast(adwh_dim_segments.create_date AS Date) Date_key, adwh_dim_merge_policies.merge_policy_name,
  count(DISTINCT adwh_dim_segments.segment_id)Segments_Added
FROM qsaccel.profile_agg.adwh_fact_profile_by_segment
JOIN qsaccel.profile_agg.adwh_dim_segments ON adwh_fact_profile_by_segment.segment_id = adwh_dim_segments.segment_id
JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON adwh_fact_profile_by_segment.merge_policy_id=adwh_dim_merge_policies.merge_policy_id
WHERE Cast(adwh_dim_segments.create_date AS date) >= dateadd(DAY, - ${dayRange}, '${lastProcessDate}')
AND adwh_fact_profile_by_segment.merge_policy_id=${mergePolicyId}
GROUP BY cast(adwh_dim_segments.create_date AS date), adwh_dim_merge_policies.merge_policy_name ;
```

+++

#### 最常使用的目的地使用案例

用於 [!UICONTROL 最常使用的目的地] 介面工具集會根據對應至組織的區段數，列出組織最常使用的目的地。 此排名可深入分析正在使用哪些目的地，同時可能顯示未充分利用的目標。 請參閱 [[!UICONTROL 最常使用的目的地] 介面](./guides/destinations.md#most-used-destinations) 以取得更多資訊。

生成 [!UICONTROL 最常使用的目的地] 介面工具集會顯示在下方的可折疊區段。

+++SQL查詢

```sql
SELECT
   adwh_dim_destination.destination_name, adwh_dim_destination.destination_id,
   count( distinct adwh_dim_br_segment_destinations.segment_id ) segment_count
FROM
   qsaccel.profile_agg.adwh_dim_destination
   join qsaccel.profile_agg.adwh_dim_br_segment_destinations
 ON
   adwh_dim_destination.destination_id = adwh_dim_br_segment_destinations.destination_id
 WHERE
   adwh_dim_destination.destination_name is not null
 group by
   adwh_dim_destination.destination_name,
   adwh_dim_destination.destination_id
   order by segment_count desc limit 5;
```

+++

#### 最近啟動的區段使用案例

邏輯 [!UICONTROL 最近啟動的區段] 介面工具集提供最近對應至目的地的區段清單。 此清單提供系統中正在使用的區段和目的地的快照，有助於疑難排解任何錯誤對應。 請參閱 [[!UICONTROL 最近啟動的區段] widget檔案](./guides/destinations.md#recently-activated-segments) 以取得更多資訊。

生成 [!UICONTROL 最近啟動的區段] 介面工具集會顯示在下方的可折疊區段。

+++SQL查詢

```sql
SELECT segment_name, segment, destination_name, a.create_time create_time
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id = c.destination_id
ORDER BY create_time desc, segment LIMIT 5;
```

+++

### 命名空間區段模型

命名空間區段模型由下列資料集組成：

- `adwh_dim_date`
- `adwh_dim_merge_policies`
- `adwh_dim_namespaces`
- `adwh_fact_profile_by_segment_and_namespace`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

下圖包含每個資料集中的相關資料欄位。

![區段模型的ERD。](./images/cdp-insights/namespace-segment-model.png)

#### 依區段使用案例身分的設定檔

用於 [!UICONTROL 依身分設定檔] 介面工具集可為指定區段，提供設定檔存放區中所有合併設定檔的身分劃分。 請參閱 [[!UICONTROL 依身分設定檔] widget檔案](./guides/segments.md#profiles-by-identity) 以取得更多資訊。

生成 [!UICONTROL 依身分設定檔] 介面工具集會顯示在下方的可折疊區段。

+++SQL查詢

```sql
SELECT adwh_dim_namespaces.namespace_description,
  sum( adwh_fact_profile_by_segment_and_namespace.count_of_profiles) count_of_profiles
FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces
ON adwh_fact_profile_by_segment_and_namespace.namespace_id = adwh_dim_namespaces.namespace_id
AND adwh_fact_profile_by_segment_and_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
WHERE adwh_fact_profile_by_segment_and_namespace.segment_id = {segment_id}
AND adwh_fact_profile_by_segment_and_namespace.merge_policy_id = {merge_policy_id}
AND adwh_fact_profile_by_segment_and_namespace.date_key = '{date}'
GROUP BY adwh_dim_namespaces.namespace_description;
```

+++

### 重疊命名空間模型

重疊命名空間模型由下列資料集組成：

- `adwh_dim_date`
- `adwh_dim_namespaces`
- `adwh_fact_profile_overlap_of_namespace`
- `adwh_dim_merge_policies`

下圖包含每個資料集中的相關資料欄位。

![區段模型的ERD。](./images/cdp-insights/overlap-namespace-model.png)

#### 身分重疊（設定檔）使用案例

用於 [!UICONTROL 身分重疊] 介面工具集會顯示您 **設定檔存放區** 包含兩個所選身分。 如需詳細資訊，請參閱 [[!UICONTROL 身分重疊] 介面工具集區段 [!UICONTROL 設定檔] 控制面板檔案](./guides/profiles.md#identity-overlap).

生成 [!UICONTROL 身分重疊] 介面工具集會顯示在下方的可折疊區段。

+++SQL查詢

```sql
SELECT Sum(overlap_col1) overlap_col1,
       Sum(overlap_col2) overlap_col2,
       coalesce(Sum(overlap_count), 0) overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            Sum(count_of_profiles) overlap_count
     FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace
     WHERE adwh_fact_profile_overlap_of_namespace.merge_policy_id = ${mergePolicyId}
       AND adwh_fact_profile_overlap_of_namespace.date_key = '${lastProcessDate}'
       AND adwh_fact_profile_overlap_of_namespace.overlap_id IN
         (SELECT adwh_dim_overlap_namespaces.overlap_id
          FROM qsaccel.profile_agg.adwh_dim_overlap_namespaces
          WHERE adwh_dim_overlap_namespaces.merge_policy_id=${mergePolicyId}
            AND adwh_dim_overlap_namespaces.overlap_namespaces IN ('${namespace1}',
                                                                   '${namespace2}')
          GROUP BY adwh_dim_overlap_namespaces.overlap_id
          HAVING Count(*) > 1)
     UNION ALL SELECT count_of_profiles overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
     FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace
     JOIN qsaccel.profile_agg.adwh_dim_namespaces ON
     adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
     AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
     WHERE adwh_fact_profile_by_namespace.merge_policy_id = ${mergePolicyId}
       AND adwh_fact_profile_by_namespace.date_key = '${lastProcessDate}'
       AND adwh_dim_namespaces.namespace_description = '${namespace1}'
     UNION ALL SELECT 0 overlap_col1,
                      count_of_profiles overlap_col2,
                      0 Overlap_count
     FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace
     JOIN qsaccel.profile_agg.adwh_dim_namespaces ON
     adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
     AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
     WHERE adwh_fact_profile_by_namespace.merge_policy_id = ${mergePolicyId}
       AND adwh_fact_profile_by_namespace.date_key = '${lastProcessDate}'
       AND adwh_dim_namespaces.namespace_description = '${namespace2}' ) a;
```

+++

### 依區段模型的重疊命名空間

依區段模型劃分的重疊命名空間由下列資料集組成：

- `adwh_dim_date`
- `adwh_dim_namespaces`
- `adwh_fact_profile_overlap_of_namespace_by_segment`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

下圖包含每個資料集中的相關資料欄位。

![區段模型的ERD。](./images/cdp-insights/overlap-namespace-by-segment-model.png)

#### 身分重疊（區段）使用案例

用於 [!UICONTROL 區段] 儀表板 [!UICONTROL 身分重疊] 介面工具集說明包含特定區段之兩個選取身分之設定檔的重疊。 如需詳細資訊，請參閱 [[!UICONTROL 身分重疊] 介面工具集區段 [!UICONTROL 區段] 控制面板檔案](./guides/segments.md#identity-overlap).

生成 [!UICONTROL 身分重疊] 介面工具集會顯示在下方的可折疊區段。

+++SQL查詢

```sql
SELECT
   Sum(overlap_col1) overlap_col1,
   Sum( overlap_col2) overlap_col2,
   Sum(overlap_count) Overlap_count
FROM
   (
      SELECT
         0 overlap_col1,
         0 overlap_col2,
         Sum(count_of_profiles) Overlap_count
      FROM
         qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment
      WHERE
         adwh_fact_profile_overlap_of_namespace_by_segment.segment_id = $ {segmentId}
         and adwh_fact_profile_overlap_of_namespace_by_segment.merge_policy_id =$ {mergePolicyId}
         and adwh_fact_profile_overlap_of_namespace_by_segment.date_key = '${lastProcessDate}'
         and adwh_fact_profile_overlap_of_namespace_by_segment.overlap_id IN
         (
            SELECT
               adwh_dim_overlap_namespaces.overlap_id
            FROM
               qsaccel.profile_agg.adwh_dim_overlap_namespaces
            WHERE
               adwh_dim_overlap_namespaces.merge_policy_id =$ {mergePolicyId}
               AND adwh_dim_overlap_namespaces.overlap_namespaces IN
               (
                  '${namespace1}',
                  '${namespace2}'
               )
            GROUP BY
               adwh_dim_overlap_namespaces.overlap_id
            HAVING
               Count(*) > 1
         )
      UNION ALL
      SELECT
         count_of_profiles overlap_col1,
         0 overlap_col2,
         0 Overlap_count
      FROM
         qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace
         LEFT OUTER JOIN
            qsaccel.profile_agg.adwh_dim_namespaces
            ON adwh_fact_profile_by_segment_and_namespace.namespace_id = adwh_dim_namespaces.namespace_id
            and adwh_fact_profile_by_segment_and_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
      WHERE
         adwh_dim_namespaces.namespace_description = '${namespace1}'
         and adwh_fact_profile_by_segment_and_namespace.segment_id = $ {segmentId}
         and adwh_fact_profile_by_segment_and_namespace.merge_policy_id =$ {mergePolicyId}
         and adwh_fact_profile_by_segment_and_namespace.date_key = '${lastProcessDate}'
      UNION ALL
      SELECT
         0 overlap_col1,
         count_of_profiles overlap_col2,
         0 Overlap_count
      FROM
         qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace
         LEFT OUTER JOIN
            qsaccel.profile_agg.adwh_dim_namespaces
            ON adwh_fact_profile_by_segment_and_namespace.namespace_id = adwh_dim_namespaces.namespace_id
            and adwh_fact_profile_by_segment_and_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
      WHERE
         adwh_dim_namespaces.namespace_description = '${namespace2}'
         and adwh_fact_profile_by_segment_and_namespace.segment_id = $ {segmentId}
         and adwh_fact_profile_by_segment_and_namespace.merge_policy_id =$ {mergePolicyId}
         and adwh_fact_profile_by_segment_and_namespace.date_key = '${lastProcessDate}'
   )
   a;
```

+++
