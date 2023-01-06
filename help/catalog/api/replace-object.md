---
keywords: Experience Platform；首頁；熱門主題；目錄；api；取代物件
solution: Experience Platform
title: 替換目錄對象
description: 您可以使用PUT要求覆寫目錄物件的內容，其中會以要求裝載取代整個資源。
exl-id: cd98d13c-5261-4bff-b5db-af5f06d093c9
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 2%

---

# 替換目錄對象

您可以覆寫 [!DNL Catalog] 物件，其中整個資源會以要求裝載取代。

>[!NOTE]
>
>如果您只需更新 [!DNL Catalog] 物件，則使用PATCH要求可能會更有效率。

**API格式**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 類型 [!DNL Catalog] 要替換的對象。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要更新的特定對象的標識符。 |

**要求**

下列請求會使用裝載中提供的值覆寫資料集。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "New Dataset Name",
        "description": "New description for dataset",
        "state": "DRAFT",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }'
```

**回應**

成功的回應會傳回包含覆寫物件ID的陣列。 此ID應符合PUT請求中傳送的ID。 現在，對此物件執行GET要求時，會顯示其詳細資料已取代為先前PUT要求之裝載中提供的詳細資料。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
