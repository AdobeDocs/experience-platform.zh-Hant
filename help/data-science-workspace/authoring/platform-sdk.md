---
keywords: Experience Platform；開發人員指南；SDK；資料存取SDK；資料科學Workspace；熱門主題
solution: Experience Platform
title: 使用Adobe Experience Platform SDK製作模型
description: 本教學課程提供在Python和R中將data_access_sdk_python轉換為新Python平台_sdk的相關資訊。
exl-id: 20909cae-5cd2-422b-8dbb-35bc63e69b2a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 3%

---

# 使用Adobe [!DNL Experience Platform] SDK製作模型

>[!NOTE]
>
>Data Science Workspace已無法購買。
>
>本檔案旨在供先前有權使用Data Science Workspace的現有客戶使用。

本教學課程提供您有關在Python和R中將`data_access_sdk_python`轉換為新Python `platform_sdk`的資訊。本教學課程提供有關下列作業的資訊：

- [建置驗證](#build-authentication)
- [基本資料讀取](#basic-reading-of-data)
- [基本資料寫入](#basic-writing-of-data)

## 建置驗證 {#build-authentication}

呼叫[!DNL Adobe Experience Platform]需要驗證，且包含API金鑰、組織ID、使用者權杖和服務權杖。

### Python

如果您使用Jupyter Notebook，請使用下列程式碼來建置`client_context`：

```python
client_context = PLATFORM_SDK_CLIENT_CONTEXT
```

如果您未使用Jupyter Notebook，或需要變更組織，請使用下列程式碼範例：

```python
from platform_sdk.client_context import ClientContext
client_context = ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

### R

如果您使用Jupyter Notebook，請使用下列程式碼來建置`client_context`：

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")

py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
```

如果您未使用Jupyter Notebook或需要變更組織，請使用下列程式碼範例：

```r
library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
client_context <- psdk$client_context$ClientContext(api_key={API_KEY},
              org_id={ORG_ID},
              user_token={USER_TOKEN},
              service_token={SERVICE_TOKEN})
```

## 基本資料讀取 {#basic-reading-of-data}

使用新的[!DNL Experience Platform] SDK時，最大讀取大小為32 GB，最大讀取時間為10分鐘。

如果您的讀取時間太長，可以嘗試使用下列其中一個篩選選項：

- [依位移和限制篩選資料](#filter-by-offset-and-limit)
- [依日期篩選資料](#filter-by-date)
- [依欄篩選資料](#filter-by-selected-columns)
- [正在取得排序的結果](#get-sorted-results)

>[!NOTE]
>
>組織是在`client_context`內設定。

### Python

若要以Python讀取資料，請使用下列程式碼範例：

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

## 依位移和限制篩選 {#filter-by-offset-and-limit}

由於不再支援依據批次ID進行篩選，若要設定資料讀取的範圍，您必須使用`offset`和`limit`。

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

日期篩選的詳細程度現在由時間戳記定義，而不是由日期設定。

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

新的[!DNL Experience Platform] SDK支援下列作業：

| 作業 | 函數 |
| --------- | -------- |
| 等於(`=`) | `eq()` |
| 大於(`>`) | `gt()` |
| 大於或等於(`>=`) | `ge()` |
| 小於(`<`) | `lt()` |
| 小於或等於(`<=`) | `le()` |
| 和(`&`) | `And()` |
| 或(`|`) | `Or()` |

## 依選取的欄篩選 {#filter-by-selected-columns}

若要進一步縮小資料的讀取範圍，您也可以依欄名稱篩選。

### Python

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### R

```r
df <- dataset_reader$select(c('column-a','column-b'))$read() 
```

## 取得排序的結果 {#get-sorted-results}

收到的結果可依目標資料集的指定欄位和它們的順序(asc/desc)分別排序。

在下列範例中，Dataframe會先依遞增順序的「column-a」排序。 之後，「column-a」具有相同值的列會依「column-b」以遞減順序排序。

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
>組織是在`client_context`內設定。

若要以Python和R撰寫資料，請使用下列其中一個範例：

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

設定`platform_sdk`資料載入器後，資料會進行準備，然後分割為`train`和`val`資料集。 若要瞭解資料準備和功能工程，請造訪教學課程中關於使用[!DNL JupyterLab]筆記本建立配方的[資料準備和功能工程](../jupyterlab/create-a-model.md#data-preparation-and-feature-engineering)一節。
