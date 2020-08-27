---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;enable dataset
solution: Adobe Experience Platform
title: 使用API為Profile and Identity Service設定資料集
topic: tutorial
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 1%

---


# 為API設定資 [!DNL Profile] 料 [!DNL Identity Service] 集

本教學課程涵蓋啟用資料集以用於和 [!DNL Real-time Customer Profile] 的 [!DNL Identity Service]程式，分為下列步驟：

1. 使用下列兩個選項之 [!DNL Real-time Customer Profile]一，啟用資料集以供使用：
   - [建立新資料集](#create-a-dataset-enabled-for-profile-and-identity)
   - [設定現有資料集](#configure-an-existing-dataset)
1. [將資料收錄至資料集](#ingest-data-into-the-dataset)
1. [按即時客戶個人檔案確認資料收錄](#confirm-data-ingest-by-real-time-customer-profile)
1. [確認由Identity Service收錄的資料](#confirm-data-ingest-by-identity-service)

## 快速入門

本教學課程需要有效瞭解管理啟用資料集時涉及的各種Adobe Experience Platform [!DNL Profile]服務。 在開始本教學課程之前，請先閱讀這些相關服務的 [!DNL Platform] 檔案：

- [[!DNL即時客戶基本資料]](../home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
- [[!DNL Identity Service]](../../identity-service/home.md):可借 [!DNL Real-time Customer Profile] 由橋接來自不同資料來源的身分識別，並將之收錄在 [!DNL Platform]中。
- [[!DNL目錄服務]](../../catalog/home.md):REST風格的API，可讓您建立資料集，並設定資料集 [!DNL Real-time Customer Profile] 和 [!DNL Identity Service]。
- [[!DNL體驗資料模型(XDM)]](../../xdm/home.md):組織客戶體驗資料 [!DNL Platform] 的標準化架構。

以下章節提供您必須知道的其他資訊，才能成功呼叫平台API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

- 授權：生產者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

中的所有資 [!DNL Experience Platform] 源都與特定虛擬沙盒隔離。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要進行操作的沙盒名稱。 如需中沙盒的詳細資訊 [!DNL Platform]，請參閱沙 [盒概述檔案](../../sandboxes/home.md)。

- x-sandbox-name: `{SANDBOX_NAME}`

## 建立啟用和的資 [!DNL Profile] 料集 [!DNL Identity] {#create-a-dataset-enabled-for-profile-and-identity}

您可以在建立資料集 [!DNL Real-time Customer Profile] 時或 [!DNL Identity Service] 在建立資料集後的任何時間點，立即啟用資料集。 如果您想要啟用已建立的資料集，請依照本檔案稍後 [找到的現有資料集](#configure-an-existing-dataset) ，設定步驟。 若要建立新資料集，您必須知道啟用即時客戶個人檔案的現有XDM架構的ID。 有關如何查找或建立啟用概要檔案的架構的資訊，請參見有關使用架構注 [冊表API建立架構的教程](../../xdm/tutorials/create-schema-api.md)。 下列對 [!DNL Catalog] API的呼叫會啟用和的資 [!DNL Profile] 料集 [!DNL Identity Service]。

**API格式**

```http
POST /dataSets
```

**請求**

借由在 `unifiedProfile` 請求主 `unifiedIdentity` 體中加入和 `tags` 在下方，資料集會立即針對和 [!DNL Profile] 分別啟 [!DNL Identity Service]用。 這些標籤的值必須是包含字串的陣列 `"enabled:true"`。

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
    "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
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
| `schemaRef.id` | 資料集所 [!DNL Profile]依據的已啟用架構ID。 |
| `{TENANT_ID}` | 包含屬於您IMS [!DNL Schema Registry] 組織之資源的命名空間。 如需詳 [細資訊，請參閱開發人](../../xdm/api/getting-started.md#know-your-tenant-id)[!DNL Schema Registry] 員指南的TENANT_ID區段。 |

**回應**

成功的回應會顯示包含新建立資料集ID的陣列，其格式為 `"@/dataSets/{DATASET_ID}"`。 成功建立並啟用資料集後，請繼續上傳資料的 [步驟](#upload-data-to-the-dataset)。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 設定現有資料集 {#configure-an-existing-dataset}

下列步驟說明如何為和啟用先前建立的資 [!DNL Real-time Customer Profile] 料集 [!DNL Identity Service]。 如果您已建立啟用描述檔的資料集，請繼續擷取資 [料的步驟](#ingest-data-into-the-dataset)。

### 檢查資料集是否已啟用 {#check-if-the-dataset-is-enabled}

使用 [!DNL Catalog] API，您可以檢查現有資料集，以判斷它是否已啟用供和 [!DNL Real-time Customer Profile] 使用 [!DNL Identity Service]。 下列呼叫會依ID擷取資料集的詳細資料。

**API格式**

```http
GET /dataSets/{DATASET_ID}
```

| 參數 | 說明 |
|---|---|
| `{DATASET_ID}` | 您要檢查的資料集ID。 |

**請求**

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
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
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

在屬 `tags` 性下，您可以看到 `unifiedProfile` 和 `unifiedIdentity` 都與值一起存在 `enabled:true`。 因此， [!DNL Real-time Customer Profile] 並分 [!DNL Identity Service] 別啟用此資料集。

### 啟用資料集 {#enable-the-dataset}

如果尚未為或啟用現有數 [!DNL Profile] 據集 [!DNL Identity Service]，則可以使用資料集ID發出PATCH請求來啟用它。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 參數 | 說明 |
|---|---|
| `{DATASET_ID}` | 您要更新的資料集ID。 |

**請求**

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

請求內文包含一 `tags` 個屬性，其中包含兩個子屬性： `"unifiedProfile"` 和 `"unifiedIdentity"`。 這些子屬性的值是包含字串的陣列 `"enabled:true"`。

**響應**&#x200B;成功的PATCH請求返回HTTP狀態200(OK)和包含更新資料集ID的陣列。 此ID應與PATCH請求中發送的ID匹配。 現在 `"unifiedProfile"` 已新 `"unifiedIdentity"` 增和標籤，且資料集已啟用供設定檔和身分服務使用。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 將資料收錄至資料集 {#ingest-data-into-the-dataset}

在 [!DNL Real-time Customer Profile] XDM資料 [!DNL Identity Service] 被收錄到資料集時，會同時使用它。 如需如何將資料上傳至資料集的指示，請參閱使用API [建立資料集的教學課程](../../catalog/datasets/create.md)。 在規劃要傳送哪些資料至啟用資 [!DNL Profile]料集時，請考慮下列最佳實務：

- 納入您要用作觀眾區隔標準的任何資料。
- 加入您從描述檔資料中可確定的盡可能多的識別碼，以最大化您的識別圖。 這可以更 [!DNL Identity Service] 有效地將身分連接到資料集上。

## 確認資料收錄方式 [!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

第一次上傳資料至新資料集，或是作為新ETL或資料來源相關程式的一部分，建議您仔細檢查資料，以確保資料已如預期上傳。 使用 [!DNL Real-time Customer Profile] Access API，您可以在批次資料載入資料集時擷取其中的資料。 如果您無法擷取任何預期的實體，您的資料集可能無法啟用 [!DNL Real-time Customer Profile]。 確認資料集已啟用後，請確定您的來源資料格式和識別碼支援您的期望。 如需如何使用 [!DNL Real-time Customer Profile] API存取資料的詳細 [!DNL Profile] 指示，請依照實 [體端點指南](../api/entities.md)，亦稱為[!DNL Profile Access] 「API」。

## 確認由Identity Service收錄的資料 {#confirm-data-ingest-by-identity-service}

包含多個身分的每個已收錄資料片段會在您的私人身分圖表中建立連結。 有關身分圖表和存取身分資料的更多資訊，請先閱讀 [Identity Service概觀](../../identity-service/home.md)。