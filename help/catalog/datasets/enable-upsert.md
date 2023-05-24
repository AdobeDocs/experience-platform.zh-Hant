---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；故障排除；API；啟用資料集
title: 使用API為配置檔案更新啟用資料集
type: Tutorial
description: 本教程介紹如何使用Adobe Experience PlatformAPI啟用具有「upsert」功能的資料集，以便更新即時客戶配置檔案資料。
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 1%

---

# 使用API為配置檔案更新啟用資料集

本教程介紹如何啟用具有「upsert」功能的資料集，以便更新即時客戶配置檔案資料。 這包括建立新資料集和配置現有資料集的步驟。

>[!NOTE]
>
>upsert工作流僅用於批接收。 流攝入 **不** 支援。

## 快速入門

本教程要求對管理啟用Profile的資料集時涉及的幾個Adobe Experience Platform服務進行有效理解。 在開始本教程之前，請查閱相關文檔 [!DNL Platform] 服務：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。
- [[!DNL Catalog Service]](../../catalog/home.md):一個REST風格的API，允許您建立資料集並為 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service]。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。
- [批量攝取](../../ingestion/batch-ingestion/overview.md):批處理接收API允許您將資料作為批處理檔案接收到Experience Platform中。

以下各節提供了成功調用平台API所需的其他資訊。

### 讀取示例API調用

本教程提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

### 收集所需標題的值

為了呼叫 [!DNL Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

包含負載(POST、PUT、PATCH)的所有請求都需要 `Content-Type` 標題。 如有必要，此標頭的正確值將顯示在示例請求中。

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要 `x-sandbox-name` 用於指定操作將在中進行的沙盒名稱的標頭。 有關中的沙箱的詳細資訊 [!DNL Platform]，請參見 [沙盒概述文檔](../../sandboxes/home.md)。

## 建立啟用配置檔案更新的資料集

建立新資料集時，可以為配置檔案啟用該資料集並在建立時啟用更新功能。

>[!NOTE]
>
>要建立啟用配置檔案的新資料集，必須知道為配置檔案啟用的現有XDM架構的ID。 有關如何查找或建立啟用配置檔案的架構的資訊，請參見上的教程 [使用架構註冊表API建立架構](../../xdm/tutorials/create-schema-api.md)。

要建立為配置檔案和更新啟用的資料集，請使用POST請求 `/dataSets` 端點。

**API格式**

```http
POST /dataSets
```

**要求**

通過包括 `unifiedIdentity` 和 `unifiedProfile` 在 `tags` 在請求正文中，將為 [!DNL Profile] 創世時。 在 `unifiedProfile` 陣列，添加 `isUpsert:true` 將添加資料集支援更新的功能。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Sample dataset",
        "description: "A sample dataset with a sample description.",
        "fields": [],
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags": {
            "unifiedIdentity": [
                "enabled: true"
            ],
            "unifiedProfile": [
                "enabled: true",
                "isUpsert: true"
            ]
        }
      }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `schemaRef.id` | 的ID [!DNL Profile] — 啟用的模式，資料集將基於此模式。 |
