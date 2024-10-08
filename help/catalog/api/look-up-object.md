---
keywords: Experience Platform；首頁；熱門主題；目錄；物件查詢；api
solution: Experience Platform
title: 查詢目錄物件
description: 如果您知道特定目錄物件的唯一識別碼，則可以執行GET要求來檢視該物件的詳細資訊。
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 0331b6bbd22255cab92c93070dda1ffaed5bbbcb
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 2%

---

# 查詢目錄物件

如果您知道特定[!DNL Catalog]物件的唯一識別碼，則可以執行GET要求來檢視該物件的詳細資訊。

>[!NOTE]
>
>檢視特定物件時，最佳實務仍是[依屬性篩選](filter-data.md)，並只傳回您感興趣的屬性。

**API格式**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要擷取的[!DNL Catalog]物件型別。 有效的物件包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | 您要擷取之特定物件的識別碼。 |

**要求**

下列要求會依其ID擷取資料集，傳回其`name`、`description`、`tags`和`files`屬性。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回指定的資料集，但內文中只包含請求的`properties`。

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset",
        "description": "Sample dataset containing important data.",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    }
}
```

>[!NOTE]
>
>值以`@`為前置詞的屬性代表相互關聯的物件。 如需如何檢視這些物件詳細資訊的步驟，請參閱[檢視相關物件](appendix.md#view-interrelated-objects)的附錄一節。
