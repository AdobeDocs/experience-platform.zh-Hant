---
keywords: Experience Platform;home；熱門主題；catalog;api；替換對象
solution: Experience Platform
title: 替換目錄對象
topic-legacy: developer guide
description: 您可以使用PUT請求覆寫目錄對象的內容，其中將整個資源替換為請求裝載。
exl-id: cd98d13c-5261-4bff-b5db-af5f06d093c9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 2%

---

# 替換目錄對象

您可以使用PUT請求覆寫[!DNL Catalog]對象的內容，其中整個資源被請求裝載替換。

>[!NOTE]
>
>如果您只需要更新[!DNL Catalog]物件中的幾個特定欄位，使用PATCH請求可能會更有效率。

**API格式**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要替換的[!DNL Catalog]對象的類型。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 您要更新的特定物件的識別碼。 |

**要求**

下列請求會以裝載中提供的值覆寫資料集。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的響應返回包含被覆蓋對象ID的陣列。 此ID應符合在PUT請求中傳送的ID。 現在，對此對象執行GET請求時，會顯示其詳細資訊已被先前PUT請求的裝載中提供的詳細資訊替換。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
