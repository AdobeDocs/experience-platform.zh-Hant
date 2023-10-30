---
title: 探索資料分析
description: 瞭解如何使用Data Distiller來探索和分析Python筆記型電腦的資料。
exl-id: 1dd4cf6e-f7cc-4f4b-afbd-bfc1d342a2c3
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 15%

---

# 探索資料分析

本檔案提供一些使用Data Distiller來探索和分析資料的基本範例和最佳實務。 [!DNL Python] 筆記本。

## 快速入門

在繼續本指南之前，請確定您已建立與Data Distiller的連線， [!DNL Python] 筆記本。 請參閱檔案以瞭解如何 [連線 [!DNL Python] Notebook to Data Distiller](./establish-connection.md).

## 取得基本統計資料 {#basic-statistics}

使用以下程式碼來擷取資料集中的列數和相異設定檔數。

```python
table_name = 'ecommerce_events'

basic_statistics_query = f"""
SELECT
    COUNT(_id) as "totalRows",
    COUNT(DISTINCT _id) as "distinctUsers"
FROM {table_name}"""

df = qs_cursor.query(basic_statistics_query, output="dataframe")
df
```

**範例輸出**

|     | totalRows | distinctUsers |
| --- | ----------- | -------------- |
| 0 | 1276563 | 1276563 |

## 建立大型資料集的取樣版本 {#create-dataset-sample}

如果您要查詢的資料集非常大，或不需要探索查詢的精確結果，請使用 [抽樣功能](../../essential-concepts/dataset-samples.md) 可用於資料Distiller查詢。 此程式分為兩個步驟：

- 首先， **分析** 要以指定取樣比率建立取樣版本的資料集
- 接下來，查詢資料集的抽樣版本。 根據您套用至樣本資料集的函式，您可能想要將輸出縮放為數字以取得完整資料集

### 建立5%樣本 {#create-sample}

以下範例會分析資料集並建立5%範例：

```python
# A sampling rate of 10 is 100% in Query Service, so for 5% use a sampling rate 0.5
sampling_rate = 0.5

analyze_table_query=f"""
SET aqp=true;
ANALYZE TABLE {table_name} TABLESAMPLE SAMPLERATE {sampling_rate}"""

qs_cursor.query(analyze_table_query, output="raw")
```

### 檢視您的範例 {#view-sample}

您可以使用 `sample_meta` 函式，可檢視從指定資料集建立的任何範例。 下列程式碼片段會示範如何使用 `sample_meta` 函式。

```python
sampled_version_of_table_query = f'''SELECT sample_meta('{table_name}')'''

df_samples = qs_cursor.query(sampled_version_of_table_query, output="dataframe")
df_samples
```

**範例輸出**：

|   | sample_table_name | sample_dataset_id | parent_dataset_id | sample_type | sampling_rate | filter_condition_on_source_dataset | sample_num_rows | 已建立 |
|---|---|---|---|---|---|---|---|---|
| 0 | cmle_synthetic_data_experience_event_dataset_c... | 650f7a09ed6c3e28d34d7fc2 | 64fb4d7a7d748828d304a2f4 | 色彩一致 | 0.5 | 6427 | 23/09/2023 | 11:51:37 |

{style="table-layout:auto"}

### 查詢您的範例 {#query-sample-data}

您可以從傳回的中繼資料中參照範例表格名稱，直接查詢範例。 然後，您可將結果乘以取樣比例，以取得預估值。

```python
sample_table_name = df_samples[df_samples["sampling_rate"] == sampling_rate]["sample_table_name"].iloc[0]

count_query=f'''SELECT count(*) as cnt from {sample_table_name}'''

df = qs_cursor.query(count_query, output="dataframe")
# Divide by the sampling rate to extrapolate to the full dataset
approx_count = df["cnt"].iloc[0] / (sampling_rate / 100)

print(f"Approximate count: {approx_count} using {sampling_rate *10}% sample")
```

**範例輸出**

```console
Approximate count: 1284600.0 using 5.0% sample
```

## 電子郵件漏斗分析 {#email-funnel-analysis}

漏斗分析是瞭解達成目標結果所需步驟，以及有多少使用者完成每個步驟的方法。 以下範例說明通往使用者訂閱電子報的步驟的簡單漏斗分析。 訂閱結果以事件型別表示，該事件型別為 `web.formFilledOut`.

首先，執行查詢以取得每個步驟的使用者人數。

```python
simple_funnel_analysis_query = f'''SELECT eventType, COUNT(DISTINCT _id) as "distinctUsers",COUNT(_id) as "distinctEvents" FROM {table_name} GROUP BY eventType ORDER BY distinctUsers DESC'''

funnel_df = qs_cursor.query(simple_funnel_analysis_query, output="dataframe")
funnel_df
```

