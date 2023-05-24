---
keywords: Experience Platform;JupyterLab；筆記本；Data Science Workspace；熱門主題；查詢服務
solution: Experience Platform
title: Jupyter筆記本中的查詢服務
type: Tutorial
description: Adobe Experience Platform允許您將查詢服務整合到JupyterLab中作為標準功能，從而在資料科學工作區中使用結構化查詢語言(SQL)。 本教程演示了SQL查詢示例，這些示例用於查看、轉換和分析Adobe Analytics資料。
exl-id: c5ac7d11-a3bd-4ef8-a650-9f496a8bbaa7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 1%

---

# Jupyter筆記本中的查詢服務

[!DNL Adobe Experience Platform] 允許您在 [!DNL Data Science Workspace] 通過 [!DNL Query Service] 入 [!DNL JupyterLab] 作為標準特徵。

本教程演示了示例SQL查詢，用於瀏覽、轉換和分析常用用例 [!DNL Adobe Analytics] 資料。

## 快速入門

在啟動本教程之前，您必須具備以下先決條件：

- 訪問 [!DNL Adobe Experience Platform]。 如果您沒有訪問 [!DNL Experience Platform]，請在繼續之前與您的系統管理員聯繫

- 安 [!DNL Adobe Analytics] 資料集

- 對本教程中使用的以下關鍵概念的有效理解：
   - [[!DNL Experience Data Model (XDM) and XDM System]](../../xdm/home.md)
   - [[!DNL Query Service]](../../query-service/home.md)
   - [[!DNL Query Service SQL Syntax]](../../query-service/sql/overview.md)
   - Adobe Analytics

## 訪問 [!DNL JupyterLab] 和 [!DNL Query Service] {#access-jupyterlab-and-query-service}

1. 在 [[!DNL Experience Platform]](https://platform.adobe.com)，導航 **[!UICONTROL 筆記本]** 的下界。 請稍等片刻，讓JupyterLab載入。

   ![](../images/jupyterlab/query/jupyterlab-launcher.png)

   >[!NOTE]
   >
   >如果未自動顯示新的「啟動程式」頁籤，請按一下 **[!UICONTROL 檔案]** 選擇 **[!UICONTROL 新建啟動程式]**。

2. 在「啟動程式」頁籤中，按一下 **[!UICONTROL 空白]** 表徵圖以開啟空筆記本。

   ![](../images/jupyterlab/query/blank_notebook.png)

   >[!NOTE]
   >
   >Python 3當前是筆記本中唯一受支援的查詢服務環境。

3. 在左側選擇滑軌上，按一下 **[!UICONTROL 資料]** 表徵圖並按兩下 **[!UICONTROL 資料集]** 清單所有資料集的目錄。

   ![](../images/jupyterlab/query/dataset.png)

4. 查找 [!DNL Adobe Analytics] 要瀏覽的資料集並按一下右鍵清單，請按一下 **[!UICONTROL 在筆記本中查詢資料]** 在空筆記本中生成SQL查詢。

5. 按一下包含該函式的第一個生成的單元格 `qs_connect()` 並通過按一下播放按鈕執行。 此函式在您的筆記本實例和 [!DNL Query Service]。

   ![](../images/jupyterlab/query/execute.png)

6. 複製 [!DNL Adobe Analytics] 資料集名稱，它將是 `FROM`。

   ![](../images/jupyterlab/query/dataset_name.png)

7. 按一下 **+** 按鈕

   ![](../images/jupyterlab/query/insert_cell.gif)

8. 在新單元格中複製、貼上和執行以下導入語句。 這些語句將用於可視化您的資料：

   ```python
   import plotly.plotly as py
   import plotly.graph_objs as go
   from plotly.offline import iplot
   ```

9. 接下來，在新單元格中複製並貼上以下變數。 根據需要修改其值，然後執行它們。

   ```python
   target_table = "your Adobe Analytics dataset name"
   target_year = "2019"
   target_month = "04"
   target_day = "01"
   ```

   - `target_table`:您的名稱 [!DNL Adobe Analytics] 資料集。
   - `target_year`:目標資料的特定年份。
   - `target_month`:目標所在的特定月份。
   - `target_day`:目標資料的特定日期。

   >[!NOTE]
   >
   >您可以隨時更改這些值。 執行此操作時，確保為要應用的更改執行變數單元格。

## 查詢資料 {#query-your-data}

在單個筆記本單元格中輸入以下SQL查詢。 通過在其單元格上選擇，然後選擇 **[!UICONTROL 玩]** 按鈕 成功的查詢結果或錯誤日誌顯示在執行的單元格下面。

當筆記本處於長時間非活動狀態時，筆記本和 [!DNL Query Service] 可能會崩潰。 在這種情況下，請重新啟動 [!DNL JupyterLab] 選擇 **重新啟動** 按鈕 ![重新啟動按鈕](../images/jupyterlab/user-guide/restart_button.png) 位於電源按鈕旁的右上角。

筆記本內核將重置，但單元格將保留，重新運行所有單元格以繼續離開的位置。

### 每小時訪問者計數 {#hourly-visitor-count}

以下查詢返回指定日期的小時訪問者計數：

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

在上述查詢中， `WHERE` 子句設定為 `target_year`。 將變數包含在大括弧中(`{}`)。

查詢的第一行包含可選變數 `hourly_visitor`。 查詢結果將作為Pactis資料幀儲存在此變數中。 將結果儲存在資料幀中允許您稍後使用所需的 [!DNL Python] 檔案。 執行以下操作 [!DNL Python] 在新單元格中生成條形圖的代碼：

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

以下查詢返回指定日期的小時操作計數：

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

執行上述查詢將將結果儲存在 `hourly_actions` 資料幀。 在新單元格中執行以下函式以預覽結果：

```python
hourly_actions.head()
```

可以修改上述查詢，以使用邏輯運算子返回指定日期範圍的小時操作計數 **位置** 子句：

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

執行修改的查詢將結果儲存在 `hourly_actions_date_range` 資料幀。 在新單元格中執行以下函式以預覽結果：

```python
hourly_actions_date_rage.head()
```

### 每訪問者會話的事件數 {#number-of-events-per-visitor-session}

以下查詢返回指定日期的每個訪問者會話的事件數：

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

執行以下操作 [!DNL Python] 生成每次訪問會話事件數直方圖的代碼：

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

### 指定日期的常用頁面 {#popular-pages-for-a-given-day}

以下查詢返回指定日期的十個最常用頁面：

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

### 指定日期的活動用戶 {#active-users-for-a-given-day}

以下查詢返回指定日期的十個最活躍的用戶：

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

### 按用戶活動列出的活躍城市 {#active-cities-by-user-activity}

以下查詢返回為指定日期生成大多數用戶活動的十個城市：

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

本教程演示了一些使用案例的示例 [!DNL Query Service] 在 [!DNL Jupyter] 筆記本。 關注 [使用Jupyter筆記本分析資料](./analyze-your-data.md) 教程，瞭解如何使用資料存取SDK執行類似操作。
