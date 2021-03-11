---
keywords: Experience Platform;JupyterLab；筆記型電腦；資料科學工作區；熱門主題；查詢服務
solution: Experience Platform
title: Jupyter筆記本中的查詢服務
topic: 教學課程
type: 教學課程
description: Adobe Experience Platform允許您將查詢服務整合到JupyterLab中作為標準功能，在資料科學工作區中使用結構化查詢語言(SQL)。 本教程示範SQL查詢範例，以瞭解、轉換和分析Adobe Analytics資料的常見使用案例。
translation-type: tm+mt
source-git-commit: 9d84fc1eb898020ed4b154c091fcc9fc4933c7de
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 1%

---


# Jupyter筆記本中的查詢服務

[!DNL Adobe Experience Platform] 允許您通過將其整合為標準功能， [!DNL Data Science Workspace] 在中 [!DNL Query Service] 使 [!DNL JupyterLab] 用結構化查詢語言。

本教程演示了用於探索、轉換和分析[!DNL Adobe Analytics]資料的常見使用案例的SQL查詢示例。

## 快速入門

開始本教學課程之前，您必須具備下列必要條件：

- 存取[!DNL Adobe Experience Platform]。 如果您沒有[!DNL Experience Platform]中IMS組織的存取權，請在繼續前先與系統管理員聯絡

- [!DNL Adobe Analytics]資料集

- 對本教學課程中使用的下列主要概念有正確認識：
   - [[!DNL Experience Data Model (XDM) and XDM System]](../../xdm/home.md)
   - [[!DNL Query Service]](../../query-service/home.md)
   - [[!DNL Query Service SQL Syntax]](../../query-service/sql/overview.md)
   - Adobe Analytics

## 訪問[!DNL JupyterLab]和[!DNL Query Service] {#access-jupyterlab-and-query-service}

1. 在[[!DNL Experience Platform]](https://platform.adobe.com)中，從左側導航列導航至&#x200B;**[!UICONTROL Notebooks]**。 請讓JupyterLab載入。

   ![](../images/jupyterlab/query/jupyterlab-launcher.png)

   >[!NOTE]
   >
   >如果未自動顯示新的「啟動器」頁籤，請按一下&#x200B;**[!UICONTROL 檔案]** ，然後選擇&#x200B;**[!UICONTROL 新的啟動器]** ，開啟新的「啟動器」頁籤。

2. 在「啟動器」頁籤中，按一下Python 3環境中的&#x200B;**[!UICONTROL Blank]**&#x200B;表徵圖以開啟空的筆記本。

   ![](../images/jupyterlab/query/blank_notebook.png)

   >[!NOTE]
   >
   >Python 3目前是筆記型電腦中唯一支援查詢服務的環境。

3. 在左選邊欄上，按一下&#x200B;**[!UICONTROL Data]**&#x200B;表徵圖，然後按兩下&#x200B;**[!UICONTROL Datasets]**&#x200B;目錄以列出所有資料集。

   ![](../images/jupyterlab/query/dataset.png)

4. 查找要瀏覽的[!DNL Adobe Analytics]資料集並按一下右鍵清單，按一下&#x200B;**[!UICONTROL 筆記本中的查詢資料]**&#x200B;在空的筆記本中生成SQL查詢。

5. 按一下包含函式`qs_connect()`的第一個產生儲存格，然後按一下播放按鈕以執行它。 此函式在筆記本實例和[!DNL Query Service]之間建立連接。

   ![](../images/jupyterlab/query/execute.png)

6. 從第二個生成的SQL查詢中複製[!DNL Adobe Analytics]資料集名稱，它將是`FROM`之後的值。

   ![](../images/jupyterlab/query/dataset_name.png)

7. 按一下&#x200B;**+**&#x200B;按鈕插入新的筆記本單元格。

   ![](../images/jupyterlab/query/insert_cell.gif)

8. 在新儲存格中複製、貼上並執行下列匯入陳述式。 這些陳述將用於直觀顯示您的資料：

   ```python
   import plotly.plotly as py
   import plotly.graph_objs as go
   from plotly.offline import iplot
   ```

9. 接著，將下列變數複製並貼至新儲存格。 視需要修改其值，然後執行這些值。

   ```python
   target_table = "your Adobe Analytics dataset name"
   target_year = "2019"
   target_month = "04"
   target_day = "01"
   ```

   - `target_table` :資料集的 [!DNL Adobe Analytics] 名稱。
   - `target_year` :目標資料的特定年份。
   - `target_month` :目標所在的特定月份。
   - `target_day` :目標資料的特定來源日。

   >[!NOTE]
   >
   >您可以隨時變更這些值。 執行此動作時，請務必執行要套用之變數儲存格。

## 查詢您的資料{#query-your-data}

在單個筆記本單元格中輸入以下SQL查詢。 在查詢的單元格上選擇，然後選擇&#x200B;**[!UICONTROL play]**&#x200B;按鈕，以執行查詢。 成功的查詢結果或錯誤日誌顯示在已執行的單元格下面。

當筆記本長時間處於非活動狀態時，筆記本和[!DNL Query Service]之間的連接可能中斷。 在這種情況下，通過選擇位於電源按鈕旁右上角的&#x200B;**重新啟動**&#x200B;按鈕![重新啟動按鈕](../images/jupyterlab/user-guide/restart_button.png)來重新啟動[!DNL JupyterLab]。

筆記本內核會重設，但儲存格會保留，重新執行所有儲存格，以繼續您離開的位置。

### 每小時訪客計數{#hourly-visitor-count}

下列查詢會傳回指定日期的每小時訪客計數：

#### 查詢

```sql
%%read_sql hourly_visitor -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                               AS Day,
       Substring(timestamp, 12, 2)                               AS Hour, 
       Count(DISTINCT concat(enduserids._experience.aaid.id, 
                             _experience.analytics.session.num)) AS Visit_Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

在上述查詢中，`WHERE`子句中的時間戳設定為`target_year`的值。 在SQL查詢中加入變數，方法是將變數以大括弧(`{}`)包含。

查詢的第一行包含可選變數`hourly_visitor`。 查詢結果將作為Pactices資料幀儲存在此變數中。 將結果儲存在資料幀中可讓您以後使用所需的[!DNL Python]包直觀顯示查詢結果。 在新儲存格中執行下列[!DNL Python]程式碼以產生長條圖：

```python
trace = go.Bar(
    x = hourly_visitor['Hour'],
    y = hourly_visitor['Visit_Count'],
    name = "Visitor Count"
)
layout = go.Layout(
    title = 'Visit Count by Hour of Day',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'Hour of Day'),
    yaxis = dict(title = 'Count')
)
fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

