---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics
solution: Experience Platform
title: Jupyter筆記本中的查詢服務
topic: Tutorial
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 1%

---


# Jupyter筆記本中的查詢服務

[!DNL Adobe Experience Platform] 允許您通過將結構化查詢語言(SQL)作為 [!DNL Data Science Workspace] 標準功能 [!DNL Query Service] 整合 [!DNL JupyterLab] 到中來使用。

本教程演示了用於探索、轉換和分析資料的常見使用案例的SQL查詢 [!DNL Adobe Analytics] 示例。

## 快速入門

開始本教學課程之前，您必須具備下列必要條件：

- 存取權 [!DNL Adobe Experience Platform]。 如果您無權存取中的IMS組織，請先與您的系統 [!DNL Experience Platform]管理員聯絡，然後再繼續

- 資料 [!DNL Adobe Analytics] 集

- 對本教學課程中使用的下列主要概念有正確認識：
   - [!DNL Experience Data Model (XDM) and XDM System](../../xdm/home.md)
   - [!DNL Query Service](../../query-service/home.md)
   - [!DNL Query Service SQL Syntax](../../query-service/sql/overview.md)
   - [Adobe Analytics]

## 存取 [!DNL JupyterLab] 和 [!DNL Query Service] {#access-jupyterlab-and-query-service}

