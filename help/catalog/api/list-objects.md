---
keywords: Experience Platform；首頁；熱門主題；篩選；篩選；篩選資料；篩選資料
solution: Experience Platform
title: 列出目錄物件
description: 您可以透過單一API呼叫來擷取特定型別的所有可用物件清單，最佳實務是加入可限制回應大小的篩選器。
exl-id: 2c65e2bc-4ddd-445a-a52d-6ceb1153ccea
source-git-commit: 409d052c119814a1cf6b79ff4448d1100b18e199
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 1%

---

# 列出目錄物件

您可以透過單一API呼叫來擷取特定型別的所有可用物件清單，最佳實務是加入可限制回應大小的篩選器。

**API格式**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 型別 [!DNL Catalog] 物件。 有效的物件包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{FILTER}` | 用來篩選回應中傳回結果的查詢引數。 多個引數會以&amp;符號(`&`)。 請參閱以下指南： [篩選目錄資料](filter-data.md) 以取得詳細資訊。 |

**要求**

以下範例請求會擷取資料集清單，並包含 `limit` 篩選條件將回應減少為五個結果，以及 `properties` 此篩選器會限制每個資料集所顯示的屬性。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回以下清單 [!DNL Catalog] 鍵值配對形式的物件，依請求中提供的查詢引數篩選。 對於每個機碼值組，機碼代表 [!DNL Catalog] 有問題的物件，然後可用於對的其他呼叫 [檢視該特定物件](look-up-object.md) 以取得更多詳細資料。

>[!NOTE]
>
>如果傳回的物件不包含 `properties` 查詢，回應只會傳回所請求的屬性，如所示 ***`Sample Dataset 3`*** 和 ***`Sample Dataset 4`*** 底下。

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bb276b03a14440000971552"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    },
    "5bda3a4228babc0000126377": {
        "name": "Sample Dataset 4",
        "files": "@/dataSetFiles?dataSetId=5bda3a4228babc0000126377"
    },
    "5bde21511dd27b0000d24e95": {
        "name": "Sample Dataset 5",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bde21511dd27b0000d24e95"
    }
}
```
