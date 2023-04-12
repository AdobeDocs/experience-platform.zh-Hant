---
keywords: Experience Platform;JupyterLab；筆記型電腦；Data Science Workspace；熱門主題；%dataset；互動式模式；批次模式；Spark sdk;python sdk；存取資料；筆記型電腦資料存取
solution: Experience Platform
title: Jupyterlab筆記型電腦中的資料存取
description: 本指南著重於如何使用Data Science Workspace內建的Jupyter Notebooks來存取您的資料。
exl-id: 2035a627-5afc-4b72-9119-158b95a35d32
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '3292'
ht-degree: 8%

---

# 中的資料存取 [!DNL Jupyterlab] 筆記本

每個支援的內核都提供內建功能，允許您從筆記型電腦內的資料集讀取Platform資料。 目前，Adobe Experience Platform Data Science Workspace中的JupyterLab支援適用於 [!DNL Python]、R、PySpark和Scala。 不過，對分頁資料的支援僅限於 [!DNL Python] 和R筆記本。 本指南著重於如何使用JupyterLab筆記型電腦存取您的資料。

## 快速入門

閱讀本指南之前，請先檢閱 [[!DNL JupyterLab] 使用手冊](./overview.md) 的 [!DNL JupyterLab] 及其在Data Science Workspace中的角色。

## 筆記本資料限制 {#notebook-data-limits}