| `{TENANT_ID}` | 中的命名空間 [!DNL Schema Registry] 包含屬於您組織的資源。 查看 [租戶ID](../../xdm/api/getting-started.md#know-your-tenant-id) 的下界 [!DNL Schema Registry] 詳細資訊。 |

**回應**

成功的響應顯示一個陣列，該陣列包含以下形式新建立的資料集的ID: `"@/dataSets/{DATASET_ID}"`。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 配置現有資料集 {#configure-an-existing-dataset}

以下步驟介紹如何配置現有啟用配置檔案的資料集以進行更新(upsert)功能。

>[!NOTE]
>
>為了為upsert配置現有啟用配置檔案的資料集，必須先禁用配置檔案的資料集，然後在 `isUpsert` 標籤。 如果未為配置檔案啟用現有資料集，則可以直接執行 [啟用Profile和upsert的資料集](#enable-the-dataset)。 如果不確定，以下步驟將顯示如何檢查資料集是否已啟用。

### 檢查是否為配置檔案啟用了資料集

使用 [!DNL Catalog] API，您可以檢查現有資料集以確定它是否在 [!DNL Real-Time Customer Profile]。 以下調用按ID檢索資料集的詳細資訊。

**API格式**

```http
GET /dataSets/{DATASET_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASET_ID}` | 要檢查的資料集的ID。 |

**要求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "{DATASET_NAME}",
        "imsOrg": "{ORG_ID}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ],
            "unifiedProfile": [
                "enabled:true"
            ]
        },
        "lastBatchId": "{BATCH_ID}",
        "lastBatchStatus": "success",
        "dule": {},
        "statsCache": {
            "startDate": null,
            "endDate": null
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "{VIEW_ID}",
        "status": "enabled",
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "{SCHEMA}",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

在 `tags` 屬性，你可以看到 `unifiedProfile` 值存在 `enabled:true`。 所以， [!DNL Real-Time Customer Profile] 已為此資料集啟用。

### 禁用配置檔案的資料集

為了配置啟用配置檔案的資料集進行更新，必須先禁用 `unifiedProfile` 和 `unifiedIdentity` 標籤，然後在 `isUpsert` 標籤。 這是使用兩個PATCH請求完成的，一個是禁用請求，另一個是重新啟用請求。

>[!WARNING]
>
>在禁用資料集時被攝取到資料集中的資料將不會被攝取到配置檔案儲存中。 應避免將資料插入資料集，直到重新啟用了配置檔案。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASET_ID}` | 要更新的資料集的ID。 |

**要求**

第一PATCH請求主體包括 `path` 至 `unifiedProfile` 和 `path` 至 `unifiedIdentity`，設定 `value` 至 `enabled:false` 以禁用標籤。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { 
            "op": "replace", 
            "path": "/tags/unifiedProfile", 
            "value": ["enabled:false"] 
        },
        {
            "op": "replace",
            "path": "/tags/unifiedIdentity",
            "value": ["enabled:false"]
        }
      ]'
```

**回應**

成功的PATCH請求返回HTTP狀態200(OK)和包含已更新資料集ID的陣列。 此ID應與在PATCH請求中發送的ID匹配。 的 `unifiedProfile` 和 `unifiedIdentity` 標籤現在已被禁用。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### 為配置檔案和upsert啟用資料集 {#enable-the-dataset}

可以使用單個PATCH請求為配置檔案和屬性更新啟用現有資料集。

>[!IMPORTANT]
>
>為配置檔案啟用資料集時，請確保與資料集關聯的架構是 **也** 已啟用配置檔案。 如果架構未啟用配置檔案，則資料集將 **不** 在平台UI中顯示為啟用了配置檔案。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASET_ID}` | 要更新的資料集的ID。 |

**要求**

請求主體包括 `path` 至 `unifiedProfile` 設定 `value` 包含 `enabled` 和 `isUpsert` 標籤，兩者均設定為 `true`的 `path` 至 `unifiedIdentity` 設定 `value` 包含 `enabled` 標籤設定為 `true`。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { 
            "op": "add", 
            "path": "/tags/unifiedProfile", 
            "value": [
                "enabled:true",
                "isUpsert:true"
            ] 
        },
        {
            "op": "add",
            "path": "/tags/unifiedIdentity",
            "value": [
                "enabled:true"
            ]
        }
      ]'
```

**回應**

成功的PATCH請求返回HTTP狀態200(OK)和包含已更新資料集ID的陣列。 此ID應與在PATCH請求中發送的ID匹配。 的 `unifiedProfile` 標籤和 `unifiedIdentity` 標籤現已啟用並配置為屬性更新。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 後續步驟

您的配置檔案和啟用更新的資料集現在可以由批處理接收工作流使用，以更新配置檔案資料。 要瞭解有關將資料導入Adobe Experience Platform的更多資訊，請首先閱讀 [資料攝取概述](../../ingestion/home.md)。
