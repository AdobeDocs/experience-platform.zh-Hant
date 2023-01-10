---
keywords: Experience Platform;JupyterLab；筆記型電腦；資料科學工作區；熱門主題；分析資料筆記型電腦；eda；探索資料分析；資料科學
solution: Experience Platform
title: 探索資料分析(EDA)筆記型電腦
type: Tutorial
description: 本指南著重說明如何使用探索資料分析(EDA)筆記型電腦來探索網路資料中的模式、以預測目標聚合事件、清除匯總資料，以及了解預測者與目標之間的關係。
exl-id: 48209326-0a07-4b5c-8b49-a2082a78fa47
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '2760'
ht-degree: 0%

---

# 使用探索資料分析(EDA)筆記型電腦探索基於Web的資料以建立預測模型

探索資料分析(EDA)筆記型電腦旨在協助您探索資料中的模式、檢查資料的健全性，以及匯總預測模型的相關資料。

針對EDA筆記型電腦實例，結合Web資料進行了優化，包括兩部分。 第一部分從使用查詢服務查看趨勢和資料快照開始。 接下來，考量探索資料分析的目標時，會在設定檔和訪客層級匯總資料。

第二部分從使用Python庫對聚合資料執行描述性分析開始。 此筆記型電腦會展示色階分佈圖、散布圖、方塊圖和關聯矩陣等視覺效果，以衍生可操作的深入分析，用於判斷哪些功能最有可能有助於預測目標。

## 快速入門

閱讀本指南之前，請先檢閱 [[!DNL JupyterLab] 使用手冊](./overview.md) 的 [!DNL JupyterLab] 及其在Data Science Workspace中的角色。 此外，如果您正在使用自己的資料，請查閱 [資料存取 [!DNL Jupyterlab] 筆記本](./access-notebook-data.md). 本指南包含有關筆記本資料限制的重要資訊。

此筆記型電腦使用Analytics Analysis Workspace中Adobe Analytics Experience Events資料形式的中值資料集。 要使用EDA筆記本，需要使用以下值定義資料表 `target_table` 和 `target_table_id`. 任何中值資料集皆可使用。

