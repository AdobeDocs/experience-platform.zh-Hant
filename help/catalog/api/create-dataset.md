---
keywords: Experience Platform；首頁；熱門主題；資料集；資料集；建立資料集；建立資料集；啟用資料集
solution: Experience Platform
title: 在API中建立資料集
description: 本檔案說明如何在目錄服務API中建立資料集物件。
exl-id: f3e5de7f-1781-4898-ac42-063eb51e661a
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---

# 在API中建立資料集

若要使用 [!DNL Catalog] API，您必須知道 `$id` 值 [!DNL Experience Data Model] (XDM)資料集所依據的結構。 取得結構ID後，您就可以向 `/datasets` 端點 [!DNL Catalog] API。

>[!NOTE]
>
>本檔案僅說明如何在 [!DNL Catalog]. 如需建立、填入和監控資料集的完整步驟，請參閱下列內容 [教學課程](../datasets/create.md).

**API格式**

```HTTP
POST /dataSets
```

**要求**

下列請求會建立參考先前定義結構的資料集。

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 要建立的資料集名稱。 |
| `schemaRef.id` | URI `$id` 資料集所根據之XDM架構的值。 |
| `schemaRef.contentType` | 指示架構的格式和版本。 請參閱 [方案版本設定](../../xdm/api/getting-started.md#versioning) （位於XDM API指南中）以取得詳細資訊。 |

>[!NOTE]
>
>此範例使用 [阿帕奇鑲木地板](https://parquet.apache.org/docs/) 檔案格式 `containerFormat` 屬性。 若需使用JSON檔案格式的範例，請參閱 [批次匯入開發人員指南](../../ingestion/batch-ingestion/api-overview.md).

**回應**

成功的回應會傳回HTTP狀態201（已建立），而回應物件則由陣列組成，陣列內含新建立資料集的ID，格式為 `"@/datasets/{DATASET_ID}"`. 資料集ID是唯讀、系統產生的字串，用於在API呼叫中參考資料集。

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
