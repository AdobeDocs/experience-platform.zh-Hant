---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;%dataset;interactive mode;batch mode;Spark sdk;python sdk;access data;notebook data access
solution: Experience Platform
title: Jupyterlab筆記型電腦中的資料存取
topic: Developer Guide
description: 本指南著重說明如何使用Jupyter筆記型電腦，此筆記型電腦是在Data Science Workspace中建立的，以存取您的資料。
translation-type: tm+mt
source-git-commit: a9d65c107d0490910239ed73ac5c19881206c189
workflow-type: tm+mt
source-wordcount: '3078'
ht-degree: 9%

---


# 筆記型電腦中的資料 [!DNL Jupyterlab] 訪問

每個支援的內核都提供內置功能，允許您從筆記本內的資料集中讀取平台資料。 Adobe Experience Platform Data Science Workspace中的JupyterLab目前支援R、PySpark [!DNL Python]和Scala的筆記型電腦。 但是，對分頁資料的支援僅限於 [!DNL Python] 和R筆記本。 本指南重點介紹如何使用JupyterLab筆記型電腦訪問資料。

## 快速入門

在閱讀本指南之前，請先閱讀 [[!DNL JupyterLab] 使用指南](./overview.md) ，以取得資料科學工作區 [!DNL JupyterLab] 的高階簡介及其角色。

## 筆記型電腦資料限制 {#notebook-data-limits}

