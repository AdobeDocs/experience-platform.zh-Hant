---
keywords: Experience Platform;JupyterLab；筆記型電腦；Data Science Workspace；熱門主題；%dataset；互動式模式；批次模式；Spark sdk;python sdk；存取資料；筆記型電腦資料存取
solution: Experience Platform
title: Jupyterlab筆記型電腦中的資料存取
topic-legacy: Developer Guide
description: 本指南著重於如何使用Data Science Workspace內建的Jupyter Notebooks來存取您的資料。
exl-id: 2035a627-5afc-4b72-9119-158b95a35d32
source-git-commit: c2c2b1684e2c2c3c76dc23ad1df720abd6c4356c
workflow-type: tm+mt
source-wordcount: '3290'
ht-degree: 8%

---

# [!DNL Jupyterlab]筆記本中的資料訪問

每個支援的內核都提供內建功能，允許您從筆記型電腦內的資料集讀取Platform資料。 目前，Adobe Experience Platform Data Science Workspace中的JupyterLab支援[!DNL Python]、R、PySpark和Scala的筆記型電腦。 但是，對分頁資料的支援僅限於[!DNL Python]和R筆記型電腦。 本指南著重於如何使用JupyterLab筆記型電腦存取您的資料。

## 快速入門

閱讀本指南之前，請參閱[[!DNL JupyterLab] 使用手冊](./overview.md) ，以了解[!DNL JupyterLab]及其在Data Science Workspace中角色的詳細介紹。

## 筆記本資料限制{#notebook-data-limits}

