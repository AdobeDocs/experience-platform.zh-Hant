---
keywords: Experience Platform；首頁；熱門主題；目錄；api;replace對象
solution: Experience Platform
title: 替換目錄對象
description: 可以使用PUT請求覆蓋目錄對象的內容，其中整個資源將替換為請求負載。
exl-id: cd98d13c-5261-4bff-b5db-af5f06d093c9
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 2%

---

# 替換目錄對象

可以覆蓋 [!DNL Catalog] 使用PUT請求的對象，其中整個資源被請求負載替換。

>[!NOTE]
>
>如果您只需更新 [!DNL Catalog] 對象，使用PATCH請求可能更有效。

**API格式**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 類型 [!DNL Catalog] 要替換的對象。 有效對象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要更新的特定對象的標識符。 |

**要求**

以下請求使用負載中提供的值覆蓋資料集。

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

成功的響應返回包含被覆蓋對象ID的陣列。 此ID應與在PUT請求中發送的ID匹配。 現在，對此對象執行GET請求時顯示其詳細資訊已替換為先前PUT請求的負載中提供的詳細資訊。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