>[!IMPORTANT]
>
>對於PySpark和Scala筆記本，如果您收到錯誤，並且原因是「遠程RPC客戶端斷開關聯」。 這通常表示驅動程式或執行器記憶體不足。 嘗試切換 [至「批次」模式](#mode) ，以解決此錯誤。

以下資訊定義可讀取的資料量上限、使用的資料類型，以及讀取資料所花費的估計時間範圍。

對於 [!DNL Python] 和R ，使用配置為40GB RAM的筆記型電腦伺服器作為基準。 對於PySpark和Scala，以下概述的基準使用了以64GB RAM、8個內核、2個DBU（最多4個工作人員）配置的資料庫群集。

使用的ExperienceEvent架構資料的大小不同，從1000(1K)列開始，最多可達10億(1B)列。 請注意，對於PySpark和 [!DNL Spark] 度量，XDM資料的日期範圍是10天。

臨機架構資料是使用「以選取方式建立表 [!DNL Query Service] 格」(CTAS)預先處理。 這些資料的大小也從1,000列(1K)開始，最多10億列(1B)。

### 何時使用批次模式與互動模式 {#mode}

使用PySpark和Scala筆記型電腦讀取資料集時，您可以選擇使用互動模式或批次模式來讀取資料集。 互動式可快速產生結果，而批次模式則適用於大型資料集。

- 對於PySpark和Scala筆記型電腦，在讀取500萬行或更多資料時應使用批次模式。 如需每種模式效率的詳細資訊，請參 [閱下方的PySpark](#pyspark-data-limits)[或Scala](#scala-data-limits) 資料限制表。

### [!DNL Python] 筆記型資料限制

**XDM ExperienceEvent架構：** 在不到22分鐘內，您最多可以讀取200萬行（磁碟上約6.1 GB的資料）的XDM資料。 新增其他列可能會導致錯誤。

| 行數 | 1K | 10K | 100K | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| 磁碟大小(MB) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK（以秒為單位） | 20.3 | 86.8 | 63 | 659 | 1315 |

**臨機架構：** 在不到14分鐘內，您最多可讀取500萬行（磁碟上約5.6 GB資料）的非XDM（臨機）資料。 新增其他列可能會導致錯誤。

| 行數 | 1K | 10K | 100K | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| 磁碟大小(MB) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK（以秒為單位） | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

### R筆記本資料限制

**XDM ExperienceEvent架構：** 在13分鐘內，您最多可讀取100萬行XDM資料（磁碟上的3GB資料）。

| 行數 | 1K | 10K | 100K | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| 磁碟大小(MB) | 18.73 | 187.5 | 308 | 3000 |
| R內核（以秒為單位） | 14.03 | 69.6 | 86.8 | 775 |

**臨機架構：** 您應能在大約10分鐘內讀取最多300萬列的臨機資料（293MB的磁碟資料）。

| 行數 | 1K | 10K | 100K | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| 磁碟大小(MB) | 0.082 | 0.612 | 9.0 | 91 | 188 | 293 |
| R SDK（秒） | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

### PySpark(內核[!DNL Python] )筆記型電腦資料限制： {#pyspark-data-limits}

**XDM ExperienceEvent架構：** 在互動模式下，您最多可在約20分鐘內讀取500萬行（磁碟上約13.42GB的資料）的XDM資料。 互動式模式最多只支援5百萬列。 如果您想要讀取較大的資料集，建議您切換到批處理模式。 在批處理模式下，您應能在大約14小時內讀取XDM資料的最多5億行（磁碟上約1.31TB資料）。

| 行數 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 磁碟大小 | 2.93MB | 4.38MB | 29.02 | 2.69 GB   | 5.39 GB   | 8.09 GB   | 13.42 GB   | 26.82 GB   | 134.24 GB   | 268.39 GB   | 1.31TB |
| SDK（互動模式） | 33s | 32.4s | 55.1s | 253.5s | 489.2s | 729.6s | 1206.8s | - | - | - | - |
| SDK（批次模式） | 815.8s | 492.8s | 379.1s | 637.4s | 624.5s | 869.2s | 1104.1s | 1786s | 5387.2s | 10624.6s | 50547s |

**臨機架構：** 在互動模式下，您最多可在3分鐘內讀取500萬行（磁碟上約5.36GB的資料）的非XDM資料。 在批處理模式下，您應能在大約18分鐘內讀取非XDM資料的10億行（磁碟上約1.05TB資料）。

| 行數 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| 磁碟大小 | 1.12MB | 11.24MB | 109.48MB | 2.69 GB   | 2.14 GB   | 3.21 GB   | 5.36 GB   | 10.71 GB   | 53.58 GB   | 107.52 GB   | 535.88 GB   | 1.05TB |
| SDK互動模式（以秒為單位） | 28.2s | 18.6s | 20.8s | 20.9s | 23.8s | 21.7s | 24.7s | - | - | - | - | - |
| SDK批次模式（以秒為單位） | 428.8s | 578.8s | 641.4s | 538.5s | 630.9s | 467.3s | 411s | 675s | 702s | 719.2s | 1022.1s | 1122.3s |

### [!DNL Spark] （Scala內核）筆記本資料限制： {#scala-data-limits}

**XDM ExperienceEvent架構：** 在互動模式下，您最多可在18分鐘內讀取500萬行（磁碟上約13.42GB的資料）的XDM資料。 互動式模式最多只支援5百萬列。 如果您想要讀取較大的資料集，建議您切換到批處理模式。 在批處理模式下，您應能在大約14小時內讀取XDM資料的最多5億行（磁碟上約1.31TB資料）。

| 行數 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 磁碟大小 | 2.93MB | 4.38MB | 29.02 | 2.69 GB   | 5.39 GB   | 8.09 GB   | 13.42 GB   | 26.82 GB   | 134.24 GB   | 268.39 GB   | 1.31TB |
| SDK互動模式（以秒為單位） | 37.9s | 22.7s | 45.6s | 231.7s | 444.7s | 660.6s | 1100s | - | - | - | - |
| SDK批次模式（以秒為單位） | 374.4s | 398.5s | 527s | 487.9s | 588.9s | 829s | 939.1s | 1441s | 5473.2s | 10118.8 | 49207.6 |

**臨機架構：** 在互動模式下，您最多可在3分鐘內讀取500萬行（磁碟上約5.36GB的資料）的非XDM資料。 在批處理模式下，您應能在大約16分鐘內讀取非XDM資料的10億行（磁碟上約1.05TB資料）。

| 行數 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| 磁碟大小 | 1.12MB | 11.24MB | 109.48MB | 2.69 GB   | 2.14 GB   | 3.21 GB   | 5.36 GB   | 10.71 GB   | 53.58 GB   | 107.52 GB   | 535.88 GB   | 1.05TB |
| SDK互動模式（以秒為單位） | 35.7s | 31s | 19.5s | 25.3s | 23s | 33.2s | 25.5s | - | - | - | - | - |
| SDK批次模式（以秒為單位） | 448.8s | 459.7s | 519s | 475.8s | 599.9s | 347.6s | 407.8s | 397s | 518.8s | 487.9s | 760.2s | 975.4s |

## Python筆記本 {#python-notebook}

[!DNL Python] 筆記型電腦允許您在訪問資料集時分頁資料。 下面顯示有分頁和無分頁讀取資料的范常式式碼。 有關可用啟動程式Python筆記本的詳細資訊，請訪問JupyterLab用戶指 [[!DNL JupyterLab] 南中的](./overview.md#launcher) Launcher部分。

下面的Python文檔概述了以下概念：

- [從資料集讀取](#python-read-dataset)
- [寫入資料集](#write-python)
- [查詢資料](#query-data-python)
- [篩選ExperienceEvent資料](#python-filter)

### 從Python資料集讀取 {#python-read-dataset}

**不分頁：**

執行下列程式碼會讀取整個資料集。 如果執行成功，則資料將保存為變數引用的Apcotis資料幀 `df`。

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**使用分頁：**

執行下列程式碼會讀取指定資料集的資料。 分頁是通過分別通過函式和函式限制和偏移資料 `limit()` 來實現 `offset()` 的。 限制資料是指要讀取的資料點數上限，而偏移指在讀取資料之前要跳過的資料點數。 如果讀取操作成功執行，則資料將被保存為變數引用的Apcotis資料幀 `df`。

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### 在Python中寫入資料集 {#write-python}

要寫入JupyterLab筆記本中的資料集，請在JupyterLab的左側導航中選擇「資料」表徵圖頁籤（在下面突出顯示）。 此時將 **[!UICONTROL 顯示Dataset]** 和 **[!UICONTROL Schemas目錄]** 。 選擇 **[!UICONTROL 資料集]** ，然後按一下滑鼠右鍵，然後從您要使用的資料集上的下拉式選單中選取「在筆記型電腦中寫入資料 **** 」選項。 可執行代碼條目出現在筆記本底部。

![](../images/jupyterlab/data-access/write-dataset.png)

- 使用「 **[!UICONTROL 筆記型電腦中的寫入資料]** 」，使用您選取的資料集產生寫入儲存格。
- 使用 **[!UICONTROL 「在筆記型電腦中探索資料]** 」，使用選取的資料集產生讀取儲存格。
- 使用 **[!UICONTROL 筆記型電腦中的查詢資料]** ，以您選取的資料集產生基本查詢儲存格。

或者，您也可以複製並貼上下列程式碼儲存格。 同時更 `{DATASET_ID}` 換和 `{PANDA_DATAFRAME}`。

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(client_context).get_by_id("{DATASET_ID}")
dataset_writer = DatasetWriter(client_context, dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### 查詢資料使 [!DNL Query Service] 用 [!DNL Python] {#query-data-python}

[!DNL JupyterLab] on可 [!DNL Platform] 讓您在筆記型電腦中使 [!DNL Python] 用SQL透過 [Adobe Experience Platform Query Service存取資料](https://www.adobe.com/go/query-service-home-en)。 由於資料的運 [!DNL Query Service] 行時間優越，通過訪問資料對處理大型資料集非常有用。 請注意，使用查詢 [!DNL Query Service] 資料的處理時間限制為10分鐘。

在中使 [!DNL Query Service] 用 [!DNL JupyterLab]之前，請確定您對 [[!DNL Query Service] SQL語法有正確的瞭解](https://www.adobe.com/go/query-service-sql-syntax-en)。

使用查詢 [!DNL Query Service] 資料需要提供目標資料集的名稱。 您可以使用「資料總管」來尋找所需的資料集，以產生必要的 **[!UICONTROL 程式碼儲存格]**。 在資料集清單上按一下滑鼠右鍵，然後按一下「筆記型 **[!UICONTROL 電腦中的查詢資料]** 」，在筆記型電腦中產生兩個程式碼儲存格。 下面將更詳細地列出這兩個儲存格。

![](../images/jupyterlab/data-access/python-query-dataset.png)

為了在中使 [!DNL Query Service] 用， [!DNL JupyterLab]您必須首先在工作筆記本和之間建立 [!DNL Python] 連接 [!DNL Query Service]。 這可以通過執行第一生成單元來實現。

```python
qs_connect()
```

在第二個生成的單元格中，第一行必須在SQL查詢之前定義。 預設情況下，生成的單元格定義一個可選變數(`df0`)，該變數將查詢結果保存為Pactices資料幀。 <br>該 `-c QS_CONNECTION` 參數是強制的，它指示內核執行SQL查詢 [!DNL Query Service]。 有關其 [他引數的清單](#optional-sql-flags-for-query-service) ，請參見附錄。

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

Python變數可在SQL查詢中直接引用，方法是使用字串格式語法，並將變數包住大括弧(`{}`)，如下列範例所示：

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Filter [!DNL ExperienceEvent] data {#python-filter}

為了存取和篩選筆記型 [!DNL ExperienceEvent] 電腦中的資料集，您必須提供資料集的ID( [!DNL Python]`{DATASET_ID}`)，以及使用邏輯運算子定義特定時間範圍的篩選規則。 定義時間範圍時，會忽略任何指定的分頁，並考慮整個資料集。

篩選運算子的清單說明如下：

- `eq()`: Equal to
- `gt()`: Greater than
- `ge()`: Greater than or equal to
- `lt()`: Less than
- `le()`: Less than or equal to
- `And()`:邏輯AND運算子
- `Or()`:邏輯OR運算子

下列儲存格會將資料 [!DNL ExperienceEvent] 集篩選為2019年1月1日至2019年12月31日止期間僅存在的資料。

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

## R筆記型電腦 {#r-notebooks}

R筆記型電腦允許您在訪問資料集時分頁資料。 下面顯示有分頁和無分頁讀取資料的范常式式碼。 有關可用啟動器R筆記本的詳細資訊，請訪問JupyterLab用戶指 [[!DNL JupyterLab] 南中的](./overview.md#launcher) Launcher部分。

以下R檔案概述下列概念：

- [從資料集讀取](#r-read-dataset)
- [寫入資料集](#write-r)
- [篩選ExperienceEvent資料](#r-filter)

### 從R中的資料集讀取 {#r-read-dataset}

**不分頁：**

執行下列程式碼會讀取整個資料集。 如果執行成功，則資料將保存為變數引用的Apcotis資料幀 `df0`。

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df0 <- dataset_reader$read()
head(df0)
```

**使用分頁：**

執行下列程式碼會讀取指定資料集的資料。 分頁是通過分別通過函式和函式限制和偏移資料 `limit()` 來實現 `offset()` 的。 限制資料是指要讀取的資料點數上限，而偏移指在讀取資料之前要跳過的資料點數。 如果讀取操作成功執行，則資料將被保存為變數引用的Apcotis資料幀 `df0`。

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 
df0 <- dataset_reader$limit(100L)$offset(10L)$read()
```

### 在R中寫入資料集 {#write-r}

要寫入JupyterLab筆記本中的資料集，請在JupyterLab的左側導航中選擇「資料」表徵圖頁籤（在下面突出顯示）。 此時將 **[!UICONTROL 顯示Dataset]** 和 **[!UICONTROL Schemas目錄]** 。 選擇 **[!UICONTROL 資料集]** ，然後按一下滑鼠右鍵，然後從您要使用的資料集上的下拉式選單中選取「在筆記型電腦中寫入資料 **** 」選項。 可執行代碼條目出現在筆記本底部。

![](../images/jupyterlab/data-access/r-write-dataset.png)

- 使用「 **[!UICONTROL 筆記型電腦中的寫入資料]** 」，使用您選取的資料集產生寫入儲存格。
- 使用 **[!UICONTROL 「在筆記型電腦中探索資料]** 」，使用選取的資料集產生讀取儲存格。

或者，您也可以複製並貼上下列程式碼儲存格：

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### Filter [!DNL ExperienceEvent] data {#r-filter}

為了存取和篩選R筆記本 [!DNL ExperienceEvent] 中的資料集，您必須提供資料集的ID(`{DATASET_ID}`)，以及使用邏輯運算子定義特定時間範圍的篩選規則。 定義時間範圍時，會忽略任何指定的分頁，並考慮整個資料集。

篩選運算子的清單說明如下：

- `eq()`: Equal to
- `gt()`: Greater than
- `ge()`: Greater than or equal to
- `lt()`: Less than
- `le()`: Less than or equal to
- `And()`:邏輯AND運算子
- `Or()`:邏輯OR運算子

下列儲存格會將資料 [!DNL ExperienceEvent] 集篩選為2019年1月1日至2019年12月31日止期間僅存在的資料。

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 

df0 <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

## PySpark 3筆記型電腦 {#pyspark-notebook}

下方的PySpark檔案概述下列概念：

- [初始化SparkSession](#spark-initialize)
- [讀取和寫入資料](#magic)
- [建立本地資料幀](#pyspark-create-dataframe)
- [篩選ExperienceEvent資料](#pyspark-filter-experienceevent)

### 初始化sparkSession {#spark-initialize}

所有 [!DNL Spark] 2.4筆記型電腦都要求您使用下列簡短字母組合代碼初始化會話。

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### 使用%dataset來讀取和寫入PySpark 3筆記本 {#magic}

隨著 [!DNL Spark] 2.4的推出， `%dataset` PySpark 3([!DNL Spark] 2.4)筆記型電腦也提供了自訂功能。 有關IPython內核中的magic命令的詳細資訊，請訪問 [IPython magic文檔](https://ipython.readthedocs.io/en/stable/interactive/magics.html)。


**使用狀況**

```scala
%dataset {action} --datasetId {id} --dataFrame {df}`
```

**說明**

用於 [!DNL Data Science Workspace] 從筆記本( [!DNL PySpark] 3內核)讀取或寫入資料集的自定[!DNL Python] 義魔術命令。

| 名稱 | 說明 | 必填 |
| --- | --- | --- |
| `{action}` | 要在資料集上執行的動作類型。 有兩個動作是「讀取」或「寫入」。 | 是 |
| `--datasetId {id}` | 用於提供要讀取或寫入的資料集的ID。 | 是 |
| `--dataFrame {df}` | 熊貓資料框。 <ul><li> 當動作為&quot;read&quot;時，{df}是資料集讀取作業結果可用的變數。 </li><li> 當動作為&quot;write&quot;時，此資料幀{df}將寫入資料集。 </li></ul> | 是 |
| `--mode` | 其他參數會變更資料的讀取方式。 允許的參數為「批次」和「互動」。 依預設，模式會設為「互動」。 建議在讀取大量資料時使用「批次」模式。 | 無 |

>[!TIP]
>
>查看筆記本資料限制部 [分中的PySpark表](#notebook-data-limits) ，以 `mode` 確定應將其設定為 `interactive` 或 `batch`。

**範例**

- **閱讀範例**: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
- **寫示例**: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

您可以使用下列方法，在JupyterLab購買中自動產生上述範例：

在JupyterLab的左側導覽中，選取「資料」圖示標籤（反白顯示如下）。 此時將 **[!UICONTROL 顯示Dataset]** 和 **[!UICONTROL Schemas目錄]** 。 選擇 **[!UICONTROL 資料集]** ，然後按一下滑鼠右鍵，然後從您要使用的資料集上的下拉式選單中選取「在筆記型電腦中寫入資料 **** 」選項。 可執行代碼條目出現在筆記本底部。

- 使用 **[!UICONTROL 「在筆記型電腦中探索資料]** 」產生讀取儲存格。
- 使用 **[!UICONTROL 筆記本中的寫資料]** ，生成寫單元。

![](../images/jupyterlab/data-access/pyspark-write-dataset.png)

### 建立本地資料幀 {#pyspark-create-dataframe}

要使用PySpark 3建立本地資料幀，請使用SQL查詢。 例如：

```scala
date_aggregation.createOrReplaceTempView("temp_df")

df = spark.sql('''
  SELECT *
  FROM sparkdf
''')

local_df
```

```scala
df = spark.sql('''
  SELECT *
  FROM sparkdf
  LIMIT limit
''')
```

```scala
sample_df = df.sample(fraction)
```

>[!TIP]
>
>您也可以指定選用的種子樣本，例如布林值withReplacement、雙分數或長種子。

### Filter [!DNL ExperienceEvent] data {#pyspark-filter-experienceevent}

在PySpark筆記型 [!DNL ExperienceEvent] 電腦中存取和篩選資料集時，您必須提供資料集識別(`{DATASET_ID}`)、組織的IMS識別，以及定義特定時間範圍的篩選規則。 篩選時間範圍是使用函式來定義的， `spark.sql()`其中函式參數是SQL查詢字串。

下列儲存格會將資料 [!DNL ExperienceEvent] 集篩選為2019年1月1日至2019年12月31日止期間僅存在的資料。

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

## Scala筆記型電腦 {#scala-notebook}

以下檔案包含下列概念的範例：

- [初始化SparkSession](#scala-initialize)
- [讀取資料集](#read-scala-dataset)
- [寫入資料集](#scala-write-dataset)
- [建立本地資料幀](#scala-create-dataframe)
- [篩選ExperienceEvent資料](#scala-experienceevent)

### 初始化SparkSession {#scala-initialize}

所有Scala筆記型電腦都要求您使用以下簡短字母組合代碼初始化會話：

```scala
import org.apache.spark.sql.{ SparkSession }
val spark = SparkSession
  .builder()
  .master("local")
  .getOrCreate()
```

### 讀取資料集 {#read-scala-dataset}

在Scala中，您可匯入以 `clientContext` 取得並傳回平台值，如此就不需要定義變數，例如 `var userToken`。 在以下的Scala範例中， `clientContext` 用於取得並傳回讀取資料集所需的所有值。

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
import com.adobe.platform.token.ClientContext
val spark = SparkSession.builder().master("local").config("spark.sql.warehouse.dir", "/").getOrCreate()

val clientContext = ClientContext.getClientContext()
val df1 = spark.read.format("com.adobe.platform.query")
  .option("user-token", clientContext.getUserToken())
  .option("ims-org", clientContext.getOrgId())
  .option("api-key", clientContext.getApiKey())
  .option("service-token", clientContext.getServiceToken())
  .option("mode", "interactive")
  .option("dataset-id", "5e68141134492718af974844")
  .load()

df1.printSchema()
df1.show(10)
```

| 元素 | 說明 |
| ------- | ----------- |
| df1 | 一個變數，它表示用於讀取和寫入資料的Pactys資料幀。 |
| user-token | 使用自動擷取的使用者Token `clientContext.getUserToken()`。 |
| service-token | 您使用自動擷取的服務Token `clientContext.getServiceToken()`。 |
| ims-org | 您的IMS組織ID，會使用自動擷取 `clientContext.getOrgId()`。 |
| api-key | 使用自動擷取的API金鑰 `clientContext.getApiKey()`。 |

>[!TIP]
>
>查看筆記本資料限制部 [分中的Scala表](#notebook-data-limits) ，以 `mode` 確定應設定為 `interactive` 還是 `batch`。

您可以在JupyterLab購買中使用下列方法自動產生上述範例：

在JupyterLab的左側導覽中，選取「資料」圖示標籤（反白顯示如下）。 此時將 **[!UICONTROL 顯示Dataset]** 和 **[!UICONTROL Schemas目錄]** 。 選擇 **[!UICONTROL 資料集]** ，然後按一下滑鼠右鍵，然後從您要使用的資料集上的下拉式選單中選取「在筆記型電腦中 **[!UICONTROL 探索資料]** 」選項。 可執行代碼條目出現在筆記本底部。
和
- 使用 **[!UICONTROL 「在筆記型電腦中探索資料]** 」產生讀取儲存格。
- 使用 **[!UICONTROL 筆記本中的寫資料]** ，生成寫單元。

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### 寫入資料集 {#scala-write-dataset}

在Scala中，您可匯入以 `clientContext` 取得並傳回平台值，如此就不需要定義變數，例如 `var userToken`。 在下面的Scala範例中， `clientContext` 用於定義並傳回寫入資料集所需的所有必要值。

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
import com.adobe.platform.token.ClientContext
val spark = SparkSession.builder().master("local").config("spark.sql.warehouse.dir", "/").getOrCreate()

val clientContext = ClientContext.getClientContext()
df1.write.format("com.adobe.platform.query")
  .option("user-token", clientContext.getUserToken())
  .option("service-token", clientContext.getServiceToken())
  .option("ims-org", clientContext.getOrgId())
  .option("api-key", clientContext.getApiKey())
  .option("mode", "interactive")
  .option("dataset-id", "5e68141134492718af974844")
  .save()
```

| 元素 | 描述 |
| ------- | ----------- |
| df1 | 一個變數，它表示用於讀取和寫入資料的Pactys資料幀。 |
| user-token | 使用自動擷取的使用者Token `clientContext.getUserToken()`。 |
| service-token | 您使用自動擷取的服務Token `clientContext.getServiceToken()`。 |
| ims-org | 您的IMS組織ID，會使用自動擷取 `clientContext.getOrgId()`。 |
| api-key | 使用自動擷取的API金鑰 `clientContext.getApiKey()`。 |

>[!TIP]
>
>查看筆記本資料限制部 [分中的Scala表](#notebook-data-limits) ，以 `mode` 確定應設定為 `interactive` 還是 `batch`。

### 建立本地資料幀 {#scala-create-dataframe}

要使用Scala建立本地資料幀，需要SQL查詢。 例如：

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### Filter [!DNL ExperienceEvent] data {#scala-experienceevent}

存取和篩選 [!DNL ExperienceEvent] Scala筆記型電腦中的資料集時，您必須提供資料集識別(`{DATASET_ID}`)、貴組織的IMS識別，以及定義特定時間範圍的篩選規則。 篩選時間範圍是使用函式定義的，其 `spark.sql()`中函式參數是SQL查詢字串。

下列儲存格會將資料 [!DNL ExperienceEvent] 集篩選為2019年1月1日至2019年12月31日止期間僅存在的資料。

```scala
// Spark (Spark 2.4)

// Turn off extra logging
import org.apache.log4j.{Level, Logger}
Logger.getLogger("org").setLevel(Level.OFF)
Logger.getLogger("com").setLevel(Level.OFF)

import org.apache.spark.sql.{Dataset, SparkSession}
val spark = org.apache.spark.sql.SparkSession.builder().appName("Notebook")
  .master("local")
  .getOrCreate()

// Stage Exploratory
val dataSetId: String = "{DATASET_ID}"
val orgId: String = sys.env("IMS_ORG_ID")
val clientId: String = sys.env("PYDASDK_IMS_CLIENT_ID")
val userToken: String = sys.env("PYDASDK_IMS_USER_TOKEN")
val serviceToken: String = sys.env("PYDASDK_IMS_SERVICE_TOKEN")
val mode: String = "batch"

var df = spark.read.format("com.adobe.platform.query")
  .option("user-token", userToken)
  .option("ims-org", orgId)
  .option("api-key", clientId)
  .option("mode", mode)
  .option("dataset-id", dataSetId)
  .option("service-token", serviceToken)
  .load()
df.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timedf.show()
```

## 後續步驟

本文檔介紹了使用JupyterLab筆記型電腦訪問資料集的一般指南。 有關查詢資料集的更深入示例，請訪問JupyterLab筆記本 [中的查詢服務](./query-service.md) 。 有關如何探索和視覺化資料集的更多資訊，請造訪使用筆記型電腦分 [析資料的檔案](./analyze-your-data.md)。

## 可選的SQL標誌 [!DNL Query Service] {#optional-sql-flags-for-query-service}

此表概述了可用於的可選SQL標誌 [!DNL Query Service]。

| **旗標** | **說明** |
| --- | --- |
| `-h`, `--help` | 顯示幫助消息並退出。 |
| `-n`, `--notify` | 切換選項以通知查詢結果。 |
| `-a`, `--async` | 使用此標誌可非同步執行查詢，並可在查詢執行時釋放內核。 在將查詢結果指派給變數時請務必小心，因為如果查詢未完成，變數可能未定義。 |
| `-d`, `--display` | 使用此標幟可防止顯示結果。 |

