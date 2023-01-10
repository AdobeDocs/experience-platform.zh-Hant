---
keywords: Experience Platform；首頁；熱門主題；資料存取；python sdk；資料存取api；讀取python；寫入python
solution: Experience Platform
title: 在Data Science Workspace中使用Python存取資料
type: Tutorial
description: 以下文檔包含有關如何在Python中訪問資料以用於Data Science Workspace的示例。
exl-id: 75aafd58-634a-4df3-a2f0-9311f93deae4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# 在Data Science Workspace中使用Python存取資料

以下文檔包含有關如何使用Python訪問資料以用於Data Science Workspace的示例。 有關使用JupyterLab筆記型電腦訪問資料的資訊，請訪問 [JupyterLab筆記型電腦資料存取](../jupyterlab/access-notebook-data.md) 檔案。

## 讀取資料集

設定環境變數並完成安裝後，您的資料集現在可以讀入到pactis dataframe中。

```python
import pandas as pd
from .utils import get_client_context
from platform_sdk.dataset_reader import DatasetReader

def load(config_properties):

client_context = get_client_context(config_properties)

dataset_reader = DatasetReader(client_context, config_properties['DATASET_ID'])

df = dataset_reader.read()
```

### 從資料集中選取欄

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

DISTINCT子句允許您從行/列級別獲取所有不同值，從響應中刪除所有重複值。

使用 `distinct()` 函式如下所示：

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### WHERE子句

Python中可以使用某些運算子來幫助篩選資料集。

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

ORDER BY子句允許按指定列按特定順序（升序或降序）對接收結果進行排序。 這需使用 `sort()` 函式。

使用 `sort()` 函式如下所示：

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### LIMIT子句

LIMIT子句允許您限制從資料集接收的記錄數。

使用 `limit()` 函式如下所示：

```python
df = dataset_reader.limit(100).read()
```

### OFFSET子句

OFFSET子句允許您從開頭跳過行，以從後一點開始返回行。 與LIMIT結合使用時，可反覆運算區塊中的列。

使用 `offset()` 函式如下所示：

```python
df = dataset_reader.offset(100).read()
```

## 寫入資料集

若要寫入資料集，您需要為資料集提供熊貓資料框。

### 大熊貓資料框

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## Userspace目錄（檢查點）

若要執行較長的作業，您可能需要儲存中間步驟。 在此情況下，您可以讀取和寫入使用者空間。

>[!NOTE]
>
>資料路徑為 **not** 儲存。 您需要儲存其個別資料的對應路徑。

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

Adobe Experience Platform Data Science Workspace提供方式範例，使用上述程式碼範例來讀取和寫入資料。 如果您想進一步了解如何使用Python訪問資料，請查看 [Data Science Workspace Python GitHub存放庫](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail).