>[!IMPORTANT]
>
>對於PySpark和Scala筆記型電腦，如果您收到錯誤，原因是「遠程RPC客戶端不關聯」。 這通常表示驅動程式或執行器記憶體不足。 嘗試切換到[&quot;batch&quot; mode](#mode)以解決此錯誤。

下列資訊定義可讀取的資料量上限、使用的資料類型，以及讀取資料所花費的估計時間範圍。

對於[!DNL Python]和R，使用配置為40GB RAM的筆記型電腦伺服器作為基準。 對於PySpark和Scala，以下列基準使用了配置為64GB RAM、8個內核、2個DBU（最多4個工作人員）的資料庫群集。

使用的ExperienceEvent結構資料大小從一千(1K)列開始，長達十億(1B)列。 請注意，對於PySpark和[!DNL Spark]量度，XDM資料使用10天的日期範圍。

已使用[!DNL Query Service]以選取方式建立表格(CTAS)來預先處理臨機架構資料。 這些資料的大小也從1000(1K)列開始，範圍高達10億(1B)列。

### 何時使用批次模式與互動式模式 {#mode}

使用PySpark和Scala筆記型電腦讀取資料集時，您可以選擇使用互動式模式或批次模式來讀取資料集。 互動式可提供快速結果，批次模式則適用於大型資料集。

- 對於PySpark和Scala筆記本，當讀取500萬行或更多資料時，應使用批次模式。 有關每種模式的效率的詳細資訊，請參閱下面的[PySpark](#pyspark-data-limits)或[Scala](#scala-data-limits)資料限制表。

### [!DNL Python] 筆記型資料限制

**XDM ExperienceEvent結構：** 您應該能在不到22分鐘內讀取最多200萬列的XDM資料（磁碟上約6.1 GB的資料）。新增其他列可能會導致錯誤。

| 列數 | 1K | 10K | 100K | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| 磁碟大小(MB) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK（秒） | 20.3 | 86.8 | 63 | 659 | 1315 |

**臨機結構：** 您應能在不到14分鐘內讀取最多500萬列非XDM（臨機）資料（磁碟上約5.6 GB資料）。新增其他列可能會導致錯誤。

| 列數 | 1K | 1萬 | 10萬 | 1M | 2M | 3M | 5米 |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| 磁碟大小(MB) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK（秒） | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

### R筆記本資料限制

**XDM ExperienceEvent結構：** 您應該能在13分鐘內最多讀取100萬列XDM資料（磁碟上3GB資料）。

| 列數 | 1K | 1萬 | 10萬 | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| 磁碟大小(MB) | 18.73 | 187.5 | 308 | 3000 |
| R內核（秒） | 14.03 | 69.6 | 86.8 | 775 |

**臨機結構：** 您最多應能在約10分鐘內讀取300萬列臨機資料（磁碟上293MB資料）。

| 列數 | 1K | 1萬 | 10萬 | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| 磁碟大小(MB) | 0.082 | 0.612 | 9.0 | 91 | 188 | 293 |
| R SDK（秒） | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

### PySpark（[!DNL Python]內核）筆記型電腦資料限制：{#pyspark-data-limits}

**XDM ExperienceEvent結構：** 在互動式模式中，大約20分鐘內應能讀取500萬列（磁碟上約13.42GB的資料）的XDM資料。互動式模式最多只支援500萬列。 如果您想要讀取較大的資料集，建議您切換至批次模式。 在批次模式下，您應能在約14小時內讀取最多5億行的XDM資料（磁碟上約1.31TB的資料）。

| 列數 | 1K | 1萬 | 10萬 | 1M | 2M | 3M | 5米 | 10米 | 50米 | 1億 | 5億 |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 磁碟大小 | 2.93兆位元組 | 4.38兆位元組 | 29.02 | 2.69 GB   | 5.39 GB   | 8.09 GB   | 13.42 GB   | 26.82 GB   | 134.24 GB   | 268.39 GB   | 1.31太位元組 |
| SDK（互動式模式） | 33秒 | 32.4秒 | 55.1秒 | 253.5秒 | 489.2秒 | 729.6秒 | 1206.8秒 | - | - | - | - |
| SDK（批次模式） | 815.8秒 | 492.8秒 | 379.1秒 | 637.4秒 | 624.5秒 | 869.2秒 | 1104.1秒 | 1786年代 | 5387.2秒 | 10624.6s | 50547s |

**臨機結構：** 在互動式模式中，您最多應能在不到3分鐘內讀取500萬列（磁碟上約5.36GB的資料）的非XDM資料。在批處理模式下，您應能在約18分鐘內讀取非XDM資料的10億行（磁碟上約1.05TB資料）。

| 列數 | 1K | 1萬 | 10萬 | 1M | 2M | 3M | 5米 | 10米 | 50米 | 1億 | 5億 | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| 磁碟大小 | 1.12兆位元組 | 11.24兆位元組 | 109.48兆位元組 | 2.69 GB   | 2.14 GB   | 3.21 GB   | 5.36 GB   | 10.71 GB   | 53.58 GB   | 107.52 GB   | 535.88 GB   | 1.05太位元組 |
| SDK互動式模式（以秒為單位） | 28.2秒 | 18.6秒 | 20.8秒 | 20.9秒 | 23.8秒 | 21.7秒 | 24.7秒 | - | - | - | - | - |
| SDK批次模式（以秒為單位） | 428.8秒 | 578.8秒 | 641.4秒 | 538.5秒 | 630.9秒 | 467.3秒 | 411s | 675秒 | 702秒 | 719.2秒 | 1022.1秒 | 1122.3秒 |

### [!DNL Spark] （擴展內核）筆記本資料限制：  {#scala-data-limits}

**XDM ExperienceEvent結構：** 在互動式模式中，大約18分鐘內可讀取500萬列（磁碟上約13.42GB的資料）的XDM資料。互動式模式最多只支援500萬列。 如果您想要讀取較大的資料集，建議您切換至批次模式。 在批次模式下，您應能在約14小時內讀取最多5億行的XDM資料（磁碟上約1.31TB的資料）。

| 列數 | 1K | 1萬 | 10萬 | 1M | 2M | 3M | 5米 | 10米 | 50米 | 1億 | 5億 |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 磁碟大小 | 2.93兆位元組 | 4.38兆位元組 | 29.02 | 2.69 GB   | 5.39 GB   | 8.09 GB   | 13.42 GB   | 26.82 GB   | 134.24 GB   | 268.39 GB   | 1.31太位元組 |
| SDK互動式模式（以秒為單位） | 37.9秒 | 22.7秒 | 45.6秒 | 231.7秒 | 444.7秒 | 660.6秒 | 1100年代 | - | - | - | - |
| SDK批次模式（以秒為單位） | 374.4秒 | 398.5秒 | 527秒 | 487.9秒 | 588.9秒 | 829秒 | 939.1秒 | 1441秒 | 5473.2秒 | 10118.8 | 49207.6 |

**臨機結構：** 在互動式模式中，您最多應能在不到3分鐘內讀取500萬列非XDM資料（磁碟上約5.36GB資料）。在批次模式下，您應能在約16分鐘內讀取非XDM資料的10億行（磁碟上約1.05TB資料）。

| 列數 | 1K | 1萬 | 10萬 | 1M | 2M | 3M | 5米 | 10米 | 50米 | 1億 | 5億 | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| 磁碟大小 | 1.12兆位元組 | 11.24兆位元組 | 109.48兆位元組 | 2.69 GB   | 2.14 GB   | 3.21 GB   | 5.36 GB   | 10.71 GB   | 53.58 GB   | 107.52 GB   | 535.88 GB   | 1.05太位元組 |
| SDK互動式模式（以秒為單位） | 35.7秒 | 31秒 | 19.5秒 | 25.3秒 | 23秒 | 33.2秒 | 25.5秒 | - | - | - | - | - |
| SDK批次模式（以秒為單位） | 448.8秒 | 459.7秒 | 519秒 | 475.8秒 | 599.9秒 | 347.6秒 | 407.8秒 | 397秒 | 518.8秒 | 487.9秒 | 760.2秒 | 975.4秒 |

## Python筆記本{#python-notebook}

[!DNL Python] 筆記本允許您在訪問資料集時分頁資料。以下示範使用和不使用分頁來讀取資料的范常式式碼。 有關可用啟動Python筆記本的詳細資訊，請訪問JupyterLab使用手冊中的[[!DNL JupyterLab] 啟動器](./overview.md#launcher)部分。

下面的Python文檔概述了以下概念：

- [從資料集讀取](#python-read-dataset)
- [寫入資料集](#write-python)
- [查詢資料](#query-data-python)
- [篩選ExperienceEvent資料](#python-filter)

### 從Python {#python-read-dataset}中的資料集讀取

**不分頁：**

執行下列程式碼會讀取整個資料集。 如果執行成功，則資料將保存為變數`df`引用的Pancits資料幀。

```python
# Python

from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**分頁：**

執行下列程式碼會讀取指定資料集的資料。 通過分別通過函式`limit()`和`offset()`限制和偏移資料來實現分頁。 限制資料是指要讀取的最大資料點數，而偏移是指在讀取資料之前要跳過的資料點數。 如果讀取操作成功執行，則資料將保存為變數`df`引用的Pancits資料幀。

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### 以Python {#write-python}寫入資料集

若要寫入JupyterLab筆記型電腦中的資料集，請在JupyterLab的左側導覽中選取「資料」圖示標籤（以下醒目提示）。 出現&#x200B;**[!UICONTROL Datates]**&#x200B;和&#x200B;**[!UICONTROL Schemas]**&#x200B;目錄。 選擇&#x200B;**[!UICONTROL 資料集]**，按一下右鍵，然後從要使用的資料集的下拉菜單中選擇&#x200B;**[!UICONTROL 在筆記本中寫入資料]**&#x200B;選項。 可執行的代碼條目出現在筆記本底部。

![](../images/jupyterlab/data-access/write-dataset.png)

- 使用&#x200B;**[!UICONTROL 在筆記本中寫入資料]**&#x200B;生成包含所選資料集的寫入單元格。
- 使用&#x200B;**[!UICONTROL 在筆記本中瀏覽資料]**&#x200B;生成包含所選資料集的讀取單元格。
- 使用「筆記本&#x200B;]**查詢資料」生成包含所選資料集的基本查詢單元格。**[!UICONTROL 

或者，您也可以複製並貼上下列程式碼儲存格。 同時更換`{DATASET_ID}`和`{PANDA_DATAFRAME}`。

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### 在[!DNL Python] {#query-data-python}中使用[!DNL Query Service]查詢資料

[!DNL JupyterLab] on [!DNL Platform] 可讓您在筆記型電腦中使 [!DNL Python] 用SQL來存取 [Adobe Experience Platform Query Service](https://www.adobe.com/go/query-service-home-en)。透過[!DNL Query Service]存取資料對於處理大型資料集非常有用，因為其執行時間較長。 請注意，使用[!DNL Query Service]查詢資料的處理時間限制為10分鐘。

在[!DNL JupyterLab]中使用[!DNL Query Service]之前，請務必了解[[!DNL Query Service] SQL語法](https://www.adobe.com/go/query-service-sql-syntax-en)。

使用[!DNL Query Service]查詢資料時，需要提供目標資料集的名稱。 您可以使用&#x200B;**[!UICONTROL 資料總管]**&#x200B;找到所需的資料集，以產生必要的程式碼儲存格。 按一下右鍵資料集清單，然後按一下「筆記本中的&#x200B;**[!UICONTROL 查詢資料]**」，在筆記本中生成兩個代碼單元格。 以下將詳細說明這兩個儲存格。

![](../images/jupyterlab/data-access/python-query-dataset.png)

要在[!DNL JupyterLab]中使用[!DNL Query Service]，必須首先在工作的[!DNL Python]筆記本和[!DNL Query Service]之間建立連接。 這可以通過執行第一生成單元來實現。

```python
qs_connect()
```

在第二個產生的儲存格中，必須在SQL查詢之前定義第一行。 依預設，產生的儲存格會定義選用變數(`df0`)，將查詢結果儲存為Pancits資料幀。 <br>引 `-c QS_CONNECTION` 數是強制的，它告訴內核執行SQL查 [!DNL Query Service]詢。如需其他引數的清單，請參閱[附錄](#optional-sql-flags-for-query-service) 。

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

可使用字串格式語法並以大括弧(`{}`)包住變數，在SQL查詢中直接引用Python變數，如以下示例所示：

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### 篩選[!DNL ExperienceEvent]資料{#python-filter}

若要存取及篩選[!DNL Python]筆記型電腦中的[!DNL ExperienceEvent]資料集，您必須提供資料集的ID(`{DATASET_ID}`)，以及使用邏輯運算子定義特定時間範圍的篩選規則。 定義時間範圍時，會忽略任何指定的分頁，並考量整個資料集。

篩選運算子的清單如下所述：

- `eq()`: Equal to
- `gt()`: Greater than
- `ge()`: Greater than or equal to
- `lt()`: Less than
- `le()`: Less than or equal to
- `And()`:邏輯AND運算子
- `Or()`:邏輯OR運算子

下列儲存格會將[!DNL ExperienceEvent]資料集篩選為2019年1月1日至2019年12月31日底之間僅存在的資料。

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

## R筆記本{#r-notebooks}

R筆記本允許您在訪問資料集時分頁資料。 以下示範使用和不使用分頁來讀取資料的范常式式碼。 有關可用啟動器R筆記本的詳細資訊，請訪問JupyterLab使用手冊中的[[!DNL JupyterLab] 啟動器](./overview.md#launcher)部分。

以下R檔案概述下列概念：

- [從資料集讀取](#r-read-dataset)
- [寫入資料集](#write-r)
- [篩選ExperienceEvent資料](#r-filter)

### 從R {#r-read-dataset}中的資料集讀取

**不分頁：**

執行下列程式碼會讀取整個資料集。 如果執行成功，則資料將保存為變數`df0`引用的Pancits資料幀。

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

執行下列程式碼會讀取指定資料集的資料。 通過分別通過函式`limit()`和`offset()`限制和偏移資料來實現分頁。 限制資料是指要讀取的最大資料點數，而偏移是指在讀取資料之前要跳過的資料點數。 如果讀取操作成功執行，則資料將保存為變數`df0`引用的Pancits資料幀。

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

### 寫入R {#write-r}中的資料集

若要寫入JupyterLab筆記型電腦中的資料集，請在JupyterLab的左側導覽中選取「資料」圖示標籤（以下醒目提示）。 出現&#x200B;**[!UICONTROL Datates]**&#x200B;和&#x200B;**[!UICONTROL Schemas]**&#x200B;目錄。 選擇&#x200B;**[!UICONTROL 資料集]**，按一下右鍵，然後從要使用的資料集的下拉菜單中選擇&#x200B;**[!UICONTROL 在筆記本中寫入資料]**&#x200B;選項。 可執行的代碼條目出現在筆記本底部。

![](../images/jupyterlab/data-access/r-write-dataset.png)

- 使用&#x200B;**[!UICONTROL 在筆記本中寫入資料]**&#x200B;生成包含所選資料集的寫入單元格。
- 使用&#x200B;**[!UICONTROL 在筆記本中瀏覽資料]**&#x200B;生成包含所選資料集的讀取單元格。

或者，您也可以複製並貼上下列程式碼儲存格：

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### 篩選[!DNL ExperienceEvent]資料{#r-filter}

若要存取及篩選R型筆記型電腦中的[!DNL ExperienceEvent]資料集，您必須提供資料集的ID(`{DATASET_ID}`)，以及使用邏輯運算子定義特定時間範圍的篩選規則。 定義時間範圍時，會忽略任何指定的分頁，並考量整個資料集。

篩選運算子的清單如下所述：

- `eq()`:等於
- `gt()`:大於
- `ge()`:大於或等於
- `lt()`:小於
- `le()`:小於或等於
- `And()`:邏輯AND運算子
- `Or()`:邏輯OR運算子

下列儲存格會將[!DNL ExperienceEvent]資料集篩選為2019年1月1日至2019年12月31日底之間僅存在的資料。

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

## PySpark 3筆記型電腦{#pyspark-notebook}

下面的PySpark文檔概述了以下概念：

- [初始化SparkSession](#spark-initialize)
- [讀和寫資料](#magic)
- [建立本地資料幀](#pyspark-create-dataframe)
- [篩選ExperienceEvent資料](#pyspark-filter-experienceevent)

### 初始化sparkSession {#spark-initialize}

所有[!DNL Spark] 2.4筆記本都要求您使用以下模板代碼初始化會話。

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### 使用%資料集，使用PySpark 3筆記本進行讀寫 {#magic}

隨著[!DNL Spark] 2.4的推出，`%dataset`自定義魔術被提供用於PySpark 3([!DNL Spark] 2.4)筆記本。 有關IPython內核中可用的魔術命令的詳細資訊，請訪問[IPython魔術文檔](https://ipython.readthedocs.io/en/stable/interactive/magics.html)。


**使用狀況**

```scala
%dataset {action} --datasetId {id} --dataFrame {df}`
```

**說明**

用於從[!DNL PySpark]筆記本（[!DNL Python] 3內核）讀取或寫入資料集的自定義[!DNL Data Science Workspace]魔術命令。

| 名稱 | 說明 | 必填 |
| --- | --- | --- |
| `{action}` | 要在資料集上執行的動作類型。 「已讀」或「已寫」兩個動作。 | 是 |
| `--datasetId {id}` | 用來提供要讀取或寫入的資料集ID。 | 是 |
| `--dataFrame {df}` | 熊貓的資料框。 <ul><li> 當動作為「read」時，{df}為變數，資料集讀取操作的結果可用。 </li><li> 當動作為「write」時，此資料幀{df}會寫入資料集。 </li></ul> | 是 |
| `--mode` | 變更資料讀取方式的其他參數。 允許的參數為「批次」和「互動式」。 預設情況下，模式會設為「互動式」。 在讀取大量資料時，建議使用「批次」模式。 | 無 |

>[!TIP]
>
>查看[筆記本資料限制](#notebook-data-limits)部分內的PySpark表，以確定`mode`應設定為`interactive`還是`batch`。

**範例**

- **閱讀範例**:  `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
- **撰寫範例**:  `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

>[!IMPORTANT]
>
> 在寫入資料之前使用`df.cache()`快取資料可以大大提高筆記型電腦的效能。 如果您收到下列任何錯誤，這將有所幫助：
> 
> - 作業因預備失敗而中止……只能壓縮每個分區中元素數量相同的RDD。
> - 遠程RPC客戶端斷開關聯和其他記憶體錯誤。
> - 讀取和寫入資料集時效能不佳。

> 
> 
如需詳細資訊，請參閱[疑難排解指南](../troubleshooting-guide.md) 。

您可以使用下列方法在JupyterLab購買中自動產生上述範例：

在JupyterLab的左側導覽中選取「資料」圖示標籤（以下醒目提示）。 出現&#x200B;**[!UICONTROL Datates]**&#x200B;和&#x200B;**[!UICONTROL Schemas]**&#x200B;目錄。 選擇&#x200B;**[!UICONTROL 資料集]**，按一下右鍵，然後從要使用的資料集的下拉菜單中選擇&#x200B;**[!UICONTROL 在筆記本中寫入資料]**&#x200B;選項。 可執行的代碼條目出現在筆記本底部。

- 使用&#x200B;**[!UICONTROL 在筆記本中瀏覽資料]**&#x200B;生成讀單元。
- 使用&#x200B;**[!UICONTROL 在筆記本中寫入資料]**&#x200B;生成寫單元。

![](../images/jupyterlab/data-access/pyspark-write-dataset.png)

### 建立本地資料幀{#pyspark-create-dataframe}

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

### 篩選[!DNL ExperienceEvent]資料{#pyspark-filter-experienceevent}

存取和篩選PySpark筆記型電腦中的[!DNL ExperienceEvent]資料集時，您必須提供資料集身分(`{DATASET_ID}`)、貴組織的IMS身分，以及定義特定時間範圍的篩選規則。 篩選時間範圍是使用函式`spark.sql()`來定義，其中函式參數為SQL查詢字串。

下列儲存格會將[!DNL ExperienceEvent]資料集篩選為2019年1月1日至2019年12月31日期末之間僅存在的資料。

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

## 縮放筆記本{#scala-notebook}

以下檔案包含下列概念的範例：

- [初始化SparkSession](#scala-initialize)
- [讀取資料集](#read-scala-dataset)
- [寫入資料集](#scala-write-dataset)
- [建立本地資料幀](#scala-create-dataframe)
- [篩選ExperienceEvent資料](#scala-experienceevent)

### 初始化SparkSession {#scala-initialize}

所有Scala筆記本都要求您使用以下模板代碼初始化會話：

```scala
import org.apache.spark.sql.{ SparkSession }
val spark = SparkSession
  .builder()
  .master("local")
  .getOrCreate()
```

### 讀取資料集{#read-scala-dataset}

在Scala中，您可以匯入`clientContext`以取得並傳回平台值，如此就不需要定義變數，例如`var userToken`。 在以下的Scala範例中， `clientContext`用於取得並傳回讀取資料集所需的所有必要值。

>[!IMPORTANT]
>
> 在寫入資料之前使用`df.cache()`快取資料可以大大提高筆記型電腦的效能。 如果您收到下列任何錯誤，這將有所幫助：
> 
> - 作業因預備失敗而中止……只能壓縮每個分區中元素數量相同的RDD。
> - 遠程RPC客戶端斷開關聯和其他記憶體錯誤。
> - 讀取和寫入資料集時效能不佳。

> 
> 
如需詳細資訊，請參閱[疑難排解指南](../troubleshooting-guide.md) 。

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
  .option("mode", "interactive")
  .option("dataset-id", "5e68141134492718af974844")
  .load()

df1.printSchema()
df1.show(10)
```

| 元素 | 說明 |
| ------- | ----------- |
| df1 | 一個變數，代表用於讀取和寫入資料的Pancotis資料幀。 |
| user-token | 使用`clientContext.getUserToken()`自動擷取的使用者代號。 |
| service-token | 使用`clientContext.getServiceToken()`自動擷取的服務代號。 |
| ims-org | 使用`clientContext.getOrgId()`自動擷取的IMS組織ID。 |
| api-key | 使用`clientContext.getApiKey()`自動擷取的API金鑰。 |

>[!TIP]
>
>查看[筆記本資料限制](#notebook-data-limits)部分中的縮放表以確定`mode`應設定為`interactive`還是`batch`。

您可以使用下列方法在JupyterLab buy中自動產生上述範例：

在JupyterLab的左側導覽中選取「資料」圖示標籤（以下醒目提示）。 出現&#x200B;**[!UICONTROL Datates]**&#x200B;和&#x200B;**[!UICONTROL Schemas]**&#x200B;目錄。 選取&#x200B;**[!UICONTROL 資料集]**，按一下滑鼠右鍵，然後在您要使用之資料集的下拉式選單中選取&#x200B;**[!UICONTROL 在筆記型電腦中探索資料]**選項。 可執行的代碼條目出現在筆記本底部。
和
- 使用&#x200B;**[!UICONTROL 在筆記本中瀏覽資料]**&#x200B;生成讀單元。
- 使用&#x200B;**[!UICONTROL 在筆記本中寫入資料]**&#x200B;生成寫單元。

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### 寫入資料集{#scala-write-dataset}

在Scala中，您可以匯入`clientContext`以取得並傳回平台值，如此就不需要定義變數，例如`var userToken`。 在以下的Scala範例中， `clientContext`用於定義並傳回寫入資料集所需的所有必要值。

>[!IMPORTANT]
>
> 在寫入資料之前使用`df.cache()`快取資料可以大大提高筆記型電腦的效能。 如果您收到下列任何錯誤，這將有所幫助：
> 
> - 作業因預備失敗而中止……只能壓縮每個分區中元素數量相同的RDD。
> - 遠程RPC客戶端斷開關聯和其他記憶體錯誤。
> - 讀取和寫入資料集時效能不佳。

> 
> 
如需詳細資訊，請參閱[疑難排解指南](../troubleshooting-guide.md) 。

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
  .option("mode", "interactive")
  .option("dataset-id", "5e68141134492718af974844")
  .save()
```

| 元素 | 說明 |
| ------- | ----------- |
| df1 | 一個變數，代表用於讀取和寫入資料的Pancotis資料幀。 |
| user-token | 使用`clientContext.getUserToken()`自動擷取的使用者代號。 |
| service-token | 使用`clientContext.getServiceToken()`自動擷取的服務代號。 |
| ims-org | 使用`clientContext.getOrgId()`自動擷取的IMS組織ID。 |
| api-key | 使用`clientContext.getApiKey()`自動擷取的API金鑰。 |

>[!TIP]
>
>查看[筆記本資料限制](#notebook-data-limits)部分中的縮放表以確定`mode`應設定為`interactive`還是`batch`。

### 建立本地資料幀{#scala-create-dataframe}

要使用Scala建立本地資料幀，需要SQL查詢。 例如：

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### 篩選[!DNL ExperienceEvent]資料{#scala-experienceevent}

存取和篩選Scala筆記型電腦中的[!DNL ExperienceEvent]資料集時，您必須提供資料集身分(`{DATASET_ID}`)、貴組織的IMS身分，以及定義特定時間範圍的篩選規則。 篩選時間範圍是使用函式`spark.sql()`定義的，其中函式參數為SQL查詢字串。

下列儲存格會將[!DNL ExperienceEvent]資料集篩選為2019年1月1日至2019年12月31日期末之間僅存在的資料。

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

本檔案說明使用JupyterLab筆記型電腦存取資料集的一般准則。 如需查詢資料集的更深入範例，請造訪JupyterLab筆記本](./query-service.md)中的[查詢服務檔案。 有關如何探索和視覺化資料集的詳細資訊，請訪問[上的文檔，使用notebooks](./analyze-your-data.md)分析資料。

## [!DNL Query Service] {#optional-sql-flags-for-query-service}的可選SQL標誌

此表概述了可用於[!DNL Query Service]的可選SQL標誌。

| **標幟** | **說明** |
| --- | --- |
| `-h`, `--help` | 顯示說明訊息並退出。 |
| `-n`,  `--notify` | 切換通知查詢結果的選項。 |
| `-a`,  `--async` | 使用此標誌會非同步地執行查詢，並且可以在查詢執行時釋放內核。 將查詢結果指派給變數時請務必小心，因為如果查詢未完成，變數可能未定義。 |
| `-d`,  `--display` | 使用此標幟可防止顯示結果。 |
