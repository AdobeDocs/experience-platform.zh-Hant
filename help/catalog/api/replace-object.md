---
keywords: Experience Platform;home;popular topics;catalog;api;replace an object
solution: Experience Platform
title: 替換對象
topic: developer guide
description: 您可以使用PUT請求覆寫目錄對象的內容，其中整個資源將替換為請求裝載。
translation-type: tm+mt
source-git-commit: dd1f508b93e8eac14e3c41fac9d8f49769d08f46
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 2%

---


# 替換對象

您可以使用PUT請求覆 [!DNL Catalog] 寫物件的內容，其中整個資源會以請求裝載取代。

>[!NOTE]
>
>如果您只需要更新對象中的幾個特定字 [!DNL Catalog] 段，則使用PATCH請求可能會更有效。

**API格式**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要替換 [!DNL Catalog] 的對象類型。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 您要更新的特定物件的識別碼。 |

**請求**

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

成功的響應返回包含被覆蓋對象ID的陣列。 此ID應符合PUT請求中傳送的ID。 現在，對此對象執行GET請求時，會顯示其詳細資訊已被先前PUT請求的裝載中提供的詳細資訊替換。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
