---
keywords: Experience Platform;JupyterLab;筆記本;數據科學工作環境;熱門話題;%資料集;互動模式;批處理模式;Spark sdk;Python SDK;訪問數據;筆記本數據訪問
solution: Experience Platform
title: Jupyterlab Notebooks 中的數據訪問
description: 本指南著重於說明如何使用Jupyter Notebooks (內建於Data Science Workspace)來存取您的資料。
exl-id: 2035a627-5afc-4b72-9119-158b95a35d32
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '3343'
ht-degree: 3%

---

# [!DNL Jupyterlab]筆記型電腦中的資料存取

>[!NOTE]
>
>Data Science Workspace已無法購買。
>
>本文檔適用於先前有權使用數據科學工作環境的現有客戶。

每個受支持的內核都提供內置功能，允許您從筆記本中的資料集讀取Platform數據。 目前，Adobe Experience Platform Data Science 工作環境中的 JupyterLab 支援 、R、PySpark 和 Scala 的 [!DNL Python]筆記本。 但是，對分頁數據的支援僅限於 [!DNL Python] 和 R 筆記本。 本指南重點介紹如何使用 JupyterLab 筆記本訪問數據。

## 快速入門

在閱讀本指南之前，請查看用戶 指南](./overview.md)，以[[!DNL JupyterLab] 深入了解[!DNL JupyterLab]數據科學工作環境及其角色。

## 筆記本數據限制 {#notebook-data-limits}

>[!IMPORTANT]
>
>對於 PySpark 和 Scala 筆記本，如果您收到錯誤，原因為“遠端RPC用戶端解除關聯”。 這通常意味著驅動程式或執行程式記憶體不足。 嘗試切換到 [「批處理」模式](#mode) 以解決此錯誤。

以下信息定義可讀取的最大数据量、使用的數據類型以及讀取數據所需的估計時間範圍。

對於 [!DNL Python] 和 R，配置在 40GB RAM 的筆記型電腦伺服器用於基準測試。 對於 PySpark 和 Scala，配置在 64GB RAM、8 個內核、2 個 DBU 和最多 4 個工作線程的 databricks 集群用於下面概述的基準測試。

使用的 ExperienceEvent 綱要數據的大小各不相同，從一千 （1K） 列到十億 （1B） 列不等。 請注意，對於 PySpark 和 [!DNL Spark] 指標，XDM 數據使用了 10 天的日期跨度。

廣告即選綱要數據是使用表建立即選 （CTAS） 進行 [!DNL Query Service] 預處理的。 此資料的大小也不同，從1,000列(1K)到10億(1B)列不等。

### 何時使用批次模式與互動模式 {#mode}

使用PySpark和Scala筆記本讀取資料集時，您可以選擇使用互動模式或批次模式來讀取資料集。 互動式有助於快速結果，而批次模式適用於大型資料集。

- 若是PySpark和Scala筆記型電腦，讀取超過500萬筆資料列時，應使用批次模式。 如需有關每種模式效率的詳細資訊，請參閱下方的[PySpark](#pyspark-data-limits)或[Scala](#scala-data-limits)資料限製表。

### [!DNL Python]筆記型電腦資料限制

**XDM ExperienceEvent 綱要：** 您應該能夠在不到22分鐘的時間內讀取最多200萬行（磁碟上~6.1 GB數據）的XDM數據。 新增其他列可能會導致錯誤。

| 列數 | 1K | 10K | 100K | 1分鐘 | 200萬 |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| 磁碟大小(MB) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK （以秒為單位） | 20.3 | 86.8 | 63 | 659 | 1315 |

**廣告點綱要：** 您應該能夠在不到 14 分鐘的時間內讀取最多 500 萬行（磁碟上 ~5.6 GB 的數據）的非 XDM （廣告-hoc） 數據。 添加其他行可能會導致錯誤。

| 行數 | 1K | 10K | 100K | 1分鐘 | 200萬 | 3分鐘 | 5分鐘 |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| 磁碟大小(MB) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK（秒） | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

### R 筆記本數據限制

**XDM ExperienceEvent 綱要：** 您應該能夠在13分鐘內讀取最多100萬行XDM數據（磁碟上3GB數據）。

| 行數 | 1K | 10K | 100K | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| 磁碟大小 （MB） | 18.73 | 187.5 | 308 | 3000 |
| R核心（以秒為單位） | 14.03 | 69.6 | 86.8 | 775 |

**臨機操作結構描述：**&#x200B;您最多可以在10分鐘內讀取300萬列臨機操作資料（磁碟上有293MB的資料）。

| 列數 | 1K | 10K | 100K | 1分鐘 | 200萬 | 3分鐘 |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| 磁碟大小(MB) | 0.082 | 0.612 | 9.0 | 91 | 188 | 293 |
| R SDK （以秒為單位） | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

### PySpark （[!DNL Python]核心）筆記本資料限制： {#pyspark-data-limits}

**XDM ExperienceEvent結構描述：**&#x200B;在互動模式中，您應該可以在20分鐘左右讀取最多500萬列（磁碟上約13.42GB的資料）的XDM資料。 互動模式僅支援最多500萬列。 如果您想要讀取較大的資料集，建議您切換到批次模式。 在批次模式中，您最多可在14小時內讀取5億列（磁碟上約1.31TB的資料）的XDM資料。

| 列數 | 1K | 10K | 100K | 1分鐘 | 200萬 | 3M | 5M | 10米 | 50米 | 100米 | 500米 |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 磁碟大小 | 2.93毫巴 | 4.38兆位元組 | 29.02 | 2.69GB   | 5.39GB   | 8.09GB   | 13.42GB   | 26.82GB   | 134.24GB   | 268.39GB   | 1.31TB |
| SDK （互動式模式） | 33 秒 | 32.4秒 | 55.1秒 | 253.5秒 | 489.2秒 | 729.6秒 | 1206.8秒 | - | - | - | - |
| SDK （批次模式） | 815.8秒 | 492.8秒 | 379.1秒 | 637.4秒 | 624.5秒 | 869.2秒 | 1104.1秒 | 1786s | 5387.2秒 | 10624.6秒 | 50547s |

**臨機結構描述：**&#x200B;在互動模式中，您應該可以在3分鐘內讀取最多500萬列（磁碟上約5.36GB的資料）的非XDM資料。 在批次模式中，您最多可在18分鐘內讀取10億列（磁碟上約1.05TB的資料）非XDM資料。

| 列數 | 1K | 10K | 100K | 1分鐘 | 200萬 | 3分鐘 | 5分鐘 | 10分鐘 | 50分鐘 | 100米 | 500米 | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| 磁碟大小 | 1.12毫巴 | 11.24毫巴 | 109.48毫巴 | 2.69GB   | 2.14GB   | 3.21GB   | 5.36GB   | 10.71GB   | 53.58GB   | 107.52GB   | 535.88GB   | 1.05TB |
| SDK 互動式模式 （秒） | 28.2秒 | 18.6秒 | 20.8秒 | 20.9秒 | 23.8秒 | 21.7秒 | 24.7秒 | - | - | - | - | - |
| SDK批次模式（以秒為單位） | 428.8秒 | 578.8秒 | 641.4秒 | 538.5秒 | 630.9秒 | 467.3秒 | 411秒 | 675秒 | 702年代 | 719.2秒 | 1022.1秒 | 1122.3秒 |

### [!DNL Spark] （Scala核心）筆記本資料限制： {#scala-data-limits}

**XDM ExperienceEvent結構描述：**&#x200B;在互動模式中，您應該可以在18分鐘左右讀取最多500萬列（磁碟上約13.42GB的資料）的XDM資料。 互動模式僅支援最多500萬列。 如果您想要讀取較大的資料集，建議您切換到批次模式。 在批次模式中，您最多可在14小時內讀取5億列（磁碟上約1.31TB的資料）的XDM資料。

| 列數 | 1K | 10K | 100K | 1分鐘 | 200萬 | 3分鐘 | 5分鐘 | 10分鐘 | 50分鐘 | 100米 | 500米 |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 磁碟大小 | 2.93毫巴 | 4.38毫巴 | 29.02 | 2.69GB   | 5.39GB   | 8.09GB   | 13.42GB   | 26.82GB   | 134.24GB   | 268.39GB   | 1.31TB |
| SDK 互動式模式 （秒） | 37.9秒 | 22.7秒 | 45.6秒 | 231.7秒 | 444.7秒 | 660.6秒 | 1100秒 | - | - | - | - |
| SDK 批次模式 （秒） | 374.4秒 | 398.5秒 | 527秒 | 487.9秒 | 588.9秒 | 829秒 | 939.1秒 | 1441s | 5473.2秒 | 10118.8 | 49207.6 |

**臨機結構描述：**&#x200B;在互動模式中，您應該可以在3分鐘內讀取最多500萬列（磁碟上約5.36GB的資料）的非XDM資料。 在批次模式中，您最多可在16分鐘內讀取10億列（磁碟上約1.05TB的資料）非XDM資料。

| 行數 | 1K | 10K | 100K | 1M | 200萬 | 3分鐘 | 5分鐘 | 10分鐘 | 50分鐘 | 100米 | 500米 | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| 磁碟大小 | 1.12毫巴 | 11.24毫巴 | 109.48毫巴 | 2.69GB   | 2.14GB   | 3.21GB   | 5.36GB   | 10.71GB   | 53.58GB   | 107.52GB   | 535.88GB   | 1.05TB |
| SDK互動模式（以秒為單位） | 35.7秒 | 31秒 | 19.5秒 | 25.3秒 | 23 秒 | 33.2秒 | 25.5秒 | - | - | - | - | - |
| SDK 批次模式 （秒） | 448.8秒 | 459.7秒 | 519秒 | 475.8秒 | 599.9秒 | 347.6秒 | 407.8秒 | 397秒 | 518.8秒 | 487.9秒 | 760.2秒 | 975.4秒 |

## Python筆記本 {#python-notebook}

[!DNL Python]筆記本可讓您在存取資料集時分頁資料。 底下示範使用分頁或不使用分頁讀取資料的範常式式碼。 如需可用入門Python筆記型電腦的詳細資訊，請造訪JupyterLab使用手冊中的[[!DNL JupyterLab] 啟動器](./overview.md#launcher)區段。

以下Python檔案會概述下列概念：

- [從資料集讀取](#python-read-dataset)
- [寫入資料集](#write-python)
- [查詢資料](#query-data-python)
- [篩選ExperienceEvent資料](#python-filter)

### 從 Python 中的資料集讀取 {#python-read-dataset}

**不分頁：**

執行以下代碼將讀取整個資料集。 如果執行成功，則數據將另存為變數 `df`引用的 Pandas 數據幀。

```python
# Python

from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**帶分頁：**

執行以下代碼將從指定的資料集讀取數據。 分頁是通過分別通過函數 `limit()` 和 `offset()` 限制和偏移數據來實現的。 限制資料是指要讀取的資料點數上限，而位移是指在讀取資料之前要略過的資料點數。 如果讀取作業執行成功，資料將會儲存為變數`df`參考的Pandas資料流。

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### 寫入Python中的資料集 {#write-python}

若要寫入JupyterLab筆記本的資料集，請在JupyterLab的左側導覽中選取「資料」圖示標籤（以下反白顯示）。 **[!UICONTROL 資料集]**&#x200B;和&#x200B;**[!UICONTROL 結構描述]**&#x200B;目錄出現。 選取&#x200B;**[!UICONTROL 資料集]**&#x200B;並按一下滑鼠右鍵，然後從您要使用之資料集的下拉式選單中選取&#x200B;**[!UICONTROL 在筆記本中寫入資料]**&#x200B;選項。 筆記本底部會顯示可執行程式碼專案。

![](../images/jupyterlab/data-access/write-dataset.png)

- 使用「在筆記本中寫入數據」]**生成**[!UICONTROL &#x200B;具有所選資料集的寫入單元。
- 使用&#x200B;**[!UICONTROL 在筆記本中探索資料]**，以使用您選取的資料集產生讀取儲存格。
- 使用&#x200B;**[!UICONTROL Notebook]**&#x200B;中的查詢資料，以使用您選取的資料集產生基本查詢儲存格。

或者，您可以複製並貼上下列程式碼儲存格。 取代`{DATASET_ID}`和`{PANDA_DATAFRAME}`。

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### 在[!DNL Python]中使用[!DNL Query Service]查詢資料 {#query-data-python}

[!DNL Platform]上的[!DNL JupyterLab]可讓您在[!DNL Python]筆記本中使用SQL，透過[Adobe Experience Platform查詢服務](https://www.adobe.com/go/query-service-home-en)存取資料。 透過[!DNL Query Service]存取資料對於處理大型資料集很有用，因為其執行時間較長。 請注意，使用[!DNL Query Service]查詢資料的處理時間限製為10分鐘。

在[!DNL JupyterLab]中使用[!DNL Query Service]之前，請確定您瞭解[[!DNL Query Service] SQL語法](https://www.adobe.com/go/query-service-sql-syntax-en)。

使用[!DNL Query Service]查詢資料需要您提供目標資料集的名稱。 您可以使用&#x200B;**[!UICONTROL 資料總管]**&#x200B;尋找所需的資料集，以產生必要的程式碼儲存格。 右鍵單擊資料集清單，然後按下「 **[!UICONTROL 查詢筆記本]** 中的數據」以在筆記本中生成兩個代碼單元格。 下面將更詳細地概述這兩個單元格。

![](../images/jupyterlab/data-access/python-query-dataset.png)

為了在 [!DNL Query Service] 中使用 [!DNL JupyterLab]，您必須首先在工作 [!DNL Python] 筆記本和 [!DNL Query Service]之間創建連接。 這可以通過執行第一個生成的單元來實現。

```python
qs_connect()
```

在第二個生成的儲存格中，必須在 SQL 查詢之前定義第一行。 依預設，產生的儲存格會定義選用變數(`df0`)，將查詢結果儲存為Pandas資料流。 <br> `-c QS_CONNECTION`引數是必要的，並告訴核心對[!DNL Query Service]執行SQL查詢。 如需其他引數的清單，請參閱[附錄](#optional-sql-flags-for-query-service)。

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

通過使用字串格式的語法並將變數包裝在大括弧 （）`{}` 中，可以在 SQL 查詢 中直接引用 Python 變數，如以下示例所示：

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### [!DNL ExperienceEvent]篩選数据 {#python-filter}

若要訪問和篩選 [!DNL ExperienceEvent] 筆記本中的 [!DNL Python] 資料集，必須提供資料集 （`{DATASET_ID}`） 的ID以及使用邏輯運算元定義特定時間範圍的篩選規則。 定義時間範圍時，將忽略任何指定的分頁，並考慮整個資料集。

篩選運算符清單說明如下：

- `eq()`：等於
- `gt()`：大於
- `ge()`：大於或等於
- `lt()`：小於
- `le()`：小於或等於
- `And()`：邏輯 AND 運算子
- `Or()`：邏輯 OR 運算符

以下單元格篩選器 [!DNL ExperienceEvent] 2019 年 1 月 1 日至 2019 年 12 月 31 日期間僅存在的數據資料集。

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

## R 筆記本 {#r-notebooks}

R 筆記本允許你在訪問數據集時對數據進行分頁。 下面演示了使用和不使用分頁讀取數據的示例代碼。 如需有關可用入門R筆記型電腦的詳細資訊，請造訪JupyterLab使用手冊中的[[!DNL JupyterLab] 啟動器](./overview.md#launcher)區段。

以下的R檔案概述了以下概念：

- [從資料集讀取](#r-read-dataset)
- [寫入資料集](#write-r)
- [篩選ExperienceEvent資料](#r-filter)

### 從 R 中的資料集讀取 {#r-read-dataset}

**不分頁：**

執行以下程式碼將會讀取整個資料集。 如果執行成功，則數據將另存為變數 `df0`引用的 Pandas 數據幀。

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

**分頁：**

執行以下程式碼將會從指定的資料集中讀取資料。 分別透過函式`limit()`和`offset()`限制及位移資料而達到分頁。 限制資料是指要讀取的資料點數上限，而位移是指在讀取資料之前要略過的資料點數。 如果讀取作業執行成功，資料將會儲存為變數`df0`參考的Pandas資料流。

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

若要寫入JupyterLab筆記本的資料集，請在JupyterLab的左側導覽中選取「資料」圖示標籤（以下反白顯示）。 **[!UICONTROL 資料集]**&#x200B;和&#x200B;**[!UICONTROL 結構描述]**&#x200B;目錄出現。 選取&#x200B;**[!UICONTROL 資料集]**&#x200B;並按一下滑鼠右鍵，然後從您要使用之資料集的下拉式選單中選取&#x200B;**[!UICONTROL 在筆記本中寫入資料]**&#x200B;選項。 筆記本底部會顯示可執行程式碼專案。

![](../images/jupyterlab/data-access/r-write-dataset.png)

- 使用&#x200B;**[!UICONTROL 在Notebook]**&#x200B;中寫入資料，以使用您選取的資料集產生寫入儲存格。
- 使用&#x200B;**[!UICONTROL 在筆記本中探索資料]**，以使用您選取的資料集產生讀取儲存格。

或者，您可以複製並貼上下列程式碼儲存格：

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### 篩選[!DNL ExperienceEvent]資料 {#r-filter}

若要存取和篩選R筆記本中的[!DNL ExperienceEvent]資料集，您必須提供資料集(`{DATASET_ID}`)的識別碼，以及使用邏輯運運算元定義特定時間範圍的篩選規則。 定義時間範圍時，會忽略任何指定的分頁，並考量整個資料集。

篩選運算符清單說明如下：

- `eq()`：等於
- `gt()`：大於
- `ge()`：大於或等於
- `lt()`：小於
- `le()`：小於或等於
- `And()`：邏輯AND運運算元
- `Or()`：邏輯OR運運算元

下列儲存格會將[!DNL ExperienceEvent]資料集篩選為2019年1月1日到2019年12月31日之間專屬存在的資料。

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

以下PySpark檔案概述了以下概念：

- [初始化sparkSession](#spark-initialize)
- [讀取和寫入資料](#magic)
- [建立本地數據幀](#pyspark-create-dataframe)
- [篩選ExperienceEvent資料](#pyspark-filter-experienceevent)

### 正在初始化sparkSession {#spark-initialize}

所有[!DNL Spark] 2.4 Notebook都需要您使用下列樣版程式碼來初始化工作階段。

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### 使用%dataset來讀取和寫入PySpark 3筆記本 {#magic}

隨著[!DNL Spark] 2.4的推出，提供`%dataset`自訂魔術用於PySpark 3 ([!DNL Spark] 2.4)筆記本。 如需有關IPython核心中可用的魔術命令的詳細資訊，請瀏覽[IPython魔術檔案](https://ipython.readthedocs.io/en/stable/interactive/magics.html)。


**使用狀況**

```scala
%dataset {action} --datasetId {id} --dataFrame {df} --mode batch
```

**說明**

用於從筆記本（3 個內核）[!DNL Python]讀取[!DNL PySpark]或寫入資料集的自定義[!DNL Data Science Workspace]魔術命令。

| 名稱 | 說明 | 必填 |
| --- | --- | --- |
| `{action}` | 要在資料集上執行的操作類型。 有兩種操作可用「讀取」或「寫入」。 | 是 |
| `--datasetId {id}` | 用於提供要讀取或寫入資料集的 ID。 | 是 |
| `--dataFrame {df}` | 熊貓數據幀。 <ul><li> 當操作為“讀取”時， {df} 是資料集讀取操作的結果可用的變數（例如數據幀）。 </li><li> 當操作為“寫入”時，此數據幀 {df} 將寫入資料集。 </li></ul> | 是 |
| `--mode` | 更改讀取資料方式的附加參數。 允許的參數包括「批次」和「互動式」。 默認情況下，模式設置為「批處理」。<br> 建議您使用「互動式」模式，以提高較小數據集上的查詢性能。 | 是 |

>[!TIP]
>
>檢視筆記本資料限制](#notebook-data-limits)部分中的 [PySpark 表，以確定是否`mode`應設定為 `interactive` 或 `batch`。

**範例**

- **讀取範例**： `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0 --mode batch`
- **寫入範例**： `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0 --mode batch`

>[!IMPORTANT]
>
> 在寫入資料之前使用`df.cache()`快取資料可大幅改善筆記型電腦效能。 如果您收到下列任何錯誤，這將會有所幫助：
> 
> - 工作已中止，因為中繼失敗……只能壓縮每個資料分割中具有相同元素數量的RDD。
> - 遠端RPC用戶端已解除關聯和其他記憶體錯誤。
> - 讀取和寫入數據集時性能不佳。
> 
> 如需詳細資訊， [請參閱疑難解答指南](../troubleshooting-guide.md) 。

您可以使用以下方法在JupyterLab buy中自動生成上述範例：

在JupyterLab的左側導覽區中選取「資料」圖示標籤（在下方反白顯示）。 **[!UICONTROL 資料集]**&#x200B;和&#x200B;**[!UICONTROL 結構描述]**&#x200B;目錄出現。 選取&#x200B;**[!UICONTROL 資料集]**&#x200B;並按一下滑鼠右鍵，然後從您要使用之資料集的下拉式選單中選取&#x200B;**[!UICONTROL 在筆記本中寫入資料]**&#x200B;選項。 筆記本底部會顯示可執行程式碼專案。

- 使用&#x200B;**[!UICONTROL 瀏覽筆記本中的資料]**&#x200B;產生讀取儲存格。
- 使用&#x200B;**[!UICONTROL 在Notebook]**&#x200B;中寫入資料，以產生寫入儲存格。

![](../images/jupyterlab/data-access/pyspark-write-dataset.png)

### 建立本機資料流 {#pyspark-create-dataframe}

若要使用PySpark 3建立本機資料流，請使用SQL查詢。 例如：

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
>您也可以指定選用的種子樣本，例如withReplacement的布林值、雙分數或長種子。

### 篩選[!DNL ExperienceEvent]資料 {#pyspark-filter-experienceevent}

存取和篩選PySpark筆記本中的[!DNL ExperienceEvent]資料集需要您提供資料集身分識別(`{DATASET_ID}`)、您組織的IMS身分識別，以及定義特定時間範圍的篩選規則。 篩選時間範圍是使用函式`spark.sql()`定義，其中函式引數是SQL查詢字串。

下列儲存格會將[!DNL ExperienceEvent]資料集篩選為2019年1月1日到2019年12月31日之間專屬存在的資料。

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

## Scala notebooks {#scala-notebook}

以下文件包含以下概念的範例：

- [初始化 SparkSession](#scala-initialize)
- [讀取資料集](#read-scala-dataset)
- [寫入資料集](#scala-write-dataset)
- [建立本地數據幀](#scala-create-dataframe)
- [篩選 ExperienceEvent 數據](#scala-experienceevent)

### 正在初始化 SparkSession {#scala-initialize}

所有 Scala 筆記本都要求您使用以下樣本代碼初始化工作階段：

```scala
import org.apache.spark.sql.{ SparkSession }
val spark = SparkSession
  .builder()
  .master("local")
  .getOrCreate()
```

### 讀取資料集 {#read-scala-dataset}

在Scala中，您可以匯入`clientContext`以取得並傳回Platform值，如此便無須定義變數，例如`var userToken`。 在以下Scala範例中，`clientContext`用於取得及傳回讀取資料集所需的所有必要值。

>[!IMPORTANT]
>
> 在寫入資料之前使用`df.cache()`快取資料可大幅改善筆記型電腦效能。 如果您收到下列任何錯誤，這將會有所幫助：
> 
> - 作業已中止，因為階段失敗...只能壓縮每個分區中具有相同數量元素的 RDD。
> - 遠端RPC用戶端已解除關聯和其他記憶體錯誤。
> - 讀取和寫入資料集時效能不佳。
> 
> 如需詳細資訊，請參閱[疑難排解指南](../troubleshooting-guide.md)。

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
| df1 | 表示用於讀取和寫入數據的 Pandas 數據幀的變數。 |
| 用戶代號 | 用戶 `clientContext.getUserToken()`使用 . |
| service-token | 使用`clientContext.getServiceToken()`自動擷取的您的服務權杖。 |
| ims-org | 使用 自動擷取 `clientContext.getOrgId()`您的組織ID。 |
| API 金鑰 | 系統會使用 `clientContext.getApiKey()`. |

>[!TIP]
>
>檢視筆記本資料限制](#notebook-data-limits)部分中的 [Scala 表以確定是否`mode`應設定為 `interactive` 或 `batch`。

您可以使用以下方法在JupyterLab buy中自動生成上述範例：

選擇 JupyterLab 左導覽標籤中的“數據”圖示（下面突出显示）。 此時 **[!UICONTROL 將顯示數據集]** 和 **[!UICONTROL 架構]** 目錄。 選擇 **[!UICONTROL 數據集]** 並按下滑鼠右鍵，然後從要使用的資料集上的下拉功能表中選擇「 **[!UICONTROL 瀏覽筆記本]** 中的數據」 選項。 可執行代碼條目將顯示在筆記本底部。及
- 使用「瀏覽筆記本&#x200B;]**中的數據」產生**[!UICONTROL &#x200B;讀取儲存格。
- 使用「在筆記本&#x200B;]**中寫入數據」生成**[!UICONTROL &#x200B;寫入單元。

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### 寫入資料集 {#scala-write-dataset}

在 Scala 中，您可以匯入 `clientContext` 以獲取和返回Platform值，這樣就無需定義諸如 `var userToken`. 在下面的 Scala 示例中， `clientContext` 用於定義和傳回寫入資料集所需的所有必需值。

>[!IMPORTANT]
>
> 在寫入數據之前緩存 `df.cache()` 數據可以大大提高筆記本性能。 如果您收到以下任何錯誤，這可以提供説明：
> 
> - 工作已中止，因為中繼失敗……只能壓縮每個資料分割中具有相同元素數量的RDD。
> - 遠端RPC使用者端已解除關聯，且發生其他記憶體錯誤。
> - 讀取和寫入資料集時效能不佳。
> 
> 如需詳細資訊，請參閱[疑難排解指南](../troubleshooting-guide.md)。

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
| df1 | 表示用於讀取和寫入數據的 Pandas 數據幀的變數。 |
| 用戶代號 | 使用`clientContext.getUserToken()`自動擷取的使用者權杖。 |
| service-token | 使用 . 自動擷取 `clientContext.getServiceToken()`的服務代號 |
| ims-org | 使用 自動擷取 `clientContext.getOrgId()`您的組織ID。 |
| API 金鑰 | 系統會使用 `clientContext.getApiKey()`. |

>[!TIP]
>
>檢閱[筆記本資料限制](#notebook-data-limits)區段內的Scala表格，以決定`mode`是否應該設定為`interactive`或`batch`。

### 建立本機資料流 {#scala-create-dataframe}

若要使用Scala建立本機資料流，需要SQL查詢。 例如：

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### 篩選[!DNL ExperienceEvent]資料 {#scala-experienceevent}

存取和篩選Scala筆記本中的[!DNL ExperienceEvent]資料集需要您提供資料集身分識別(`{DATASET_ID}`)、您組織的IMS身分識別，以及定義特定時間範圍的篩選規則。 篩選時間範圍是使用函式`spark.sql()`定義，其中函式引數是SQL查詢字串。

下列儲存格會將[!DNL ExperienceEvent]資料集篩選為2019年1月1日到2019年12月31日之間專屬存在的資料。

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

本檔案說明使用JupyterLab Notebook存取資料集的一般准則。 如需查詢資料集的更深入範例，請瀏覽JupyterLab Notebooks](./query-service.md)檔案中的[查詢服務。 如需有關如何探索及視覺化資料集的詳細資訊，請瀏覽檔案： [使用筆記本分析資料](./analyze-your-data.md)。

## [!DNL Query Service]的可選SQL標幟 {#optional-sql-flags-for-query-service}

此表格概述可用於[!DNL Query Service]的可選SQL標幟。

| **旗標** | **說明** |
| --- | --- |
| `-h`、`--help` | 顯示說明訊息並退出。 |
| `-n`、`--notify` | 切換通知查詢結果的選項。 |
| `-a`、`--async` | 使用此旗標以非同步方式執行查詢，並可在查詢執行時釋放核心。 將查詢結果指派給變數時，請務必小心，因為如果查詢未完成，變數可能會未定義。 |
| `-d`、`--display` | 使用此標幟可防止显示結果。 |
