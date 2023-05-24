---
keywords: Experience Platform；首頁；熱門主題；資料存取；python sdk；資料存取api;read python;write python
solution: Experience Platform
title: Python在資料科學工作區中的資料存取
type: Tutorial
description: 以下文檔包含有關如何在Python中訪問資料以在Data Science Workspace中使用的示例。
exl-id: 75aafd58-634a-4df3-a2f0-9311f93deae4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# 使用Python在資料科學工作區中訪問資料

以下文檔包含有關如何使用Python訪問資料以在Data Science Workspace中使用的示例。 有關使用JupyterLab筆記本訪問資料的資訊，請訪問 [JupyterLab筆記型電腦資料存取](../jupyterlab/access-notebook-data.md) 文檔。

## 讀取資料集

在設定環境變數並完成安裝後，您的資料集現在可以讀入pactis資料幀。

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

DISTINCT子句允許您提取行/列級別的所有不同值，從響應中刪除所有重複值。

使用 `distinct()` 函式如下所示：

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### WHERE子句

可以在Python中使用某些運算子來幫助篩選資料集。

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

下面可以看到使用這些篩選函式的示例：

```python
df = dataset_reader.where(experience_ds['timestamp'].gt(87879779797).And(experience_ds['timestamp'].lt(87879779797)).Or(experience_ds['a'].eq(123)))
```

### ORDER BY子句

ORDER BY子句允許按指定列按特定順序（升序或降序）對接收結果進行排序。 這是通過 `sort()` 的子菜單。

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

OFFSET子句允許您從開頭跳過行，以從以後開始返回行。 與LIMIT結合使用，可用於迭代塊中的行。

使用 `offset()` 函式如下所示：

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

## 用戶空間目錄（檢查點）

對於運行時間較長的作業，可能需要儲存中間步驟。 在這樣的情況下，您可以讀取和寫入用戶空間。

>[!NOTE]
>
>資料路徑為 **不** 儲存。 您需要儲存其相應資料的相應路徑。

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

Adobe Experience Platform資料科學工作區提供了使用上述代碼樣本讀取和寫入資料的處方樣本。 如果您想瞭解有關如何使用Python訪問資料的更多資訊，請查看 [Data Science Workspace Python GitHub儲存庫](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail)。
