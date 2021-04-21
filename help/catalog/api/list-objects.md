---
keywords: Experience Platform;home；熱門主題；filter;Filter;filter data;filter data;filter data
solution: Experience Platform
title: 清單目錄對象
topic-legacy: developer guide
description: 您可以透過單一API呼叫擷取特定類型所有可用物件的清單，最佳實務是納入限制回應大小的篩選。
exl-id: 2c65e2bc-4ddd-445a-a52d-6ceb1153ccea
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 1%

---

# 清單目錄對象

您可以透過單一API呼叫擷取特定類型所有可用物件的清單，最佳實務是納入限制回應大小的篩選。

**API格式**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要列出的[!DNL Catalog]對象類型。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{FILTER}` | 用於篩選在回應中傳回結果的查詢參數。 多個參數以&amp;符號(`&`)分隔。 如需詳細資訊，請參閱[篩選目錄資料](filter-data.md)指南。 |

**要求**

以下範例請求會擷取資料集清單，其中`limit`篩選器會減少對五個結果的回應，而`properties`篩選器則會限制每個資料集顯示的屬性。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應以鍵值對的形式返回[!DNL Catalog]對象的清單，該清單由請求中提供的查詢參數篩選。 對於每個鍵值對，鍵代表有關[!DNL Catalog]對象的唯一標識符，然後該標識符可用於對[查看該特定對象](look-up-object.md)的另一調用，以獲得更多詳細資訊。

>[!NOTE]
>
>如果返回的對象不包含`properties`查詢所指示的一個或多個請求屬性，則響應僅返回其所包含的請求屬性，如下面的&#x200B;***`Sample Dataset 3`***&#x200B;和&#x200B;***`Sample Dataset 4`***&#x200B;所示。

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
