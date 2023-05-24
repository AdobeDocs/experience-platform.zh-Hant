---
keywords: Experience Platform；首頁；熱門主題；目錄；多個對象查找；api
solution: Experience Platform
title: 查找多個目錄對象
description: 如果您希望查看多個特定對象，而不是對每個對象發出一個請求，則「目錄」提供了一個簡單快捷方式，用於請求多個同類型的對象。 可以使用單個GET請求通過包含逗號分隔的ID清單來返回多個特定對象。
exl-id: b2329b32-6139-4557-aff3-a584e03b09f3
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 1%

---

# 查找多個目錄對象

如果您希望查看多個特定對象，而不是對每個對象發出一個請求， [!DNL Catalog] 提供了請求同一類型的多個對象的簡單快捷方式。 可以使用單個GET請求通過包含逗號分隔的ID清單來返回多個特定對象。

>[!NOTE]
>
>即使在請求特定 [!DNL Catalog] 對象，它仍然是 `properties` 查詢參數以僅返回所需的屬性。

**API格式**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{OBJECT_TYPE}` | 類型 [!DNL Catalog] 要檢索的對象。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{ID}` | 要檢索的特定對象之一的標識符。 |

**要求**

以下請求包括以逗號分隔的資料集ID清單以及要為每個資料集返回的以逗號分隔的屬性清單。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回指定資料集的清單，該清單僅包含請求的屬性(`name`。 `description`, `files`)。

>[!NOTE]
>
>如果返回的對象不包含由 `properties` 查詢時，響應僅返回它確實包含的請求屬性，如中所示 ***`Sample Dataset 3`*** 和 ***`Sample Dataset 4`*** 下。

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bb276b03a14440000971552/views/5bb276b01250b012f9acc75b/files"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    },
    "5bda3a4228babc0000126377": {
        "name": "Sample Dataset 4",
        "files": "@/dataSets/5bda3a4228babc0000126377/views/5bda3a4228babc0000126378/files"
    },
    "5bde21511dd27b0000d24e95": {
        "name": "Sample Dataset 5",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bde21511dd27b0000d24e95/views/5bde21511dd27b0000d24e96/files"
    }
}
```
