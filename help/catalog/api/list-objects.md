---
keywords: Experience Platform；首頁；熱門主題；過濾器；過濾器；過濾器資料；過濾器資料
solution: Experience Platform
title: 列出目錄對象
description: 您可以通過單個API調用檢索特定類型的所有可用對象的清單，最佳做法是包括限制響應大小的篩選器。
exl-id: 2c65e2bc-4ddd-445a-a52d-6ceb1153ccea
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 1%

---

# 列出目錄對象

您可以通過單個API調用檢索特定類型的所有可用對象的清單，最佳做法是包括限制響應大小的篩選器。

**API格式**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 類型 [!DNL Catalog] 列出的對象。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{FILTER}` | 用於篩選在響應中返回的結果的查詢參數。 多個參數用和符號分隔(`&`)。 請參閱上的指南 [篩選目錄資料](filter-data.md) 的子菜單。 |

**要求**

下面的示例請求檢索資料集清單， `limit` 過濾器減少對五個結果的響應，以及 `properties` 用於限制每個資料集顯示的屬性的篩選器。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回 [!DNL Catalog] 按請求中提供的查詢參數篩選的鍵值對形式的對象。 對於每個鍵值對，該鍵表示 [!DNL Catalog] 對象，然後可用於另一個調用 [查看特定對象](look-up-object.md) 的子菜單。

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
