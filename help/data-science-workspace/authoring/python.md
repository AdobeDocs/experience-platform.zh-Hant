---
keywords: Experience Platform；首頁；熱門主題；資料存取；python sdk；資料存取api;read python;write python
solution: Experience Platform
title: 在資料科學工作區中使用Python訪問資料
topic-legacy: tutorial
type: Tutorial
description: 以下檔案包含如何在Python中存取資料以用於資料科學工作區的範例。
exl-id: 75aafd58-634a-4df3-a2f0-9311f93deae4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# 在資料科學工作區中使用Python存取資料

以下檔案包含如何使用Python存取資料以用於資料科學工作區的範例。 有關使用JupyterLab筆記型電腦訪問資料的資訊，請訪問[JupyterLab筆記型電腦資料存取](../jupyterlab/access-notebook-data.md)文檔。

## 讀取資料集

在設定環境變數並完成安裝後，您的資料集現在可以讀入熊貓資料幀。

```python
import pandas as pd
from .utils import get_client_context
from platform_sdk.dataset_reader import DatasetReader

def load(config_properties):

client_context = get_client_context(config_properties)

dataset_reader = DatasetReader(client_context, config_properties['DATASET_ID'])

df = dataset_reader.read()
```

### 從資料集中選擇列

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### 獲取分區資訊：

```python
client_context = get_client_context(config_properties)

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### DISTINCT子句

DISTINCT子句允許您在行／列級別讀取所有不同值，從響應中刪除所有重複值。

以下是使用`distinct()`函式的範例：

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### WHERE子句

您可以在Python中使用某些運算子來協助篩選資料集。

>[!NOTE]
>
>用於篩選的函式區分大小寫。

```python
eq() = '='
gt() = '>'
ge() = '>='
lt() = '<'
le() = '<='
And = and operator
Or = or operator
```

以下是使用這些篩選函式的範例：

```python
df = dataset_reader.where(experience_ds['timestamp'].gt(87879779797).And(experience_ds['timestamp'].lt(87879779797)).Or(experience_ds['a'].eq(123)))
```

### ORDER BY子句

ORDER BY子句允許按指定列按特定順序（升序或降序）對接收結果進行排序。 這是使用`sort()`函式來完成的。

以下是使用`sort()`函式的範例：

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### LIMIT子句

LIMIT子句允許您限制從資料集接收的記錄數。

以下是使用`limit()`函式的範例：

```python
df = dataset_reader.limit(100).read()
```

### OFFSET子句

OFFSET子句允許您從開頭跳過行，從後一點開始返回行。 與LIMIT結合使用，可用於迭代塊中的行。

以下是使用`offset()`函式的範例：

```python
df = dataset_reader.offset(100).read()
```

## 寫入資料集

要寫入資料集，您需要向資料集提供熊貓資料框。

### 編寫熊貓資料框

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## Userspace目錄（檢查點）

對於運行時間較長的作業，您可能需要儲存中間步驟。 在此類情況下，您可以讀取和寫入用戶空間。

>[!NOTE]
>
>資料的路徑被儲存在&#x200B;**not**&#x200B;中。 您需要將對應的路徑儲存到其各自的資料。

### 寫入用戶空間

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### 從用戶空間讀取

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

## 後續步驟

Adobe Experience Platform資料科學工作區提供方式範例，使用上述程式碼範例來讀取和寫入資料。 如果您想要進一步瞭解如何使用Python存取您的資料，請參閱[資料科學工作區Python GitHub Repository](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail)。
