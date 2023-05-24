---
keywords: Experience Platform；首頁；熱門主題；資料集；資料集；建立資料集；建立資料集；啟用資料集
solution: Experience Platform
title: 在API中建立資料集
description: 本文檔介紹如何在目錄服務API中建立資料集對象。
exl-id: f3e5de7f-1781-4898-ac42-063eb51e661a
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---

# 在API中建立資料集

為使用 [!DNL Catalog] API，你必須知道 `$id` 值 [!DNL Experience Data Model] (XDM)資料集所基於的架構。 一旦您擁有了架構ID，就可以通過向 `/datasets` 端點 [!DNL Catalog] API。

>[!NOTE]
>
>此文檔僅介紹如何在中建立資料集對象 [!DNL Catalog]。 有關如何建立、填充和監視資料集的完整步驟，請參閱以下內容 [教程](../datasets/create.md)。

**API格式**

```HTTP
POST /dataSets
```

**要求**

以下請求建立引用先前定義的模式的資料集。

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
| `name` | 要建立的資料集的名稱。 |
| `schemaRef.id` | URI `$id` 資料集將基於的XDM模式的值。 |
| `schemaRef.contentType` | 指示架構的格式和版本。 請參閱 [架構版本](../../xdm/api/getting-started.md#versioning) 的子菜單。 |

>[!NOTE]
>
>此示例使用 [阿帕奇鑲木地板](https://parquet.apache.org/docs/) 檔案格式 `containerFormat` 屬性。 在中可找到使用JSON檔案格式的示例 [批量攝取顯影劑指南](../../ingestion/batch-ingestion/api-overview.md)。

**回應**

成功的響應返回HTTP狀態201（已建立）和響應對象，該響應對象由包含新建立資料集ID的陣列組成，格式為 `"@/datasets/{DATASET_ID}"`。 資料集ID是只讀的系統生成字串，用於在API調用中引用資料集。

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
