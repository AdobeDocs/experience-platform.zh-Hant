---
keywords: Experience Platform；首頁；熱門主題；目錄；api；取代物件
solution: Experience Platform
title: 取代目錄物件
description: 您可以使用PUT要求覆寫目錄物件的內容，其中要求裝載會取代整個資源。
exl-id: cd98d13c-5261-4bff-b5db-af5f06d093c9
source-git-commit: 2d6167ee7aaa0b79514be6e532e61602ae5cc640
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 2%

---

# 取代目錄物件

您可以覆寫 [!DNL Catalog] 使用PUT請求的物件，其中整個資源已替換為請求承載。

>[!NOTE]
>
>如果您只需要更新中的幾個特定欄位 [!DNL Catalog] 物件，使用PATCH請求可能更有效率。

**API格式**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 型別 [!DNL Catalog] 要取代的物件。 有效的物件包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | 您要更新之特定物件的識別碼。 |

**要求**

以下請求會使用承載中提供的值覆寫資料集。

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
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    }'
```

**回應**

成功的回應會傳回包含覆寫物件之識別碼的陣列。 此ID應符合PUT請求中傳送的ID。 執行此物件的GET要求時，現在會顯示其詳細資料已取代為先前PUT要求之裝載中提供的詳細資料。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
