---
keywords: Experience Platform；JupyterLab；筆記本；資料科學Workspace；熱門主題；查詢服務
solution: Experience Platform
title: Jupyter Notebook中的查詢服務
type: Tutorial
description: Adobe Experience Platform允許您在數據科學工作環境中使用結構化查詢語言（SQL），方法是將查詢服務作為標準功能集成到JupyterLab中。 本教學課程演示了常見用例的示例 SQL 查詢，以探索、轉換和分析Adobe Analytics數據。
exl-id: c5ac7d11-a3bd-4ef8-a650-9f496a8bbaa7
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 0%

---

# Jupyter Notebook中的查詢服務

>[!NOTE]
>
>Data Science Workspace已無法購買。
>
>本檔案旨在供先前有權使用Data Science Workspace的現有客戶使用。

[!DNL Adobe Experience Platform]可讓您將[!DNL Query Service]整合至[!DNL JupyterLab]作為標準功能，以在[!DNL Data Science Workspace]中使用結構化查詢語言(SQL)。

本教學課程示範常見使用案例的範例SQL查詢，以探索、轉換及分析[!DNL Adobe Analytics]資料。

## 快速入門

開始進行本教學課程前，您必須具備下列必要條件：

- 存取[!DNL Adobe Experience Platform]。 如果您沒有[!DNL Experience Platform]中組織的存取權，請在繼續之前與您的系統管理員交談

- [!DNL Adobe Analytics]資料集

- 深入瞭解本教學課程使用的下列重要概念：
   - [[!DNL Experience Data Model (XDM) and XDM System]](../../xdm/home.md)
   - [[!DNL Query Service]](../../query-service/home.md)
   - [[!DNL Query Service SQL Syntax]](../../query-service/sql/overview.md)
   - Adobe Analytics

## 存取 [!DNL JupyterLab] 和 [!DNL Query Service] {#access-jupyterlab-and-query-service}

