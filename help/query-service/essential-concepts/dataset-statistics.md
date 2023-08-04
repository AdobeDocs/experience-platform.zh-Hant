---
title: 資料集統計資料計算
description: 本檔案說明如何使用SQL命令計算Azure Data Lake Storage (ADLS)資料集的欄層級統計資料。
source-git-commit: c05df76976e58da1f96c6e8c030c919ff5b1eb19
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 0%

---

# 資料集統計資料計算

您現在可以在以下位置計算欄層級統計資料： [!DNL Azure Data Lake Storage] (ADLS)資料集與 `COMPUTE STATISTICS` 和 `SHOW STATISTICS` SQL命令。 計算資料集統計資料的SQL命令是 `ANALYZE TABLE` 命令。 的完整詳細資料 `ANALYZE TABLE` 命令位於 [SQL參考檔案](../sql/syntax.md#analyze-table).

>[!NOTE]
>
>計算的統計資料會儲存在具有工作階段層級持續性的暫存表格中。 您可以在該作業階段期間隨時存取運算結果。 無法跨不同的PSQL階段作業存取它們。

若要檢視使用計算的統計資料 `ANALYZE TABLE COMPUTE STATISTICS` 命令之後，您就可以對別名或「統計ID」使用SELECT查詢。 您也可以將統計分析的範圍限制在整個資料集、資料集的子集、所有欄或欄的子集。

>[!IMPORTANT]
>
>此 `COMPUTE STATISTICS`， `FILTERCONTEXT`， `FOR COLUMNS`、和 `SHOW STATISTICS` 加速存放區資料表不支援命令。 這些擴充功能適用於 `ANALYZE TABLE` 目前只有ADLS表格支援命令。 如需詳細資訊，請參閱 [分析表格段落](../sql/syntax.md#analyze-table) SQL語法指南中的。

本指南可協助您建構查詢，以便您計算ADLS資料集的欄統計資料。 使用這些命令，您可以透過PSQL使用者端使用SQL查詢來檢視階段作業中產生的統計資料。

## 計算統計資料 {#compute-statistics}

已將其他建構新增至 `ANALYZE TABLE` 指令可讓您 **資料集子集和特定欄的計算統計資料**. 若要計算資料集統計資料，您必須使用 `ANALYZE TABLE <tableName> COMPUTE STATISTICS` 格式。

>[!IMPORTANT]
>
>預設行為會計算 **整個資料集** 和 **所有欄**. 若要計算所有欄的統計資料，您可以使用查詢格式 `ANALYZE TABLE COMPUTE STATISTICS`. 您是 **非** 建議使用 `COMPUTE STATISTICS` 命令時，不會對ADLS資料集使用篩選條件，因為資料集的大小可能非常大（可能是PB的資料）。 您應該一律考慮使用執行分析指令 `FILTERCONTEXT` 和指定的欄清單。 請參閱以下小節： [限制已分析的欄](#limit-included-columns) 和 [新增篩選條件](#filter-condition) 以取得更多詳細資料。

以下範例計算 `adc_geometric` 資料集和 **全部** 資料集中的欄。

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>此 `COMPUTE STATISTICS` 命令不支援陣列或對應資料型別。 您可以設定 `skip_stats_for_complex_datatypes` 如果輸入資料框架有具有陣列和對應資料型別的欄，則為通知或發生錯誤的標幟。 依預設，標幟會設為true。 若要啟用通知或錯誤，請使用下列命令： `SET skip_stats_for_complex_datatypes = false`.

## 建立別名 {#alias-name}

由於計算結果可能是大量資料，因此直接在主控台輸出中傳回已計算的資料是不合理的。 雖然別名是選用名稱，但建議您在計算統計資料時使用這些別名作為最佳實務。 在陳述式中提供別名，以描述性參考SQL查詢中的結果。 或者，自動產生的 `Statistics ID` 產生並用來儲存計算的資訊。

以下範例將輸出計算統計資料儲存在 `alias_name` 以供日後參考。 查詢中使用的別名可在 `ANALYZE TABLE` 命令已執行。

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS AS alias_name;
```

上述範例的輸出為 `SUCCESSFULLY COMPLETED, alias_name`. 主控台輸出不會在回應analyze table compute statistics命令時顯示統計資料。 若要檢視詳細結果，您必須對別名或「統計值ID」使用SELECT查詢。

## 檢視計算統計資料的輸出 {#view-output-of-computed-statistics}

如果您未預先提供別名，查詢服務會自動為產生名稱 `Statistics ID` 格式如下 `<tableName_stats_{incremental_number}>`. 如果提供了別名，它會顯示在 `Statistics ID` 欄。

範例輸出 `COMPUTE STATISTICS` 查詢如下：

```console
| Statistics ID         | 
| --------------------- |
| adc_geometric_stats_1 |
(1 row)
```

您可以 **直接查詢計算的統計資料** 藉由參考 `Statistics ID`. 以下範例陳述式可讓您在搭配使用時完整檢視輸出 `Statistics ID` 或別名。

```sql
SELECT * FROM adc_geometric_stats_1; 
```

計算的統計資料輸出看起來可能類似於下面的範例。

```console
 columnName                                                 |      mean      |      max       |      min       | standardDeviation | approxDistinctCount | nullCount | dataType  
------------------------------------------------------------+----------------+----------------+----------------+-------------------+---------------------+-----------+-----------
 marketing.trackingcode                                     |            0.0 |            0.0 |            0.0 |               0.0 |              1213.0 |         0 | String
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
(12 rows)
```

## 顯示統計分析中繼資料 {#show-statistics}

您可以使用 `SHOW STATISTICS` 命令來顯示工作階段中產生之所有暫時統計資料的中繼資料。 這個指令可以協助您縮小統計分析的範圍。

範例輸出 `SHOW STATISTICS` 如下所示。

```console
      statsId         |   tableName   | columnSet |         filterContext       |      timestamp
----------------------+---------------+-----------+-----------------------------+--------------------
adc_geometric_stats_1 | adc_geometric |   (age)   |                             | 25/06/2023 09:22:26
demo_table_stats_1    |  demo_table   |    (*)    |       ((age > 25))          | 25/06/2023 12:50:26
age_stats             | castedtitanic |   (age)   | ((age > 25) AND (age < 40)) | 25/06/2023 09:22:26
```

以下提供中繼資料欄名稱的說明。

| 資料行名稱 | 說明 |
|---|---|
| `statsId` | 此ID會參照產生的臨時統計資料表。 `COMPUTE STATISTICS` 命令。 |
| `tableName` | 用於分析的原始表格。 |
| `columnSet` | 特別選擇用於分析的任何欄的清單。 空值表示已分析所有欄。 請參閱以下小節： [限制欄](#limit-included-columns) 以取得詳細資訊。 |
| `filterContext` | 套用至分析的任何篩選器清單。 |
| `timestamp` | 套用至您的資料分析的任何時間順序篩選器，以聚焦於特定時段。 請參閱 [時間戳記篩選條件區段](#filter-condition) 以取得更多詳細資料。 |

您可以隨時在該階段作業中使用SELECT敘述句來查詢計算的統計資料，並使用統計資料ID或別名。 產生的統計值ID和統計值只適用於此特定階段作業，而且無法跨不同的PSQL階段作業存取。 計算的統計資料目前不是持續性的。 請參閱如何操作的區段 [檢視已計算統計資料的輸出](#view-output-of-computed-statistics) 以取得更多詳細資料。

## 限制包含的欄 {#limit-included-columns}

若要集中進行分析，您可以依名稱參照特定資料集欄，藉此計算其統計資料。 使用 `FOR COLUMNS (<col1>, <col2>)` 定位特定欄的語法。 以下範例會計算欄的統計資料  `commerce`， `id`、和 `timestamp` 用於資料集 `tableName`.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

您可以計算任何根層級或巢狀資料行的統計資料。 下列範例示範這些參照。

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## 新增時間戳記篩選條件 {#filter-condition}

若要根據時間順序重點分析欄，您可以新增時間戳記篩選條件。 此條件可用來篩選掉歷史資料，或將資料分析聚焦於特定期間。 此 `FILTERCONTEXT` command會根據您提供的篩選條件，計算資料集子集的統計資料。

在以下範例中，統計資料會在資料集的所有欄上計算 `tableName`，其中欄時間戳記的值介於以下指定範圍之間： `2023-04-01 00:00:00` 和 `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

您可以結合欄限制和篩選器，為您的資料集欄建立高度具體的計算查詢。 例如，下列查詢會計算欄的統計資料 `commerce`， `id`、和 `timestamp` 用於資料集 `tableName`，其中欄時間戳記的值介於以下指定範圍之間： `2023-04-01 00:00:00` 和 `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在已能更加瞭解如何使用SQL查詢，從ADLS資料集產生欄級統計資料。 建議您閱讀 [SQl語法指南](../sql/syntax.md) 以探索Adobe Experience Platform查詢服務的更多功能。
