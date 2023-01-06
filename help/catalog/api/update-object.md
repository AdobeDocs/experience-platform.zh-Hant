---
keywords: Experience Platform；首頁；熱門主題；目錄；api；更新物件
solution: Experience Platform
title: 更新目錄物件
description: 您可以在目錄請求的路徑中加入其ID，以更新目錄物件的部分。 本檔案涵蓋使用欄位，以及使用JSON修補程式記號，對目錄物件執行PATCH作業。
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 3%

---

# 更新目錄物件

您可以更新 [!DNL Catalog] 物件，請在PATCH要求的路徑中加入其ID。 本文檔涵蓋對目錄對象執行PATCH操作的兩種方法：

* 使用欄位
* 使用JSON修補程式標籤法

>[!NOTE]
>
>對對象的PATCH操作無法修改其可擴展欄位，這些欄位表示相關對象。 必須直接修改相關對象。

## 使用欄位更新

下列範例呼叫示範如何使用欄位和值更新物件。

**API格式**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 類型 [!DNL Catalog] 要更新的物件。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要更新的特定對象的標識符。 |

**要求**

下列請求會更新 `name` 和 `description` 資料集的欄位，以及有效負載中提供的值。 不要更新的物件欄位可從裝載中排除。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "name":"Updated Dataset Name",
       "description":"Updated description for Sample Dataset"
      }'
```

**回應**

成功的回應會傳回包含已更新資料集ID的陣列。 此ID應符合PATCH請求中傳送的ID。 現在，對此資料集執行GET請求時，只會顯示 `name` 和 `description` 已更新，而所有其他值維持不變。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## 使用JSON修補程式標籤法進行更新

下列範例呼叫示範如何使用JSON修補程式更新物件，如 [RFC-6902](https://tools.ietf.org/html/rfc6902).

<!-- (Include once API fundamentals guide is published) 

For more information on JSON Patch syntax, see the [API fundamentals guide](). 

-->

**API格式**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 類型 [!DNL Catalog] 要更新的物件。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要更新的特定對象的標識符。 |

**要求**

下列請求會更新 `name` 和 `description` 資料集的欄位，以及每個JSON修補程式物件中提供的值。 使用JSON修補程式時，您也必須將Content-Type標題設為 `application/json-patch+json`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
        { "op": "add", "path": "/name", "value": "New Dataset Name" },
        { "op": "add", "path": "/description", "value": "New description for dataset" }
      ]'
```

**回應**

成功的回應會傳回包含已更新物件ID的陣列。 此ID應符合PATCH請求中傳送的ID。 現在，對此物件執行GET要求時，只會顯示 `name` 和 `description` 已更新，而所有其他值維持不變。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