1. 在中 [!DNL Experience Platform](https://platform.adobe.com)，從左側導 **[!UICONTROL 航列導航到Notebooks]** 。 請讓JupyterLab載入。

   ![](../images/jupyterlab/query/jupyterlab_launcher.png)

   > [!NOTE] 如果未自動顯示新的「啟動器」頁籤，請按一下「檔案」開啟新的「啟動器」 **[!UICONTROL 頁籤]** ，然後選 **[!UICONTROL 擇「新建啟動器」]**。

2. 在「啟動器」(Launcher)頁籤中，按一下 **[!UICONTROL Python]** 3環境中的「空白」(Blank)表徵圖以開啟空的筆記本。

   ![](../images/jupyterlab/query/blank_notebook.png)

   > [!NOTE] Python 3目前是筆記型電腦中唯一支援查詢服務的環境。

3. 在左側選擇邊欄上，按一下「 **[!UICONTROL 資料]** 」圖示，然後按兩下「資料集 **** 」目錄以列出所有資料集。

   ![](../images/jupyterlab/query/dataset.png)

4. 查找要 [!DNL Adobe Analytics] 瀏覽的資料集並按一下右鍵清單，按一下「筆記本」( **[!UICONTROL Notebook]** )中的「查詢資料」(Query Data)，在空的筆記本中生成SQL查詢。

5. 按一下包含函式的第一個產生的儲存格， `qs_connect()` 然後按一下播放按鈕以執行它。 此函式在筆記本實例和之間建立連接 [!DNL Query Service]。

   ![](../images/jupyterlab/query/execute.png)

6. 從第二個生 [!DNL Adobe Analytics] 成的SQL查詢中複製資料集名稱，它將是後面的值 `FROM`。

   ![](../images/jupyterlab/query/dataset_name.png)

7. 按一下+按鈕插入新的筆記本 **單元格** 。

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

   - `target_table` : 資料集的 [!DNL Adobe Analytics] 名稱。
   - `target_year` : 目標資料的特定年份。
   - `target_month` : 目標所在的特定月份。
   - `target_day` : 目標資料的特定來源日。
   >[!NOTE] 您可以隨時變更這些值。 執行此動作時，請務必執行要套用之變數儲存格。

## 查詢您的資料 {#query-your-data}

在單個筆記本單元格中輸入以下SQL查詢。 按一下查詢的單元格，然後按一下播放按 **[!UICONTROL 鈕]** 。 成功的查詢結果或錯誤日誌顯示在已執行的單元格下面。

當筆記本長時間處於非活動狀態時，筆記本和筆記本之間的連接可能 [!DNL Query Service] 中斷。 在這種情況下，請 [!DNL JupyterLab] 按一下右上角的 **[!UICONTROL Power]** （電源）按鈕重新啟動。

![](../images/jupyterlab/query/restart_button.png)

筆記本內核將重置，但單元格將保留，重 **[!UICONTROL 新運行]** 所有單元格以繼續您離開的位置。

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
WHERE _acp_year = {target_year} 
      AND _acp_month = {target_month}  
      AND _acp_day = {target_day}
GROUP  BY Day, Hour
ORDER  BY Hour;
```

在上述查詢中，子 `_acp_year` 句中 `WHERE` 的目標設定為值 `target_year`。 在SQL查詢中加入變數，方法是將變數以大括弧(`{}`)括住。

查詢的第一行包含可選變數 `hourly_visitor`。 查詢結果將作為Pactices資料幀儲存在此變數中。 將結果儲存在資料幀中，可讓您以後使用所需的包直觀地顯示查詢 [!DNL Python] 結果。 在新儲存 [!DNL Python] 格中執行下列程式碼以產生長條圖：

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
WHERE  _acp_year = {target_year} 
       AND _acp_month = {target_month}  
       AND _acp_day = {target_day}
GROUP  BY Day, Hour
ORDER  BY Hour;
```

執行上述查詢會將結果儲存 `hourly_actions` 為資料幀。 在新儲存格中執行下列函式以預覽結果：

```python
hourly_actions.head()
```

可以修改上述查詢，以使用 **** WHERE子句中的邏輯運算子返回指定日期範圍的每小時操作計數：

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

執行修改的查詢會將結果儲存 `hourly_actions_date_range` 為資料幀。 在新儲存格中執行下列函式以預覽結果：

```python
hourly_actions_date_rage.head()
```

### 每個訪客作業的事件數 {#number-of-events-per-visitor-session}

下列查詢會傳回指定日期每個訪客作業的事件數：

#### 查詢 <!-- omit in toc -->

```sql
%%read_sql events_per_session -c QS_CONNECTION
SELECT concat(enduserids._experience.aaid.id, 
              '-#', 
              _experience.analytics.session.num) AS aaid_sess_key, 
       Count(timestamp)                          AS Count 
FROM   {target_table}
WHERE  _acp_year = {target_year} 
       AND _acp_month = {target_month}  
       AND _acp_day = {target_day}
GROUP BY aaid_sess_key
ORDER BY Count DESC;
```

執行下列程 [!DNL Python] 式碼，以產生每次瀏覽作業事件數的色階分佈圖：

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

下列查詢會傳回指定日期中十個人氣最高的頁面：

#### 查詢 <!-- omit in toc -->

```sql
%%read_sql popular_pages -c QS_CONNECTION
SELECT web.webpagedetails.name                 AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP  BY web.webpagedetails.name 
ORDER  BY page_views DESC 
LIMIT  10;
```

### 指定日期的作用中使用者 {#active-users-for-a-given-day}

下列查詢會傳回指定日期中十位最活躍的使用者：

#### 查詢 <!-- omit in toc -->

```sql
%%read_sql active_users -c QS_CONNECTION
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp)               AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP  BY aaid
ORDER  BY Count DESC
LIMIT  10;
```

### 依使用者活動劃分的活躍城市 {#active-cities-by-user-activity}

以下查詢返回在指定日期生成大多數用戶活動的十個城市：

#### 查詢 <!-- omit in toc -->

```sql
%%read_sql active_cities -c QS_CONNECTION
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp)                                                     AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP  BY state_city
ORDER  BY Count DESC
LIMIT  10;
```

## 下一步 <!-- omit in toc -->

本教程演示了在筆記型電腦中使用的一些 [!DNL Query Service] 示例使 [!DNL Jupyter] 用案例。 請依循「 [使用Jupyter Notebooks](./analyze-your-data.md) 」教學課程分析資料，以瞭解如何使用資料存取SDK執行類似作業。