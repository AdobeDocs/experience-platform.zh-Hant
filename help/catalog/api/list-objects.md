---
keywords: Experience Platform;home;popular topics;filter;Filter;filter data;Filter data
solution: Experience Platform
title: 清單對象
topic: developer guide
description: 您可以透過單一API呼叫擷取特定類型所有可用物件的清單，最佳實務是納入限制回應大小的篩選。
translation-type: tm+mt
source-git-commit: c081a7521be9715ca32d35504922a70767924fd7
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 1%

---


# 清單對象

您可以透過單一API呼叫擷取特定類型所有可用物件的清單，最佳實務是納入限制回應大小的篩選。

**API格式**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要列出 [!DNL Catalog] 的對象類型。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{FILTER}` | 用於篩選在回應中傳回結果的查詢參數。 多個參數會以&amp;符號(`&`)分隔。 如需詳細資訊，請 [參閱篩選目錄資料](filter-data.md) 指南。 |

**請求**

以下的範例請求會擷取資料集清單，其中 `limit` 有一個篩選器會降低對五個結果的回應，以及一個篩選器 `properties` ，可限制每個資料集顯示的屬性。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應以鍵值對的 [!DNL Catalog] 形式返回對象清單，該清單由請求中提供的查詢參數過濾。 對於每個鍵值對，鍵代表有關對象的唯一標識符，然後，該標識符可用於另一個調用中，以查看該 [!DNL Catalog] 特定對象 [](look-up-object.md) ，以瞭解詳細資訊。

>[!NOTE]
>
>如果返回的對象不包含查詢所指示的一個或多個請求屬性，則響應僅返回它所包含的請求屬性，如下 `properties` 所示 ***`Sample Dataset 3`******`Sample Dataset 4`*** 。

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