**範例輸出**

|   | eventType | distinctUsers | distinctEvents |
|---|---|---|---|
| 0 | directMarketing.emailSent | 598840 | 598840 |
| 1 | directMarketing.emailOpened | 239028 | 239028 |
| 2 | web.webpagedetails.pageViews | 120118 | 120118 |
| 3 | advertising.impressions | 119669 | 119669 |
| 4 | directMarketing.emailClicked | 51581 | 51581 |
| 5 | commerce.productViews | 37915 | 37915 |
| 6 | decisioning.propositionDisplay | 37650 | 37650 |
| 7 | web.webinteraction.linkClicks | 37581 | 37581 |
| 8 | web.formFilledOut | 17860 | 17860 |
| 9 | advertising.clicks | 7610 | 7610 |
| 10 | decisioning.propositionInteract | 2964 | 2964 |
| 11 | decisioning.propositionDismiss | 2889 | 2889 |
| 12 | commerce.purchases | 2858 | 2858 |

{style="table-layout:auto"}

### 繪製查詢結果 {#plot-results}

接下來，使用下列工具繪製查詢結果： [!DNL Python] `plotly` 資料庫：

```python
import plotly.express as px

email_funnel_events = ["directMarketing.emailSent", "directMarketing.emailOpened", "directMarketing.emailClicked", "web.formFilledOut"]
email_funnel_df = funnel_df[funnel_df["eventType"].isin(email_funnel_events)]

fig = px.funnel(email_funnel_df, y='eventType', x='distinctUsers')
fig.show()
```

**範例輸出**

![eventType電子郵件漏斗的資訊圖。](../../images/data-distiller/email-funnel.png)

## 事件關聯 {#event-correlations}

另一種常見分析是計算事件型別與目標轉換事件型別之間的關聯。 在此範例中，訂閱事件由表示 `web.formFilledOut`. 此範例使用 [!DNL Spark] 資料Distiller查詢中可用的函式，用以實現下列步驟：

1. 依設定檔計算每種事件型別的事件數。
2. 彙總各設定檔中每種事件型別的計數，並計算每種事件型別的關聯，其中 `web,formFilledOut`.
3. 將計數和相關性的資料流轉換為每個功能的Pearson相關係數（事件型別計數）表格與目標事件。
4. 將結果以視覺化方式顯示在繪圖中。

此 [!DNL Spark] 函式會彙總資料以傳回小型結果表格，因此您可以在完整資料集上執行這類查詢。

```python
large_correlation_query=f'''
SELECT SUM(webFormsFilled) as webFormsFilled_totalUsers,
       SUM(advertisingClicks) as advertisingClicks_totalUsers,
       SUM(productViews) as productViews_totalUsers,
       SUM(productPurchases) as productPurchases_totalUsers,
       SUM(propositionDismisses) as propositionDismisses_totaUsers,
       SUM(propositionDisplays) as propositionDisplays_totaUsers,
       SUM(propositionInteracts) as propositionInteracts_totalUsers,
       SUM(emailClicks) as emailClicks_totalUsers,
       SUM(emailOpens) as emailOpens_totalUsers,
       SUM(webLinkClicks) as webLinksClicks_totalUsers,
       SUM(webPageViews) as webPageViews_totalusers,
       corr(webFormsFilled, emailOpens) as webForms_EmailOpens,
       corr(webFormsFilled, advertisingClicks) as webForms_advertisingClicks,
       corr(webFormsFilled, productViews) as webForms_productViews,
       corr(webFormsFilled, productPurchases) as webForms_productPurchases,
       corr(webFormsFilled, propositionDismisses) as webForms_propositionDismisses,
       corr(webFormsFilled, propositionInteracts) as webForms_propositionInteracts,
       corr(webFormsFilled, emailClicks) as webForms_emailClicks,
       corr(webFormsFilled, emailOpens) as webForms_emailOpens,
       corr(webFormsFilled, emailSends) as webForms_emailSends,
       corr(webFormsFilled, webLinkClicks) as webForms_webLinkClicks,
       corr(webFormsFilled, webPageViews) as webForms_webPageViews
FROM(
    SELECT _{tenant_id}.cmle_id as userID,
            SUM(CASE WHEN eventType='web.formFilledOut' THEN 1 ELSE 0 END) as webFormsFilled,
            SUM(CASE WHEN eventType='advertising.clicks' THEN 1 ELSE 0 END) as advertisingClicks,
            SUM(CASE WHEN eventType='commerce.productViews' THEN 1 ELSE 0 END) as productViews,
            SUM(CASE WHEN eventType='commerce.productPurchases' THEN 1 ELSE 0 END) as productPurchases,
            SUM(CASE WHEN eventType='decisioning.propositionDismiss' THEN 1 ELSE 0 END) as propositionDismisses,
            SUM(CASE WHEN eventType='decisioning.propositionDisplay' THEN 1 ELSE 0 END) as propositionDisplays,
            SUM(CASE WHEN eventType='decisioning.propositionInteract' THEN 1 ELSE 0 END) as propositionInteracts,
            SUM(CASE WHEN eventType='directMarketing.emailClicked' THEN 1 ELSE 0 END) as emailClicks,
            SUM(CASE WHEN eventType='directMarketing.emailOpened' THEN 1 ELSE 0 END) as emailOpens,
            SUM(CASE WHEN eventType='directMarketing.emailSent' THEN 1 ELSE 0 END) as emailSends,
            SUM(CASE WHEN eventType='web.webinteraction.linkClicks' THEN 1 ELSE 0 END) as webLinkClicks,
            SUM(CASE WHEN eventType='web.webinteraction.pageViews' THEN 1 ELSE 0 END) as webPageViews
    FROM {table_name}
    GROUP BY userId
)
'''
large_correlation_df = qs_cursor.query(large_correlation_query, output="dataframe")
large_correlation_df
```