>[!IMPORTANT]
>
>對於PySpark和Scala筆記型電腦，如果您收到錯誤，原因是「遠程RPC客戶端不關聯」。 這通常表示驅動程式或執行器記憶體不足。 嘗試切換為 [&quot;batch&quot;模式](#mode) 來解決此錯誤。

下列資訊定義可讀取的資料量上限、使用的資料類型，以及讀取資料所花費的估計時間範圍。

針對 [!DNL Python] 和R，配置為40GB RAM的筆記型電腦伺服器用於基準測試。 對於PySpark和Scala，以下列基準使用了配置為64GB RAM、8個內核、2個DBU（最多4個工作人員）的資料庫群集。

使用的ExperienceEvent結構資料大小從一千(1K)列開始，長達十億(1B)列。 請注意，對於PySpark和 [!DNL Spark] 量度中，XDM資料的日期範圍為10天。

臨機結構資料是使用 [!DNL Query Service] 將表建立為選擇(CTAS)。 這些資料的大小也從1000(1K)列開始，範圍高達10億(1B)列。

### 何時使用批次模式與互動式模式 {#mode}

使用PySpark和Scala筆記型電腦讀取資料集時，您可以選擇使用互動式模式或批次模式來讀取資料集。 互動式可提供快速結果，批次模式則適用於大型資料集。

- 對於PySpark和Scala筆記本，當讀取500萬行或更多資料時，應使用批次模式。 如需每個模式的效率詳細資訊，請參閱 [PySpark](#pyspark-data-limits) 或 [斯卡拉](#scala-data-limits) 下面的資料限制表。

### [!DNL Python] 筆記型資料限制

**XDM ExperienceEvent結構：** 在22分鐘內，您最多應能讀取200萬行（磁碟上約6.1 GB的資料）的XDM資料。 新增其他列可能會導致錯誤。

| 列數 | 1K | 10K | 100K | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| 磁碟大小(MB) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK（秒） | 20.3 | 86.8 | 63 | 659 | 1315 |

**臨機結構：** 在14分鐘內，您最多應能讀取500萬列（磁碟上約5.6 GB的資料）的非XDM（臨機）資料。 新增其他列可能會導致錯誤。

| 列數 | 1K | 10K | 100K | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| 磁碟大小(MB) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK（秒） | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

### R筆記本資料限制

**XDM ExperienceEvent結構：** 13分鐘內，您最多應能讀取100萬列XDM資料（磁碟上3GB資料）。

| 列數 | 1K | 10K | 100K | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| 磁碟大小(MB) | 18.73 | 187.5 | 308 | 3000 |
| R內核（秒） | 14.03 | 69.6 | 86.8 | 775 |

**臨機結構：** 在大約10分鐘內，您最多應能讀取300萬列臨機資料（磁碟上293MB的資料）。

| 列數 | 1K | 10K | 100K | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| 磁碟大小(MB) | 0.082 | 0.612 | 9.0 | 91 | 188 | 293 |
| R SDK（秒） | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

### PySpark([!DNL Python] 內核)筆記本資料限制： {#pyspark-data-limits}

**XDM ExperienceEvent結構：** 在互動式模式下，您應能在約20分鐘內讀取最多500萬列的XDM資料（磁碟上約13.42GB的資料）。 互動式模式最多只支援500萬列。 如果您想要讀取較大的資料集，建議您切換至批次模式。 在批次模式下，您應能在約14小時內讀取最多5億行的XDM資料（磁碟上約1.31TB的資料）。

| 列數 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 磁碟大小 | 2.93MB | 4.38MB | 29.02 | 2.69 GB   | 5.39 GB   | 8.09 GB   | 13.42 GB   | 26.82 GB   | 134.24 GB   | 268.39 GB   | 1.31TB |
| SDK（互動式模式） | 33s | 32.4s | 55.1s | 253.5s | 489.2s | 729.6s | 1206.8s | - | - | - | - |
| SDK（批次模式） | 815.8s | 492.8s | 379.1s | 637.4s | 624.5s | 869.2s | 1104.1s | 1786s | 5387.2s | 10624.6s | 50547s |

**臨機結構：** 在互動式模式下，您最多應能在3分鐘內讀取500萬行（磁碟上約5.36GB的資料）的非XDM資料。 在批處理模式下，您應能在約18分鐘內讀取非XDM資料的10億行（磁碟上約1.05TB資料）。

| 列數 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| 磁碟大小 | 1.12MB | 11.24MB | 109.48MB | 2.69 GB   | 2.14 GB   | 3.21 GB   | 5.36 GB   | 10.71 GB   | 53.58 GB   | 107.52 GB   | 535.88 GB   | 1.05TB |
| SDK互動式模式（以秒為單位） | 28.2s | 18.6s | 20.8s | 20.9s | 23.8s | 21.7s | 24.7s | - | - | - | - | - |
| SDK批次模式（以秒為單位） | 428.8s | 578.8s | 641.4s | 538.5s | 630.9s | 467.3s | 411s | 675s | 702s | 719.2s | 1022.1s | 1122.3s |

### [!DNL Spark] （擴展內核）筆記本資料限制： {#scala-data-limits}

**XDM ExperienceEvent結構：** 在互動式模式下，您應能在約18分鐘內讀取最多500萬列的XDM資料（磁碟上約13.42GB的資料）。 互動式模式最多只支援500萬列。 如果您想要讀取較大的資料集，建議您切換至批次模式。 在批次模式下，您應能在約14小時內讀取最多5億行的XDM資料（磁碟上約1.31TB的資料）。

| 列數 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| 磁碟大小 | 2.93MB | 4.38MB | 29.02 | 2.69 GB   | 5.39 GB   | 8.09 GB   | 13.42 GB   | 26.82 GB   | 134.24 GB   | 268.39 GB   | 1.31TB |
| SDK互動式模式（以秒為單位） | 37.9s | 22.7s | 45.6s | 231.7s | 444.7s | 660.6s | 1100s | - | - | - | - |
| SDK批次模式（以秒為單位） | 374.4s | 398.5s | 527s | 487.9s | 588.9s | 829s | 939.1s | 1441s | 5473.2s | 10118.8 | 49207.6 |

**臨機結構：** 在互動式模式下，您最多應能在3分鐘內讀取500萬行（磁碟上約5.36GB的資料）的非XDM資料。 在批次模式下，您應能在約16分鐘內讀取非XDM資料的10億行（磁碟上約1.05TB資料）。

| 列數 | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| 磁碟大小 | 1.12MB | 11.24MB | 109.48MB | 2.69 GB   | 2.14 GB   | 3.21 GB   | 5.36 GB   | 10.71 GB   | 53.58 GB   | 107.52 GB   | 535.88 GB   | 1.05TB |
| SDK互動式模式（以秒為單位） | 35.7s | 31s | 19.5s | 25.3s | 23s | 33.2s | 25.5s | - | - | - | - | - |
| SDK批次模式（以秒為單位） | 448.8s | 459.7s | 519s | 475.8s | 599.9s | 347.6s | 407.8s | 397s | 518.8s | 487.9s | 760.2s | 975.4s |

## Python筆記本 {#python-notebook}

[!DNL Python] 筆記本允許您在訪問資料集時分頁資料。 以下示範使用和不使用分頁來讀取資料的范常式式碼。 有關可用的入門Python筆記本的詳細資訊，請訪問 [[!DNL JupyterLab] 啟動器](./overview.md#launcher) JupyterLab使用手冊中的一節。

下面的Python文檔概述了以下概念：

- [從資料集讀取](#python-read-dataset)
- [寫入資料集](#write-python)
- [查詢資料](#query-data-python)
- [篩選ExperienceEvent資料](#python-filter)

### 從Python資料集中讀取 {#python-read-dataset}

**不分頁：**

執行下列程式碼會讀取整個資料集。 如果執行成功，則資料會儲存為變數參考的Pancits資料框架 `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

**分頁：**

執行下列程式碼會讀取指定資料集的資料。 分頁是通過通過函式限制和偏移資料來實現的 `limit()` 和 `offset()` 分別為5個。 限制資料是指要讀取的最大資料點數，而偏移是指在讀取資料之前要跳過的資料點數。 如果讀取操作成功執行，則資料將保存為變數引用的Pancits資料幀 `df`.

```python
# Python

from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(get_platform_sdk_client_context(), dataset_id="{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

### 以Python寫入資料集 {#write-python}

若要寫入JupyterLab筆記型電腦中的資料集，請在JupyterLab的左側導覽中選取「資料」圖示標籤（以下醒目提示）。 此 **[!UICONTROL 資料集]** 和 **[!UICONTROL 結構]** 目錄。 選擇 **[!UICONTROL 資料集]** ，然後按一下右鍵，然後選取 **[!UICONTROL 在筆記本中寫入資料]** 選項（位於您要使用的資料集上的下拉式功能表）。 可執行的代碼條目出現在筆記本底部。

![](../images/jupyterlab/data-access/write-dataset.png)

- 使用 **[!UICONTROL 在筆記本中寫入資料]** 以使用您選取的資料集產生寫入儲存格。
- 使用 **[!UICONTROL 在筆記本中探索資料]** 以使用您選取的資料集產生讀取儲存格。
- 使用 **[!UICONTROL 筆記本中的查詢資料]** 以使用您選取的資料集產生基本查詢儲存格。

或者，您也可以複製並貼上下列程式碼儲存格。 將 `{DATASET_ID}` 和 `{PANDA_DATAFRAME}`.

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(get_platform_sdk_client_context()).get_by_id(dataset_id="{DATASET_ID}")
dataset_writer = DatasetWriter(get_platform_sdk_client_context(), dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### 查詢資料使用 [!DNL Query Service] in [!DNL Python] {#query-data-python}

[!DNL JupyterLab] on [!DNL Platform] 允許在 [!DNL Python] 筆記型電腦，通過 [Adobe Experience Platform查詢服務](https://www.adobe.com/go/query-service-home-en). 透過 [!DNL Query Service] 因為執行時間長，因此可用於處理大型資料集。 請注意，使用 [!DNL Query Service] 處理時間限制為10分鐘。

使用之前 [!DNL Query Service] in [!DNL JupyterLab]，確保您對 [[!DNL Query Service] SQL語法](https://www.adobe.com/go/query-service-sql-syntax-en).

使用查詢資料 [!DNL Query Service] 需要您提供target資料集的名稱。 您可以使用 **[!UICONTROL 資料總管]**. 以滑鼠右鍵按一下資料集清單，然後按一下 **[!UICONTROL 筆記本中的查詢資料]** 在筆記本中生成兩個代碼單元格。 以下將詳細說明這兩個儲存格。

![](../images/jupyterlab/data-access/python-query-dataset.png)

為了利用 [!DNL Query Service] in [!DNL JupyterLab]，您必須先在工作之間建立連線 [!DNL Python] 筆記本和 [!DNL Query Service]. 這可以通過執行第一生成單元來實現。

```python
qs_connect()
```

在第二個產生的儲存格中，必須在SQL查詢之前定義第一行。 依預設，產生的儲存格會定義選用變數(`df0`)，會將查詢結果儲存為Pancits資料框。 <br>此 `-c QS_CONNECTION` 參數是必需的，它告訴內核執行SQL查詢 [!DNL Query Service]. 請參閱 [附錄](#optional-sql-flags-for-query-service) 以取得其他引數的清單。

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

使用字串格式語法並以大括弧(`{}`)，如下列範例所示：

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

若要存取及篩選 [!DNL ExperienceEvent] 資料集 [!DNL Python] 筆記型電腦，您必須提供資料集的ID(`{DATASET_ID}`)，以及使用邏輯運算子定義特定時間範圍的篩選規則。 定義時間範圍時，會忽略任何指定的分頁，並考量整個資料集。

篩選運算子的清單如下所述：

- `eq()`: Equal to
- `gt()`: Greater than
- `ge()`: 大於或等於
- `lt()`: 少於
- `le()`: Less than or equal to
- `And()`:邏輯AND運算子
- `Or()`:邏輯OR運算子

下列儲存格會篩選 [!DNL ExperienceEvent] 2019年1月1日至2019年12月31日底期間完全存在的資料集。

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

R筆記本允許您在訪問資料集時分頁資料。 以下示範使用和不使用分頁來讀取資料的范常式式碼。 有關可用入門R筆記本的詳細資訊，請訪問 [[!DNL JupyterLab] 啟動器](./overview.md#launcher) JupyterLab使用手冊中的一節。

以下R檔案概述下列概念：

- [從資料集讀取](#r-read-dataset)
- [寫入資料集](#write-r)
- [篩選ExperienceEvent資料](#r-filter)

### 從R中的資料集讀取 {#r-read-dataset}

**不分頁：**

執行下列程式碼會讀取整個資料集。 如果執行成功，則資料會儲存為變數參考的Pancits資料框架 `df0`.

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

執行下列程式碼會讀取指定資料集的資料。 分頁是通過通過函式限制和偏移資料來實現的 `limit()` 和 `offset()` 分別為5個。 限制資料是指要讀取的最大資料點數，而偏移是指在讀取資料之前要跳過的資料點數。 如果讀取操作成功執行，則資料將保存為變數引用的Pancits資料幀 `df0`.

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

若要寫入JupyterLab筆記型電腦中的資料集，請在JupyterLab的左側導覽中選取「資料」圖示標籤（以下醒目提示）。 此 **[!UICONTROL 資料集]** 和 **[!UICONTROL 結構]** 目錄。 選擇 **[!UICONTROL 資料集]** ，然後按一下右鍵，然後選取 **[!UICONTROL 在筆記本中寫入資料]** 選項（位於您要使用的資料集上的下拉式功能表）。 可執行的代碼條目出現在筆記本底部。

![](../images/jupyterlab/data-access/r-write-dataset.png)

- 使用 **[!UICONTROL 在筆記本中寫入資料]** 以使用您選取的資料集產生寫入儲存格。
- 使用 **[!UICONTROL 在筆記本中探索資料]** 以使用您選取的資料集產生讀取儲存格。

或者，您也可以複製並貼上下列程式碼儲存格：

```R
psdk <- import("platform_sdk")
dataset <- psdk$models$Dataset(py$get_platform_sdk_client_context())$get_by_id(dataset_id="{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(py$get_platform_sdk_client_context(), dataset)
write_tracker <- dataset_writer$write(df, file_format='json')
```

### 篩選 [!DNL ExperienceEvent] 資料 {#r-filter}

若要存取及篩選 [!DNL ExperienceEvent] 資料集，您必須提供資料集的ID(`{DATASET_ID}`)，以及使用邏輯運算子定義特定時間範圍的篩選規則。 定義時間範圍時，會忽略任何指定的分頁，並考量整個資料集。

篩選運算子的清單如下所述：

- `eq()`: Equal to
- `gt()`: Greater than
- `ge()`: 大於或等於
- `lt()`: 少於
- `le()`: Less than or equal to
- `And()`:邏輯AND運算子
- `Or()`:邏輯OR運算子

下列儲存格會篩選 [!DNL ExperienceEvent] 2019年1月1日至2019年12月31日底期間完全存在的資料集。

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

## PySpark 3筆記型電腦 {#pyspark-notebook}

下面的PySpark文檔概述了以下概念：

- [初始化SparkSession](#spark-initialize)
- [讀和寫資料](#magic)
- [建立本地資料幀](#pyspark-create-dataframe)
- [篩選ExperienceEvent資料](#pyspark-filter-experienceevent)

### 初始化sparkSession {#spark-initialize}

全部 [!DNL Spark] 2.4筆記型電腦要求您使用下列模板代碼初始化會話。

```scala
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```

### 使用%資料集，使用PySpark 3筆記本進行讀寫 {#magic}

隨著 [!DNL Spark] 2.4, `%dataset` 自定義魔術用於PySpark 3([!DNL Spark] 2.4)筆記本。 有關IPython內核中可用的魔術命令的詳細資訊，請訪問 [IPython魔術文檔](https://ipython.readthedocs.io/en/stable/interactive/magics.html).


**使用狀況**

```scala
%dataset {action} --datasetId {id} --dataFrame {df} --mode batch
```

**說明**

自訂 [!DNL Data Science Workspace] 用於從 [!DNL PySpark] 筆記型電腦([!DNL Python] 3內核)。

| 名稱 | 說明 | 必填 |
| --- | --- | --- |
| `{action}` | 要在資料集上執行的動作類型。 「已讀」或「已寫」兩個動作。 | 是 |
| `--datasetId {id}` | 用來提供要讀取或寫入的資料集ID。 | 是 |
| `--dataFrame {df}` | 熊貓的資料框。 <ul><li> 當動作為「read」時，{df}為變數，資料集讀取操作的結果可供使用（例如資料幀）。 </li><li> 當動作為「write」時，此資料幀{df}會寫入資料集。 </li></ul> | 是 |
| `--mode` | 變更資料讀取方式的其他參數。 允許的參數為「批次」和「互動式」。 預設情況下，模式設定為「batch」。<br> 建議您使用「互動式」模式，提高較小資料集的查詢效能。 | 是 |

>[!TIP]
>
>查看 [筆記型資料限制](#notebook-data-limits) 區段，判斷 `mode` 應設為 `interactive` 或 `batch`.

**範例**

- **閱讀範例**: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0 --mode batch`
- **撰寫範例**: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0 --mode batch`

>[!IMPORTANT]
>
> 快取資料使用 `df.cache()` 在寫入資料之前，可以大大提高筆記型電腦的效能。 如果您收到下列任何錯誤，這將有所幫助：
> 
> - 作業因預備失敗而中止……只能壓縮每個分區中元素數量相同的RDD。
> - 遠程RPC客戶端斷開關聯和其他記憶體錯誤。
> - 讀取和寫入資料集時效能不佳。
> 
> 請參閱 [疑難排解指南](../troubleshooting-guide.md) 以取得更多資訊。

您可以使用下列方法在JupyterLab購買中自動產生上述範例：

在JupyterLab的左側導覽中選取「資料」圖示標籤（以下醒目提示）。 此 **[!UICONTROL 資料集]** 和 **[!UICONTROL 結構]** 目錄。 選擇 **[!UICONTROL 資料集]** ，然後按一下右鍵，然後選取 **[!UICONTROL 在筆記本中寫入資料]** 選項（位於您要使用的資料集上的下拉式功能表）。 可執行的代碼條目出現在筆記本底部。

- 使用 **[!UICONTROL 在筆記本中探索資料]** 來生成讀取單元格。
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
>您也可以指定選用的種子樣本，例如布林值withReplacement、雙分數或長種子。

### 篩選 [!DNL ExperienceEvent] 資料 {#pyspark-filter-experienceevent}

存取和篩選 [!DNL ExperienceEvent] PySpark筆記型電腦中的資料集需要您提供資料集身分(`{DATASET_ID}`)、貴組織的IMS身分，以及定義特定時間範圍的篩選規則。 篩選時間範圍是使用函式來定義 `spark.sql()`，其中函式參數為SQL查詢字串。

下列儲存格會篩選 [!DNL ExperienceEvent] 2019年1月1日至2019年12月31日底期間完全存在的資料集。

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

## Scala筆記本 {#scala-notebook}

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

### 讀取資料集 {#read-scala-dataset}

在Scala中，您可以匯入 `clientContext` 若要取得並傳回Platform值，便不需要定義變數，例如 `var userToken`. 在下面的Scala示例中， `clientContext` 可用來取得並傳回讀取資料集所需的所有值。

>[!IMPORTANT]
>
> 快取資料使用 `df.cache()` 在寫入資料之前，可以大大提高筆記型電腦的效能。 如果您收到下列任何錯誤，這將有所幫助：
> 
> - 作業因預備失敗而中止……只能壓縮每個分區中元素數量相同的RDD。
> - 遠程RPC客戶端斷開關聯和其他記憶體錯誤。
> - 讀取和寫入資料集時效能不佳。
> 
> 請參閱 [疑難排解指南](../troubleshooting-guide.md) 以取得更多資訊。

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
| df1 | 一個變數，代表用於讀取和寫入資料的Pancotis資料幀。 |
| user-token | 使用自動擷取的使用者代號 `clientContext.getUserToken()`. |
| service-token | 您的服務代號會使用 `clientContext.getServiceToken()`. |
| ims-org | 您的組織ID會使用 `clientContext.getOrgId()`. |
| api-key | 使用自動擷取的API金鑰 `clientContext.getApiKey()`. |

>[!TIP]
>
>查看 [筆記型資料限制](#notebook-data-limits) 區段，判斷 `mode` 應設為 `interactive` 或 `batch`.

您可以使用下列方法在JupyterLab buy中自動產生上述範例：

在JupyterLab的左側導覽中選取「資料」圖示標籤（以下醒目提示）。 此 **[!UICONTROL 資料集]** 和 **[!UICONTROL 結構]** 目錄。 選擇 **[!UICONTROL 資料集]** ，然後按一下右鍵，然後選取 **[!UICONTROL 在筆記本中探索資料]** 選項（位於您要使用的資料集上的下拉式功能表）。 可執行的代碼條目出現在筆記本底部。
和
- 使用 **[!UICONTROL 在筆記本中探索資料]** 來生成讀取單元格。
- 使用 **[!UICONTROL 在筆記本中寫入資料]** 生成寫單元格。

![](../images/jupyterlab/data-access/scala-write-dataset.png)

### 寫入資料集 {#scala-write-dataset}

在Scala中，您可以匯入 `clientContext` 若要取得並傳回Platform值，便不需要定義變數，例如 `var userToken`. 在下面的Scala示例中， `clientContext` 可用來定義並傳回寫入資料集所需的所有必要值。

>[!IMPORTANT]
>
> 快取資料使用 `df.cache()` 在寫入資料之前，可以大大提高筆記型電腦的效能。 如果您收到下列任何錯誤，這將有所幫助：
> 
> - 作業因預備失敗而中止……只能壓縮每個分區中元素數量相同的RDD。
> - 遠程RPC客戶端斷開關聯和其他記憶體錯誤。
> - 讀取和寫入資料集時效能不佳。
> 
> 請參閱 [疑難排解指南](../troubleshooting-guide.md) 以取得更多資訊。

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
| df1 | 一個變數，代表用於讀取和寫入資料的Pancotis資料幀。 |
| user-token | 使用自動擷取的使用者代號 `clientContext.getUserToken()`. |
| service-token | 您的服務代號會使用 `clientContext.getServiceToken()`. |
| ims-org | 您的組織ID會使用 `clientContext.getOrgId()`. |
| api-key | 使用自動擷取的API金鑰 `clientContext.getApiKey()`. |

>[!TIP]
>
>查看 [筆記型資料限制](#notebook-data-limits) 區段，判斷 `mode` 應設為 `interactive` 或 `batch`.

### 建立本地資料幀 {#scala-create-dataframe}

要使用Scala建立本地資料幀，需要SQL查詢。 例如：

```scala
sparkdf.createOrReplaceTempView("sparkdf")

val localdf = spark.sql("SELECT * FROM sparkdf LIMIT 1)
```

### 篩選 [!DNL ExperienceEvent] 資料 {#scala-experienceevent}

存取和篩選 [!DNL ExperienceEvent] Scala筆記本中的資料集要求您提供資料集標識(`{DATASET_ID}`)、貴組織的IMS身分，以及定義特定時間範圍的篩選規則。 篩選時間範圍是使用函式來定義 `spark.sql()`，其中函式參數為SQL查詢字串。

下列儲存格會篩選 [!DNL ExperienceEvent] 2019年1月1日至2019年12月31日底期間完全存在的資料集。

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

本檔案說明使用JupyterLab筆記型電腦存取資料集的一般准則。 如需查詢資料集的更深入範例，請造訪 [JupyterLab筆記型電腦中的查詢服務](./query-service.md) 檔案。 如需如何探索和視覺化資料集的詳細資訊，請造訪 [使用筆記本分析資料](./analyze-your-data.md).

## 的可選SQL標誌 [!DNL Query Service] {#optional-sql-flags-for-query-service}

此表概述了可用於的可選SQL標誌 [!DNL Query Service].

| **標幟** | **說明** |
| --- | --- |
| `-h`、`--help` | 顯示說明訊息並退出。 |
| `-n`、`--notify` | 切換通知查詢結果的選項。 |
| `-a`、`--async` | 使用此標誌會非同步地執行查詢，並且可以在查詢執行時釋放內核。 將查詢結果指派給變數時請務必小心，因為如果查詢未完成，變數可能未定義。 |
| `-d`、`--display` | 使用此標幟可防止顯示結果。 |