### 每小時活動計數{#hourly-activity-count}

以下查詢返回指定日期的每小時活動計數：

#### 查詢 <!-- omit in toc -->

```sql
%%read_sql hourly_actions -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

執行上述查詢會將結果儲存在`hourly_actions`中作為資料幀。 在新儲存格中執行下列函式以預覽結果：

```python
hourly_actions.head()
```

可以修改上述查詢，使用&#x200B;**WHERE**&#x200B;子句中的邏輯運算子返回指定日期範圍的每小時操作計數：

#### 查詢 <!-- omit in toc -->

```sql
%%read_sql hourly_actions_date_range -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE  timestamp >= TO_TIMESTAMP('2019-06-01 00', 'YYYY-MM-DD HH')
       AND timestamp <= TO_TIMESTAMP('2019-06-02 23', 'YYYY-MM-DD HH')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

執行修改的查詢會將結果儲存在`hourly_actions_date_range`中作為資料幀。 在新儲存格中執行下列函式以預覽結果：

```python
hourly_actions_date_rage.head()
```

### 每個訪客作業的事件數{#number-of-events-per-visitor-session}

下列查詢會傳回指定日期每個訪客作業的事件數：

#### 查詢 <!-- omit in toc -->

```sql
%%read_sql events_per_session -c QS_CONNECTION
SELECT concat(enduserids._experience.aaid.id, 
              '-#', 
              _experience.analytics.session.num) AS aaid_sess_key, 
       Count(timestamp)                          AS Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP BY aaid_sess_key
ORDER BY Count DESC;
```

執行下列[!DNL Python]程式碼，以產生每個瀏覽作業事件數的色階分佈圖：

```python
data = [go.Histogram(x = events_per_session['Count'])]

layout = go.Layout(
    title = 'Histogram of Number of Events per Visit Session',
    xaxis = dict(title = 'Number of Events'),
    yaxis = dict(title = 'Count')
)

fig = go.Figure(data = data, layout = layout)
iplot(fig)
```

### 指定日期的熱門頁面{#popular-pages-for-a-given-day}

下列查詢會傳回指定日期中十個人氣最高的頁面：

#### 查詢 <!-- omit in toc -->

```sql
%%read_sql popular_pages -c QS_CONNECTION
SELECT web.webpagedetails.name                 AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY web.webpagedetails.name 
ORDER  BY page_views DESC 
LIMIT  10;
```

### 指定日期{#active-users-for-a-given-day}的作用中使用者

下列查詢會傳回指定日期中十位最活躍的使用者：

#### 查詢 <!-- omit in toc -->

```sql
%%read_sql active_users -c QS_CONNECTION
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp)               AS Count
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY aaid
ORDER  BY Count DESC
LIMIT  10;
```

### 依使用者活動劃分的活躍城市{#active-cities-by-user-activity}

以下查詢返回在指定日期生成大多數用戶活動的十個城市：

#### 查詢 <!-- omit in toc -->

```sql
%%read_sql active_cities -c QS_CONNECTION
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp)                                                     AS Count
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY state_city
ORDER  BY Count DESC
LIMIT  10;
```

## 後續步驟

本教程演示了在[!DNL Jupyter]筆記本中使用[!DNL Query Service]的一些示例使用案例。 請依照[使用Jupyter Notebooks](./analyze-your-data.md)教學課程分析資料，瞭解如何使用Data Access SDK執行類似作業。