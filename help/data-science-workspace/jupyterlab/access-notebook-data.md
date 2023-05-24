---
keywords: Experience Platform;JupyterLab；筆記本；資料科學工作區；熱門主題；%dataset；交互模式；批處理模式；Spark sdk;python sdk；訪問資料；筆記本資料存取
solution: Experience Platform
title: Jupyterlab筆記本中的資料存取
description: 本指南重點介紹如何使用Jupyter Notebooks（在Data Science Workspace中構建）來訪問資料。
exl-id: 2035a627-5afc-4b72-9119-158b95a35d32
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '3292'
ht-degree: 8%

---

# 資料存取 [!DNL Jupyterlab] 筆記本

每個支援的內核都提供內置功能，允許您從筆記本中的資料集讀取平台資料。 目前，Adobe Experience Platform資料科學工作區中的JupyterLab支援筆記本 [!DNL Python]、R、PySpark和Scala。 但是，對分頁資料的支援僅限於 [!DNL Python] 和R筆記本。 本指南重點介紹如何使用JupyterLab筆記本訪問資料。

## 快速入門

閱讀本指南前，請閱讀 [[!DNL JupyterLab] 使用手冊](./overview.md) 高級介紹 [!DNL JupyterLab] 以及它在Data Science Workspace中的角色。

## 筆記本資料限制 {#notebook-data-limits}

