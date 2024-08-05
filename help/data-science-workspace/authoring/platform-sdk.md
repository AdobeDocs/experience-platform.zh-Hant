---
keywords: Experience Platform;開發者指南;SDK;數據存取 SDK;數據科學工作環境;熱門主題
solution: Experience Platform
title: 使用 Adobe Experience Platform Platform SDK 進行模型創作
description: 此教學課程提供了有關在 Python 和 R 中將data_access_sdk_python轉換為新的 Python platform_sdk的信息。
exl-id: 20909cae-5cd2-422b-8dbb-35bc63e69b2a
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 3%

---

# 使用 Adobe Experience Platform [!DNL Platform] SDK 進行模型創作

>[!NOTE]
>
>不再提供 Data Science 工作環境 購買。
>
>本文檔適用於先前有權使用數據科學工作環境的現有客戶。

此教學課程為您提供了有關在 Python 和 R 中轉換為 `data_access_sdk_python` 新 Python `platform_sdk` 的信息。此教學課程提供有關以下操作的信息：

- [生成身份驗證](#build-authentication)
- [基本讀取數據](#basic-reading-of-data)
- [數據的基本寫入](#basic-writing-of-data)

## 生成身份驗證 {#build-authentication}

Authentication 是調用 [!DNL Adobe Experience Platform]所必需的，由 API 金鑰、組織 ID、用戶 令牌和服務令牌組成。

### Python

如果您使用的是 Jupyter Notebook，請使用以下代碼版本編號 `client_context`：

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

如果您沒有使用 Jupyter Notebook 或需要更改組織，請使用以下代碼範例：

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

如果您使用的是 Jupyter Notebook，請使用以下代碼版本編號 `client_context`：

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

如果您沒有使用 Jupyter Notebook 或需要更改組織，請使用以下代碼範例：

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
client_context <- psdk$client_context$ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

## 基本讀取數據 {#basic-reading-of-data}

使用新 [!DNL Platform] SDK，最大讀取大小為 32 GB，最長讀取時間為 10 分鐘。

如果讀取時間過長，可以嘗試使用以下篩選選項之一：

- [按偏移量和限制過濾數據](#filter-by-offset-and-limit)
- [依據日期篩選數據](#filter-by-date)
- [按欄篩選數據](#filter-by-selected-columns)
- [獲取排序結果](#get-sorted-results)

>[!NOTE]
>
>組織設定在 內 `client_context`。

### Python

要在 Python 中讀取資料，請使用下面的代碼範例：

```python
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).read()
df.head()
```

### R

要在 R 中讀取資料，請使用下面的代碼範例：

```r
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

## 按偏移量和限制篩選 {#filter-by-offset-and-limit}

由於不再支持按批次 ID 篩選，因此為了範圍讀取數據，需要使用 `offset` 和 `limit`。

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

## 依日期篩選 {#filter-by-date}

日期篩選的粒度現在由時間戳定義，而不是按日設定。

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

新版 [!DNL Platform] SDK 支援以下操作：

| 操作 | 函數 |
| --------- | -------- |
| 等於 （`=`） | `eq()` |
| 大於 （`>`） | `gt()` |
| 大於或等於 （`>=`） | `ge()` |
| 小於 （`<`） | `lt()` |
| 小於或等於 （`<=`） | `le()` |
| 和 （`&`） | `And()` |
| 或 （`|`） | `Or()` |

## 依選取的欄篩選 {#filter-by-selected-columns}

若要進一步優化數據讀取，還可以按列名稱進行篩選。

### Python

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### R

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## 獲取排序結果 {#get-sorted-results}

接收的結果可以分別按目標 資料集的指定列和順序（asc/desc）排序。

在以下示例中，數據幀首先按「列-a」升序排序。 具有相同「列-a」值的行然後按「列-b」降序排序。

### Python

```python
df = dataset_reader.sort([('column-a', 'asc'), ('column-b', 'desc')])
```

### R

```r
df <- dataset_reader$sort(c(('column-a', 'asc'), ('column-b', 'desc')))$read()
```

## 數據的基本寫入 {#basic-writing-of-data}

>[!NOTE]
>
>組織設定在 內 `client_context`。

要在 Python 和 R 中寫入數據，請使用以下範例之一：

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

配置 `platform_sdk` 數據載入程式後，將進行數據準備工作，然後將其拆分為AND `train` `val` 數據集。 要了解數據準備和特徵工程，請造訪使用筆記本創建[!DNL JupyterLab]方式教學課程中有關數據準備和特徵工程](../jupyterlab/create-a-model.md#data-preparation-and-feature-engineering)的部分[。
