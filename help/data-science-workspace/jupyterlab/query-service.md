---
keywords: Experience Platform;JupyterLab；筆記型電腦；Data Science Workspace；熱門主題；查詢服務
solution: Experience Platform
title: Jupyter筆記本中的查詢服務
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform可讓您將Query Service整合至JupyterLab作為標準功能，以便在Data Science Workspace中使用結構化查詢語言(SQL)。 本教學課程示範常見使用案例的SQL查詢範例，以探索、轉換和分析Adobe Analytics資料。
exl-id: c5ac7d11-a3bd-4ef8-a650-9f496a8bbaa7
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 1%

---

# Jupyter筆記本中的查詢服務

[!DNL Adobe Experience Platform] 可讓您在 [!DNL Data Science Workspace] 整合 [!DNL Query Service] into [!DNL JupyterLab] 作為標準功能。

本教學課程示範常見使用案例的SQL查詢範例，以供探索、轉換和分析 [!DNL Adobe Analytics] 資料。

## 快速入門

開始本教學課程之前，您必須具備下列必要條件：

- 存取 [!DNL Adobe Experience Platform]. 如果您無權存取 [!DNL Experience Platform]，請在繼續之前與您的系統管理員聯繫

- 安 [!DNL Adobe Analytics] 資料集

- 深入了解本教學課程中使用的下列重要概念：
   - [[!DNL Experience Data Model (XDM) and XDM System]](../../xdm/home.md)
   - [[!DNL Query Service]](../../query-service/home.md)
   - [[!DNL Query Service SQL Syntax]](../../query-service/sql/overview.md)
   - Adobe Analytics

## 存取 [!DNL JupyterLab] 和 [!DNL Query Service] {#access-jupyterlab-and-query-service}

1. 在 [[!DNL Experience Platform]](https://platform.adobe.com)，導覽至 **[!UICONTROL 筆記本]** 從左側導覽欄。 請讓JupyterLab載入一下。

   ![](../images/jupyterlab/query/jupyterlab-launcher.png)

   >[!NOTE]
   >
   >如果未自動顯示新的「啟動器」頁簽，請按一下以開啟新的「啟動器」頁簽 **[!UICONTROL 檔案]** 然後選取 **[!UICONTROL 新啟動器]**.

2. 在「啟動器」標籤中，按一下 **[!UICONTROL 空白]** 表徵圖，以開啟空的筆記本。

   ![](../images/jupyterlab/query/blank_notebook.png)

   >[!NOTE]
   >
   >Python 3是目前筆記型電腦中唯一支援查詢服務的環境。

3. 在左側選取邊欄上，按一下 **[!UICONTROL 資料]** 按兩下 **[!UICONTROL 資料集]** 目錄，列出所有資料集。

   ![](../images/jupyterlab/query/dataset.png)

4. 尋找 [!DNL Adobe Analytics] 要瀏覽的資料集，然後按一下右鍵清單，按一下 **[!UICONTROL 筆記本中的查詢資料]** 在空筆記本中生成SQL查詢。

5. 按一下包含函式的第一個產生儲存格 `qs_connect()` 並按一下播放按鈕執行。 此函式將在筆記本實例和 [!DNL Query Service].

   ![](../images/jupyterlab/query/execute.png)

6. 複製 [!DNL Adobe Analytics] 來自第二個產生的SQL查詢的資料集名稱，將會是 `FROM`.

   ![](../images/jupyterlab/query/dataset_name.png)

7. 按一下 **+** 按鈕。

   ![](../images/jupyterlab/query/insert_cell.gif)

8. 在新儲存格中複製、貼上並執行下列匯入陳述式。 這些陳述式將用於視覺化您的資料：

   ```python
   import plotly.plotly as py
   import plotly.graph_objs as go
   from plotly.offline import iplot
   ```

9. 接著，將下列變數複製並貼到新儲存格中。 視需要修改其值，然後執行它們。

   ```python
   target_table = "your Adobe Analytics dataset name"
   target_year = "2019"
   target_month = "04"
   target_day = "01"
   ```

   - `target_table`:您的 [!DNL Adobe Analytics] 資料集。
   - `target_year`:目標資料的特定年份。
   - `target_month`:目標所在的特定月份。
   - `target_day`:目標資料的來源特定日期。

   >[!NOTE]
   >
   >您隨時都可以變更這些值。 執行此動作時，請務必執行要套用之變更的變數儲存格。

## 查詢您的資料 {#query-your-data}

在單個筆記本單元格中輸入以下SQL查詢。 在查詢的儲存格上選取，然後選取 **[!UICONTROL play]** 按鈕。 成功的查詢結果或錯誤記錄會顯示在執行的儲存格下方。

當筆記本長時間處於非活動狀態時，筆記本和 [!DNL Query Service] 可能會崩潰。 在這種情況下，請重新啟動 [!DNL JupyterLab] 選取 **重新啟動** 按鈕 ![重新啟動按鈕](../images/jupyterlab/user-guide/restart_button.png) 位於電源按鈕旁的右上角。

筆記本內核重置，但單元格將保持，重新運行所有單元格以繼續您離開的位置。

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

在上述查詢中， `WHERE` 子句設定為 `target_year`. 以大括弧包含變數，以在SQL查詢中納入變數(`{}`)。

查詢的第一行包含可選變數 `hourly_visitor`. 查詢結果將作為Pancits資料幀儲存在此變數中。 將結果儲存在資料幀中，可讓您稍後使用所需的視覺化查詢結果 [!DNL Python] 包。 執行下列 [!DNL Python] 新儲存格中的程式碼來產生長條圖：

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

### 每小時活動計數 {#hourly-activity-count}

下列查詢會傳回指定日期的每小時動作計數：

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

執行上述查詢會將結果儲存於 `hourly_actions` 資料幀。 在新儲存格中執行下列函式以預覽結果：

```python
hourly_actions.head()
```

您可以修改上述查詢，以使用 **其中** 子句：

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

執行修改的查詢會將結果儲存在 `hourly_actions_date_range` 資料幀。 在新儲存格中執行下列函式以預覽結果：

```python
hourly_actions_date_rage.head()
```

### 每個訪客工作階段的事件數 {#number-of-events-per-visitor-session}

下列查詢會傳回指定日期每個訪客工作階段的事件數：

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

執行下列 [!DNL Python] 用以為每次造訪工作階段事件數產生色階分佈圖的程式碼：

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

下列查詢會傳回指定日期中10個最受歡迎的頁面：

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

### 指定日期的作用中使用者 {#active-users-for-a-given-day}

下列查詢會傳回指定日期中10個最活躍的使用者：

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

### 按用戶活動列出的活動城市 {#active-cities-by-user-activity}

以下查詢返回在指定日期生成大部分用戶活動的十個城市：

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

本教學課程示範一些使用案例的範例 [!DNL Query Service] in [!DNL Jupyter] 筆記本。 關注 [使用Jupyter Notebooks分析資料](./analyze-your-data.md) 教學課程，以了解如何使用資料存取SDK執行類似操作。
