---
title: 客戶資料平台(CDP)洞察力資料模型
description: 瞭解如何使用CDP Insights資料模型中的SQL查詢來定制您自己的CDP報告，以用於您的營銷和KPI使用案例。
source-git-commit: 62e282138de8cf2d74b4a62f4ced39e3fb78001a
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 0%

---

# （測試版）客戶資料平台(CDP)洞察力資料模型

>[!IMPORTANT]
>
>CDP Insights資料模型功能是測試版。 其功能和文檔可能會更改。

客戶資料平台(CDP)Insights資料模型功能公開了資料模型和SQL，這些模型和SQL為各種配置檔案、目標和分段小部件提供了見解。 您可以自定義這些SQL查詢模板，以為您的市場營銷和關鍵績效指標(KPI)使用案例建立CDP報告。 然後，這些見解可以用作已使用定義儀表板的自定義小部件。

## 先決條件

本指南要求對 [用戶定義的儀表板功能](./user-defined-dashboards.md)。 請閱讀文檔，然後繼續閱讀本指南。

## CDP深入瞭解報告和使用案例

CDP報告可讓您深入瞭解您的配置檔案資料及其與段和目標的關係。 針對各種常見的營銷用例，開發了各種星型模式模型，每個資料模型都能支援多種使用例。

>[!IMPORTANT]
>
>用於CDP報告的資料對於所選合併策略和最近的每日快照是準確的。

### 輪廓模型 {#profile-model}

配置檔案模型由三個資料集組成：

- `adwh_dim_date`
- `adwh_fact_profile`
- `adwh_dim_merge_policies`

下圖包含每個資料集中的相關資料欄位。

![配置檔案模型的ERD。](./images/cdp-insights/profile-model.png)

#### 配置檔案計數使用案例