若要尋找這些值，請遵循 [用python寫入資料集](./access-notebook-data.md#write-python) JupyterLab資料存取指南的一節。 資料集名稱(`target_table`)位於資料集目錄中。 在您以滑鼠右鍵按一下資料集，即可在筆記型電腦中探索或寫入資料後，資料集ID(`target_table_id`)提供於可執行程式碼項目中。

## 資料探索

本節包含用來檢視趨勢的設定步驟和範例查詢，例如「依使用者活動排名前10的城市」或「檢視前10的產品」。

### 程式庫的設定

JupyterLab支援多個程式庫。 可將下列程式碼貼上並在程式碼儲存格中執行，以收集和安裝此範例中使用的所有必要套件。 您可以使用此範例以外的其他或替代套件，以自行進行資料分析。 如需支援套件的清單，請複製並貼上 `!pip list --format=columns` 在新單元格中。

```python
!pip install colorama
import chart_studio.plotly as py
import plotly.graph_objs as go
from plotly.offline import iplot
from scipy import stats
import numpy as np
import warnings
warnings.filterwarnings('ignore')
from scipy.stats import pearsonr
import matplotlib.pyplot as plt
from scipy.stats import pearsonr
import pandas as pd
import math
import re
import seaborn as sns
from datetime import datetime
import colorama
from colorama import Fore, Style
pd.set_option('display.max_columns', None)
pd.set_option('display.max_rows', None)
pd.set_option('display.width', 1000)
pd.set_option('display.expand_frame_repr', False)
pd.set_option('display.max_colwidth', -1)
```

### 連線至Adobe Experience Platform [!DNL Query Service]

[!DNL JupyterLab] 在平台上，可讓您在 [!DNL Python] 筆記型電腦，通過 [查詢服務](https://www.adobe.com/go/query-service-home-en). 透過 [!DNL Query Service] 因為執行時間長，因此可用於處理大型資料集。 請注意，使用 [!DNL Query Service] 處理時間限制為10分鐘。

使用之前 [!DNL Query Service] in [!DNL JupyterLab]，確保您對 [[!DNL Query Service] SQL語法](https://www.adobe.com/go/query-service-sql-syntax-en).

要在JupyterLab中利用查詢服務，必須首先在工作的Python筆記本和查詢服務之間建立連接。 這可透過執行下列儲存格來達成。

```python
qs_connect()
```

### 定義中值資料集以進行探索

若要開始查詢和探索資料，必須提供中值資料集表格。 複製並更換 `table_name` 和 `table_id` 值與您自己的資料表值。

```python
target_table = "table_name"
target_table_id = "table_id"
```

完成後，此儲存格看起來應類似下列範例：

```python
target_table = "cross_industry_demo_midvalues"
target_table_id = "5f7c40ef488de5194ba0157a"
```

### 探索資料集以取得可用日期

使用下方提供的儲存格，即可檢視表格中涵蓋的日期範圍。 探索天數、首日和最後日期的目的，是協助選取日期範圍以供進一步分析。

```python
%%read_sql -c QS_CONNECTION
SELECT distinct Year(timestamp) as Year, Month(timestamp) as Month, count(distinct DAY(timestamp)) as Count_days, min(DAY(timestamp)) as First_date, max(DAY(timestamp)) as Last_date, count(timestamp) as Count_hits
from {target_table}
group by Month(timestamp), Year(timestamp)
order by Year, Month;
```

運行單元格將生成以下輸出：

![查詢日期輸出](../images/jupyterlab/eda/query-date-output.PNG)

### 設定資料集探索的日期

決定資料集探索的可用日期後，需更新下列參數。 此儲存格中設定的日期僅用於查詢形式的資料探索。 本指南稍後會將日期重新更新至適當的範圍，以便進行探索資料分析。

```python
target_year = "2020" ## The target year
target_month = "02" ## The target month
target_day = "(01,02,03)" ## The target days
```

### 資料集探索

設定好所有參數後，請開始 [!DNL Query Service]，且有日期範圍，您就可以開始讀取資料列了。 您應限制讀取的列數。

```python
from platform_sdk.dataset_reader import DatasetReader
from datetime import date
dataset_reader = DatasetReader(PLATFORM_SDK_CLIENT_CONTEXT, dataset_id=target_table_id)
# If you do not see any data or would like to expand the default date range, change the following query
Table = dataset_reader.limit(5).read()
```

若要檢視資料集中可用的欄數，請使用下列儲存格：

```python
print("\nNumber of columns:",len(Table.columns))
```

若要檢視資料集的列，請使用下列儲存格。 在此範例中，列數限制為五。

```python
Table.head(5)
```

![表格列輸出](../images/jupyterlab/eda/data-table-overview.PNG)

了解資料集中包含哪些資料後，進一步劃分資料集就十分實用。 在此示例中，列出每列的列名和資料類型，而輸出用於檢查資料類型是否正確。

```python
ColumnNames_Types = pd.DataFrame(Table.dtypes)
ColumnNames_Types = ColumnNames_Types.reset_index()
ColumnNames_Types.columns = ["Column_Name", "Data_Type"]
ColumnNames_Types
```

![欄名稱和資料類型清單](../images/jupyterlab/eda/data-columns.PNG)

### 資料集趨勢探索

以下章節包含四個查詢範例，用於探索資料中的趨勢和模式。 下列範例並非詳盡無遺，而是涵蓋一些較常檢視的功能。

**指定日的每小時活動計數**

此查詢會分析一天中的動作和點按次數。 輸出會以表格的形式表示，表格包含一天中每小時活動計數的量度。

```sql
%%read_sql query_2_df -c QS_CONNECTION

SELECT Substring(timestamp, 12, 2)                        AS Hour, 
       Count(enduserids._experience.aaid.id) AS Count 
FROM   {target_table}
WHERE  Year(timestamp) = {target_year} 
       AND Month(timestamp) = {target_month}  
       AND Day(timestamp) in {target_day}
GROUP  BY Hour
ORDER  BY Hour;
```

![查詢1輸出](../images/jupyterlab/eda/hour-count-raw.PNG)

確認查詢後，資料可以呈現在單變數的圖形直方圖中，以求視覺清晰。

```python
trace = go.Bar(
    x = query_2_df['Hour'],
    y = query_2_df['Count'],
    name = "Activity Count"
)

layout = go.Layout(
    title = 'Activity Count by Hour of Day',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'Hour of Day'),
    yaxis = dict(title = 'Count')
)

fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

![查詢1的條形圖輸出](../images/jupyterlab/eda/activity-count-by-hour-of-day.png)

**指定日期前10個檢視頁面**

此查詢會分析指定一天中檢視次數最多的頁面。 輸出會以包含頁面名稱和頁面檢視計數量度的表格形式表示。

```sql
%%read_sql query_4_df -c QS_CONNECTION

SELECT web.webpagedetails.name                 AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE  Year(timestamp) = {target_year}
       AND Month(timestamp) = {target_month}
       AND Day(timestamp) in {target_day}
GROUP  BY web.webpagedetails.name 
ORDER  BY page_views DESC 
LIMIT  10;
```

確認查詢後，資料可以呈現在單變數的圖形直方圖中，以求視覺清晰。

```python
trace = go.Bar(
    x = query_4_df['Page_Name'],
    y = query_4_df['Page_Views'],
    name = "Page Views"
)

layout = go.Layout(
    title = 'Top Ten Viewed Pages For a Given Day',
    width = 1000,
    height = 600,
    xaxis = dict(title = 'Page_Name'),
    yaxis = dict(title = 'Page_Views')
)

fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

![前10個檢視頁面](../images/jupyterlab/eda/top-ten-viewed-pages-for-a-given-day.png)

**依使用者活動分組的前10個城市**

此查詢會分析資料的來源城市。

```sql
%%read_sql query_6_df -c QS_CONNECTION

SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp)                                                     AS Count
FROM   {target_table}
WHERE  Year(timestamp) = {target_year}
       AND Month(timestamp) = {target_month}
       AND Day(timestamp) in {target_day}
GROUP  BY state_city
ORDER  BY Count DESC
LIMIT  10;
```

確認查詢後，資料可以呈現在單變數的圖形直方圖中，以求視覺清晰。

```python
trace = go.Bar(
    x = query_6_df['state_city'],
    y = query_6_df['Count'],
    name = "Activity by City"
)

layout = go.Layout(
    title = 'Top Ten Cities by User Activity',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'City'),
    yaxis = dict(title = 'Count')
)

fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

![十大城市](../images/jupyterlab/eda/top-ten-cities-by-user-activity.png)

**前10名檢視產品**

此查詢提供前10個檢視產品的清單。 在以下範例中， `Explode()` 函式可用來傳回 `productlistitems` 物件。 這可讓您執行巢狀查詢，以匯總不同SKU的產品檢視。

```sql
%%read_sql query_7_df -c QS_CONNECTION

SELECT Product_List_Items.sku AS Product_SKU,
       Sum(Product_Views) AS Total_Product_Views
FROM  (SELECT Explode(productlistitems) AS Product_List_Items, 
              commerce.productviews.value   AS Product_Views 
       FROM   {target_table}
       WHERE  Year(timestamp) = {target_year}
              AND Month(timestamp) = {target_month}
              AND Day(timestamp) in {target_day}
              AND commerce.productviews.value IS NOT NULL) 
GROUP BY Product_SKU 
ORDER BY Total_Product_Views DESC
LIMIT  10;
```

確認查詢後，資料可以呈現在單變數的圖形直方圖中，以求視覺清晰。

```python
trace = go.Bar(
    x = "SKU-" + query_7_df['Product_SKU'],
    y = query_7_df['Total_Product_Views'],
    name = "Product View"
)

layout = go.Layout(
    title = 'Top Ten Viewed Products',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'SKU'),
    yaxis = dict(title = 'Product View Count')
)

fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

![前10個產品檢視](../images/jupyterlab/eda/top-ten-viewed-products.png)

在探索資料的趨勢和模式之後，您應該清楚了解要建立哪些功能以預測目標。 瀏覽表格可以快速突顯每個資料屬性的形式、明顯的錯誤表示和值中的大量離群值，並開始提出候選關係以探討屬性之間的關係。

## 探索資料分析

探索性資料分析可用來改善您對資料的了解，並建立引人入勝的問題的直覺，以作為建模的基礎。

完成資料探索步驟後，您將探索事件層級的資料，在事件、城市或使用者ID層級進行一些匯總，以查看一天的趨勢。 雖然此資料很重要，但並未完整說明。 您仍不了解網站上促成購買的因素。

若要了解這點，您需要在設定檔/訪客層級匯總資料、定義購買目標，並套用關聯、方塊圖和散布圖等統計概念。 這些方法可用來比較您所定義之預測視窗中買方與非買方的活動模式。

本節將建立並探討下列功能：

- `COUNT_UNIQUE_PRODUCTS_PURCHASED`:購買的不重複產品數量。
- `COUNT_CHECK_OUTS`:結帳次數。
- `COUNT_PURCHASES`:購買次數。
- `COUNT_INSTANCE_PRODUCTADDS`:產品新增例項的數量。
- `NUMBER_VISITS`:造訪次數。
- `COUNT_PAID_SEARCHES`:付費搜尋的數量。
- `DAYS_SINCE_VISIT`:距離上次造訪的天數。
- `TOTAL_ORDER_REVENUE`:總訂單收入。
- `DAYS_SINCE_PURCHASE`:距離上次購買的天數。
- `AVG_GAP_BETWEEN_ORDERS_DAYS`:購買之間的平均間隔（以天為單位）。
- `STATE_CITY`:包含州和城市。

在繼續進行資料匯總之前，您需要為探索性資料分析中使用的預測變數定義參數。 換句話說，您想從資料科學模型中得到什麼？ 常見參數包括目標、預測週期和分析週期。

如果使用EDA筆記本，則在繼續操作之前，需要替換以下值。

```python
goal = "commerce.`order`.purchaseID" #### prediction variable
goal_column_type = "numerical" #### choose either "categorical" or "numerical"
prediction_window_day_start = "2020-01-01" #### YYYY-MM-DD
prediction_window_day_end = "2020-01-31" #### YYYY-MM-DD
analysis_period_day_start = "2020-02-01" #### YYYY-MM-DD
analysis_period_day_end = "2020-02-28" #### YYYY-MM-DD

### If the goal is a categorical goal then select threshold for the defining category and creating bins. 0 is no order placed, and 1 is at least one order placed:
threshold = 1
```

### 功能和目標建立的資料匯總

若要開始探索性分析，您必須在設定檔層級建立目標，然後匯總資料集。 在此範例中，提供兩個查詢。 第一個查詢包含目標的建立。 第二個查詢需要更新，以包含第一個查詢中除了變數以外的任何變數。 您可以更新 `limit` 的子句。 執行下列查詢後，現在可探索匯總的資料。

```sql
%%read_sql target_df -d -c QS_CONNECTION

SELECT DISTINCT endUserIDs._experience.aaid.id                  AS ID,
       Count({goal})                                            AS TARGET
FROM   {target_table}
WHERE DATE(TIMESTAMP) BETWEEN '{prediction_window_day_start}' AND '{prediction_window_day_end}'
GROUP BY endUserIDs._experience.aaid.id;
```

```sql
%%read_sql agg_data -d -c QS_CONNECTION

SELECT z.*, z1.state_city as STATE_CITY
from
((SELECT y.*,a2.AVG_GAP_BETWEEN_ORDERS_DAYS as AVG_GAP_BETWEEN_ORDERS_DAYS
from
(select a1.*, f.DAYS_SINCE_PURCHASE as DAYS_SINCE_PURCHASE
from
(SELECT DISTINCT a.ID  AS ID,
COUNT(DISTINCT Product_Items.SKU) as COUNT_UNIQUE_PRODUCTS_PURCHASED,
COUNT(a.check_out) as COUNT_CHECK_OUTS,
COUNT(a.purchases) as COUNT_PURCHASES, 
COUNT(a.product_list_adds) as COUNT_INSTANCE_PRODUCTADDS,
sum(CASE WHEN a.search_paid = 'TRUE' THEN 1 ELSE 0 END) as COUNT_PAID_SEARCHES,
DATEDIFF('{analysis_period_day_end}', MAX(a.date_a)) as DAYS_SINCE_VISIT,
ROUND(SUM(Product_Items.priceTotal * Product_Items.quantity), 2) AS TOTAL_ORDER_REVENUE
from 
(SELECT endUserIDs._experience.aaid.id as ID,
commerce.`checkouts`.value as check_out,
commerce.`order`.purchaseID as purchases, 
commerce.`productListAdds`.value as product_list_adds,
search.isPaid as search_paid,
DATE(TIMESTAMP) as date_a,
Explode(productlistitems) AS Product_Items
from {target_table}
Where DATE(TIMESTAMP) BETWEEN '{analysis_period_day_start}' AND '{analysis_period_day_end}') as a
group by a.ID) as a1
left join 
(SELECT DISTINCT endUserIDs._experience.aaid.id as ID,
DATEDIFF('{analysis_period_day_end}', max(DATE(TIMESTAMP))) as DAYS_SINCE_PURCHASE
from {target_table}
where DATE(TIMESTAMP) BETWEEN '{analysis_period_day_start}' AND '{analysis_period_day_end}'
and commerce.`order`.purchaseid is not null
GROUP BY endUserIDs._experience.aaid.id) as f
on f.ID = a1.ID
where a1.COUNT_PURCHASES>0) as y
left join
(select ab.ID, avg(DATEDIFF(ab.ORDER_DATES, ab.PriorDate)) as AVG_GAP_BETWEEN_ORDERS_DAYS
from
(SELECT distinct endUserIDs._experience.aaid.id as ID, TO_DATE(DATE(TIMESTAMP)) as ORDER_DATES, 
TO_DATE(LAG(DATE(TIMESTAMP),1) OVER (PARTITION BY endUserIDs._experience.aaid.id ORDER BY DATE(TIMESTAMP))) as PriorDate
FROM {target_table}
where DATE(TIMESTAMP) BETWEEN '{analysis_period_day_start}' AND '{analysis_period_day_end}'
AND commerce.`order`.purchaseid is not null) AS ab
where ab.PriorDate is not null
GROUP BY ab.ID) as a2
on a2.ID = y.ID) z    
left join
(select t.ID, t.state_city from
(
SELECT DISTINCT endUserIDs._experience.aaid.id as ID,
concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) as state_city, 
ROW_NUMBER() OVER(PARTITION BY endUserIDs._experience.aaid.id ORDER BY DATE(TIMESTAMP) DESC) AS ROWNUMBER
FROM   {target_table}
WHERE  DATE(TIMESTAMP) BETWEEN '{analysis_period_day_start}' AND '{analysis_period_day_end}') as t
where t.ROWNUMBER = 1) z1
on z.ID = z1.ID)
limit 500000;
```

### 合併匯總資料集中的功能與目標

下列儲存格可用來合併上一個範例中概述之匯總資料集的功能與預測目標。

```python
Data = pd.merge(agg_data,target_df, on='ID',how='left')
Data['TARGET'].fillna(0, inplace=True)
```

接下來的三個範例儲存格是用來確認合併成功。

`Data.shape` 傳回欄數後接列數，例如：(11913, 12)。

```python
Data.shape
```

`Data.head(5)` 傳回含有5列資料的表格。 傳回的表格包含所有12欄已對應至設定檔ID的匯總資料。

```python
Data.head(5)
```

![範例表格](../images/jupyterlab/eda/raw-aggregate-data.PNG)

此儲存格會列印不重複設定檔的數量。

```python
print("Count of unique profiles:", (len(Data)))
```

### 檢測丟失值和離群值

完成資料匯總並與目標合併後，您需要檢閱有時稱為資料健康狀況檢查的資料。

此過程涉及識別缺失值和離群值。 當發現問題時，下一個任務是制定具體的策略來處理這些問題。

>[!NOTE]
>
>在此步驟中，您可能會發現值損壞，這些值可能指示資料記錄過程中的故障。

```python
Missing = pd.DataFrame(round(Data.isnull().sum()*100/len(Data),2))
Missing.columns =['Percentage_missing_values'] 
Missing['Features'] = Missing.index
```

以下儲存格用於視覺化遺失的值。

```python
trace = go.Bar(
    x = Missing['Features'],
    y = Missing['Percentage_missing_values'],
    name = "Percentage_missing_values")

layout = go.Layout(
    title = 'Missing values',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'Features'),
    yaxis = dict(title = 'Percentage of missing values')
)

fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

![缺少值](../images/jupyterlab/eda/missing-values.png)

在檢測到丟失值後，識別離群值至關重要。 平均值、標準差和關聯等參數統計對離群值非常敏感。 此外，常用統計過程的假設（如線性回歸）也基於這些統計資料。 這意味著離群值真的會搞砸分析。

為了識別離群值，此範例使用四分位數範圍。 四分位數範圍(IQR)是第一個和第三個四分位數（第25和第75個百分位數）之間的範圍。 此示例收集所有低於第25個百分位數的IQR的1.5倍，或低於第75個百分位數的IQR的1.5倍的資料點。 落在其中一個以下的值，會在下列儲存格中定義為極端值。

>[!TIP]
>
>糾正異常值需要你了解你所從事的業務和行業。 有時，您無法只因為觀察值是極端值而捨棄觀察值。 離群值可以是合法的觀察值，而且往往是最有趣的觀察值。 若要進一步了解如何刪除離群值，請造訪 [可選資料清除步驟](#optional-data-clean).

```python
TARGET = Data.TARGET

Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
Data_numerical.drop(['TARGET'],axis = 1,inplace = True)
Data_numerical1 = Data_numerical

for i in range(0,len(Data_numerical1.columns)):
    Q1 = Data_numerical1.iloc[:,i].quantile(0.25)
    Q3 = Data_numerical1.iloc[:,i].quantile(0.75)
    IQR = Q3 - Q1
    Data_numerical1.iloc[:,i] = np.where(Data_numerical1.iloc[:,i]<(Q1 - 1.5 * IQR),np.nan, np.where(Data_numerical1.iloc[:,i]>(Q3 + 1.5 * IQR),
                                                                                                    np.nan,Data_numerical1.iloc[:,i]))
    
Outlier = pd.DataFrame(round(Data_numerical1.isnull().sum()*100/len(Data),2))
Outlier.columns =['Percentage_outliers'] 
Outlier['Features'] = Outlier.index   
```

和以往一樣，將結果視覺化非常重要。

```python
trace = go.Bar(
    x = Outlier['Features'],
    y = Outlier['Percentage_outliers'],
    name = "Percentage_outlier")

layout = go.Layout(
    title = 'Outliers',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'Features'),
    yaxis = dict(title = 'Percentage of outliers')
)

fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

![離群圖](../images/jupyterlab/eda/outliers.png)

### 單變數分析

修正資料中遺失的值和離群值後，您就可以開始分析。 分析有三種類型：單變數、雙變數及多變數分析。 單變數分析會使用單變數關係擷取資料、摘要，以及尋找資料中的模式。 雙變數分析一次會查看多個變數，而多變數分析一次會查看三個或多個變數。

以下示例將生成一個表，以可視化特徵的分佈。

```python
Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
distribution = pd.DataFrame([Data_numerical.count(),Data_numerical.mean(),Data_numerical.quantile(0), Data_numerical.quantile(0.01),
                             Data_numerical.quantile(0.05),Data_numerical.quantile(0.25), Data_numerical.quantile(0.5),
                        Data_numerical.quantile(0.75),  Data_numerical.quantile(0.95),Data_numerical.quantile(0.99), Data_numerical.max()])
distribution = distribution.T
distribution.columns = ['Count', 'Mean', 'Min', '1st_perc','5th_perc','25th_perc', '50th_perc','75th_perc','95th_perc','99th_perc','Max']
distribution
```

![功能分佈](../images/jupyterlab/eda/distribution-of-features.PNG)

在功能分佈後，您可以使用陣列來建立視覺化的資料圖表。 下列儲存格可用來以數值資料視覺化上表。

```python
A = sns.palplot(sns.color_palette("Blues"))
```

```python
for column in Data_numerical.columns[0:]:
    plt.figure(figsize=(5, 4))
    plt.ticklabel_format(style='plain', axis='y')
    sns.distplot(Data_numerical[column], color = A, kde=False, bins=6, hist_kws={'alpha': 0.4});
```

![數值資料圖](../images/jupyterlab/eda/univaiate-graphs.png)

### 類別資料

分組分類資料用於了解聚合資料的每一列中包含的值及其分佈。 此示例使用前10個類別來協助繪製分佈。 請務必注意，欄中可能包含數千個不重複值。 您不想呈現雜亂的圖案，使其無法辨認。 考慮到您的業務目標，將資料分組可產生更有意義的結果。

```python
Data_categorical = Data.select_dtypes(include='object')
Data_categorical.drop(['ID'], axis = 1, inplace = True, errors = 'ignore')
```

```python
for column in Data_categorical.columns[0:]:
    if (len(Data_categorical[column].value_counts())>10):
        plt.figure(figsize=(12, 8))
        sns.countplot(x=column, data = Data_categorical, order = Data_categorical[column].value_counts().iloc[:10].index, palette="Set2");
    else:
        plt.figure(figsize=(12, 8))
        sns.countplot(x=column, data = Data_categorical, palette="Set2");
```

![分類欄](../images/jupyterlab/eda/graph-category.PNG)

### 僅刪除單個不重複值的列

只有值的欄不會新增任何資訊至分析，且可移除。

```python
for col in Data.columns:
    if len(Data[col].unique()) == 1:
        if col == 'TARGET':
            print(Fore.RED + '\033[1m' + 'WARNING: TARGET HAS A SINGLE UNIQUE VALUE, ANY BIVARIATE ANALYSIS (NEXT STEP IN THIS NOTEBOOK) OR PREDICTION WILL BE MEANINGLESS' + Fore.RESET + '\x1b[21m')
        elif col == 'ID':
            print(Fore.RED + '\033[1m' + 'WARNING: THERE IS ONLY ONE PROFILE IN THE DATA, ANY BIVARIATE ANALYSIS (NEXT STEP IN THIS NOTEBOOK) OR PREDICTION WILL BE MEANINGLESS' + Fore.RESET + '\x1b[21m')
        else:
            print('Dropped column:',col)
            Data.drop(col,inplace=True,axis=1)
```

移除單值欄後，請使用 `Data.columns` 命令。

### 對缺少的值正確

以下章節包含一些修正遺失值的範例方法。 事件（在上述資料中）雖然只有一欄缺少值，但所有資料類型的正確值下方的範例儲存格。 這些類別包括：

- 數值資料類型：適用時輸入0或最大值
- 類別資料類型：輸入模態值

```python
#### Select only numerical data
Data_numerical = Data.select_dtypes(include=['float64', 'int64'])

#### For columns that contain days we impute max days of history for null values, for rest all we impute 0

# Imputing days with max days of history
Days_cols = [col for col in Data_numerical.columns if 'DAYS_' in col]
d1 = datetime.strptime(analysis_period_day_start, "%Y-%m-%d")
d2 = datetime.strptime(analysis_period_day_end, "%Y-%m-%d")
A = abs((d2 - d1).days)

for column in Days_cols:
    Data[column].fillna(A, inplace=True)

# Imputing 0
Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
Missing_numerical = Data_numerical.columns[Data_numerical.isnull().any()].tolist()

for column in Missing_numerical:
    Data[column].fillna(0, inplace=True)
```

```python
#### Correct for missing values in categorical columns (Replace with mode)
Data_categorical = Data.select_dtypes(include='object')
Missing_cat = Data_categorical.columns[Data_categorical.isnull().any()].tolist() 
for column in Missing_cat:
    Data[column].fillna(Data[column].mode()[0], inplace=True)
```

完成後，乾淨的資料便可用於雙變數分析。

### 雙變數分析

雙變數分析可用來協助了解兩組值（例如您的功能和目標變數）之間的關係。 由於不同的圖應用於類別和數值資料類型，因此應針對每個資料類型分別進行此分析。 建議使用下列圖表進行雙變數分析：

- **關聯**:相關係數是測量兩個特徵之間關係的強度。 關聯的值介於–1和1之間，其中：1表示強正關係，-1表示強負關係，而結果為零表示完全沒有關係。
- **配對圖**:配對圖是視覺化每個變數之間關係的簡單方式。 它會產生資料中每個變數之間關係的矩陣。
- **熱度圖**:熱度圖是資料集中所有變數的相關係數。
- **框圖**:方塊圖是根據五個數字摘要(最小、第一四分位數(Q1)、中位數、第三四分位數(Q3)和最大值)來顯示資料分佈的標準化方式。
- **計數圖**:計數圖就像某些類別特徵的色階分佈圖或長條圖。 它會根據特定類型的類別顯示項目的發生次數。

為了了解「目標」變數與預測器/功能之間的關係，會根據資料類型使用圖表。 對於數值特徵，如果「目標」變數是類別，則應使用方塊圖；如果「目標」變數是數值，則也應使用配對圖和熱度圖。

對於類別特徵，如果「goal」變數為類別，則應使用計數圖；如果「goal」變數為數值，則也應使用方塊圖。 使用這些方法有助於了解關係。 這些關係可以是功能、預測器和目標的形式。

**數值預測器**

```python
if len(Data) == 1:
    print(Fore.RED + '\033[1m' + 'THERE IS ONLY ONE PROFILE IN THE DATA, BIVARIATE ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE AT LEAST ONE MORE PROFILE TO DO BIVARIATE ANALYSIS')
elif len(Data['TARGET'].unique()) == 1:
    print(Fore.RED + '\033[1m' + 'TARGET HAS A SINGLE UNIQUE VALUE, BIVARIATE ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE PROFILES WITH ATLEAST ONE DIFFERENT VALUE OF TARGET TO DO BIVARIATE ANALYSIS')
else:
    if (goal_column_type == "categorical"):
        TARGET_categorical = pd.DataFrame(np.where(TARGET>=threshold,"1","0"))
        TARGET_categorical.rename(columns={TARGET_categorical.columns[0]: "TARGET_categorical" }, inplace = True)
        Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
        Data_numerical.drop(['TARGET'],inplace=True,axis=1)
        Data_numerical = pd.concat([Data_numerical, TARGET_categorical.astype(int)], axis = 1)
        ncols_for_charts = len(Data_numerical.columns)-1
        nrows_for_charts = math.ceil(ncols_for_charts/4)
        fig, axes = plt.subplots(nrows=nrows_for_charts, ncols=4, figsize=(18, 15))
        for idx, feat in enumerate(Data_numerical.columns[:-1]):
            ax = axes[int(idx // 4), idx % 4]
            sns.boxplot(x='TARGET_categorical', y=feat, data=Data_numerical, ax=ax)
            ax.set_xlabel('')
            ax.set_ylabel(feat)
            fig.tight_layout();
    else:
        Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
        TARGET = pd.DataFrame(Data_numerical.TARGET)
        Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
        Data_numerical.drop(['TARGET'],inplace=True,axis=1)
        Data_numerical = pd.concat([Data_numerical, TARGET.astype(int)], axis = 1)
        for i in Data_numerical.columns[:-1]:
            sns.pairplot(x_vars=i, y_vars=['TARGET'], data=Data_numerical, height = 4)
        f, ax = plt.subplots(figsize = (10,8))
        corr = Data_numerical.corr()
```

執行儲存格會產生下列輸出：

![圖](../images/jupyterlab/eda/bivariant-graphs.png)

![熱度圖](../images/jupyterlab/eda/bi-graph10.PNG)

**類別預測器**

以下範例用於繪製和檢視每個類別變數的前10個類別的頻率圖。

```python
if len(Data) == 1:
    print(Fore.RED + '\033[1m' + 'THERE IS ONLY ONE PROFILE IN THE DATA, BIVARIATE ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE AT LEAST ONE MORE PROFILE TO DO BIVARIATE ANALYSIS')
elif len(Data['TARGET'].unique()) == 1:
    print(Fore.RED + '\033[1m' + 'TARGET HAS A SINGLE UNIQUE VALUE, BIVARIATE ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE PROFILES WITH ATLEAST ONE DIFFERENT VALUE OF TARGET TO DO BIVARIATE ANALYSIS')
else:
    if (goal_column_type == "categorical"):
        TARGET_categorical = pd.DataFrame(np.where(TARGET>=threshold,"1","0"))
        TARGET_categorical.rename(columns={TARGET_categorical.columns[0]: "TARGET_categorical" }, inplace = True)
        Data_categorical = Data.select_dtypes(include='object')
        Data_categorical.drop(["ID"], axis =1, inplace = True)
        Cat_columns = Data_categorical
        Data_categorical = pd.concat([TARGET_categorical,Data_categorical], axis =1)
        for column in Cat_columns.columns:
            A = Data_categorical[column].value_counts().iloc[:10].index
            Data_categorical1 = Data_categorical[Data_categorical[column].isin(A)]
            plt.figure(figsize=(12, 8))
            sns.countplot(x="TARGET_categorical",hue=column, data = Data_categorical1, palette = 'Blues')
            plt.xlabel("GOAL")
            plt.ylabel("COUNT")
            plt.show();
    else:
        Data_categorical = Data.select_dtypes(include='object')
        Data_categorical.drop(["ID"], axis =1, inplace = True)
        Target = Data.TARGET
        Data_categorical = pd.concat([Data_categorical,Target], axis =1)
        for column in Data_categorical.columns[:-1]:
            A = Data_categorical[column].value_counts().iloc[:10].index
            Data_categorical1 = Data_categorical[Data_categorical[column].isin(A)]
            sns.catplot(x=column, y="TARGET", kind = "boxen", data =Data_categorical1, height=5, aspect=13/5);
```

運行單元格將生成以下輸出：

![類別關係](../images/jupyterlab/eda/categorical-predictor.PNG)

### 重要數值特徵

使用關聯分析，您可以建立前10個重要數值特徵的清單。 這些功能都可用來預測「目標」功能。 此清單可用作開始建立模型時的特徵清單。

```python
if len(Data) == 1:
    print(Fore.RED + '\033[1m' + 'THERE IS ONLY ONE PROFILE IN THE DATA, BIVARIATE ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE AT LEAST ONE MORE PROFILE TO FIND IMPORTANT VARIABLES')
elif len(Data['TARGET'].unique()) == 1:
    print(Fore.RED + '\033[1m' + 'TARGET HAS A SINGLE UNIQUE VALUE, BIVARIATE ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE PROFILES WITH ATLEAST ONE DIFFERENT VALUE OF TARGET TO FIND IMPORTANT VARIABLES')
else:
    Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
    Correlation = pd.DataFrame(Data_numerical.drop("TARGET", axis=1).apply(lambda x: x.corr(Data_numerical.TARGET)))
    Correlation['Corr_abs'] = abs(Correlation)
    Correlation = Correlation.sort_values(by = 'Corr_abs', ascending = False)
    Imp_features = pd.DataFrame(Correlation.index[0:10])
    Imp_features.rename(columns={0:'Important Feature'}, inplace=True)
    print(Imp_features)
```

![重要功能](../images/jupyterlab/eda/important-feature-model.PNG)

### 範例分析

在您分析資料的過程中，揭露深入分析並不罕見。 以下範例是可映射目標事件的造訪間隔和貨幣值的分析。

```python
# Proxy for monetary value is TOTAL_ORDER_REVENUE and proxy for frequency is NUMBER_VISITS
if len(Data) == 1:
    print(Fore.RED + '\033[1m' + 'THERE IS ONLY ONE PROFILE IN THE DATA, INSIGHTS ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE AT LEAST ONE MORE PROFILE TO FIND IMPORTANT VARIABLES')
elif len(Data['TARGET'].unique()) == 1:
    print(Fore.RED + '\033[1m' + 'TARGET HAS A SINGLE UNIQUE VALUE, INSIGHTS ANALYSIS IS NOT APPLICABLE, PLEASE INCLUDE PROFILES WITH ATLEAST ONE DIFFERENT VALUE OF TARGET TO FIND IMPORTANT VARIABLES')
else:
    sns.lmplot("DAYS_SINCE_VISIT", "TOTAL_ORDER_REVENUE", Data, hue="TARGET", fit_reg=False);
```

![範例分析](../images/jupyterlab/eda/insight.PNG)

## 可選資料清除步驟 {#optional-data-clean}

糾正異常值需要你了解你所從事的業務和行業。 有時，您無法只因為觀察值是極端值而捨棄觀察值。 離群值可以是合法的觀察值，而且往往是最有趣的觀察值。

有關離群值以及是否刪除離群值的詳細資訊，請從 [分析因素](https://www.theanalysisfactor.com/outliers-to-drop-or-not-to-drop/).

下列範例儲存格大寫和地板資料點，使用 [間隔範圍](https://www.thoughtco.com/what-is-the-interquartile-range-rule-3126244).

```python
TARGET = Data.TARGET

Data_numerical = Data.select_dtypes(include=['float64', 'int64'])
Data_numerical.drop(['TARGET'],axis = 1,inplace = True)

for i in range(0,len(Data_numerical.columns)):
    Q1 = Data_numerical.iloc[:,i].quantile(0.25)
    Q3 = Data_numerical.iloc[:,i].quantile(0.75)
    IQR = Q3 - Q1
    Data_numerical.iloc[:,i] = np.where(Data_numerical.iloc[:,i]<(Q1 - 1.5 * IQR), (Q1 - 1.5 * IQR), np.where(Data_numerical.iloc[:,i]>(Q3 + 1.5 * IQR),
                                                                                                     (Q3 + 1.5 * IQR),Data_numerical.iloc[:,i]))
Data_categorical = Data.select_dtypes(include='object')
Data = pd.concat([Data_categorical, Data_numerical, TARGET], axis = 1)
```

## 後續步驟

完成探索資料分析後，即可開始建立模型。 或者，您也可以使用衍生的資料和深入分析，以使用工具(例如Power BI)建立控制面板。

Adobe Experience Platform將模型建立程式分為兩個不同的階段：方式（模型例項）和模型。 若要開始建立方式，請瀏覽相關檔案 [在JupyerLab Notebooks中建立配方](./create-a-model.md). 本檔案包含在中建立、訓練和計分的資訊和範例，方式為 [!DNL JupyterLab] 筆記本。
