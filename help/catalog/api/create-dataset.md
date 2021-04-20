---
keywords: Experience Platform;home；熱門主題；dataset;Dataset；建立資料集；建立資料集；啟用資料集
solution: Experience Platform
title: 在API中建立資料集
topic: developer guide
description: 本檔案說明如何在Catalog Service API中建立資料集物件。
exl-id: f3e5de7f-1781-4898-ac42-063eb51e661a
translation-type: tm+mt
source-git-commit: 727c9dbd87bacfd0094ca29157a2d0283c530969
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---

# 在API中建立資料集

要使用[!DNL Catalog] API建立資料集，您必須知道資料集所基於的[!DNL Experience Data Model](XDM)模式的`$id`值。 一旦擁有架構ID，您就可以透過對[!DNL Catalog] API中的`/datasets`端點發出POST請求來建立資料集。

>[!NOTE]
>
>本文檔僅涵蓋如何在[!DNL Catalog]中建立資料集物件。 有關如何建立、填充和監視資料集的完整步驟，請參閱以下[教程](../datasets/create.md)。

**API格式**

```HTTP
POST /dataSets
```

**要求**

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
    }
}'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 要建立的資料集的名稱。 |
| `schemaRef.id` | 資料集將基於的XDM模式的URI `$id`值。 |
| `schemaRef.contentType` | 指示方案的格式和版本。 如需詳細資訊，請參閱XDM API指南中有關[架構版本控制](../../xdm/api/getting-started.md#versioning)的章節。 |

>[!NOTE]
>
>此示例使用[Apache Parce](https://parquet.apache.org/documentation/latest/)檔案格式作為其`containerFormat`屬性。 使用JSON檔案格式的範例，請參閱[批次擷取開發人員指南](../../ingestion/batch-ingestion/api-overview.md)。

**回應**

成功的響應返回HTTP狀態201（已建立）和一個響應對象，該響應對象由一個陣列組成，該陣列包含以`"@/datasets/{DATASET_ID}"`格式新建立的資料集的ID。 資料集ID是唯讀、系統產生的字串，用於在API呼叫中參考資料集。

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
