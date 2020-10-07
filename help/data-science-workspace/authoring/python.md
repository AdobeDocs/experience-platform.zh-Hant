---
keywords: Experience Platform;home;popular topics;data access;python sdk;data access api;read python;write python
solution: Experience Platform
title: 使用Python訪問資料
topic: tutorial
type: Tutorial
description: 以下檔案包含如何在Python中存取資料以用於資料科學工作區的範例。
translation-type: tm+mt
source-git-commit: fcb4088ecac76d10b0cb69b04ad55167f5cdac3e
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# 使用Python訪問資料

以下檔案包含如何使用Python存取資料以用於資料科學工作區的範例。 有關使用JupyterLab筆記型電腦訪問資料的資訊，請訪問 [JupyterLab筆記型電腦資料存取文檔](../jupyterlab/access-notebook-data.md) 。

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

以下是使用函 `distinct()` 數的範例：

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

ORDER BY子句允許按指定列按特定順序（升序或降序）對接收結果進行排序。 這是使用函式來完 `sort()` 成的。

以下是使用函 `sort()` 數的範例：

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### LIMIT子句

LIMIT子句允許您限制從資料集接收的記錄數。

以下是使用函 `limit()` 數的範例：

```python
df = dataset_reader.limit(100).read()
```

### OFFSET子句

OFFSET子句允許您從開頭跳過行，從後一點開始返回行。 與LIMIT結合使用，可用於迭代塊中的行。

以下是使用函 `offset()` 數的範例：

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
>不會儲存資料的 **路徑** 。 您需要將對應的路徑儲存到其各自的資料。

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

Adobe Experience Platform Data Science Workspace提供使用上述程式碼範例來讀取和寫入資料的方式範例。 如果您想要進一步瞭解如何使用Python存取您的資料，請參閱資料科學工作區Python GitHub [資料庫](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail)。