**範例輸出**：

|   | webFormsFilled_totalUsers | advertisingClicks_totalUsers | productViews_totalUsers | productPurchases_totalUsers | propositionDismisses_totaUsers | propositionDisplays_totaUsers | propositionInteracts_totalUsers | emailClicks_totalUsers | emailOpens_totalUsers | webLinksClicks_totalUsers | ... | webForms_advertisingClicks | webForms_productViews | webForms_productPurchases | webForms_propositionDismisses | webForms_propositionInteracts | webForms_emailClicks | webForms_emailOpens | webForms_emailSends | webForms_webLinkClicks | webForms_webPageViews |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 17860 | 7610 | 37915 | 0 | 2889 | 37650 | 2964 | 51581 | 239028 | 37581 | … | 0.026805 | 0.2779 | None | 0.06014 | 0.143656 | 0.305657 | 0.218874 | 0.192836 | 0.259353 | None |

{style="table-layout:auto"}

### 將列轉換為事件型別關聯 {#event-type-correlation}

接下來，將以上查詢輸出中的單一資料列轉換為表格，顯示每個事件型別與目標訂閱事件的關聯：

```python
cols = large_correlation_df.columns
corrdf = large_correlation_df[[col for col in cols if ("webForms_"  in col)]].melt()
corrdf["feature"] = corrdf["variable"].apply(lambda x: x.replace("webForms_", ""))
corrdf["pearsonCorrelation"] = corrdf["value"]

corrdf.fillna(0)
```

**範例輸出**：

|    | 變數 | 值 | 功能 | pearsonCorrelation |
| --- | ---  |  ---  |  ---  | --- |
| 0 | `webForms_EmailOpens` | 0.218874 | EmailOpens | 0.218874 |
| 1 | `webForms_advertisingClicks` | 0.026805 | 廣告點選次數 | 0.026805 |
| 2 | `webForms_productViews` | 0.277900 | 產品檢視 | 0.277900 |
| 3 | `webForms_productPurchases` | 0.000000 | productPurchases | 0.000000 |
| 4 | `webForms_propositionDismisses` | 0.060140 | propositionDismiss | 0.060140 |
| 5 | `webForms_propositionInteracts` | 0.143656 | propositionInteracts | 0.143656 |
| 6 | `webForms_emailClicks` | 0.305657 | 電子郵件點按次數 | 0.305657 |
| 7 | `webForms_emailOpens` | 0.218874 | emailOpens | 0.218874 |
| 8 | `webForms_emailSends` | 0.192836 | 電子郵件傳送 | 0.192836 |
| 9 | `webForms_webLinkClicks` | 0.259353 | webLinkClicks | 0.259353 |
| 10 | `webForms_webPageViews` | 0.000000 | webPageViews | 0.000000 |


最後，您可以將下列各項的相關性視覺化： `matplotlib` Python資料庫：

```python
import matplotlib.pyplot as plt
fig, ax = plt.subplots(figsize=(5,10))
sns.barplot(data=corrdf.fillna(0), y="feature", x="pearsonCorrelation")
ax.set_title("Pearson Correlation of Events with the outcome event")
```

![事件結果的事件皮爾遜關聯長條圖](../../images/data-distiller/pearson-correlations.png)

## 後續步驟

閱讀本檔案後，您已瞭解如何使用Data Distiller來探索和分析資料 [!DNL Python] 筆記本。 在機器學習環境中，從Experience Platform建立功能管道以饋送自訂模型的 [機器學習的工程師功能](./feature-engineering.md).
