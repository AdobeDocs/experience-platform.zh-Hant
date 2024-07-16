---
keywords: Experience Platform；首頁；熱門主題；資料集；資料集；建立資料集；建立資料集；啟用資料集
solution: Experience Platform
title: 在API中建立資料集
description: 本文介紹如何在目錄服務API中建立資料集物件。
exl-id: f3e5de7f-1781-4898-ac42-063eb51e661a
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 1%

---

# 在API中建立資料集

若要使用[!DNL Catalog] API建立資料集，您必須知道資料集將依據的[!DNL Experience Data Model] (XDM)結構描述的`$id`值。 一旦您擁有結構描述ID，您就可以對[!DNL Catalog] API中的`/datasets`端點發出POST要求來建立資料集。

>[!NOTE]
>
>本檔案僅說明如何在[!DNL Catalog]中建立資料集物件。 如需如何建立、填入及監控資料集的完整步驟，請參閱下列[教學課程](../datasets/create.md)。

**API格式**

```HTTP
POST /dataSets
```

**要求**

以下請求會建立參考先前定義之結構描述的資料集。

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
| `schemaRef.id` | 資料集將依據的XDM結構描述的URI `$id`值。 |
| `schemaRef.contentType` | 表示結構描述的格式和版本。 如需詳細資訊，請參閱XDM API指南中[架構版本設定](../../xdm/api/getting-started.md#versioning)的相關章節。 |

>[!NOTE]
>
>此範例將[Apache Parquet](https://parquet.apache.org/docs/)檔案格式用於其`containerFormat`屬性。 您可以在[批次擷取開發人員指南](../../ingestion/batch-ingestion/api-overview.md)中找到使用JSON檔案格式的範例。

**回應**

成功的回應會傳回HTTP狀態201 （已建立）和一個回應物件，該回應物件包含一個陣列，其中包含以`"@/datasets/{DATASET_ID}"`格式建立的新資料集識別碼。 資料集ID是系統產生的唯讀字串，用來參考API呼叫中的資料集。

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
