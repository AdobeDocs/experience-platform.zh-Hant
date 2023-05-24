---
keywords: Experience Platform；首頁；熱門主題；刪除對象；目錄服務；api
solution: Experience Platform
title: 刪除API中的對象
description: 通過在DELETE請求的路徑中提供目錄對象的ID，可以刪除目錄對象。
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 1%

---

# 刪除API中的對象

可以刪除 [!DNL Catalog] 在DELETE請求的路徑中提供其ID。

>[!WARNING]
>
>刪除對象時要格外小心，因為這無法撤消，並且可能會在中的其他位置產生中斷更改 [!DNL Experience Platform]。

**API格式**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>的 `DELETE /batches/{ID}` 終結點已棄用。 要刪除批，應使用 [批處理接收API](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch)。

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 類型 [!DNL Catalog] 要刪除的對象。 有效對象包括： <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要更新的特定對象的標識符。 |

**要求**

以下請求刪除在請求路徑中指定ID的資料集。

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200(OK)和包含已刪除資料集ID的陣列。 此ID應與在DELETE請求中發送的ID匹配。 對已刪除對象執行GET請求時，返回HTTP狀態404（未找到），確認已成功刪除資料集。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>否 [!DNL Catalog] 對象與請求中提供的ID匹配，您仍可能收到HTTP狀態代碼200，但響應陣列將為空。
