---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 安全的Python資料存取SDK
topic: tutorial
translation-type: tm+mt
source-git-commit: 49aa2e2664fe658d89b6279d1f869eb30c48ccad
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 1%

---


# Secure Python [!DNL Data Access] SDK

Secure Python [!DNL Data Access] SDK是軟體開發套件，可讓您從Adobe Experience Platform讀取和寫入資料集。

## 快速入門

您必須完成驗證教 [學課程](../../tutorials/authentication.md) ，才能存取值以呼叫Secure Python [!DNL Data Access] SDK:

- `{ACCESS_TOKEN}`
- `{API_KEY}`
- `{IMS_ORG}`

中的所有資 [!DNL Experience Platform] 源都與特定虛擬沙盒隔離。 使用 [!DNL Python] SDK時，需要執行下列作業的沙盒名稱和ID:

- `{SANDBOX_NAME}`
- `{SANDBOX_ID}`

如需中沙盒的詳細資訊 [!DNL Platform]，請參閱沙 [盒概述檔案](../../sandboxes/home.md)。

## 環境設定

預設情況下，服務端點設定為整合環境端點。 因此，要指向生產，請將以下環境變數設定為以下值：

| 變數 | 端點 |
| -------- | -------- |
| `ENV_CATALOG_URL` | `https://platform.adobe.io/data/foundation/catalog/` |
| `ENV_QUERY_SERVICE_URL` | `https://platform.adobe.io/data/foundation/query` |
| `ENV_BULK_INGEST_URL` | `https://platform.adobe.io/data/foundation/import/` |
| `ENV_REGISTRY_URL` | `https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas` |

此外，您的認證也可以新增為環境變數。

| 變數 | 值 |
| -------- | ----- |
| `ORG_ID` | 您的 `{IMS_ORG}` ID。 |
| `SERVICE_API_KEY` | 您的 `{API_KEY}` 價值。 |
| `USER_TOKEN` | 您的 `{ACCESS_TOKEN}` 價值。 |
| `SERVICE_TOKEN` | 您 `{SERVICE_TOKEN}`的，您可能需要授權服務之間的反向通道請求。 |
| `SANDBOX_ID` | 沙 `{SANDBOX_ID}` 盒的值。 |
| `SANDBOX_NAME` | 沙 `{SANDBOX_NAME}` 盒的值。 |

## 安裝

所有封裝在建置後都輸 `./dist` 出至。

### 車輪

```python
python3 setup.py bdist_wheel --universal
```

從項目目錄，將載輪載入Python 3環境。

```python
pip3 install ./dist/<name_of_wheel_file>.whl
```

### 卵子檔案

```python
python3 setup.py bdist_egg
```

## 讀取資料集

在設定環境變數並完成安裝後，現在可以將資料集讀入熊貓資料幀。

```python
from platform_sdk.client_context import ClientContext
from platform_sdk.dataset_reader import DatasetReader

client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

dataset_reader = DatasetReader(client_context, {DATASET_ID})
df = dataset_reader.read()
```

### 從資料集中選擇列

```python
df = dataset_reader.select(['column-a','column-b']).read()
```

### 獲取分區資訊：

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

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

SDK支 [!DNL Python] 援某些運算子，以協助篩選資料集。

>[!NOTE] 用於篩選的函式區分大小寫。

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

ORDER BY子句允許按指定列按特定順序（升序或降序）對接收結果進行排序。 在Python SDK中，這是使用函式來完成 `sort()` 的。

以下是使用函 `sort()` 數的範例：

```python
df = dataset_reader.sort([('column_1', 'asc'), ('column_2', 'desc')])
```

### LIMIT子句

LIMIT子句允許用戶限制從資料集接收的記錄數。

以下是使用函 `limit()` 數的範例：

```python
df = dataset_reader.limit(100).read()
```

### OFFSET子句

OFFSET子句允許用戶從開始跳過行，從以後開始返回行。 與LIMIT結合使用，可用於迭代塊中的行。

以下是使用函 `offset()` 數的範例：

```python
df = dataset_reader.offset(100).read()
```

## 寫入資料集

SDK支 [!DNL Python] 援編寫資料集。 用戶需要提供熊貓資料幀，這些資料幀需要寫入資料集。

### 編寫熊貓資料框

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})

# To fetch existing dataset
dataset = Dataset(client_context).get_by_id({DATASET_ID})

dataset_writer = DatasetWriter(client_context, dataset)

write_tracker = dataset_writer.write(<dataFrame>, file_format='json')
```

## Userspace目錄（檢查點）

對於運行時間較長的作業，用戶可能需要儲存中間步驟。 在此類情況下， [!DNL Python] SDK可讓使用者讀取和寫入使用者空間。

>!![NOTE] SDK不會儲存資 **料** 的路徑。 使用者需要儲存對應的資料路徑。

### 寫入用戶空間

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})
                               
user_helper = UserSpaceHelper(client_context)
user_helper.write(data_frame=<data_frame>, path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```

### 從用戶空間讀取

```python
client_context = ClientContext(api_key={API_KEY},
                               org_id={IMS_ORG_ID},
                               service_token={SERVICE_TOKEN},
                               user_token={USER_TOKEN},
                               sandbox_id={SANDBOX_ID},
                               sandbox_name={SANDBOX_NAME})
                               
user_helper = UserSpaceHelper(client_context)
my_df = user_helper.read(path=<path_to_directory>, ref_dataset_id=<ref_dataset_id>)
```
