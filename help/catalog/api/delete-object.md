---
keywords: Experience Platform;home;popular topics;delete an object;catalog service;api
solution: Experience Platform
title: 刪除API中的物件
topic: developer guide
description: 可以通過在DELETE請求的路徑中提供目錄對象的ID來刪除目錄對象。
translation-type: tm+mt
source-git-commit: b395535cbe7e4030606ee2808eb173998f5c32e0
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 1%

---


# 刪除API中的物件

您可以在DELETE請求的路徑中提供[!DNL Catalog]物件的ID，以刪除它。

>[!WARNING]
>
>刪除物件時請格外小心，因為這無法復原，而且可能會在[!DNL Experience Platform]的其他位置產生中斷變更。

**API格式**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>`DELETE /batches/{ID}`端點已過時。 若要刪除批，您應使用[批次擷取API](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch)。

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要刪除的[!DNL Catalog]對象類型。 有效對象包括： <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 您要更新的特定物件的識別碼。 |

**請求**

下列請求會刪除在請求路徑中指定ID的資料集。

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200（確定）和包含已刪除資料集ID的陣列。 此ID應符合在DELETE請求中傳送的ID。 對刪除的對象執行GET請求時，返回HTTP狀態404（找不到），確認資料集已成功刪除。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>如果沒有[!DNL Catalog]物件符合您請求中提供的ID，您仍可能收到HTTP狀態代碼200，但回應陣列會是空的。
