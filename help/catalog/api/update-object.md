---
keywords: Experience Platform;home;popular topics;catalog;api;update an object
solution: Experience Platform
title: 更新物件
topic: developer guide
description: '通過將目錄對象的ID包含在PATCH請求的路徑中，可以更新其部分。 本檔案涵蓋使用欄位和使用JSON修補符號對目錄物件執行PATCH作業。 '
translation-type: tm+mt
source-git-commit: 9ba229195892245d29fb4f17b9f2e5cd6c6ea567
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 3%

---


# 更新物件

通過在PATCH請求的路 [!DNL Catalog] 徑中包括對象的ID，可以更新對象的一部分。 本文檔介紹對目錄對象執行PATCH操作的兩種方法：

* 使用欄位
* 使用JSON修補程式符號

>[!NOTE]
>
>對對象的PATCH操作不能修改其可展開欄位，這些欄位表示相互關聯的對象。 必須直接對相關對象進行修改。

## 使用欄位更新

下列範例呼叫示範如何使用欄位和值來更新物件。

**API格式**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要更新 [!DNL Catalog] 的對象類型。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 您要更新的特定物件的識別碼。 |

**請求**

下列請求會將資 `name` 料集 `description` 的和欄位更新為裝載中提供的值。 不要更新的物件欄位可從裝載中排除。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "name":"Updated Dataset Name",
       "description":"Updated description for Sample Dataset"
      }'
```

**回應**

成功的回應會傳回包含已更新資料集ID的陣列。 此ID應與PATCH請求中發送的ID匹配。 現在，對此資料集執行GET請求時，只會顯示 `name` 和已 `description` 更新，而所有其他值保持不變。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## 使用JSON修補程式符號進行更新

以下範例呼叫示範如何使用JSON修補程式更新物件，如 [RFC-6902所述](https://tools.ietf.org/html/rfc6902)。

<!-- (Include once API fundamentals guide is published) 

For more information on JSON Patch syntax, see the [API fundamentals guide](). 

-->

**API格式**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要更新 [!DNL Catalog] 的對象類型。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 您要更新的特定物件的識別碼。 |

**請求**

下列請求會將資 `name` 料集 `description` 的和欄位更新為每個JSON修補程式物件中提供的值。 使用JSON修補程式時，您也必須將「內容類型」標題設為 `application/json-patch+json`。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
        { "op": "add", "path": "/name", "value": "New Dataset Name" },
        { "op": "add", "path": "/description", "value": "New description for dataset" }
      ]'
```

**回應**

成功的響應返回包含已更新對象的ID的陣列。 此ID應與PATCH請求中發送的ID匹配。 現在，對此對象執行GET請求時，只顯示 `name` 和已 `description` 更新，而所有其他值保持不變。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
