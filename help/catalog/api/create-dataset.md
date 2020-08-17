---
keywords: Experience Platform;home;popular topics;dataset;Dataset;create a dataset;create dataset;enable dataset
solution: Experience Platform
title: 建立資料集
topic: developer guide
description: 本文檔介紹如何在目錄中建立資料集對象。
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 1%

---


# 建立資料集

若要使用 [!DNL Catalog] API建立資料集，您必須知 `$id` 道資料 [!DNL Experience Data Model] 集所依據的(XDM)架構值。 一旦您擁有架構ID，就可以透過對API中的端點提出POST要求來 `/datasets` 建立資 [!DNL Catalog] 料集。

>[!NOTE]
>
>本文檔僅介紹如何在中建立資料集對象 [!DNL Catalog]。 有關如何建立、填入和監視資料集的完整步驟，請參閱下列教 [學課程](../datasets/create.md)。

**API格式**

```HTTP
POST /dataSets
```

**請求**

下列請求會建立參照先前定義之架構的資料集。

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 要建立的資料集的名稱。 |
| `schemaRef.id` | 資料 `$id` 集所依據之XDM架構的URI值。 |

>[!NOTE]
>
>此示例使用 [parce](https://parquet.apache.org/documentation/latest/) file for its `containerFormat` property. 如需使用JSON檔案格式的範例，請參閱批次擷取開發 [人員指南](../../ingestion/batch-ingestion/api-overview.md)。

**回應**

成功的響應返回HTTP狀態201（已建立）和一個響應對象，該響應對象由一個陣列組成，該陣列包含以該格式新建立的資料集的ID `"@/datasets/{DATASET_ID}"`。 資料集ID是唯讀、系統產生的字串，用於在API呼叫中參考資料集。

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
