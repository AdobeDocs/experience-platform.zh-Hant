---
keywords: Experience Platform；開發人員指南；SDK;Data Access SDK;Data Science Workspace；熱門主題
solution: Experience Platform
title: 使用Adobe Experience Platform平台SDK進行模型製作
topic-legacy: SDK authoring
description: 本教學課程提供有關在Python和R中將data_access_sdk_python轉換為新Python平台_sdk的資訊。
exl-id: 20909cae-5cd2-422b-8dbb-35bc63e69b2a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 5%

---

# 使用Adobe Experience Platform[!DNL Platform] SDK進行模型製作

本教程提供有關在Python和R中將`data_access_sdk_python`轉換為新Python `platform_sdk`的資訊。本教學課程提供下列操作的相關資訊：

- [建立驗證](#build-authentication)
- [資料的基本讀取](#basic-reading-of-data)
- [基本資料寫入](#basic-writing-of-data)

## 構建驗證{#build-authentication}

必須進行驗證才能呼叫[!DNL Adobe Experience Platform]，且由API金鑰、IMS組織ID、使用者Token和服務Token組成。

### Python

如果您使用Jupyter Notebook，請使用以下代碼來構建`client_context`:

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

如果您不使用Jupyter Notebook，或需要變更IMS組織，請使用下列程式碼範例：

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={IMS_ORG},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

如果您使用Jupyter Notebook，請使用以下代碼來構建`client_context`:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

如果您不使用Jupyter Notebook，或需要變更IMS組織，請使用下列程式碼範例：

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
client_context <- psdk$client_context$ClientContext(api_key={API_KEY},
              org_id={IMS_ORG},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

## 資料{#basic-reading-of-data}的基本讀取

使用新的[!DNL Platform] SDK，最大讀取大小為32 GB，最長讀取時間為10分鐘。

如果您的讀取時間過長，可以嘗試使用下列其中一個篩選選項：

- [依偏移和限制篩選資料](#filter-by-offset-and-limit)
- [依日期篩選資料](#filter-by-date)
- [依欄篩選資料](#filter-by-selected-columns)
- [取得排序結果](#get-sorted-results)

>[!NOTE]
>
>IMS組織設定在`client_context`中。

### Python

若要讀取Python中的資料，請使用下列程式碼範例：

```python
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).read()
df.head()
```

### R

若要讀取R中的資料，請使用下列程式碼範例：

```r
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

## 依偏移和限制篩選{#filter-by-offset-and-limit}

由於不再支援依批次ID篩選，因此您必須使用`offset`和`limit`才能進行資料範圍讀取。

### Python

```python
df = dataset_reader.limit(100).offset(1).read()
df.head
```

### R

```r
df <- dataset_reader$limit(100L)$offset(1L)$read() 
df
```

## 依日期篩選{#filter-by-date}

日期篩選的詳細程度現在由時間戳記定義，而非依日期設定。

### Python

```python
df = dataset_reader.where(\
    dataset_reader['timestamp'].gt('2019-04-10 15:00:00').\
    And(dataset_reader['timestamp'].lt('2019-04-10 17:00:00'))\
).read()
df.head()
```

### R

```r
df2 <- dataset_reader$where(
    dataset_reader['timestamp']$gt('2018-12-10 15:00:00')$
    And(dataset_reader['timestamp']$lt('2019-04-10 17:00:00'))
)$read()
df2
```

新的[!DNL Platform] SDK支援下列作業：

| 操作 | 函數 |
| --------- | -------- |
| 等於 (`=`) | `eq()` |
| Greater than (`>`) | `gt()` |
| Greater than or equal to (`>=`) | `ge()` |
| Less than (`<`) | `lt()` |
| Less than or equal to (`<=`) | `le()` |
| 和(`&`) | `And()` |
| 或 (`|`) | `Or()` |

## 依選取的欄{#filter-by-selected-columns}篩選

若要進一步細化資料讀取，您也可以依欄名稱篩選。

### Python

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### R

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## 取得排序結果{#get-sorted-results}

接收的結果可以分別按目標資料集的指定列及其順序(asc/desc)排序。

在以下示例中，資料幀首先按&quot;column-a&quot;的升序排序。 對&quot;column-a&quot;具有相同值的行按&quot;column-b&quot;以降序排序。

### Python

```python
df = dataset_reader.sort([('column-a', 'asc'), ('column-b', 'desc')])
```

### R

```r
df <- dataset_reader$sort(c(('column-a', 'asc'), ('column-b', 'desc')))$read()
```

## 資料{#basic-writing-of-data}的基本寫入

>[!NOTE]
>
>IMS組織設定在`client_context`中。

要在Python和R中寫入資料，請使用以下示例之一：

### Python

```python
from platform_sdk.models import Dataset
from platform_sdk.dataset_writer import DatasetWriter

dataset = Dataset(client_context).get_by_id("{DATASET_ID}")
dataset_writer = DatasetWriter(client_context, dataset)
write_tracker = dataset_writer.write({PANDA_DATAFRAME}, file_format='json')
```

### R

```r
dataset <- psdk$models$Dataset(client_context)$get_by_id("{DATASET_ID}")
dataset_writer <- psdk$dataset_writer$DatasetWriter(client_context, dataset)
write_tracker <- dataset_writer$write({PANDA_DATAFRAME}, file_format='json')
```

## 後續步驟

配置`platform_sdk`資料載入器後，資料將進行準備，然後分割到`train`和`val`資料集。 若要瞭解資料準備和功能工程，請造訪使用[!DNL JupyterLab]筆記型電腦建立配方的教學課程中[資料準備和功能工程](../jupyterlab/create-a-recipe.md#data-preparation-and-feature-engineering)一節。
