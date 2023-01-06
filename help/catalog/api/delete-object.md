---
keywords: Experience Platform；首頁；熱門主題；刪除物件；目錄服務；api
solution: Experience Platform
title: 刪除API中的物件
description: 您可以在目錄請求的路徑中提供其ID，以刪除目錄物件。
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 1%

---

# 刪除API中的物件

您可以刪除 [!DNL Catalog] 物件，在DELETE請求的路徑中提供其ID。

>[!WARNING]
>
>刪除物件時請格外小心，因為此動作無法還原，且可能會在中的其他位置產生中斷變更 [!DNL Experience Platform].

**API格式**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>此 `DELETE /batches/{ID}` 已棄用端點。 若要刪除批次，您應使用 [批次內嵌API](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch).

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 類型 [!DNL Catalog] 要刪除的對象。 有效對象包括： <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要更新的特定對象的標識符。 |

**要求**

下列請求會刪除請求路徑中指定ID的資料集。

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200(OK)，以及包含已刪除資料集ID的陣列。 此ID應符合DELETE請求中傳送的ID。 對已刪除的物件執行GET要求時，會傳回HTTP狀態404（找不到），確認資料集已成功刪除。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>若否 [!DNL Catalog] 物件符合要求中提供的ID，您仍可能收到HTTP狀態代碼200，但回應陣列將會是空的。
