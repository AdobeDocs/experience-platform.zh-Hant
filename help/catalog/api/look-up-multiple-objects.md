---
keywords: Experience Platform;home；熱門主題；catalog；多對象查找；api
solution: Experience Platform
title: 查找多個目錄對象
topic-legacy: developer guide
description: 如果您想要檢視數個特定物件，而不是每個物件提出一個要求，「目錄」會提供簡單的捷徑，讓您要求同一類型的多個物件。 您可以使用單一GET請求來傳回多個特定物件，方法是包含逗號分隔的ID清單。
exl-id: b2329b32-6139-4557-aff3-a584e03b09f3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 1%

---

# 查找多個目錄對象

如果您想要檢視數個特定物件，而不是每個物件提出一個要求，[!DNL Catalog]會提供簡單的捷徑，讓您要求多個相同類型的物件。 您可以使用單一GET請求來傳回多個特定物件，方法是包含逗號分隔的ID清單。

>[!NOTE]
>
>即使在請求特定[!DNL Catalog]物件時，`properties`查詢參數仍是最佳實務，只傳回您所需的屬性。

**API格式**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{OBJECT_TYPE}` | 要檢索的[!DNL Catalog]對象的類型。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{ID}` | 您要擷取之特定物件之一的識別碼。 |

**要求**

下列請求包含以逗號分隔的資料集ID清單，以及要針對每個資料集傳回之屬性的逗號分隔清單。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回指定資料集的清單，其中僅包含每個資料集的請求屬性（`name`、`description`和`files`）。

>[!NOTE]
>
>如果返回的對象不包含`properties`查詢所指示的一個或多個請求屬性，則響應只返回其所包含的請求屬性，如以下&#x200B;***`Sample Dataset 3`***&#x200B;和&#x200B;***`Sample Dataset 4`***&#x200B;所示。

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
