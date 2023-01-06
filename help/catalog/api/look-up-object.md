---
keywords: Experience Platform；首頁；熱門主題；目錄；物件查閱；API
solution: Experience Platform
title: 查找目錄對象
description: 如果您知道特定目錄物件的唯一識別碼，則可執行GET請求以檢視該物件的詳細資訊。
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 2%

---

# 查找目錄對象

如果您知道特定 [!DNL Catalog] 物件，您可以執行GET請求來檢視該物件的詳細資訊。

>[!NOTE]
>
>檢視特定物件時，仍最佳作法是 [按屬性篩選](filter-data.md) 並只傳回您感興趣的房產。

**API格式**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 類型 [!DNL Catalog] 要擷取的物件。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要檢索的特定對象的標識符。 |

**要求**

下列請求會依資料集的ID擷取資料集，並傳回資料集 `name`, `description`, `state`, `tags`，和 `files` 屬性。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應只會傳回請求的指定資料集 `properties` 在屍體里。

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
>值前面有的屬性 `@` 表示相互關聯的對象。 請參閱附錄一節 [查看相關對象](appendix.md#view-interrelated-objects) 以了解如何檢視這些物件的詳細資訊的步驟。
