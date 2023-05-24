---
keywords: Experience Platform；首頁；熱門主題；目錄；api；更新對象
solution: Experience Platform
title: 更新目錄對象
description: 通過將目錄對象的ID包括在PATCH請求的路徑中，可以更新該對象的一部分。 本文檔介紹使用欄位和JSON修補程式表示法對目錄對象執行PATCH操作。
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 3%

---

# 更新目錄對象

您可以更新 [!DNL Catalog] 將其ID包含在PATCH請求的路徑中。 本文檔介紹對目錄對象執行PATCH操作的兩種方法：

* 使用欄位
* 使用JSON修補程式表示法

>[!NOTE]
>
>對對象的PATCH操作無法修改其可擴展欄位，這些欄位表示相互關聯的對象。 必須直接對相關對象進行修改。

## 使用欄位更新

以下示例調用演示了如何使用欄位和值更新對象。

**API格式**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 類型 [!DNL Catalog] 要更新的對象。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要更新的特定對象的標識符。 |

**要求**

以下請求更新 `name` 和 `description` 資料集的欄位到負載中提供的值。 不要更新的對象欄位可以從負載中排除。

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

成功的響應返回包含已更新資料集ID的陣列。 此ID應與在PATCH請求中發送的ID匹配。 現在，對此資料集執行GET請求時僅顯示 `name` 和 `description` 已更新，而所有其它值保持不變。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## 使用JSON修補程式表示法更新

以下示例調用演示了如何使用JSON修補程式更新對象，如中所述 [RFC-6902](https://tools.ietf.org/html/rfc6902)。

<!-- (Include once API fundamentals guide is published) 

For more information on JSON Patch syntax, see the [API fundamentals guide](). 

-->

**API格式**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 類型 [!DNL Catalog] 要更新的對象。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要更新的特定對象的標識符。 |

**要求**

以下請求更新 `name` 和 `description` 資料集的欄位到每個JSON修補程式對象中提供的值。 使用JSON修補程式時，還必須將Content-Type頭設定為 `application/json-patch+json`。

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

成功的響應返回包含已更新對象ID的陣列。 此ID應與在PATCH請求中發送的ID匹配。 現在，對此對象執行GET請求時僅顯示 `name` 和 `description` 已更新，而所有其它值保持不變。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
