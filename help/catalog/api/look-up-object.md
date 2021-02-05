---
keywords: Experience Platform;home;popular topics;catalog;object lookup;api
solution: Experience Platform
title: 查找目錄對象
topic: developer guide
description: '如果您知道特定目錄物件的唯一識別碼，則可執行GET要求以檢視該物件的詳細資訊。 '
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 2%

---


# 查找目錄對象

如果您知道特定[!DNL Catalog]物件的唯一識別碼，則可執行GET請求以檢視該物件的詳細資料。

>[!NOTE]
>
>在檢視特定物件時，依屬性](filter-data.md)篩選並僅傳回您感興趣的屬性仍是最佳實務。[

**API格式**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要檢索的[!DNL Catalog]對象的類型。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 您要擷取之特定物件的識別碼。 |

**請求**

下列請求依其ID擷取資料集，傳回其`name`、`description`、`state`、`tags`和`files`屬性。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回指定的資料集，但內文中只有請求的`properties`。

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset",
        "description": "Sample dataset containing important data.",
        "state": "DRAFT",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }
}
```

>[!NOTE]
>
>值前置詞為`@`的屬性表示相關對象。 有關如何查看這些對象詳細資訊的步驟，請參見[查看相關對象](appendix.md#view-interrelated-objects)的附錄部分。
