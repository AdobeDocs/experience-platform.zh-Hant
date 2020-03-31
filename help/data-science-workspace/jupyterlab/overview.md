---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics
solution: Experience Platform
title: JupyterLab使用指南
topic: Overview
translation-type: tm+mt
source-git-commit: 700c927680d9b9ba4dabc2d2e068e4da3c801cce

---


# JupyterLab使用指南

JupyterLab是專案Jupyter的網路使用者介面， <a href="https://jupyter.org/" target="_blank"></a> 並與Adobe Experience Platform緊密整合。 它為資料科學家提供互動式開發環境，以便與Jupyter筆記型電腦、程式碼和資料搭配使用。

本文檔概述了JupyterLab及其功能，以及執行常見操作的說明。

## JupyterLab在Experience Platform上的應用

Experience Platform的JupyterLab整合隨附架構變更、設計考量、自訂的筆記型電腦擴充功能、預先安裝的程式庫和Adobe主題介面。

下列清單概述JupyterLab在Platform上獨有的一些功能：

| 功能 | 說明 |
| --- | --- |
| **內核** | 內核提供筆記型電腦和其他JupyterLab前端，以不同的寫程式語言執行和查看代碼。 Experience Platform提供額外的核心，以支援在Python、R、PySpark和Spark中進行開發。 有關詳細 [資訊](#kernels) ，請參閱內核部分。 |
| **資料存取** | 直接從JupyterLab存取現有資料集，並具備完整的讀取和寫入功能支援。 |
| **平台服務整合** | 內建整合可讓您直接從JupyterLab運用其他平台服務。 「與其他平台服務整合」一節提供支援整合的 [完整清單](#service-integration)。 |
| **驗證** | 除了 <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">JupyterLab的內建安全性模型外</a>，您的應用程式與Experience Platform（包括平台服務對服務通訊）之間的每次互動都會透過 <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">Adobe Identity Management System(IMS)進行加密和驗證</a>。 |
| **開發程式庫** | 在Experience Platform中，JupyterLab提供Python、R和PySpark的預先安裝程式庫。 如需支援 [的程式庫](#supported-libraries) ，請參閱附錄。 |
| **程式庫控制器** | 當預先安裝的程式庫不符合您的需求時，可為Python和R安裝其他程式庫，並暫時儲存在隔離的容器中，以維護平台的完整性並確保資料的安全。 有關詳細 [資訊](#kernels) ，請參閱內核部分。 |

>[!NOTE] 其他程式庫僅適用於安裝程式庫的作業階段。 啟動新會話時，必須重新安裝所需的任何其他庫。

## 與其他平台服務整合 {#service-integration}

標準化和互操作性是Experience Platform的主要概念。 JupyterLab與Platform的整合為內嵌的IDE，可讓它與其他平台服務互動，讓您充份運用平台。 JupyterLab提供下列平台服務：

* **目錄服務：** 使用讀寫功能存取和探索資料集。
* **查詢服務：** 使用SQL訪問和探索資料集，在處理大量資料時提供較低的資料存取開銷。
* **Sensei ML框架：** 模型開發具備訓練和評分資料的能力，而且只要按一下，就能建立配方。

>[!NOTE] JupyterLab上的某些平台服務整合僅限於特定內核。 有關詳細資訊，請參 [閱](#kernels) 「內核」部分。

## 主要功能與常用作業

有關JupyterLab主要功能和執行常見操作說明的資訊，請參見以下各節：

* [存取JupyterLab](#access-jupyterlab)
* [JupyterLab介面](#jupyterlab-interface)
* [程式碼儲存格](#code-cells)
* [內核](#kernels)
* [內核會話](#kernel-sessions)
* [PySpark/Spark執行資源](#pysparkspark-execution-resource)
* [啟動程式](#launcher)

### 存取JupyterLab

在 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a>，按一下左側導覽欄中的 **Models** ，然後按一下頂端導覽中的 **Notebooks** ，以存取JupyterLab。 請給JupyterLab留出一些時間以完全初始化。

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### JupyterLab介面

JupyterLab介麵包含功能表列、可折疊的左側邊欄，以及包含檔案和活動標籤的主要工作區。

**選單列**

介面頂部的菜單欄具有頂級菜單，這些菜單使用鍵盤快捷鍵顯示JupyterLab中可用的操作：

* **檔案：** 與檔案和目錄相關的操作
* **編輯：** 與編輯檔案和其他活動相關的動作
* **檢視：** 改變JupyterLab外觀的動作
* **執行：** 在不同活動（如筆記型電腦和代碼控制台）中運行代碼的操作
* **內核：** 用於管理內核的操作
* **標籤：** 開啟的檔案與活動清單
* **設定：** 常用設定和進階設定編輯器
* **說明：** JupyterLab和內核幫助連結清單

**左側欄**

左側邊欄包含可點選的標籤，可存取下列功能：

* **檔案瀏覽器：** 已保存的筆記本文檔和目錄清單
* **資料總管：** 瀏覽、存取和探索資料集和結構
* **運行內核和終端：** 具有終止能力的活動內核和終端會話清單
* **命令：** 有用命令的清單
* **儲存格偵測器：** 一種單元格編輯器，它提供對工具和元資料的訪問，這些工具和元資料對於設定用於演示的筆記本有用
* **頁籤：** 開啟的標籤清單

按一下標籤以顯示其功能，或按一下展開的標籤以收合左側邊欄，如下所示：

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**主要工作區**

JupyterLab的主要工作區域可讓您將檔案和其他活動排列成標籤面板，這些標籤可以調整大小或細分。 將標籤拖曳至標籤面板的中央，以移轉標籤。 將標籤拖曳至面板的左、右、上或下方，以劃分面板：

![](../images/jupyterlab/user-guide/main_work_area.gif)

### 程式碼儲存格

代碼單元格是筆記型電腦的主要內容。 它們包含的原始碼為筆記型電腦相關內核的語言，以及執行代碼單元格後的輸出。 每個代碼單元格的右側顯示一個執行計數，該代碼單元格表示其執行順序。

![](../images/jupyterlab/user-guide/code_cell.png)

常見的儲存格動作說明如下：

* **新增儲存格：** 按一下筆記本菜單中的加&#x200B;**號(+**)可添加空單元格。 新儲存格會置於目前正在互動的儲存格下方，或在筆記型電腦的結尾處（如果沒有特定儲存格在焦點中）。

* **移動儲存格：** 將游標置於您要移動的儲存格右側，然後按一下並拖曳儲存格至新位置。 此外，將一個單元格從一個筆記本移動到另一個筆記本會複製該單元格及其內容。

* **執行儲存格：** 按一下要執行的單元格的主體，然後按一下筆記本菜 **單中的****** play表徵圖()。 當內核處理執行時，單元格的執行計數器中會顯示星號(**\***)，並在完成時被整數替換。

* **刪除儲存格：** 按一下要刪除的單元格的主體，然後按一下剪 **式** 表徵圖。

### 內核 {#kernels}

<!-- will need to edit this sparkmagic %% for data bricks not supported -->

筆記型電腦內核是用於處理筆記型電腦單元的語言專用計算引擎。 除了Python外，JupyterLab還提供R、PySpark和Spark的其他語言支援。 開啟筆記本文檔時，將啟動關聯內核。 當執行筆記本單元時，內核執行計算並產生可能消耗大量CPU和記憶體資源的結果。 請注意，在內核關閉之前，不會釋放已分配的記憶體。

>[!NOTE] Spark和Spark功能由 <a href="https://github.com/jupyter-incubator/sparkmagic" target="_blank">Sparkmagic支援</a>。

某些特性和功能限於下表所述的特定內核：

| 內核 | 資料庫安裝支援 | 平台整合 |
| :----: | :--------------------------: | :-------------------- |
| **Python** | 是 | <ul><li>Sensei ML框架</li><li>目錄服務</li><li>查詢服務</li></ul> |
| **R** | 是 | <ul><li>Sensei ML框架</li><li>目錄服務</li></ul> |
| **PySpark** | 無 | <ul><li>Sensei ML框架</li><li>目錄服務</li></ul> |
| **Spark** | 無 | <ul><li>Sensei ML框架</li><li>目錄服務</li></ul> |

### 內核會話

JupyterLab上的每個活動筆記本或活動都使用內核會話。 從左側邊欄展開「運行終端和內核」 **頁籤，可找到所有活動會話** 。 通過觀察筆記本介面的右上角，可以確定筆記本內核的類型和狀態。 在下圖中，筆記本的關聯內核是 **Python 3** ，其當前狀態由右側的灰色圓表示。 空心圓表示空閒內核，實心圓表示忙碌內核。

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

如果內核長時間處於關閉或非活動狀態，則無 **內核！** 顯示實心圓。 通過按一下內核狀態並選擇相應的內核類型激活內核，如下所示：

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### PySpark/Spark執行資源 {#execution-resource}

<!-- need to update with databricks -->

PySpark和Spark內核可讓您在PySpark或Spark筆記型電腦中使用configure命令(`%%configure`)配置Spark叢集資源，並提供組態清單。 理想情況下，這些組態是在Spark應用程式初始化之前定義的。 在Spark應用程式啟動時修改組態，需要在命令(`%%configure -f`)之後加上強制標幟，以重新啟動應用程式，以便套用變更，如下所示：

```python
%%configure -f 
{
    "numExecutors": 10,
    "executorMemory": "8G",
    "executorCores":4,
    "driverMemory":"2G",
    "driverCores":2,
    "conf": {
        "spark.cores.max": "40"
    }
}
```

>[!TIP] 使用help命令(`%%help`)查看所有可用命令。

下表列出了所有可配置屬性：

| 屬性 | 說明 | 類型 |
| :------- | :---------- | :-----:|
| fold | 會話類型（必需） | `session kind`_ |
| proxyUser | 要模擬執行此作業的使用者（例如bob） | 字串 |
| 罐子 | 要放置在java上的檔案 `classpath` | 路徑清單 |
| pyFiles | 要放置在 `PYTHONPATH` | 路徑清單 |
| 檔案 | 要放置在執行器工作目錄中的檔案 | 路徑清單 |
| driverMemory | 驅動程式的記憶體（以兆位元組或千兆位元組為單位）（例如1000M、2G） | 字串 |
| driverCores | 驅動程式使用的芯數（僅限HAIRN模式） | int |
| executorMemory | 執行器的記憶體（以兆位元組或千兆位元組為單位）（例如1000M、2G） | 字串 |
| executorCores | 執行器使用的核數 | int |
| numExecutors | 執行者數（僅限HAIR模式） | int |
| 檔案 | 要在執行器工作目錄中解壓縮的存檔（僅限HAIRN模式） | 路徑清單 |
| 隊列 | 要提交的HAIR隊列（僅限HAIRN模式） | 字串 |
| 名稱 | 應用程式的名稱 | 字串 |
| 會議 | Spark設定屬性 | key=val的映射 |

### 啟動程式

<!-- Databricks update -->

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

自定義的 *Launcher* （啟動器）為您提供了實用的筆記本模板，用於支援的內核，可幫助您啟動任務，包括：

| 範本 | 說明 |
| --- | --- |
| 空白 | 空的筆記本檔案。 |
| 入門者 | 預填充的筆記型電腦演示使用樣本資料進行資料探索。 |
| 零售銷售 | 預先填入的筆記型電腦，使用 <a href="https://adobe.ly/2wOgO3L" target="_blank">範例資料</a> ，提供零售銷售方式。 |
| 方式產生器 | 用於在JupyterLab中建立配方的筆記本模板。 它預先填入程式碼和評註，以示範並說明方式建立程式。 請參閱筆記 <a href="https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en" target="_blank">本至配方教學課程</a> ，以取得詳細的逐步說明。 |
| 查詢服務 | 預填充的筆記本直接在JupyterLab中演示查詢服務的使用，並提供了可大規模分析資料的示例工作流。 |
| XDM事件 | 預先填入的筆記型電腦，展示後值Experience Event資料的資料探索，著重於資料結構中常見的功能。 |
| XDM查詢 | 預先填入的筆記型電腦，展示Experience Event資料的範例商業查詢。 |
| 聚總 | 預先填充的筆記本演示了將大量資料匯總到較小、可管理的塊中的示例工作流。 |
| 叢集 | 預填充的筆記型電腦，演示使用群集算法的端到端機器學習建模過程。 |

某些筆記型電腦模板僅限於某些內核。 每個內核的模板可用性在下表中映射：

<table>
    <tr>
        <td></td>
        <th><strong>空白</strong></th>
        <th><strong>入門者</strong></th>
        <th><strong>零售銷售</strong></th>
        <th><strong>方式產生器</strong></th>
        <th><strong>查詢服務</strong></th>
        <th><strong>XDM事件</strong></th>
        <th><strong>XDM查詢</strong></th>
        <th><strong>聚總</strong></th>
        <th><strong>叢集</strong></th>
    </tr>
    <tr>
        <th><strong>Python</strong></th>
        <td >是</td>
        <td >是</td>
        <td >是</td>
        <td >是</td>
        <td >是</td>
        <td >是</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
    </tr>
    <tr>
        <th ><strong>R</strong></th>
        <td >是</td>
        <td >是</td>
        <td >是</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
    </tr>
    <tr>
        <th  ><strong>PySpark</strong></th>
        <td >是</td>
        <td >是</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >是</td>
        <td >是</td>
        <td >no</td>
    </tr>
    <tr>
        <th ><strong>Spark</strong></th>
        <td >是</td>
        <td >是</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >是</td>
    </tr>
</table>

若要開啟新的啟動 *器*，請按一 **下「檔案>新增啟動器」**。 或者，從左側邊 **欄展開** 「檔案」瀏覽器，然後按一下加號(**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## 使用筆記本訪問平台資料

每個支援的內核都提供內置功能，允許您從筆記本內的資料集中讀取平台資料。 但是，對分頁資料的支援僅限於Python和R筆記型電腦。

### 從Python/R的資料集讀取

Python和R筆記型電腦允許您在訪問資料集時分頁資料。 下面顯示有分頁和無分頁讀取資料的范常式式碼。

[//]: # (In the following samples, the first step is currently required but once the SDK is complete, users are no longer required to explicitly define client_context)

#### 從Python/R中的資料集讀取，無需編頁

執行下列程式碼會讀取整個資料集。 如果執行成功，則資料將保存為變數引用的Apcotis資料幀 `df`。

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

* `{DATASET_ID}`:要訪問的資料集的唯一標識

#### 從Python/R的資料集讀取並分頁

執行下列程式碼會讀取指定資料集的資料。 分頁是通過分別通過函式和函式限制和偏移資料 `limit()` 來實現 `offset()` 的。 限制資料是指要讀取的資料點數上限，而偏移指在讀取資料之前要跳過的資料點數。 如果讀取操作成功執行，則資料將被保存為變數引用的Apcotis資料幀 `df`。

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$limit(100L)$offset(10L)$read() 
```

* `{DATASET_ID}`:要訪問的資料集的唯一標識

### 從PySpark/Spark中的資料集讀取

在開啟作用中的PySpark或Spark筆記型電腦時，從左側邊欄展開「資料總管 **」標籤，然後按兩下「資料集****** 」以檢視可用資料集清單。 按一下右鍵要訪問的資料集清單，然後按一下「 **Explore Data in Notebook**（在筆記本中瀏覽資料）」。 產生下列程式碼儲存格：

```python
# PySpark

pd0 = spark.read.format("com.adobe.platform.dataset").\
    option('orgId', "YOUR_IMS_ORG_ID@AdobeOrg").\
    load("{DATASET_ID}")
pd0.describe()
pd0.show(10, False)
```

```scala
// Spark

import com.adobe.platform.dataset.DataSetOptions
val dataFrame = spark.read.
    format("com.adobe.platform.dataset").
    option(DataSetOptions.orgId, "YOUR_IMS_ORG_ID@AdobeOrg").
    load("{DATASET_ID}")
dataFrame.printSchema()
dataFrame.show()
```

### Python中使用查詢服務的查詢資料

JupyterLab on Platform可讓您在Python筆記型電腦中使用SQL，以透過 <a href="https://www.adobe.com/go/query-service-home-en" target="_blank">Adobe Experience Platform查詢服務存取資料</a>。 通過查詢服務訪問資料由於其優異的運行時間而對處理大型資料集非常有用。 請注意，使用查詢服務查詢資料的處理時間限制為10分鐘。

在JupyterLab中使用查詢服務之前，請確保您對查詢服務SQL語 <a href="https://www.adobe.com/go/query-service-sql-syntax-en" target="_blank">法有正確的理解</a>。

使用查詢服務查詢資料需要提供目標資料集的名稱。 您可以使用「資料總管」來尋找所需的資料集，以產生必要的 **程式碼儲存格**。 按一下右鍵資料集清單，然後按一下「 **Notebook（筆記本）」中的** 「Query Data（查詢資料）」 ，在筆記本中生成以下兩個代碼單元格：


為了在JupyterLab中利用查詢服務，您必須首先在工作的Python筆記本和查詢服務之間建立連接。 這可以通過執行第一生成單元來實現。

```python
qs_connect()
```

在第二個生成的單元格中，第一行必須在SQL查詢之前定義。 預設情況下，生成的單元格定義一個可選變數(`df0`)，該變數將查詢結果保存為Pactices資料幀。 <br>該 `-c QS_CONNECTION` 參數是強制的，並指示內核對查詢服務執行SQL查詢。 有關其 [他引數的清單](#optional-sql-flags-for-query-service) ，請參見附錄。

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

### 在Python/R中篩選ExperienceEvent資料

若要存取和篩選Python或R筆記型電腦中的ExperienceEvent資料集，您必須提供資料集的ID(`{DATASET_ID}`)，以及使用邏輯運算子定義特定時間範圍的篩選規則。 定義時間範圍時，會忽略任何指定的分頁，並考慮整個資料集。

篩選運算子的清單說明如下：

* `eq()`:等於
* `gt()`:大於
* `ge()`:大於或等於
* `lt()`:小於
* `le()`:小於或等於
* `And()`:邏輯AND運算子
* `Or()`:邏輯OR運算子

以下儲存格會將ExperienceEvent資料集篩選為2019年1月1日至2019年12月31日止期間僅存在的資料。

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

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

### 在PySpark/Spark中篩選ExperienceEvent資料

在PySpark或Spark筆記型電腦中存取和篩選ExperienceEvent資料集時，您必須提供資料集識別(`{DATASET_ID}`)、組織的IMS識別，以及定義特定時間範圍的篩選規則。 篩選時間範圍是使用函式來定義的， `spark.sql()`其中函式參數是SQL查詢字串。

以下儲存格會將ExperienceEvent資料集篩選為2019年1月1日至2019年12月31日止期間僅存在的資料。

```python
# PySpark

pd = spark.read.format("com.adobe.platform.dataset").\
    option("orgId", "YOUR_IMS_ORG_ID@AdobeOrg").\
    load("{DATASET_ID}")

pd.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
```

```scala
// Spark

import com.adobe.platform.dataset.DataSetOptions
val dataFrame = spark.read.
    format("com.adobe.platform.dataset").
    option(DataSetOptions.orgId, "YOUR_IMS_ORG_ID@AdobeOrg").
    load("{DATASET_ID}")

dataFrame.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
```


## 支援的程式庫 {#supported-libraries}

### Python / R

| 資料庫 | 版本 |
| :------ | :------ |
| 筆記本 | 6.0.0 |
| 請求 | 2.22.0 |
| 隱晦 | 4.0.0 |
| 青葉 | 0.10.0 |
| ipywidget | 7.5.1 |
| bokeh | 1.3.1 |
| gensim | 3.7.3 |
| ipyparallel | 0.5.2 |
| jq | 1.6 |
| keras | 2.2.4 |
| nltk | 3.2.5 |
| 熊貓 | 0.22.0 |
| 潘達斯 | 0.7.3 |
| 枕 | 6.0.0 |
| scikit-image | 0.15.0 |
| scikit-learn | 0.21.3 |
| 接骨 | 1.3.0 |
| 發癢 | 1.3.0 |
| 西伯恩 | 0.9.0 |
| statmodels | 0.10.1 |
| 彈性 | 5.1.0.17 |
| gplot | 0.11.5 |
| py-xgboost | 0.90 |
| opencv | 3.4.1 |
| 皮什帕克 | 2.4.3 |
| 火炬 | 1.0.1 |
| wxpython | 4.0.6 |
| colorlover | 0.3.0 |
| geopandas | 0.5.1 |
| 地源 | 2.1.0 |
| 風格 | 1.6.4 |
| rpy2 | 2.9.4 |
| r-essentials | 3.6 |
| r-arules | 1.6_3 |
| r-fpc | 2.2_3 |
| r-e1071 | 1.7_2 |
| r-gam | 1.16.1 |
| r-gbm | 2.1.5 |
| r-ggthemes | 4.2.0 |
| r-ggvis | 0.4.4 |
| r-igraph | 1.2.4.1 |
| r-lapes | 3.0 |
| r-操縱 | 1.0.1 |
| r-rocr | 1.0_7 |
| r-rmysql | 0.10.17 |
| r-rodbc | 1.3_15 |
| r-rsqlite | 2.1.2 |
| r-rstan | 2.19.2 |
| r-sqldf | 0.4_11 |
| r-存活 | 2.44_1.1 |
| r-zoo | 1.8_6 |
| r弦長 | 0.9.5.2 |
| r-quadprog | 1.5_7 |
| r-rjson | 0.2.20 |
| r-forecast | 8.7 |
| r-rsolnp | 1.16 |
| r-網狀 | 1.12 |
| r-mlr | 2.14.0 |
| r-viridis | 0.5.1 |
| r-corplot | 0.84 |
| r-fnn | 1.1.3 |
| r-lubridate | 1.7.4 |
| r-隨機森林 | 4.6_14 |
| 逆向 | 1.2.1 |
| r樹 | 1.0_39 |
| 皮蒙戈 | 3.8.0 |
| pyarrow | 0.14.1 |
| boto3 | 1.9.199 |
| ipyvolume | 0.5.2 |
| fast鑲木地板 | 0.3.2 |
| python-snappy | 0.5.4 |
| ipywebrtc | 0.5.0 |
| jupyter_client | 5.3.1 |
| wordcloud | 1.5.0 |
| graphviz | 2.40.1 |
| python-graphviz | 0.11.1 |
| azure儲存 | 0.36.0 |
| jupterlab | 1.0.4 |
| 熊貓-ml | 0.6.1 |
| tensorflow-gpu | 1.14.0 |
| nodejs | 12.3.0 |
| 模擬 | 3.0.5 |
| ipympl | 0.3.3 |
| fonts-anacond | 1.0 |
| psycopg2 | 2.8.3 |
| 鼻子 | 1.3.7 |
| autovizwidget | 0.12.9 |
| 阿爾塔 | 3.1.0 |
| vega_datasets | 0.7.0 |
| 平磨機 | 1.0.1 |
| sql_magic | 0.0.4 |
| iso3166 | 1.0 |
| nbimporter | 0.3.1 |

### PySpark

| 資料庫 | 版本 |
| :------ | :------ |
| 請求 | 2.18.4 |
| gensim | 2.3.0 |
| keras | 2.0.6 |
| nltk | 3.2.4 |
| 熊貓 | 0.20.1 |
| 潘達斯 | 0.7.3 |
| 枕 | 5.3.0 |
| scikit-image | 0.13.0 |
| scikit-learn | 0.19.0 |
| 接骨 | 0.19.1 |
| 發癢 | 1.3.3 |
| statmodels | 0.8.0 |
| 彈性 | 4.0.30.44 |
| py-xgboost | 0.60 |
| opencv | 3.1.0 |
| pyarrow | 0.8.0 |
| boto3 | 1.5.18 |
| azure-storage-blob | 1.4.0 |
| python | 3.6.7 |
| mkl-rt | 11.1 |

## 查詢服務的可選SQL標誌

此表概述了可用於查詢服務的可選SQL標誌。

| **旗標** | **說明** |
| --- | --- |
| `-h`, `--help` | 顯示幫助消息並退出。 |
| `-n`, `--notify` | 切換選項以通知查詢結果。 |
| `-a`, `--async` | 使用此標誌可非同步執行查詢，並可在查詢執行時釋放內核。 在將查詢結果指派給變數時請務必小心，因為如果查詢未完成，變數可能未定義。 |
| `-d`, `--display` | 使用此標幟可防止顯示結果。 |