1. 在 中 [[!DNL Experience Platform]](https://platform.adobe.com)， **[!UICONTROL 從左導覽列導航到“筆記本]** ”。 請稍等片刻讓 JupyterLab 載入。

   ![](../images/jupyterlab/query/jupyterlab-launcher.png)

   >[!NOTE]
   >
   >如果未自動顯示新的啟動器標籤，請按下檔案打開&#x200B;**[!UICONTROL 新的啟動器標籤，然後選擇**&#x200B;[!UICONTROL &#x200B;新&#x200B;]&#x200B;**啟動器]**。

2. 在「啟動器」標籤中，按一下Python 3環境中的&#x200B;**[!UICONTROL 空白]**&#x200B;圖示以開啟空白筆記本。

   ![](../images/jupyterlab/query/blank_notebook.png)

   >[!NOTE]
   >
   >Python 3是目前在筆記型電腦中唯一支援查詢服務的環境。

3. 在左側選取範圍邊欄上，按一下&#x200B;**[!UICONTROL 資料]**&#x200B;圖示，然後按兩下&#x200B;**[!UICONTROL 資料集]**&#x200B;目錄以列出所有資料集。

   ![](../images/jupyterlab/query/dataset.png)

4. 尋找要探索的[!DNL Adobe Analytics]資料集並在清單上按一下滑鼠右鍵，按一下&#x200B;**[!UICONTROL 在筆記本中查詢資料]**&#x200B;以在空白筆記本中產生SQL查詢。

5. 按一下包含函式`qs_connect()`的第一個產生儲存格，然後按一下播放按鈕來執行它。 此函數在筆記本執行個體和 之間 [!DNL Query Service]建立連接。

   ![](../images/jupyterlab/query/execute.png)

6. [!DNL Adobe Analytics]從第二個生成的 SQL 查詢複製 資料集 名稱，它將是 之後`FROM`的值。

   ![](../images/jupyterlab/query/dataset_name.png)

7. 按兩下 **+** 按鈕插入新的筆記本儲存格。

   ![](../images/jupyterlab/query/insert_cell.gif)

8. 在新儲存格中複製、貼上及執行以下匯入陳述式。 這些陳述式將用來視覺化您的資料：

   ```python
   import plotly.plotly as py
   import plotly.graph_objs as go
   from plotly.offline import iplot
   ```

9. 接下來，將下列變數複製並貼到新儲存格中。 視需要修改其值，然後執行。

   ```python
   target_table = "your Adobe Analytics dataset name"
   target_year = "2019"
   target_month = "04"
   target_day = "01"
   ```

   - `target_table`： [!DNL Adobe Analytics]資料集的名稱。
   - `target_year`：目標資料來自的特定年份。
   - `target_month`：目標來自的特定月份。
   - `target_day`：目標資料來源的特定日期。

   >[!NOTE]
   >
   >您可以隨時變更這些值。 執行時，請務必執行變數儲存格以套用變更。

## 查詢您的資料 {#query-your-data}

在個別筆記本儲存格中輸入下列SQL查詢。 在查詢的儲存格上選取，接著選取&#x200B;**[!UICONTROL 播放]**&#x200B;按鈕，以執行查詢。 成功的 查詢 結果或錯誤日誌將顯示在已執行的儲存格下方。

當筆記本長時間處於非活動狀態時，筆記本和 [!DNL Query Service] 筆記本之間的連接可能會中斷。 在這種情況下，請通過選擇&#x200B;**位於電源按鈕右上角的重新啟動**&#x200B;按鈕![重新啟動按鈕](/help/images/icons/restart.png)來重新啟動[!DNL JupyterLab]。

筆記型電腦核心會重設，但儲存格會保留，請重新執行所有儲存格，繼續您中斷的儲存格。

### 每小時訪客計數 {#hourly-visitor-count}

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

在上述查詢中，子句中的 `WHERE` 時間戳設置為 的值 `target_year`。 通過將變數包含在大括弧 （）`{}` 中，將變數包含在 SQL 查詢中。

查詢的第一行包含可選變數 `hourly_visitor`。 查詢結果將作為 Pandas 數據幀存儲在此變數中。 通過將結果存儲在數據幀中，您可以稍後使用所需的 [!DNL Python] 包可視化查詢結果。 在新單元中執行以下 [!DNL Python] 代碼以生成條狀圖：

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

### 每小時活動計数 {#hourly-activity-count}

下列查詢會傳回指定日期的每小時動作計數：

#### 查詢<!-- omit in toc -->

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

執行上述查詢會將結果以`hourly_actions`的資料流形式儲存。 在新儲存格中執行以下函式以預覽結果：

```python
hourly_actions.head()
```

可以修改上述查詢，以使用&#x200B;**WHERE**&#x200B;子句中的邏輯運運算元，傳回指定日期範圍的每小時動作計數：

#### 查詢<!-- omit in toc -->

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

執行修改後的查詢會將結果存儲為 `hourly_actions_date_range` 數據幀。 在新單元格中執行以下函數以預覽結果：

```python
hourly_actions_date_rage.head()
```

### 每個訪客會話的事件数 {#number-of-events-per-visitor-session}

以下查詢返回指定日期内每個訪客會話的事件數：

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

執行下列[!DNL Python]程式碼以產生每次造訪工作階段事件數的長條圖：

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

### 指定日期的熱門頁面 {#popular-pages-for-a-given-day}

下列查詢會傳回指定日期前十個最受歡迎的頁面：

#### 查詢<!-- omit in toc -->

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

### 指定日的作用中使用者 {#active-users-for-a-given-day}

以下查詢將返回指定日期中十個最活躍的使用者：

#### 查詢<!-- omit in toc -->

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

### 依使用者活動列出的活躍城市 {#active-cities-by-user-activity}

下列查詢會傳回在指定日期產生大部分使用者活動的十個城市：

#### 查詢<!-- omit in toc -->

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

本教學課程示範在[!DNL Jupyter]筆記型電腦中運用[!DNL Query Service]的一些使用案例。 請依照[使用Jupyter Notebooks分析您的資料](./analyze-your-data.md)教學課程，瞭解如何使用Data Access SDK執行類似的作業。
