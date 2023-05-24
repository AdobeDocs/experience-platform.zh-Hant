---
keywords: Experience Platform；首頁；熱門主題；目錄；對象查找；api
solution: Experience Platform
title: 查找目錄對象
description: 如果您知道特定目錄對象的唯一標識符，則可以執行GET請求以查看該對象的詳細資訊。
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 2%

---

# 查找目錄對象

如果您知道特定的唯一標識符 [!DNL Catalog] 對象，可以執行GET請求以查看該對象的詳細資訊。

>[!NOTE]
>
>在查看特定對象時，仍然最好 [按屬性篩選](filter-data.md) 只歸還你感興趣的房產。

**API格式**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 類型 [!DNL Catalog] 要檢索的對象。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要檢索的特定對象的標識符。 |

**要求**

以下請求按資料集的ID檢索資料集，返回其 `name`。 `description`。 `state`。 `tags`, `files` 屬性。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回僅具有請求的指定資料集 `properties` 身體里。

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
>值前置詞為的屬性 `@` 表示相互關聯的對象。 請參閱附錄部分， [查看相關對象](appendix.md#view-interrelated-objects) 以獲取有關如何查看這些對象詳細資訊的步驟。
