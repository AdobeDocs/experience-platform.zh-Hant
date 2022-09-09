---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；啟用資料集
title: 使用API啟用資料集以進行設定檔更新
type: Tutorial
description: 本教學課程說明如何使用Adobe Experience Platform API來啟用具有「更新」功能的資料集，以便更新即時客戶設定檔資料。
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: 5bd3e43e6b307cc1527e8734936c051fb4fc89c4
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 1%

---

# 使用API啟用資料集以進行設定檔更新

本教學課程涵蓋啟用具有「更新」功能的資料集以更新即時客戶個人檔案資料的程式。 這包括建立新資料集和設定現有資料集的步驟。

>[!NOTE]
>
>更新工作流程只適用於批次內嵌。 串流內嵌是 **not** 支援。

## 快速入門

本教學課程需要妥善了解管理啟用設定檔的資料集時涉及的數個Adobe Experience Platform服務。 開始本教學課程之前，請檢閱這些相關檔案 [!DNL Platform] 服務：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
- [[!DNL Catalog Service]](../../catalog/home.md):RESTful API可讓您建立資料集，並針對 [!DNL Real-time Customer Profile] 和 [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。
- [批次內嵌](../../ingestion/batch-ingestion/overview.md):批次內嵌API可讓您將資料以批次檔案的形式內嵌至Experience Platform。

以下小節提供您需要了解的其他資訊，以便成功呼叫Platform API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

若要對 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的 `Content-Type` 頁首。 如有需要，此標題的正確值會顯示在範例要求中。

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要 `x-sandbox-name` 用於指定操作將進行的沙箱名稱的標頭。 如需中沙箱的詳細資訊，請參閱 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

## 建立已啟用設定檔更新的資料集

建立新資料集時，您可以為「設定檔」啟用該資料集，並在建立時啟用更新功能。

>[!NOTE]
>
>若要建立啟用設定檔的新資料集，您必須知道已啟用設定檔的現有XDM結構的ID。 如需如何查詢或建立已啟用設定檔的結構的詳細資訊，請參閱 [使用方案註冊表API建立結構](../../xdm/tutorials/create-schema-api.md).

若要建立已啟用「設定檔」和更新的資料集，請使用POST請求 `/dataSets` 端點。

**API格式**

```http
POST /dataSets
```

**要求**

將 `unifiedIdentity` 和 `unifiedProfile` 在 `tags` 在請求內文中，資料集將啟用 [!DNL Profile] 建立時。 在 `unifiedProfile` 陣列，添加 `isUpsert:true` 將新增資料集支援更新的功能。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
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
| `schemaRef.id` | 的ID [!DNL Profile] — 啟用資料集的基礎架構。 |
| `{TENANT_ID}` | 中的命名空間 [!DNL Schema Registry] 其中包含您組織的資源。 請參閱 [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) 區段 [!DNL Schema Registry] 開發人員指南，以取得詳細資訊。 |

**回應**

成功的回應會以下列形式顯示包含新建立資料集ID的陣列： `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 設定現有資料集 {#configure-an-existing-dataset}

下列步驟說明如何設定現有已啟用設定檔的資料集，以便進行更新（更新）功能。

>[!NOTE]
>
>若要設定現有的已啟用設定檔的資料集以進行更新，您必須先停用設定檔的資料集，然後在啟用資料集的同時重新啟用 `isUpsert` 標籤。 如果沒有為「設定檔」啟用現有資料集，您可以直接執行 [啟用「設定檔」資料集並重新插入](#enable-the-dataset). 如果您不確定，下列步驟會示範如何檢查資料集是否已啟用。

### 檢查資料集是否已啟用設定檔

使用 [!DNL Catalog] API，您可以檢查現有的資料集，以判斷資料集是否已啟用並用於 [!DNL Real-time Customer Profile]. 下列呼叫會依ID擷取資料集的詳細資訊。

**API格式**

```http
GET /dataSets/{DATASET_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASET_ID}` | 您要檢查的資料集ID。 |

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
            "dule": [],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

在 `tags` 屬性，您可以看到 `unifiedProfile` 值存在 `enabled:true`. 因此， [!DNL Real-time Customer Profile] 已針對此資料集啟用。

### 停用設定檔的資料集

若要設定啟用設定檔的資料集以進行更新，您必須先停用 `unifiedProfile` 和 `unifiedIdentity` 標籤，然後在 `isUpsert` 標籤。 這是使用兩個PATCH請求來完成，一個是停用，另一個是重新啟用。

>[!WARNING]
>
>停用時擷取至資料集的資料不會擷取至設定檔存放區。 在重新啟用設定檔之前，您應避免將資料擷取至資料集。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASET_ID}` | 您要更新的資料集ID。 |

**要求**

第一PATCH請求內文包含 `path` to `unifiedProfile` 和 `path` to `unifiedIdentity`，設定 `value` to `enabled:false` 來停用標籤。

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

成功的PATCH要求會傳回HTTP狀態200（確定），以及包含更新資料集ID的陣列。 此ID應符合PATCH請求中傳送的ID。 此 `unifiedProfile` 和 `unifiedIdentity` 標籤現已停用。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### 啟用設定檔資料集並重新插入 {#enable-the-dataset}

現有資料集可使用單一PATCH請求來啟用設定檔和屬性更新。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASET_ID}` | 您要更新的資料集ID。 |

**要求**

請求內文包含 `path` to `unifiedProfile` 設定 `value` 包括 `enabled` 和 `isUpsert` 標籤，都設為 `true`和 `path` to `unifiedIdentity` 設定 `value` 包括 `enabled` 標籤設為 `true`.

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

成功的PATCH要求會傳回HTTP狀態200（確定），以及包含更新資料集ID的陣列。 此ID應符合PATCH請求中傳送的ID。 此 `unifiedProfile` 標籤和 `unifiedIdentity` 標籤現在已啟用，並已針對屬性更新進行設定。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 後續步驟

您的設定檔和已啟用更新的資料集現在可透過批次擷取工作流程來更新設定檔資料。 若要進一步了解將資料擷取至Adobe Experience Platform，請先閱讀 [資料擷取概觀](../../ingestion/home.md).
