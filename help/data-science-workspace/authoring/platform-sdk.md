---
keywords: Experience Platform；開發人員指南； SDK；資料存取SDK；資料科學工作區；熱門主題
solution: Experience Platform
title: 使用Adobe Experience Platform Platform SDK進行模型編寫
description: 本教程提供了有關在Python和R中將data_access_sdk_python轉換為新的Python平台_sdk的資訊。
exl-id: 20909cae-5cd2-422b-8dbb-35bc63e69b2a
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 5%

---

# 使用Adobe Experience Platform製作模型 [!DNL Platform] SDK

本教學課程提供轉換的相關資訊 `data_access_sdk_python` 新蟒蛇 `platform_sdk` 在Python和R中。本教程提供了有關以下操作的資訊：

- [建立驗證](#build-authentication)
- [資料的基本讀取](#basic-reading-of-data)
- [基本資料寫入](#basic-writing-of-data)

## 建立驗證 {#build-authentication}

必須進行驗證才能對 [!DNL Adobe Experience Platform]，且由API金鑰、IMS組織ID、使用者代號和服務代號組成。

### Python

如果您使用Jupyter筆記型電腦，請使用以下代碼來建立 `client_context`:

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

如果您未使用Jupyter筆記型電腦，或需要變更IMS組織，請使用下列程式碼範例：

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

如果您使用Jupyter筆記型電腦，請使用以下代碼來建立 `client_context`:

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

如果您未使用Jupyter筆記型電腦，或需要變更IMS組織，請使用下列程式碼範例：

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

使用 [!DNL Platform] SDK，最大讀取大小為32 GB，最長讀取時間為10分鐘。

如果您的讀取時間太長，您可以嘗試使用下列其中一個篩選選項：

- [依偏移和限制篩選資料](#filter-by-offset-and-limit)
- [依日期篩選資料](#filter-by-date)
- [依欄篩選資料](#filter-by-selected-columns)
- [獲取排序結果](#get-sorted-results)

>[!NOTE]
>
>IMS組織設定於 `client_context`.

### Python

要在Python中讀取資料，請使用以下代碼示例：

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

## 依偏移和限制篩選 {#filter-by-offset-and-limit}

由於不再支援依批次ID篩選，因此若要限定資料讀取範圍，您必須使用 `offset` 和 `limit`.

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

日期篩選的粒度現在由時間戳記定義，而非由日期設定。

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

新 [!DNL Platform] SDK支援下列操作：

| 操作 | 函數 |
| --------- | -------- |
| 等於 (`=`) | `eq()` |
| Greater than (`>`) | `gt()` |
| 大於或等於 (`>=`) | `ge()` |
| 少於 (`<`) | `lt()` |
| Less than or equal to (`<=`) | `le()` |
| 和(`&`) | `And()` |
| 或 (`|`) | `Or()` |

## 依選取的欄篩選 {#filter-by-selected-columns}

若要進一步精簡資料的讀取，您也可以依欄名稱篩選。

### Python

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### R

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## 獲取排序結果 {#get-sorted-results}

接收的結果可以按目標資料集的指定列和它們的順序(asc/desc)分別排序。

在以下範例中，資料幀首先按「column-a」的升序排序。 接著，對&quot;column-a&quot;具有相同值的列會以降序依&quot;column-b&quot;排序。

### Python

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
>IMS組織設定於 `client_context`.

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

在您設定 `platform_sdk` 資料載入器，資料會進行準備，然後分割到 `train` 和 `val` 資料集。 若要了解資料準備和功能工程，請造訪 [資料準備與特徵工程](../jupyterlab/create-a-model.md#data-preparation-and-feature-engineering) 在使用建立方式的教學課程中 [!DNL JupyterLab] 筆記本。
