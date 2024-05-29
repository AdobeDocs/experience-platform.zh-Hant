---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；啟用資料集
title: 使用API啟用設定檔更新的資料集
type: Tutorial
description: 本教學課程說明如何使用Adobe Experience Platform API來啟用具有「更新插入」功能的資料集，以更新即時客戶設定檔資料。
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 6%

---

# 啟用資料集以使用API更新設定檔

本教學課程涵蓋以「更新插入」功能啟用資料集的程式，以更新即時客戶設定檔資料。 這包括建立新資料集和設定現有資料集的步驟。

>[!NOTE]
>
>本教學課程中說明的工作流程僅適用於批次擷取。 如需串流擷取更新插入，請參閱上的指南 [使用「資料準備」將部分列更新傳送至「即時客戶個人檔案」](../../data-prep/upserts.md).

## 快速入門

若要參閱本教學課程，請先實際瞭解管理已啟用設定檔的資料集所牽涉到的多項Adobe Experience Platform服務。 開始進行本教學課程之前，請先檢閱相關檔案 [!DNL Platform] 服務：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者個人檔案。
- [[!DNL Catalog Service]](../../catalog/home.md)：此RESTful API可讓您建立資料集並加以設定，用於 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Platform] 組織客戶體驗資料。
- [批次擷取](../../ingestion/batch-ingestion/overview.md)：批次擷取API可讓您將資料以批次檔案的形式擷取到Experience Platform中。

以下章節提供您需瞭解的其他資訊，才能成功呼叫Platform API。

### 讀取範例 API 呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集所需標頭的值

為了呼叫 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的 `Content-Type` 標頭。 必要時，此標頭的正確值會顯示在範例要求中。

中的所有資源 [!DNL Experience Platform] 會隔離至特定的虛擬沙箱。 所有要求至 [!DNL Platform] API需要 `x-sandbox-name` 標頭，指定執行作業的沙箱名稱。 如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

## 建立已啟用設定檔更新的資料集

建立新資料集時，您可以為設定檔啟用該資料集，並在建立時啟用更新功能。

>[!NOTE]
>
>若要建立新的已啟用設定檔的資料集，您必須知道已為設定檔啟用的現有XDM結構描述的ID。 如需如何查詢或建立已啟用設定檔的結構描述的詳細資訊，請參閱以下教學課程： [使用結構描述登入API建立結構描述](../../xdm/tutorials/create-schema-api.md).

若要建立已啟用設定檔和更新的資料集，請使用POST請求 `/dataSets` 端點。

**API格式**

```http
POST /dataSets
```

**要求**

藉由包含兩者 `unifiedIdentity` 和 `unifiedProfile` 在 `tags` 在請求內文中，將會啟用資料集 [!DNL Profile] 建立時。 在 `unifiedProfile` 陣列，新增 `isUpsert:true` 將新增資料集支援更新的功能。

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
| `schemaRef.id` | 的ID [!DNL Profile]資料集將依據的已啟用結構描述。 |
| `{TENANT_ID}` | 內的名稱空間 [!DNL Schema Registry] 包含屬於您組織的資源。 請參閱 [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) 的區段 [!DNL Schema Registry] 開發人員指南，以取得詳細資訊。 |

**回應**

成功的回應會顯示一個陣列，其中包含以形式建立之資料集的ID `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 設定現有的資料集 {#configure-an-existing-dataset}

下列步驟說明如何設定已啟用設定檔的現有資料集，以進行更新（更新插入）功能。

>[!NOTE]
>
>為了設定要更新插入的現有設定檔啟用的資料集，您必須先停用設定檔的資料集，然後隨著 `isUpsert` 標籤之間。 如果現有的資料集未針對設定檔啟用，您可以直接進行的步驟 [為設定檔和更新插入啟用資料集](#enable-the-dataset). 如果您不確定，下列步驟將說明如何檢查資料集是否已啟用。

### 檢查資料集是否已針對設定檔啟用

使用 [!DNL Catalog] API時，您可以檢查現有資料集以判斷是否已啟用它以用於中 [!DNL Real-Time Customer Profile]. 以下呼叫會依ID擷取資料集的詳細資料。

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
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "{VIEW_ID}",
        "files": "@/dataSetFiles?dataSetId=5b020a27e7040801dedbf46e",
        "schema": "{SCHEMA}",
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

在 `tags` 屬性，您會看到 `unifiedProfile` 與值同時存在 `enabled:true`. 因此， [!DNL Real-Time Customer Profile] 已針對此資料集啟用。

### 停用設定檔的資料集

若要設定已啟用設定檔的資料集以進行更新，您必須先停用 `unifiedProfile` 和 `unifiedIdentity` 標籤，並連同以下重新啟用它們 `isUpsert` 標籤之間。 這是使用兩個PATCH要求來完成，一次為停用，另一次為重新啟用。

>[!WARNING]
>
>在停用時擷取到資料集中的資料將不會擷取到設定檔存放區。 在為設定檔重新啟用資料之前，您應該避免將資料擷取到資料集中。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASET_ID}` | 您要更新之資料集的ID。 |

**要求**

第一個PATCH請求內文包含 `path` 至 `unifiedProfile` 和 `path` 至 `unifiedIdentity`，設定 `value` 至 `enabled:false` 以停用標籤。

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

成功的PATCH要求會傳回HTTP狀態200 （確定）以及包含已更新資料集ID的陣列。 此ID應符合PATCH請求中傳送的ID。 此 `unifiedProfile` 和 `unifiedIdentity` 標籤現已停用。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### 為設定檔和更新插入啟用資料集 {#enable-the-dataset}

現有資料集可以使用單一PATCH請求進行設定檔和屬性更新。

>[!IMPORTANT]
>
>為設定檔啟用資料集時，請確保與該資料集相關聯的結構描述為 **另外** 已啟用設定檔。 如果結構描述未啟用設定檔，資料集將會 **非** 在Platform UI中顯示為已啟用設定檔。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{DATASET_ID}` | 您要更新之資料集的ID。 |

**要求**

請求內文包含 `path` 至 `unifiedProfile` 設定 `value` 以包含 `enabled` 和 `isUpsert` 標籤，均設為 `true`，和 `path` 至 `unifiedIdentity` 設定 `value` 以包含 `enabled` 標籤已設為 `true`.

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

成功的PATCH要求會傳回HTTP狀態200 （確定）以及包含已更新資料集ID的陣列。 此ID應符合PATCH請求中傳送的ID。 此 `unifiedProfile` 標籤和 `unifiedIdentity` 標籤現在已啟用並設定用於屬性更新。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 後續步驟

批次擷取工作流程現在可以使用您的設定檔和已啟用更新插入的資料集，來更新設定檔資料。 若要進一步瞭解如何將資料擷取至Adobe Experience Platform，請先閱讀 [資料擷取概觀](../../ingestion/home.md).
