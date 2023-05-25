---
title: 資料集統計資料計算
description: 本檔案說明如何使用SQL命令計算Azure Data Lake Storage (ADLS)資料集的資料行層級統計資料。
source-git-commit: b063bcf7b3d2079715ac18fde55f47cea078b609
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# 資料集統計資料計算

您現在可以在以下位置計算欄層級統計資料： [!DNL Azure Data Lake Storage] (ADLS)資料集具有 `COMPUTE STATISTICS` 和 `SHOW STATISTICS` SQL命令。 計算資料集統計資料的SQL命令是 `ANALYZE TABLE` 命令。 的完整詳細資料 `ANALYZE TABLE` 命令位於 [SQL參考檔案](../sql/syntax.md#analyze-table).

>[!NOTE]
>
>目前，產生的統計資料僅對該工作階段有效，不會持續存在於工作階段之間。 無法跨不同的PSQL階段作業存取這些專案。

使用 `SHOW STATISTICS FOR <alias_name>` 命令後，您可以看到使用計算出的統計資料 `ANALYZE TABLE COMPUTE STATISTICS` 命令。 透過這些命令的組合，您現在可以計算整個資料集、資料集子集、所有欄或欄子集上的欄統計資料。

>[!IMPORTANT]
>
>此 `COMPUTE STATISTICS`， `FILTERCONTEXT`， `FOR COLUMNS`、和 `SHOW STATISTICS` Data Warehouse表格不支援命令。 這些擴充功能適用於 `ANALYZE TABLE` 目前只有ADLS表格支援命令。 如需詳細資訊，請參閱 [分析表格段落](../sql/syntax.md#analyze-table) SQL語法指南中的。

本指南可協助您建構查詢，以便您計算ADLS資料集的欄統計資料。 使用這些命令，您可以透過使用SQL查詢的PSQL使用者端，檢視工作階段中產生的統計資料。

## 計算統計資料 {#compute-statistics}

已將其他建構新增至 `ANALYZE TABLE` 命令允許您 **資料集子集和特定欄的計算統計資料**. 若要這麼做，您必須使用 `ANALYZE TABLE <tableName> COMPUTE STATISTICS` 格式。

>[!IMPORTANT]
>
>預設行為會計算 **整個資料集** 和for **所有欄**. 若要計算所有欄的統計資料，您可以使用查詢格式 `ANALYZE TABLE COMPUTE STATISTICS`. 您是 **not** 建議將此用於ADLS資料集，因為資料集的大小可能非常大（可能是PB的資料）。 您應一律考慮使用下列專案執行分析命令： `FILTERCONTEXT` 和指定的欄清單。 請參閱以下小節： [限制分析的欄](#limit-included-columns) 和 [新增篩選條件](#filter-condition) 以取得更多詳細資料。

以下範例會計算 `adc_geometric` 資料集和 **全部** 資料集中的欄。

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>`COMPUTE STATISTICS` 不支援陣列或對應資料型別。 您可以設定 `skip_stats_for_complex_datatypes` 標幟在輸入資料流有具有陣列和對應資料型別的欄時收到通知或發生錯誤。 根據預設，標幟會設為true。 若要啟用通知或錯誤，請使用下列命令： `SET skip_stats_for_complex_datatypes = false`.

<!-- Commented out until the <alias_name> feature is released.
This second example, is a more real-world example as it uses an alias name. See the [alias name section](#alias-name) for more details on this feature.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS as <alias_name>;
``` -->

主控台輸出不會顯示回應analyze table compute statistics命令的統計資料。 相反地，主控台將顯示單列欄， `Statistics ID` 具有通用唯一識別碼以參考結果。 成功完成 `COMPUTE STATISTICS` 查詢，結果顯示如下：

```console
| Statistics ID    | 
| ---------------- |
| QqMtDfHQOdYJpZlb |
(1 row)
```

若要檢視輸出，您必須使用 `SHOW STATISTICS` 命令。 指示 [如何顯示統計資料](#show-statistics) 稍後在檔案中提供。

## 限制包含的欄 {#limit-included-columns}

您可以依名稱參照特定資料集欄，以計算其統計資料。 使用 `FOR COLUMNS (<col1>, <col2>)` 定位特定欄的語法。 以下範例會計算欄的統計資料  `commerce`， `id`、和 `timestamp` 用於資料集 `tableName`.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

您可以計算任何根層級或巢狀資料行的統計資料。 下列範例示範這些參照。

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## 新增時間戳記篩選條件 {#filter-condition}

您可以新增時間戳記篩選條件，以集中分析欄。 這可用來篩選掉歷史資料，或將您的資料分析聚焦於特定時段。 此 `FILTERCONTEXT` command會根據您提供的篩選條件，計算資料集子集的統計資料。

在以下範例中，統計資料會在資料集的所有欄上計算 `tableName`，其中欄時間戳記的值介於指定的範圍之間 `2023-04-01 00:00:00` 和 `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

您可以結合欄限制和篩選器，為您的資料集欄建立高度特定的計算查詢。 例如，下列查詢會計算欄的統計資料 `commerce`， `id`、和 `timestamp` 用於資料集 `tableName`，其中欄時間戳記的值介於指定的範圍之間 `2023-04-01 00:00:00` 和 `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR (columns commerce, id, timestamp);
```

<!-- ## Create an alias name {#alias-name}

Since the filter condition and the column list can target a large amount of data, it is unrealistic to remember the exact values. Instead, you can provide an `<alias_name>` to store this calculated information. If you do not provide an alias name for these calculations, Query Service generates a universally unique identifier for the alias ID. You can then use this alias ID to look up the computed statistics with the `SHOW STATISTICS` command. 

>[!NOTE]
>
>Although alias names are optional, you are recommended to use them as best practice.

The example below stores the output computed statistics in the `alias_name` for later reference.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS FOR ALL COLUMNS as alias_name;
```

The output for the above example is `SUCCESSFULLY COMPLETED, alias_name`. The console output does not display the statistics in the response of the analyze table compute statistics command. To see the output, you must use the `SHOW STATISTICS` command discussed below. -->

## 顯示統計資料 {#show-statistics}

<!-- Commented out until the <alias_name> feature is released.
The alias name used in the query is available as soon as the `ANALYZE TABLE` command has been run.  -->

即使使用篩選條件和欄清單，計算仍可鎖定大量資料。 查詢服務會產生統計資料ID的通用唯一識別碼，以儲存此計算的資訊。 然後，您可以使用此統計資料ID來查詢運算出的統計資料，並附上 `SHOW STATISTICS` 命令。

產生的統計值ID和統計值只適用於此特定階段作業，無法跨不同的PSQL階段作業存取。 計算的統計資料目前不是永久性的。 若要顯示統計資料，請使用下列命令。

```sql
SHOW STATISTICS FOR <STATISTICS_ID>;
```

輸出內容可能類似於以下範例。

```console
                         columnName                         |      mean      |      max       |      min       | standardDeviation | approxDistinctCount | nullCount | dataType  
------------------------------------------------------------+----------------+----------------+----------------+-------------------+---------------------+-----------+-----------
 marketing.trackingcode                                     |            0.0 |            0.0 |            0.0 |               0.0 |              1213.0 |         0 | String
 _experience.analytics.session.timestamp                    |            450 |          -2313 |          21903 |               7.0 |                 0.0 |         0 | Long
 _experience.analytics.customdimensions.evars.evar13        |            0.0 |            0.0 |            0.0 |               0.0 |              8765.0 |        20 | String
 _experience.analytics.customdimensions.evars.evar74        |            0.0 |            0.0 |            0.0 |               0.0 |                11.0 |         0 | String
 web.webpagedetails.name                                    |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | String
 _experience.analytics.event1to100.event8.value             |            5.0 |         9077.0 |          123.0 |              10.0 |              1001.0 |        80 | Double
 search.ispaid                                              |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | Boolean
 commerce.productlistviews.value                            |            0.0 |            0.0 |            0.0 |               0.0 |                 0.0 |        10 | Double
 device.typeid                                              |            0.0 |            0.0 |            0.0 |               0.0 |                 0.0 |        10 | String
 commerce.purchases.value                                   |          765.0 |        98760.0 |         -980.0 |              32.0 |                99.0 |        90 | Double
 _experience.analytics.customdimensions.props.prop45        |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | String
 environment.browserdetails.javaenabled                     |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | Boolean
 timestamp                                                  |            0.0 |            0.0 |            0.0 |               0.0 |                98.0 |         3 | Timestamp
(13 rows)
```

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在就能更清楚瞭解如何使用SQL查詢從ADLS資料集產生欄層級統計資料。 建議您閱讀 [SQl語法指南](../sql/syntax.md) 以探索Adobe Experience Platform查詢服務的更多功能。
