---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 查找對象
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 2%

---


# 查找對象

如果您知道特定目錄物件的唯一識別碼，則可執行GET要求以檢視該物件的詳細資訊。

>[!NOTE]
>
>在檢視特定物件時，依屬性篩選 [並僅傳回您感興趣的屬性](filter-data.md) ，仍是最佳實務。

**API格式**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要檢索的目錄對象的類型。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 您要擷取之特定物件的識別碼。 |

**請求**

下列請求會依其ID擷取資料集，並傳回 `name`其 `description`、 `state`、 `tags`和 `files` 屬性。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回指定的資料集，但內文中只 `properties` 有請求的資料集。

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
>其值前置詞為前置詞的屬性代表 `@` 相互關聯的對象。 有關如何查看這些對 [像的詳細資訊](appendix.md#view-interrelated-objects) ，請參見查看相關對象的附錄部分。
