---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；啟用資料集
title: 使用API設定設定檔與身分服務的資料集
topic-legacy: tutorial
type: Tutorial
description: 本教學課程說明如何使用Adobe Experience Platform API啟用資料集，以便與即時客戶個人檔案和身分服務搭配使用。
exl-id: 142cb7df-072a-4f3a-8a9c-9a78afb35312
source-git-commit: bcca4d6212ee3f0d661549eca359ab8c8aaf905c
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 1%

---

# 使用API為[!DNL Profile]和[!DNL Identity Service]設定資料集

本教學課程涵蓋啟用資料集以用於[!DNL Real-time Customer Profile]和[!DNL Identity Service]的程式，並細分為下列步驟：

1. 使用下列兩個選項之一，啟用資料集以用於[!DNL Real-time Customer Profile]:
   - [建立新資料集](#create-a-dataset-enabled-for-profile-and-identity)
   - [設定現有資料集](#configure-an-existing-dataset)
1. [將資料內嵌至資料集](#ingest-data-into-the-dataset)
1. [按即時客戶設定檔確認資料內嵌](#confirm-data-ingest-by-real-time-customer-profile)
1. [確認由Identity Service擷取的資料](#confirm-data-ingest-by-identity-service)

## 快速入門

本教學課程需要妥善了解管理[!DNL Profile]啟用資料集時涉及的各種Adobe Experience Platform服務。 開始本教學課程之前，請先檢閱以下相關[!DNL Platform]服務的檔案：

- [[!DNL Real-time Customer Profile]](../home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
- [[!DNL Identity Service]](../../identity-service/home.md):可透 [!DNL Real-time Customer Profile] 過從擷取到的不同資料來源橋接身分來 [!DNL Platform]啟用。
- [[!DNL Catalog Service]](../../catalog/home.md):RESTful API可讓您建立資料集，並針對和進行 [!DNL Real-time Customer Profile] 設 [!DNL Identity Service]定。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):組織客戶體驗資 [!DNL Platform] 料的標準化架構。

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

## 建立為[!DNL Profile]和[!DNL Identity]啟用的資料集 {#create-a-dataset-enabled-for-profile-and-identity}

您可以在建立時或在建立資料集後的任何時間點立即啟用[!DNL Real-time Customer Profile]和[!DNL Identity Service]的資料集。 如果要啟用已建立的資料集，請按照以下步驟操作： [配置本文檔後面找到的現有資料集](#configure-an-existing-dataset)。 若要建立新資料集，您必須知道已啟用「即時客戶個人檔案」的現有XDM結構的ID。 有關如何查找或建立啟用配置檔案的架構的資訊，請參閱有關使用架構註冊表API](../../xdm/tutorials/create-schema-api.md)建立架構的[教程。 以下對[!DNL Catalog] API的呼叫會啟用[!DNL Profile]和[!DNL Identity Service]的資料集。

**API格式**

```http
POST /dataSets
```

**要求**

透過在要求內文的`tags`下加入`unifiedProfile`和`unifiedIdentity`，資料集將分別立即啟用[!DNL Profile]和[!DNL Identity Service]。 這些標籤的值必須是包含字串`"enabled:true"`的陣列。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fileDescription" : {
        "persisted": true
    },
    "fields":[],
    "schemaRef" : {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
    },
    "tags" : {
       "unifiedProfile": ["enabled:true"],
       "unifiedIdentity": ["enabled:true"]
    }
  }'
```

| 屬性 | 說明 |
|---|---|
| `schemaRef.id` | 資料集所依據之[!DNL Profile]啟用架構的ID。 |
| `{TENANT_ID}` | [!DNL Schema Registry]中的命名空間，其中包含屬於您IMS組織的資源。 如需詳細資訊，請參閱[!DNL Schema Registry]開發人員指南的[ TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id)一節。 |

**回應**

成功的回應會顯示一個陣列，內含以`"@/dataSets/{DATASET_ID}"`形式建立之新資料集的ID。 成功建立並啟用資料集後，請繼續執行[上傳資料](#upload-data-to-the-dataset)的步驟。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 設定現有資料集 {#configure-an-existing-dataset}

下列步驟說明如何為[!DNL Real-time Customer Profile]和[!DNL Identity Service]啟用先前建立的資料集。 如果您已建立已啟用設定檔的資料集，請繼續執行[擷取資料](#ingest-data-into-the-dataset)的步驟。

### 檢查資料集是否已啟用 {#check-if-the-dataset-is-enabled}

使用[!DNL Catalog] API，您可以檢查現有資料集，以判斷資料集是否已啟用以用於[!DNL Real-time Customer Profile]和[!DNL Identity Service]。 下列呼叫會依ID擷取資料集的詳細資訊。

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
        "name": "Commission Program Events DataSet",
        "imsOrg": "{IMS_ORG}",
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
        "fileDescription": {
            "persisted": true
        },
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "@/xdms/context/experienceevent",
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

在`tags`屬性下，您會看到`unifiedProfile`和`unifiedIdentity`都與值`enabled:true`存在。 因此，會分別為此資料集啟用[!DNL Real-time Customer Profile]和[!DNL Identity Service]。

### 啟用資料集 {#enable-the-dataset}

如果尚未為[!DNL Profile]或[!DNL Identity Service]啟用現有資料集，您可以使用資料集ID提出PATCH請求來啟用該資料集。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true"] },
        { "op": "add", "path": "/tags/unifiedIdentity", "value": ["enabled:true"] }	
      ]'
```

要求內文包含`path`和`unifiedIdentity`這兩種類型的標籤。 `unifiedProfile`每個的`value`是包含字串`enabled:true`的陣列。

****
回應成功的PATCH要求會傳回HTTP狀態200（確定），以及包含已更新資料集ID的陣列。此ID應符合PATCH請求中傳送的ID。 現在已新增`unifiedProfile`和`unifiedIdentity`標籤，且資料集已啟用，供設定檔和Identity服務使用。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 將資料內嵌至資料集 {#ingest-data-into-the-dataset}

[!DNL Real-time Customer Profile]和[!DNL Identity Service]會在擷取至資料集時使用XDM資料。 如需如何將資料上傳至資料集的指示，請參閱有關使用API](../../catalog/datasets/create.md)建立資料集的[教學課程。 規劃要傳送哪些資料至已啟用[!DNL Profile]的資料集時，請考慮下列最佳實務：

- 納入您要用作受眾區隔條件的任何資料。
- 納入您從設定檔資料中可確定的盡可能多的識別碼，以最大化您的身分圖表。 這可讓[!DNL Identity Service]更有效地拼接資料集間的身分。

## 確認[!DNL Real-time Customer Profile]資料內嵌 {#confirm-data-ingest-by-real-time-customer-profile}

第一次將資料上傳至新資料集時，或是在涉及新ETL或資料來源的程式中，建議您仔細檢查資料，以確保資料已如預期般上傳。 使用[!DNL Real-time Customer Profile]存取API，您可以在將批次資料載入資料集時擷取該資料。 如果您無法擷取任何預期的實體，您的資料集可能無法啟用[!DNL Real-time Customer Profile]。 確認資料集已啟用後，請確定來源資料格式和識別碼支援您的期望。 有關如何使用[!DNL Real-time Customer Profile] API訪問[!DNL Profile]資料的詳細說明，請遵循[entities端點指南](../api/entities.md)，也稱為「[!DNL Profile Access] API」。

## 確認由Identity Service擷取的資料 {#confirm-data-ingest-by-identity-service}

擷取的每個包含多個身分的資料片段，會在您的私人身分圖表中建立連結。 有關身份圖和訪問身份資料的詳細資訊，請從閱讀[Identity服務概述](../../identity-service/home.md)開始。