>[!IMPORTANT]
>
>對於PySpark和Scala筆記本，如果您收到錯誤，原因是「遠程RPC客戶端不關聯」。 這通常表示驅動程式或執行器記憶體不足。 嘗試切換到 [&quot;批處理&quot;模式](#mode) 來解決此錯誤。

以下資訊定義可讀取的最大資料量、使用的資料類型以及讀取資料所需的估計時間範圍。

對於 [!DNL Python] 和R ，配置為40GB RAM的筆記型電腦伺服器用於基準測試。 對於PySpark和Scala，使用配置為64GB RAM、8個內核、2 DBU（最多4個工作程式）的資料庫群集來執行下面概述的基準測試。

使用的ExperienceEvent架構資料的大小從1000(1K)行開始，最多可達10億(1B)行。 請注意，對於PySpark和 [!DNL Spark] 度量， XDM資料使用的日期跨度為10天。

已使用 [!DNL Query Service] 將表建立為選擇(CTAS)。 該資料在從1000(1K)行開始到1000(1B)行之間的大小上也有所變化。

### 何時使用批處理模式與交互模式 {#mode}

在使用PySpark和Scala筆記本讀取資料集時，您可以選擇使用交互模式或批處理模式來讀取資料集。 互動式是快速結果，批處理模式是大資料集。

- 對於PySpark和Scala筆記本，在讀取500萬行或更多資料時應使用批處理模式。 有關每種模式的效率的詳細資訊，請參見 [PySpark](#pyspark-data-limits) 或 [斯卡拉](#scala-data-limits) 下面的資料限制表。

### [!DNL Python] 筆記本資料限制

**XDM ExperienceEvent架構：** 在22分鐘內，您最多可以讀取200萬行XDM資料（磁碟上約6.1 GB資料）。 添加其他行可能會導致錯誤。

| 行數 | 1K | 10K | 100K | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| 磁碟大小(MB) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK（秒） | 20.3 | 86.8 | 63 | 659 | 1315 |

**即席模式：** 在14分鐘內，您最多可以讀取500萬行（磁碟上約5.6 GB的資料）的非XDM（即席）資料。 添加其他行可能會導致錯誤。

| 行數 | 1K | 10K | 100K | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| 磁碟大小(MB) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK（秒） | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

### R筆記本資料限制

**XDM ExperienceEvent架構：** 在13分鐘內，您最多可以讀取100萬行XDM資料（磁碟上的3GB資料）。

| 行數 | 1K | 10K | 100K | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| 磁碟大小(MB) | 18.73 | 187.5 | 308 | 3000 |
| R內核（秒） | 14.03 | 69.6 | 86.8 | 775 |

**即席模式：** 您應能在大約10分鐘內讀取最多300萬行即席資料（磁碟上293MB的資料）。

| 行數 | 1K | 10K | 100K | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| 磁碟大小(MB) | 0.082 | 0.612 | 9.0 | 91 | 188 | 293 |
| R SDK（秒） | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

### PySpark([!DNL Python] 內核)筆記本資料限制： {#pyspark-data-limits}

**XDM ExperienceEvent架構：** 在交互模式下，您應能在大約20分鐘內讀取XDM資料的最多500萬行（磁碟上約13.42GB的資料）。 交互模式最多只支援500萬行。 如果您想讀取較大的資料集，建議您切換到批處理模式。 在批處理模式下，您應能在大約14小時內讀取XDM資料的最多5億行（磁碟上約1.31TB的資料）。

| 行數 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 磁碟大小 | 2.93MB | 4.38MB | 29.02 | 2.69 GB   | 5.39 GB   | 8.09 GB   | 13.42 GB   | 26.82 GB   | 134.24 GB   | 268.39 GB   | 1.31TB |
| SDK（交互模式） | 33s | 32.4s | 55.1s | 253.5s | 489.2s | 729.6s | 1206.8s | - | - | - | - |
| SDK（批處理模式） | 815.8s | 492.8s | 379.1s | 637.4s | 624.5s | 869.2s | 1104.1s | 1786s | 5387.2s | 10624.6s | 50547s |

**即席模式：** 在交互模式下，您應能在不到3分鐘內讀取非XDM資料的最多500萬行（磁碟上的資料約為5.36GB）。 在批處理模式下，您應能在大約18分鐘內讀取非XDM資料的最多10億行（磁碟上的資料約為1.05TB）。

| 行數 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| 磁碟大小 | 1.12MB | 11.24MB | 109.48MB | 2.69 GB   | 2.14 GB   | 3.21 GB   | 5.36 GB   | 10.71 GB   | 53.58 GB   | 107.52 GB   | 535.88 GB   | 1.05TB |
| SDK交互模式（秒） | 28.2s | 18.6s | 20.8s | 20.9s | 23.8s | 21.7s | 24.7s | - | - | - | - | - |
| SDK批處理模式（秒） | 428.8s | 578.8s | 641.4s | 538.5s | 630.9s | 467.3s | 411s | 675s | 702s | 719.2s | 1022.1s | 1122.3s |

### [!DNL Spark] （Scala內核）筆記本資料限制： {#scala-data-limits}

**XDM ExperienceEvent架構：** 在交互模式下，您應能在大約18分鐘內讀取XDM資料的最多500萬行（磁碟上約13.42GB的資料）。 交互模式最多只支援500萬行。 如果您想讀取較大的資料集，建議您切換到批處理模式。 在批處理模式下，您應能在大約14小時內讀取XDM資料的最多5億行（磁碟上約1.31TB的資料）。

| 行數 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 磁碟大小 | 2.93MB | 4.38MB | 29.02 | 2.69 GB   | 5.39 GB   | 8.09 GB   | 13.42 GB   | 26.82 GB   | 134.24 GB   | 268.39 GB   | 1.31TB |
| SDK交互模式（秒） | 37.9s | 22.7s | 45.6s | 231.7s | 444.7s | 660.6s | 1100s | - | - | - | - |
| SDK批處理模式（秒） | 374.4s | 398.5s | 527s | 487.9s | 588.9s | 829s | 939.1s | 1441s | 5473.2s | 10118.8 | 49207.6 |

**即席模式：** 在交互模式下，您應能在3分鐘內讀取非XDM資料的最多500萬行（磁碟上的資料約為5.36GB）。 在批處理模式下，您應能在大約16分鐘內讀取非XDM資料的最多10億行（磁碟上的資料約為1.05TB）。

| 行數 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| 磁碟大小 | 1.12MB | 11.24MB | 109.48MB | 2.69 GB   | 2.14 GB   | 3.21 GB   | 5.36 GB   | 10.71 GB   | 53.58 GB   | 107.52 GB   | 535.88 GB   | 1.05TB |
| SDK交互模式（秒） | 35.7s | 31s | 19.5s | 25.3s | 23s | 33.2s | 25.5s | - | - | - | - | - |
| SDK批處理模式（秒） | 448.8s | 459.7s | 519s | 475.8s | 599.9s | 347.6s | 407.8s | 397s | 518.8s | 487.9s | 760.2s | 975.4s |

## Python筆記本 {#python-notebook}

[!DNL Python] 筆記本允許您在訪問資料集時分頁資料。 下面演示了讀取有分頁和無分頁資料的示例代碼。 有關可用的入門版Python筆記本的詳細資訊，請訪問 [[!DNL JupyterLab] 啟動程式](./overview.md#launcher) JupyterLab使用手冊中的「JupyterLab」部分。

下面的Python文檔概述了以下概念：

- [從資料集讀取](#python-read-dataset)
- [寫入資料集](#write-python)
- [查詢資料](#query-data-python)
- [篩選ExperienceEvent資料](#python-filter)

### 從Python中的資料集讀取 {#python-read-dataset}

**不分頁：**

執行以下代碼將讀取整個資料集。 如果執行成功，則資料將保存為變數引用的Pactis資料框 `df`。

```python
# Python

from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**使用分頁：**

執行以下代碼將從指定的資料集中讀取資料。 通過函式限制和偏移資料實現分頁 `limit()` 和 `offset()` 分別進行。 限制資料是指要讀取的資料點的最大數量，而偏移是指在讀取資料之前要跳過的資料點的數量。 如果讀取操作執行成功，則資料將另存為變數引用的Pactis資料幀 `df`。

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### 在Python中寫入資料集 {#write-python}

要寫入JupyterLab筆記本中的資料集，請在JupyterLab左導航中選擇「資料」表徵圖頁籤（下面突出顯示）。 的 **[!UICONTROL 資料集]** 和 **[!UICONTROL 架構]** 的下界。 選擇 **[!UICONTROL 資料集]** ，然後選擇 **[!UICONTROL 在筆記本中寫入資料]** 選項。 可執行代碼條目出現在筆記本底部。

![](../images/jupyterlab/data-access/write-dataset.png)

- 使用 **[!UICONTROL 在筆記本中寫入資料]** 生成包含所選資料集的寫單元格。
- 使用 **[!UICONTROL 在筆記本中瀏覽資料]** 以使用所選資料集生成讀取單元格。
- 使用 **[!UICONTROL 在筆記本中查詢資料]** 生成基本查詢單元格。

或者，可複製並貼上以下代碼單元格。 替換 `{DATASET_ID}` 和 `{PANDA_DATAFRAME}`。

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### 查詢資料使用 [!DNL Query Service] 在 [!DNL Python] {#query-data-python}

[!DNL JupyterLab] 上 [!DNL Platform] 允許您在 [!DNL Python] 筆記本訪問資料 [Adobe Experience Platform查詢服務](https://www.adobe.com/go/query-service-home-en)。 通過 [!DNL Query Service] 由於其運行時間長，對於處理大資料集非常有用。 請注意，使用 [!DNL Query Service] 處理時間限制為10分鐘。

使用前 [!DNL Query Service] 在 [!DNL JupyterLab]，確保您對 [[!DNL Query Service] SQL語法](https://www.adobe.com/go/query-service-sql-syntax-en)。

使用 [!DNL Query Service] 要求您提供目標資料集的名稱。 通過使用 **[!UICONTROL 資料瀏覽器]**。 按一下右鍵資料集清單，然後按一下 **[!UICONTROL 在筆記本中查詢資料]** 在筆記本中生成兩個代碼單元格。 下面將詳細介紹這兩個單元格。

![](../images/jupyterlab/data-access/python-query-dataset.png)

為了利用 [!DNL Query Service] 在 [!DNL JupyterLab]，您必須首先在您的工作之間建立連接 [!DNL Python] 筆記本和 [!DNL Query Service]。 這可以通過執行第一生成單元來實現。

```python
qs_connect()
```

在第二個生成的單元格中，必須在SQL查詢之前定義第一行。 預設情況下，生成的單元格定義一個可選變數(`df0`)，將查詢結果保存為Pactis資料框。 <br>的 `-c QS_CONNECTION` 參數是必需的，並指示內核執行SQL查詢 [!DNL Query Service]。 查看 [附錄](#optional-sql-flags-for-query-service) 的子常式。

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

Python變數可通過使用字串格式的語法並在大括弧(`{}`)，如下例所示：

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### 篩選 [!DNL ExperienceEvent] 資料 {#python-filter}

為了訪問和篩選 [!DNL ExperienceEvent] 資料集 [!DNL Python] 筆記本，必須提供資料集的ID(`{DATASET_ID}`)以及使用邏輯運算子定義特定時間範圍的篩選器規則。 定義時間範圍時，將忽略任何指定的分頁，並考慮整個資料集。

下面介紹了篩選運算子的清單：

- `eq()`: Equal to
- `gt()`: Greater than
- `ge()`: 大於或等於
- `lt()`: 少於
- `le()`: Less than or equal to
- `And()`:邏輯與運算子
- `Or()`:邏輯OR運算子

以下單元格篩選 [!DNL ExperienceEvent] 2019年1月1日至2019年12月31日底期間完全存在的資料。

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

## R筆記本 {#r-notebooks}

R筆記本允許您在訪問資料集時分頁資料。 下面演示了讀取有分頁和無分頁資料的示例代碼。 有關可用的入門級R筆記本的詳細資訊，請訪問 [[!DNL JupyterLab] 啟動程式](./overview.md#launcher) JupyterLab使用手冊中的「JupyterLab」部分。

下面的R文檔概括了以下概念：

- [從資料集讀取](#r-read-dataset)
- [寫入資料集](#write-r)
- [篩選ExperienceEvent資料](#r-filter)

### 從R中的資料集讀取 {#r-read-dataset}

**不分頁：**

執行以下代碼將讀取整個資料集。 如果執行成功，則資料將保存為變數引用的Pactis資料框 `df0`。

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df0 <- dataset_reader$read()
head(df0)
```

**使用分頁：**

執行以下代碼將從指定的資料集中讀取資料。 通過函式限制和偏移資料實現分頁 `limit()` 和 `offset()` 分別進行。 限制資料是指要讀取的資料點的最大數量，而偏移是指在讀取資料之前要跳過的資料點的數量。 如果讀取操作執行成功，則資料將另存為變數引用的Pactis資料幀 `df0`。

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 
df0 <- dataset_reader$limit(100L)$offset(10L)$read()
```

### 寫入R中的資料集 {#write-r}

要寫入JupyterLab筆記本中的資料集，請在JupyterLab左導航中選擇「資料」表徵圖頁籤（下面突出顯示）。 的 **[!UICONTROL 資料集]** 和 **[!UICONTROL 架構]** 的下界。 選擇 **[!UICONTROL 資料集]** ，然後選擇 **[!UICONTROL 在筆記本中寫入資料]** 選項。 可執行代碼條目出現在筆記本底部。

![](../images/jupyterlab/data-access/r-write-dataset.png)

- 使用 **[!UICONTROL 在筆記本中寫入資料]** 生成包含所選資料集的寫單元格。
- 使用 **[!UICONTROL 在筆記本中瀏覽資料]** 以使用所選資料集生成讀取單元格。

或者，可以複製並貼上以下代碼單元格：

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### 篩選 [!DNL ExperienceEvent] 資料 {#r-filter}

為了訪問和篩選 [!DNL ExperienceEvent] 資料集，必須提供資料集的ID(`{DATASET_ID}`)以及使用邏輯運算子定義特定時間範圍的篩選器規則。 定義時間範圍時，將忽略任何指定的分頁，並考慮整個資料集。

下面介紹了篩選運算子的清單：

- `eq()`: Equal to
- `gt()`: Greater than
- `ge()`: 大於或等於
- `lt()`: 少於
- `le()`: Less than or equal to
- `And()`:邏輯與運算子
- `Or()`:邏輯OR運算子

以下單元格篩選 [!DNL ExperienceEvent] 2019年1月1日至2019年12月31日底期間完全存在的資料。

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
datetime <- import("datetime", convert = FALSE)
py_run_file("~/.ipython/profile_default/startup/platform_sdk_context.py")

client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(py$get_platform_sdk_client_context(), dataset_id="{DATASET_ID}") 

df0 <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

## PySpark 3筆記本 {#pyspark-notebook}

下面的PySpark文檔概括了以下概念：

- [初始化sparkSession](#spark-initialize)
- [讀和寫資料](#magic)
- [建立本地資料幀](#pyspark-create-dataframe)
- [篩選ExperienceEvent資料](#pyspark-filter-experienceevent)

### 正在初始化sparkSession {#spark-initialize}

全部 [!DNL Spark] 2.4筆記本要求您使用以下模板代碼初始化會話。

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### 使用%dataset使用PySpark 3筆記本讀寫 {#magic}

隨著 [!DNL Spark] 2.4, `%dataset` 為PySpark 3([!DNL Spark] 2.4)筆記型電腦。 有關IPython內核中提供的magic命令的詳細資訊，請訪問 [IPython幻方文檔](https://ipython.readthedocs.io/en/stable/interactive/magics.html)。


**使用狀況**

```scala
%dataset {action} --datasetId {id} --dataFrame {df} --mode batch
```

**說明**

自定義 [!DNL Data Science Workspace] 用於從中讀取或寫入資料集的magic命令 [!DNL PySpark] 筆記本(N)[!DNL Python] 3內核)。

| 名稱 | 說明 | 必填 |
| --- | --- | --- |
| `{action}` | 要在資料集上執行的操作類型。 有兩個操作可用於「讀取」或「寫入」。 | 是 |
| `--datasetId {id}` | 用於提供要讀或寫的資料集的ID。 | 是 |
| `--dataFrame {df}` | 熊貓資料框。 <ul><li> 當操作為「read」時，{df}是資料集讀取操作結果可用的變數（如資料幀）。 </li><li> 當操作為「write」時，此資料幀{df}將寫入資料集。 </li></ul> | 是 |
| `--mode` | 更改資料讀取方式的附加參數。 允許的參數為「批處理」和「交互」。 預設情況下，模式設定為「批處理」。<br> 建議您使用「交互」模式來提高較小資料集上的查詢效能。 | 是 |

>[!TIP]
>
>查看 [筆記本資料限制](#notebook-data-limits) 確定 `mode` 應設定為 `interactive` 或 `batch`。

**範例**

- **閱讀示例**: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0 --mode batch`
- **寫示例**: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0 --mode batch`

>[!IMPORTANT]
>
> 使用快取資料 `df.cache()` 在寫入資料之前，可以大大提高筆記型電腦的效能。 如果您收到以下任何錯誤，這將有所幫助：
> 
> - 由於階段失敗而中止作業……只能壓縮每個分區中元素數相同的RDD。
> - 遠程RPC客戶端已斷開關聯和其他記憶體錯誤。
> - 讀取和寫入資料集時效能較差。
> 
> 查看 [故障排除指南](../troubleshooting-guide.md) 的子菜單。

您可以使用以下方法在JupyterLab購買中自動生成上述示例：

選擇JupyterLab左導航中的「資料」表徵圖頁籤（下面突出顯示）。 的 **[!UICONTROL 資料集]** 和 **[!UICONTROL 架構]** 的下界。 選擇 **[!UICONTROL 資料集]** ，然後選擇 **[!UICONTROL 在筆記本中寫入資料]** 選項。 可執行代碼條目出現在筆記本底部。

- 使用 **[!UICONTROL 在筆記本中瀏覽資料]** 生成讀取單元格。
- 使用 **[!UICONTROL 在筆記本中寫入資料]** 生成寫單元格。

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
>您還可以指定可選的種子樣例，如boolean withReplacement、雙分數或長種子。

### 篩選 [!DNL ExperienceEvent] 資料 {#pyspark-filter-experienceevent}

訪問和篩選 [!DNL ExperienceEvent] PySpark筆記本中的資料集要求您提供資料集標識(`{DATASET_ID}`)、組織的IMS標識以及定義特定時間範圍的篩選器規則。 使用該函式定義過濾時間範圍 `spark.sql()`，其中函式參數是SQL查詢字串。

以下單元格篩選 [!DNL ExperienceEvent] 2019年1月1日至2019年12月31日底期間完全存在的資料。

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df --mode batch

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

## 斯卡拉筆記本 {#scala-notebook}

下面的文檔包含以下概念的示例：

- [初始化sparkSession](#scala-initialize)
- [讀取資料集](#read-scala-dataset)
- [寫入資料集](#scala-write-dataset)
- [建立本地資料幀](#scala-create-dataframe)
- [篩選ExperienceEvent資料](#scala-experienceevent)

### 正在初始化SparkSession {#scala-initialize}

所有Scala筆記本都要求您使用以下模板代碼初始化會話：

```scala
import org.apache.spark.sql.{ SparkSession }
val spark = SparkSession
  .builder()
  .master("local")
  .getOrCreate()
```

### 讀取資料集 {#read-scala-dataset}

在Scala中，可以導入 `clientContext` 獲取和返回平台值，這樣就無需定義變數，如 `var userToken`。 在下面的Scala示例中， `clientContext` 用於獲取並返回讀取資料集所需的所有值。

>[!IMPORTANT]
>
> 使用快取資料 `df.cache()` 在寫入資料之前，可以大大提高筆記型電腦的效能。 如果您收到以下任何錯誤，這將有所幫助：
> 
> - 由於階段失敗而中止作業……只能壓縮每個分區中元素數相同的RDD。
> - 遠程RPC客戶端已斷開關聯和其他記憶體錯誤。
> - 讀取和寫入資料集時效能較差。
> 
> 查看 [故障排除指南](../troubleshooting-guide.md) 的子菜單。

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
  .option("sandbox-name", clientContext.getSandboxName())
  .option("mode", "batch")
  .option("dataset-id", "5e68141134492718af974844")
  .load()

df1.printSchema()
df1.show(10)
```

| 元素 | 說明 |
| ------- | ----------- |
| df1 | 一個變數，它表示用於讀取和寫入資料的Pactis資料幀。 |
| 用戶令牌 | 您的用戶令牌已使用 `clientContext.getUserToken()`。 |
| 服務令牌 | 使用自動獲取的服務令牌 `clientContext.getServiceToken()`。 |
| ims-org | 您的組織ID是使用 `clientContext.getOrgId()`。 |
| api鍵 | 使用自動獲取的API密鑰 `clientContext.getApiKey()`。 |

>[!TIP]
>
>查看 [筆記本資料限制](#notebook-data-limits) 確定 `mode` 應設定為 `interactive` 或 `batch`。

您可以使用以下方法在JupyterLab購買中自動生成上述示例：

選擇JupyterLab左導航中的「資料」表徵圖頁籤（下面突出顯示）。 的 **[!UICONTROL 資料集]** 和 **[!UICONTROL 架構]** 的下界。 選擇 **[!UICONTROL 資料集]** ，然後選擇 **[!UICONTROL 在筆記本中瀏覽資料]** 選項。 可執行代碼條目出現在筆記本底部。
和
- 使用 **[!UICONTROL 在筆記本中瀏覽資料]** 生成讀取單元格。
- 使用 **[!UICONTROL 在筆記本中寫入資料]** 生成寫單元格。

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### 寫入資料集 {#scala-write-dataset}

在Scala中，可以導入 `clientContext` 獲取和返回平台值，這樣就無需定義變數，如 `var userToken`。 在下面的Scala示例中， `clientContext` 用於定義和返回寫入資料集所需的所有值。

>[!IMPORTANT]
>
> 使用快取資料 `df.cache()` 在寫入資料之前，可以大大提高筆記型電腦的效能。 如果您收到以下任何錯誤，這將有所幫助：
> 
> - 由於階段失敗而中止作業……只能壓縮每個分區中元素數相同的RDD。
> - 遠程RPC客戶端已斷開關聯和其他記憶體錯誤。
> - 讀取和寫入資料集時效能較差。
> 
> 查看 [故障排除指南](../troubleshooting-guide.md) 的子菜單。

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
  .option("sandbox-name", clientContext.getSandboxName())
  .option("mode", "batch")
  .option("dataset-id", "5e68141134492718af974844")
  .save()
```

| 元素 | 說明 |
| ------- | ----------- |
| df1 | 一個變數，它表示用於讀取和寫入資料的Pactis資料幀。 |
| 用戶令牌 | 您的用戶令牌已使用 `clientContext.getUserToken()`。 |
| 服務令牌 | 使用自動獲取的服務令牌 `clientContext.getServiceToken()`。 |
| ims-org | 您的組織ID是使用 `clientContext.getOrgId()`。 |
| api鍵 | 使用自動獲取的API密鑰 `clientContext.getApiKey()`。 |

>[!TIP]
>
>查看 [筆記本資料限制](#notebook-data-limits) 確定 `mode` 應設定為 `interactive` 或 `batch`。

### 建立本地資料幀 {#scala-create-dataframe}

要使用Scala建立本地資料幀，需要SQL查詢。 例如：

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### 篩選 [!DNL ExperienceEvent] 資料 {#scala-experienceevent}

訪問和篩選 [!DNL ExperienceEvent] scala筆記本中的資料集要求您提供資料集標識(`{DATASET_ID}`)、組織的IMS標識以及定義特定時間範圍的篩選器規則。 使用函式定義過濾時間範圍 `spark.sql()`，其中函式參數是SQL查詢字串。

以下單元格篩選 [!DNL ExperienceEvent] 2019年1月1日至2019年12月31日底期間完全存在的資料。

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

本文檔介紹了使用JupyterLab筆記本訪問資料集的一般准則。 有關查詢資料集的更深入示例，請訪問 [JupyterLab筆記本中的查詢服務](./query-service.md) 文檔。 有關如何瀏覽和可視化資料集的詳細資訊，請訪問 [使用筆記本分析資料](./analyze-your-data.md)。

## 可選的SQL標誌 [!DNL Query Service] {#optional-sql-flags-for-query-service}

此表概述了可用於 [!DNL Query Service]。

| **標誌** | **說明** |
| --- | --- |
| `-h`、`--help` | 顯示幫助消息並退出。 |
| `-n`、`--notify` | 切換通知查詢結果的選項。 |
| `-a`、`--async` | 使用此標誌以非同步方式執行查詢，並可在查詢執行時釋放內核。 在將查詢結果分配給變數時要小心，因為如果查詢不完成，則可能未定義它。 |
| `-d`、`--display` | 使用此標誌可阻止顯示結果。 |
