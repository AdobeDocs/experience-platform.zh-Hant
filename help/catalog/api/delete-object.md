---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 刪除對象
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 2%

---


# 刪除對象

您可以在DELETE [!DNL Catalog] 請求的路徑中提供物件ID來刪除物件。

>[!WARNING]
>
>刪除物件時請格外小心，因為這無法復原，而且可能會在其他位置產生中斷變更 [!DNL Experience Platform]。

**API格式**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>端 `DELETE /batches/{ID}` 點已過時。 若要刪除批次，您應使用「批次擷取 [API」](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch)。

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要刪除 [!DNL Catalog] 的對象類型。 有效對象包括： <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
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
>如果沒 [!DNL Catalog] 有物件符合您請求中提供的ID，您仍可能收到HTTP狀態碼200，但回應陣列會是空的。
