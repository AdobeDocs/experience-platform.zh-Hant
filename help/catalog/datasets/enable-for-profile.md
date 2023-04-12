---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；啟用資料集
title: 使用API啟用設定檔與身分服務的資料集
type: Tutorial
description: 本教學課程說明如何使用Adobe Experience Platform API啟用資料集，以便與即時客戶個人檔案和身分服務搭配使用。
exl-id: a115e126-6775-466d-ad7e-ee36b0b8b49c
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 1%

---

# 為啟用資料集 [!DNL Profile] 和 [!DNL Identity Service] 使用API

本教學課程涵蓋啟用資料集以用於 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service]，細分為下列步驟：

1. 啟用資料集以用於 [!DNL Real-Time Customer Profile]，使用下列兩個選項之一：
   - [建立新資料集](#create-a-dataset-enabled-for-profile-and-identity)
   - [設定現有資料集](#configure-an-existing-dataset)
1. [將資料內嵌至資料集](#ingest-data-into-the-dataset)
1. [按即時客戶設定檔確認資料內嵌](#confirm-data-ingest-by-real-time-customer-profile)
1. [確認由Identity Service擷取的資料](#confirm-data-ingest-by-identity-service)

## 快速入門

本教學課程需要妥善了解管理啟用設定檔的資料集時涉及的數個Adobe Experience Platform服務。 開始本教學課程之前，請檢閱這些相關檔案 [!DNL Platform] 服務：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
- [[!DNL Identity Service]](../../identity-service/home.md):啟用 [!DNL Real-Time Customer Profile] 將不同資料來源的身分擷取至 [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md):RESTful API可讓您建立資料集，並針對 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。

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

## 建立為「設定檔與身分」啟用的資料集 {#create-a-dataset-enabled-for-profile-and-identity}

您可以在建立資料集時或建立資料集後的任何時間點，立即啟用「即時客戶個人檔案與身分服務」的資料集。 如果您要啟用已建立的資料集，請依照 [設定現有資料集](#configure-an-existing-dataset) 在本檔案的後面找到。

>[!NOTE]
>
>若要建立啟用設定檔的新資料集，您必須知道已啟用設定檔的現有XDM結構的ID。 如需如何查詢或建立已啟用設定檔的結構的詳細資訊，請參閱 [使用方案註冊表API建立結構](../../xdm/tutorials/create-schema-api.md).

若要建立已啟用「設定檔」的資料集，您可以使用POST請求 `/dataSets` 端點。

**API格式**

```http
POST /dataSets
```

**要求**

包括 `unifiedProfile` 和 `unifiedIdentity` 在 `tags` 請求內文會立即為啟用資料集 [!DNL Profile] 和 [!DNL Identity Service]，分別為。 這些標籤的值必須是包含字串的陣列 `"enabled:true"`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields":[],
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
    },
    "tags": {
       "unifiedProfile": ["enabled:true"],
       "unifiedIdentity": ["enabled:true"]
    }
  }'
```

| 屬性 | 說明 |
|---|---|
| `schemaRef.id` | 的ID [!DNL Profile] — 啟用資料集的基礎架構。 |
| `{TENANT_ID}` | 中的命名空間 [!DNL Schema Registry] 其中包含您組織的資源。 請參閱 [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) 區段 [!DNL Schema Registry] 開發人員指南，以取得詳細資訊。 |

**回應**

成功的回應會以下列形式顯示包含新建立資料集ID的陣列： `"@/dataSets/{DATASET_ID}"`. 成功建立並啟用資料集後，請繼續執行 [上傳資料](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 設定現有資料集 {#configure-an-existing-dataset}

下列步驟說明如何為啟用先前建立的資料集 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service]. 如果您已建立已啟用設定檔的資料集，請繼續進行 [擷取資料](#ingest-data-into-the-dataset).

### 檢查資料集是否已啟用 {#check-if-the-dataset-is-enabled}

使用 [!DNL Catalog] API，您可以檢查現有的資料集，以判斷資料集是否已啟用並用於 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service]. 下列呼叫會依ID擷取資料集的詳細資訊。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "Commission Program Events DataSet",
        "imsOrg": "{ORG_ID}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedProfile": [
                "enabled:true"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ]
        },
        "lastBatchId": "6dcd9128a1c84e6aa5177641165e18e4",
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
        "viewId": "5b020a27e7040801dedbf46f",
        "status": "enabled",
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "@/xdms/context/experienceevent",
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

在 `tags` 屬性，您可以看到 `unifiedProfile` 和 `unifiedIdentity` 都與值存在 `enabled:true`. 因此， [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service] 已針對此資料集啟用。

### 啟用資料集 {#enable-the-dataset}

如果尚未為啟用現有資料集 [!DNL Profile] 或 [!DNL Identity Service]，您可以使用資料集ID提出PATCH請求來啟用。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 參數 | 說明 |
|---|---|
| `{DATASET_ID}` | 您要更新的資料集ID。 |

**要求**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true"] },
        { "op": "add", "path": "/tags/unifiedIdentity", "value": ["enabled:true"] } 
      ]'
```

請求內文包含 `path` 兩種標籤， `unifiedProfile` 和 `unifiedIdentity`. 此 `value` 每個都是包含字串的陣列 `enabled:true`.

**回應**

成功的PATCH要求會傳回HTTP狀態200（確定），以及包含更新資料集ID的陣列。 此ID應符合PATCH請求中傳送的ID。 此 `unifiedProfile` 和 `unifiedIdentity` 標籤現已新增，且資料集已啟用，供「設定檔」和「身分識別」服務使用。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 將資料內嵌至資料集 {#ingest-data-into-the-dataset}

兩者 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service] 將XDM資料擷取至資料集時使用。 如需如何將資料上傳至資料集的指示，請參閱 [使用API建立資料集](../../catalog/datasets/create.md). 規劃要傳送哪些資料至您的 [!DNL Profile]啟用資料集時，請考量下列最佳實務：

- 納入您要用作區段條件的任何資料。
- 納入您從設定檔資料中可確定的盡可能多的識別碼，以最大化您的身分圖表。 這允許 [!DNL Identity Service] 更有效地拼接資料集的身分。

## 確認資料內嵌方式 [!DNL Real-Time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

第一次將資料上傳至新資料集時，或是在涉及新ETL或資料來源的程式中，建議您仔細檢查資料，以確保資料已如預期般上傳。 使用 [!DNL Real-Time Customer Profile] 存取API時，您可以在批次資料載入至資料集時加以擷取。 如果您無法擷取任何預期的實體，資料集可能無法啟用 [!DNL Real-Time Customer Profile]. 確認資料集已啟用後，請確定來源資料格式和識別碼支援您的期望。 如需如何使用 [!DNL Real-Time Customer Profile] 存取API [!DNL Profile] 資料，請參閱 [entities endpoint guide（圖元端點指南）](../../profile/api/entities.md)，也稱為「[!DNL Profile Access]&quot; API.

## 確認由Identity Service擷取的資料 {#confirm-data-ingest-by-identity-service}

擷取的每個包含多個身分的資料片段，會在您的私人身分圖表中建立連結。 如需身分圖表和存取身分資料的詳細資訊，請先閱讀 [Identity服務概述](../../identity-service/home.md).
