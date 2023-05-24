---
keywords: Experience Platform；開發人員指南；SDK；資料存取SDK；資料科學工作區；熱門主題
solution: Experience Platform
title: 使用Adobe Experience Platform平台SDK進行模型創作
description: 本教程提供了有關將data_access_sdk_python轉換為Python和R中的新Python平台_sdk的資訊。
exl-id: 20909cae-5cd2-422b-8dbb-35bc63e69b2a
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 5%

---

# 使用Adobe Experience Platform [!DNL Platform] SDK

本教程提供了有關轉換的資訊 `data_access_sdk_python` 新蟒蛇隊 `platform_sdk` 在Python和R本教程提供了以下操作的資訊：

- [生成身份驗證](#build-authentication)
- [資料的基本讀取](#basic-reading-of-data)
- [基本資料寫入](#basic-writing-of-data)

## 生成身份驗證 {#build-authentication}

調用時需要身份驗證 [!DNL Adobe Experience Platform]，由API密鑰、組織ID、用戶令牌和服務令牌組成。

### 蟒

如果您使用的是Jupyter筆記本，請使用以下代碼生成 `client_context`:

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

如果您未使用Jupyter筆記本或需要更改組織，請使用以下代碼示例：

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

如果您使用的是Jupyter筆記本，請使用以下代碼生成 `client_context`:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

如果您未使用Jupyter筆記本或需要更改組織，請使用以下代碼示例：

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
client_context <- psdk$client_context$ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

## 資料的基本讀取 {#basic-reading-of-data}

新 [!DNL Platform] SDK，最大讀取大小為32 GB，最大讀取時間為10分鐘。

如果您的讀取時間太長，可以嘗試使用以下篩選選項之一：

- [按偏移和限制篩選資料](#filter-by-offset-and-limit)
- [按日期篩選資料](#filter-by-date)
- [按列篩選資料](#filter-by-selected-columns)
- [獲取排序結果](#get-sorted-results)

>[!NOTE]
>
>組織設定在 `client_context`。

### 蟒

要在Python中讀取資料，請使用以下代碼示例：

```python
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).read()
df.head()
```

### R

要讀取R中的資料，請使用以下代碼示例：

```r
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

## 按偏移和限制篩選 {#filter-by-offset-and-limit}

由於不再支援按批ID篩選，因此，為了確定資料讀取的範圍，您需要使用 `offset` 和 `limit`。

### 蟒

```python
df = dataset_reader.limit(100).offset(1).read()
df.head
```

### R

```r
df <- dataset_reader$limit(100L)$offset(1L)$read() 
df
```

## 按日期篩選 {#filter-by-date}

日期篩選的粒度現在由時間戳定義，而不是按日設定。

### 蟒

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

新 [!DNL Platform] SDK支援以下操作：

| 操作 | 函數 |
| --------- | -------- |
| 等於 (`=`) | `eq()` |
| Greater than (`>`) | `gt()` |
| 大於或等於 (`>=`) | `ge()` |
| 少於 (`<`) | `lt()` |
| Less than or equal to (`<=`) | `le()` |
| 和(`&`) | `And()` |
| 或 (`|`) | `Or()` |

## 按選定列篩選 {#filter-by-selected-columns}

要進一步細化資料讀取，還可以按列名進行篩選。

### 蟒

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### R

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## 獲取排序結果 {#get-sorted-results}

接收的結果可以按目標資料集的指定列和它們的順序(asc/desc)分別排序。

在以下示例中，資料幀首先按&quot;column-a&quot;的升序排序。 對於&quot;column-a&quot;具有相同值的行按&quot;column-b&quot;按降序排序。

### 蟒

```python
df = dataset_reader.sort([('column-a', 'asc'), ('column-b', 'desc')])
```

### R

```r
df <- dataset_reader$sort(c(('column-a', 'asc'), ('column-b', 'desc')))$read()
```

## 基本資料寫入 {#basic-writing-of-data}

>[!NOTE]
>
>組織設定在 `client_context`。

要在Python和R中寫入資料，請使用以下示例之一：

### 蟒

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

配置 `platform_sdk` 資料載入器，資料經過準備，然後被拆分到 `train` 和 `val` 資料集。 要瞭解資料準備和功能工程，請訪問 [資料準備與特徵工程](../jupyterlab/create-a-model.md#data-preparation-and-feature-engineering) 在教程中使用 [!DNL JupyterLab] 筆記本。
