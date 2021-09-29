---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；啟用資料集
title: 使用API啟用資料集以進行設定檔更新
type: Tutorial
description: 本教學課程說明如何使用Adobe Experience Platform API來啟用具有「更新」功能的資料集，以便更新即時客戶設定檔資料。
source-git-commit: 3b34cf37182ae98545651a7b54f586df7d811f34
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 2%

---


# 使用API啟用資料集以進行設定檔更新

本教學課程涵蓋啟用具有「更新」功能的資料集以更新即時客戶個人檔案資料的程式。 這包括建立新資料集和設定現有資料集的步驟。

## 快速入門

本教學課程需要妥善了解管理啟用設定檔的資料集時涉及的數個Adobe Experience Platform服務。 開始本教學課程之前，請先檢閱這些相關DNL平台服務的檔案：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
- [[!DNL Catalog Service]](../../catalog/home.md):RESTful API可讓您建立資料集，並針對和進行 [!DNL Real-time Customer Profile] 設 [!DNL Identity Service]定。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):組織客戶體驗資 [!DNL Platform] 料的標準化架構。
- [批次擷取](../../ingestion/batch-ingestion/overview.md)

以下小節提供您需要了解的其他資訊，以便成功呼叫Platform API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[authentication tutorial](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有[!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的`Content-Type`標題。 如有需要，此標題的正確值會顯示在範例要求中。

[!DNL Experience Platform]中的所有資源都與特定虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要`x-sandbox-name`標頭，以指定要執行操作的沙箱名稱。 如需[!DNL Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

## 建立已啟用設定檔更新的資料集

建立新資料集時，您可以為「設定檔」啟用該資料集，並在建立時啟用更新功能。

>[!NOTE]
>
>若要建立啟用設定檔的新資料集，您必須知道已啟用設定檔的現有XDM結構的ID。 有關如何查找或建立啟用配置檔案的架構的資訊，請參閱有關使用架構註冊表API](../../xdm/tutorials/create-schema-api.md)建立架構的[教程。

若要建立已啟用「設定檔」和更新的資料集，請使用`/dataSets`端點的POST請求。

**API格式**

```http
POST /dataSets
```

**要求**

透過在要求內文的`tags`底下加入`unifiedProfile`，資料集將在建立時啟用[!DNL Profile]。 在`unifiedProfile`陣列中，新增`isUpsert:true`即可讓資料集支援更新。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "fields":[],
        "schemaRef" : {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
          "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags" : {
          "unifiedProfile": [
            "enabled:true",
            "isUpsert:true"
          ]
        }
      }'
```

| 屬性 | 說明 |
|---|---|
| `schemaRef.id` | 資料集所依據之[!DNL Profile]啟用架構的ID。 |
| `{TENANT_ID}` | [!DNL Schema Registry]中的命名空間，其中包含屬於您IMS組織的資源。 如需詳細資訊，請參閱[!DNL Schema Registry]開發人員指南的[ TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id)一節。 |

**回應**

成功的回應會顯示一個陣列，內含以`"@/dataSets/{DATASET_ID}"`形式建立之新資料集的ID。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 設定現有資料集 {#configure-an-existing-dataset}

下列步驟說明如何設定現有已啟用設定檔的資料集以進行更新(「upsert」)功能。

>[!NOTE]
>
>若要為「upsert」設定現有啟用設定檔的資料集，您必須先停用「設定檔」的資料集，然後在`isUpsert`標籤旁重新啟用該資料集。 如果沒有為「設定檔」啟用現有資料集，您可以直接執行[為「設定檔」啟用資料集和upsert](#enable-the-dataset)的步驟。 如果您不確定，下列步驟會示範如何檢查資料集是否已啟用。

### 檢查資料集是否已啟用設定檔

使用[!DNL Catalog] API可以檢查現有資料集，以判斷資料集是否已啟用以用於[!DNL Real-time Customer Profile]。 下列呼叫會依ID擷取資料集的詳細資訊。

**API格式**

```http
GET /dataSets/{DATASET_ID}
```

| 參數 | 說明 |
|---|---|
| `{DATASET_ID}` | 您要檢查的資料集ID。 |

**要求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "{DATASET_NAME}",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
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

在`tags`屬性下，您會看到`unifiedProfile`與值`enabled:true`一起存在。 因此，此資料集已啟用[!DNL Real-time Customer Profile]。

### 停用設定檔的資料集

若要設定已啟用設定檔的資料集以進行更新，您必須先停用`unifiedProfile`標籤，然後在`isUpsert`標籤旁重新啟用該標籤。 這是使用兩個PATCH請求來完成，一個是停用，另一個是重新啟用。

>[!WARNING]
>
>停用時擷取至資料集的資料不會擷取至設定檔存放區。 建議您在重新啟用設定檔之前，避免將資料擷取到資料集中。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 參數 | 說明 |
|---|---|
| `{DATASET_ID}` | 您要更新的資料集ID。 |

**要求**

第一個PATCH請求內文包含`path`至`unifiedProfile`，將`value`設為`enabled:false`以停用標籤。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "replace", "path": "/tags/unifiedProfile", "value": ["enabled:false"] },
      ]'
```

****
回應成功的PATCH要求會傳回HTTP狀態200（確定），以及包含已更新資料集ID的陣列。此ID應符合PATCH請求中傳送的ID。 `unifiedProfile`標籤現已停用。

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
|---|---|
| `{DATASET_ID}` | 您要更新的資料集ID。 |

**要求**

請求內文包含`path`至`unifiedProfile`，將`value`設定為包含`enabled`和`isUpsert`標籤，兩者均設為`true`。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true","isUpsert:true"] },
      ]'
```

****
回應成功的PATCH要求會傳回HTTP狀態200（確定），以及包含已更新資料集ID的陣列。此ID應符合PATCH請求中傳送的ID。 `unifiedProfile`標籤現在已啟用並設定，以進行屬性更新。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 後續步驟

您的設定檔和已啟用更新的資料集現在可透過批次和串流擷取工作流程，對設定檔資料進行更新。 若要進一步了解如何將資料擷取至Adobe Experience Platform，請先閱讀[資料擷取概述](../../ingestion/home.md)。
