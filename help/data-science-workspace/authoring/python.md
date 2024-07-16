---
keywords: Experience Platform；首頁；熱門主題；資料存取；python sdk；資料存取api；讀取python；寫入python
solution: Experience Platform
title: 在資料科學Workspace中使用Python存取資料
type: Tutorial
description: 以下檔案包含如何在Python中存取資料以用於資料科學Workspace的範例。
exl-id: 75aafd58-634a-4df3-a2f0-9311f93deae4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# 在資料科學Workspace中使用Python存取資料

以下檔案包含有關如何使用Python存取資料以用於資料科學Workspace的範例。 如需使用JupyterLab Notebooks存取資料的資訊，請瀏覽[JupyterLab Notebooks資料存取](../jupyterlab/access-notebook-data.md)檔案。

## 讀取資料集

設定環境變數並完成安裝後，您現在可以將資料集讀入pandas dataframe中。

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

### 取得分割資訊：

```python
client_context = get_client_context(config_properties)

dataset = Dataset(client_context).get_by_id({DATASET_ID})
partitions = dataset.get_partitions_info()
```

### DISTINCT子句

DISTINCT子句可讓您在列/欄層級擷取所有不同的值，從回應中移除所有重複的值。

以下顯示使用`distinct()`函式的範例：

```python
df = dataset_reader.select(['column-a']).distinct().read()
```

### WHERE子句

您可以在Python中使用某些運運算元，協助篩選資料集。

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

您可以在下方看到使用這些篩選函式的範例：

```python
df = dataset_reader.where(experience_ds['timestamp'].gt(87879779797).And(experience_ds['timestamp'].lt(87879779797)).Or(experience_ds['a'].eq(123)))
```

### ORDER BY子句

ORDER BY子句允許接收的結果以特定順序（升序或降序）依指定的資料行排序。 這是使用`sort()`函式完成的。

以下顯示使用`sort()`函式的範例：

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### LIMIT子句

LIMIT子句可讓您限制從資料集接收的記錄數。

以下顯示使用`limit()`函式的範例：

```python
df = dataset_reader.limit(100).read()
```

### OFFSET子句

OFFSET子句可讓您從頭開始略過資料列，以開始從後面傳回資料列。 在搭配LIMIT的情況下，這可用來疊代區塊中的列。

以下顯示使用`offset()`函式的範例：

```python
df = dataset_reader.offset(100).read()
```

## 寫入資料集

若要寫入資料集，您必須提供熊貓資料流至資料集。

### 正在寫入熊貓資料流

```python
client_context = get_client_context(config_properties)

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<your_dataFrame>, file_format='json')
```

## Userspace目錄（檢查點）

若要讓工作執行時間更長，您可能需要儲存中間步驟。 在類似的情況下，您可以讀取和寫入使用者空間。

>[!NOTE]
>
>資料路徑&#x200B;**未儲存**。 您需要儲存其個別資料的對應路徑。

### 寫入使用者空間

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### 從使用者空間讀取

```python
client_context = get_client_context(config_properties)
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

## 後續步驟

Adobe Experience Platform Data Science Workspace提供的配方範例會使用上述程式碼範例來讀取和寫入資料。 如果您想進一步瞭解如何使用Python存取您的資料，請檢閱[資料科學Workspace Python GitHub存放庫](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail)。