用於配置檔案計數構件的邏輯返回建立快照時配置檔案儲存中合併的配置檔案總數。 查看 [[!UICONTROL 配置檔案計數] 構件文檔](./guides/profiles.md#profile-count) 的子菜單。

生成 [!UICONTROL 配置檔案計數] 在下面的可折疊部分中可以看到小部件。

++SQL查詢

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

#### 單一身份配置檔案使用案例

用於 [!UICONTROL 單個身份配置檔案] 小部件提供了組織的配置檔案計數，這些配置檔案只具有一種類型的ID類型，可建立其標識。 查看[[!UICONTROL 單個身份配置檔案] 構件文檔](./guides/profiles.md#single-identity-profiles) 的子菜單。

生成 [!UICONTROL 單個身份配置檔案] 在下面的可折疊部分中可以看到小部件。

++SQL查詢

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

命名空間模型由以下資料集組成：

- `adwh_fact_profile_by_namespace`
- `adwh_dim_date`
- `adwh_dim_namespaces`
- `adwh_dim_merge_policies`

下圖包含每個資料集中的相關資料欄位。

![命名空間模型的ERD。](./images/cdp-insights/namespace-model.png)

#### 按標識用例分列的配置檔案

的 [!UICONTROL 按身份顯示的配置檔案] 小部件顯示配置檔案儲存中所有合併配置檔案的標識細分。 查看 [[!UICONTROL 按身份顯示的配置檔案] 構件文檔](./guides/profiles.md#profiles-by-identity) 的子菜單。

生成 [!UICONTROL 按身份顯示的配置檔案] 在下面的可折疊部分中可以看到小部件。

++SQL查詢

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

#### 按身份用例劃分的單個身份配置檔案

用於 [!UICONTROL 單個身份配置檔案（按身份）] 構件說明了僅使用單個唯一標識符標識的配置檔案的總數。 查看 [按身份構件文檔劃分的單個身份配置檔案](./guides/profiles.md#single-identity-profiles-by-identity) 的子菜單。

生成 [!UICONTROL 單個身份配置檔案（按身份）] 在下面的可折疊部分中可以看到小部件。

++SQL查詢

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

### 段模型 {#segment-model}

段模型由以下資料集組成：

- `adwh_dim_date`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_fact_profile_by_segment`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

下圖包含每個資料集中的相關資料欄位。

![段模型的ERD。](./images/cdp-insights/segment-model.png)

#### 受眾大小使用案例

用於 [!UICONTROL 受眾大小] 構件返回在最近快照時選定段內合併的配置檔案總數。 查看 [[!UICONTROL 受眾大小] 構件文檔](./guides/segments.md#audience-size) 的子菜單。

生成 [!UICONTROL 受眾大小] 在下面的可折疊部分中可以看到小部件。

++SQL查詢

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

#### 受眾大小更改趨勢使用案例

用於 [!UICONTROL 受眾大小變化趨勢] 構件提供線形圖圖，說明在最近的每日快照之間限定給定段的配置檔案總數之間的差異。 查看 [[!UICONTROL 受眾大小變化趨勢] 構件文檔](./guides/segments.md#audience-size-change-trend) 的子菜單。

生成 [!UICONTROL 受眾大小變化趨勢] 在下面的可折疊部分中可以看到小部件。

++SQL查詢

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

#### 最常用的目標使用案例

中使用的邏輯 [!UICONTROL 最常用的目標] 小部件根據映射到的段數列出組織最常用的目標。 此排名可以深入瞭解哪些目標正被利用，同時可能還顯示那些可能未充分利用的目標。 請參閱 [[!UICONTROL 最常用的目標] 構件](./guides/destinations.md#most-used-destinations) 的子菜單。

生成 [!UICONTROL 最常用的目標] 在下面的可折疊部分中可以看到小部件。

++SQL查詢

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

#### 最近激活的段使用案例

邏輯 [!UICONTROL 最近激活的段] 構件提供最近映射到目標的段的清單。 此清單提供系統中正在使用的段和目標的快照，並有助於排除任何錯誤映射。 查看 [[!UICONTROL 最近激活的段] 構件文檔](./guides/destinations.md#recently-activated-segments) 的子菜單。

生成 [!UICONTROL 最近激活的段] 在下面的可折疊部分中可以看到小部件。

++SQL查詢

```sql
SELECT segment_name, segment, destination_name, a.create_time create_time
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id = c.destination_id
ORDER BY create_time desc, segment LIMIT 5;
```

+++

### 命名空間段模型

命名空間段模型由以下資料集組成：

- `adwh_dim_date`
- `adwh_dim_merge_policies`
- `adwh_dim_namespaces`
- `adwh_fact_profile_by_segment_and_namespace`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

下圖包含每個資料集中的相關資料欄位。

![段模型的ERD。](./images/cdp-insights/namespace-segment-model.png)

#### 按段用例標識的配置檔案

中使用的邏輯 [!UICONTROL 按身份顯示的配置檔案] 小部件提供給定段的配置檔案儲存中所有合併配置檔案的標識的細分。 查看 [[!UICONTROL 按身份顯示的配置檔案] 構件文檔](./guides/segments.md#profiles-by-identity) 的子菜單。

生成 [!UICONTROL 按身份顯示的配置檔案] 在下面的可折疊部分中可以看到小部件。

++SQL查詢

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

重疊命名空間模型由以下資料集組成：

- `adwh_dim_date`
- `adwh_dim_namespaces`
- `adwh_fact_profile_overlap_of_namespace`
- `adwh_dim_merge_policies`

下圖包含每個資料集中的相關資料欄位。

![段模型的ERD。](./images/cdp-insights/overlap-namespace-model.png)

#### 身份重疊（配置檔案）用例

中使用的邏輯 [!UICONTROL 身份重疊] 小部件顯示您的配置檔案的重疊 **配置檔案儲存** 包含兩個選定身份。 有關詳細資訊，請參見 [[!UICONTROL 身份重疊] 小部件部分 [!UICONTROL 配置檔案] 儀表板文檔](./guides/profiles.md#identity-overlap)。

生成 [!UICONTROL 身份重疊] 在下面的可折疊部分中可以看到小部件。

++SQL查詢

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

### 按段模型的重疊命名空間

按段模型劃分的重疊命名空間由以下資料集組成：

- `adwh_dim_date`
- `adwh_dim_namespaces`
- `adwh_fact_profile_overlap_of_namespace_by_segment`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

下圖包含每個資料集中的相關資料欄位。

![段模型的ERD。](./images/cdp-insights/overlap-namespace-by-segment-model.png)

#### 標識重疊（段）用例

中使用的邏輯 [!UICONTROL 段] 儀表板 [!UICONTROL 身份重疊] 構件說明了包含特定段的兩個選定標識的配置檔案的重疊。 有關詳細資訊，請參見 [[!UICONTROL 身份重疊] 小部件部分 [!UICONTROL 分段] 儀表板文檔](./guides/segments.md#identity-overlap)。

生成 [!UICONTROL 身份重疊] 在下面的可折疊部分中可以看到小部件。

++SQL查詢

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
