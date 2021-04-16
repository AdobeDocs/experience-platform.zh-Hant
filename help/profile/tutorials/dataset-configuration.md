---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；故障排除；API；啟用資料集
title: 使用API設定描述檔和身分服務的資料集
topic: 教學課程
type: Tutorial
description: 本教學課程示範如何啟用資料集以搭配使用Adobe Experience PlatformAPI的即時客戶個人檔案和身分服務。
exl-id: 142cb7df-072a-4f3a-8a9c-9a78afb35312
translation-type: tm+mt
source-git-commit: 87729e4996b0b2ac26e1a0abaa80af717825f9e6
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 1%

---

# 使用API為[!DNL Profile]和[!DNL Identity Service]配置資料集

本教學課程涵蓋啟用資料集以用於[!DNL Real-time Customer Profile]和[!DNL Identity Service]的程式，分為下列步驟：

1. 使用下列兩個選項之一，啟用資料集以供[!DNL Real-time Customer Profile]使用：
   - [建立新資料集](#create-a-dataset-enabled-for-profile-and-identity)
   - [設定現有資料集](#configure-an-existing-dataset)
1. [將資料收錄至資料集](#ingest-data-into-the-dataset)
1. [按即時客戶個人檔案確認資料收錄](#confirm-data-ingest-by-real-time-customer-profile)
1. [確認由Identity Service收錄的資料](#confirm-data-ingest-by-identity-service)

## 快速入門

本教學課程需要對管理[!DNL Profile]啟用資料集時涉及的各種Adobe Experience Platform服務有正確的理解。 在開始本教學課程之前，請先閱讀相關[!DNL Platform]服務的說明檔案：

- [[!DNL Real-time Customer Profile]](../home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
- [[!DNL Identity Service]](../../identity-service/home.md):可 [!DNL Real-time Customer Profile] 借由將不同資料來源的身分橋接到其中 [!DNL Platform]。
- [[!DNL Catalog Service]](../../catalog/home.md):REST風格的API，可讓您建立資料集，並設定資料 [!DNL Real-time Customer Profile] 集 [!DNL Identity Service]。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):組織客戶體驗資 [!DNL Platform] 料的標準化架構。

以下章節提供您必須知道的其他資訊，才能成功呼叫平台API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

- 授權：載體`{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

[!DNL Experience Platform]中的所有資源都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要進行操作的沙盒的名稱。 如需[!DNL Platform]中沙盒的詳細資訊，請參閱[沙盒概述檔案](../../sandboxes/home.md)。

- x-sandbox-name:`{SANDBOX_NAME}`

## 建立已啟用[!DNL Profile]和[!DNL Identity] {#create-a-dataset-enabled-for-profile-and-identity}的資料集

您可以在建立時或在建立資料集後的任何點立即啟用[!DNL Real-time Customer Profile]和[!DNL Identity Service]的資料集。 如果要啟用已建立的資料集，請遵循[配置本文檔稍後找到的現有資料集](#configure-an-existing-dataset)的步驟。 若要建立新資料集，您必須知道啟用即時客戶個人檔案的現有XDM架構的ID。 有關如何查找或建立啟用概要檔案的架構的資訊，請參見有關使用架構註冊表API](../../xdm/tutorials/create-schema-api.md)建立架構的[教程。 以下對[!DNL Catalog] API的調用為[!DNL Profile]和[!DNL Identity Service]啟用資料集。

**API格式**

```http
POST /dataSets
```

**要求**

借由在請求主體中的`tags`下方加入`unifiedProfile`和`unifiedIdentity`，資料集將會立即分別啟用[!DNL Profile]和[!DNL Identity Service]。 這些標籤的值必須是包含字串`"enabled:true"`的陣列。

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
| `{TENANT_ID}` | [!DNL Schema Registry]中包含屬於您IMS組織之資源的命名空間。 如需詳細資訊，請參閱[!DNL Schema Registry]開發人員指南的[TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id)一節。 |

**回應**

成功的響應顯示一個包含新建立資料集ID的陣列，其形式為`"@/dataSets/{DATASET_ID}"`。 成功建立並啟用資料集後，請繼續[上傳資料](#upload-data-to-the-dataset)的步驟。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 配置現有資料集{#configure-an-existing-dataset}

以下步驟介紹如何為[!DNL Real-time Customer Profile]和[!DNL Identity Service]啟用先前建立的資料集。 如果您已建立啟用設定檔的資料集，請繼續[擷取資料](#ingest-data-into-the-dataset)的步驟。

### 檢查資料集是否已啟用{#check-if-the-dataset-is-enabled}

使用[!DNL Catalog] API，您可以檢查現有資料集，以判斷它是否已啟用以用於[!DNL Real-time Customer Profile]和[!DNL Identity Service]。 下列呼叫會依ID擷取資料集的詳細資料。

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

在`tags`屬性下，您可以看到`unifiedProfile`和`unifiedIdentity`都與值`enabled:true`一起存在。 因此，[!DNL Real-time Customer Profile]和[!DNL Identity Service]分別啟用此資料集。

### 啟用資料集{#enable-the-dataset}

如果[!DNL Profile]或[!DNL Identity Service]尚未啟用現有資料集，則可使用資料集ID進行PATCH請求以啟用它。

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
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags" : {
        "unifiedProfile": ["enabled:true"],
        "unifiedIdentity": ["enabled:true"]
    }
  }'
```

請求主體包含`tags`屬性，其中包含兩個子屬性：`"unifiedProfile"`和`"unifiedIdentity"`。 這些子屬性的值是包含字串`"enabled:true"`的陣列。

**回**
應成功的PATCH請求會傳回HTTP狀態200（確定）和包含更新資料集ID的陣列。此ID應符合在PATCH請求中傳送的ID。 `"unifiedProfile"`和`"unifiedIdentity"`標籤現在已新增，且資料集已啟用供Profile和Identity Services使用。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 將資料收錄至資料集{#ingest-data-into-the-dataset}

[!DNL Real-time Customer Profile]和[!DNL Identity Service]在將XDM資料收錄到資料集時都會使用XDM資料。 有關如何將資料上傳至資料集的說明，請參閱[使用API建立資料集的教學課程。 ](../../catalog/datasets/create.md)在規劃要傳送哪些資料至啟用[!DNL Profile]的資料集時，請考慮下列最佳實務：

- 納入您要用作觀眾區隔標準的任何資料。
- 加入您從描述檔資料中可確定的盡可能多的識別碼，以最大化您的識別圖。 這可讓[!DNL Identity Service]更有效地將身分連接在資料集上。

## 確認由[!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}收錄資料

第一次上傳資料至新資料集，或是作為新ETL或資料來源相關程式的一部分，建議您仔細檢查資料，以確保資料已如預期上傳。 使用[!DNL Real-time Customer Profile]存取API，您可以在批次資料載入資料集時擷取其中的資料。 如果您無法擷取任何預期的實體，您的資料集可能無法啟用[!DNL Real-time Customer Profile]。 確認資料集已啟用後，請確定您的來源資料格式和識別碼支援您的期望。 有關如何使用[!DNL Real-time Customer Profile] API存取[!DNL Profile]資料的詳細說明，請遵循[實體端點指南](../api/entities.md)，亦稱為&quot;[!DNL Profile Access] API&quot;。

## 確認由Identity Service {#confirm-data-ingest-by-identity-service}進行的資料收錄

包含多個身分的每個已收錄資料片段會在您的私人身分圖表中建立連結。 有關身份圖和訪問身份資料的詳細資訊，請從閱讀[Identity Service概述](../../identity-service/home.md)開始。
