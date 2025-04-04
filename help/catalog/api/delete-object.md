---
keywords: Experience Platform；首頁；熱門主題；刪除物件；目錄服務；api
solution: Experience Platform
title: 刪除API中的物件
description: 您可以在DELETE請求的路徑中提供目錄物件的ID，以刪除目錄物件。
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
source-git-commit: d88336d314e767a068ef6524161baeb642a58433
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 1%

---

# 刪除API中的物件

您可以在DELETE要求的路徑中提供其ID，以刪除[!DNL Catalog]物件。

>[!WARNING]
>
>刪除物件時請格外小心，因為此動作無法復原，且可能會在[!DNL Experience Platform]的其他位置產生重大變更。

**API格式**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>`DELETE /batches/{ID}`端點已過時。 若要刪除批次，您應該使用[批次擷取API](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch)。

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要刪除的[!DNL Catalog]物件的型別。 有效的物件包括： <ul><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | 您要更新之特定物件的識別碼。 |

**要求**

以下請求會刪除在請求路徑中指定ID的資料集。

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200 （確定）以及包含已刪除資料集ID的陣列。 此ID應符合DELETE請求中傳送的ID。 對已刪除的物件執行GET要求時，會傳回HTTP狀態404 （找不到），確認資料集已成功刪除。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>如果沒有[!DNL Catalog]物件符合您請求中提供的ID，您仍可能收到HTTP狀態碼200，但回應陣列將是空的。
