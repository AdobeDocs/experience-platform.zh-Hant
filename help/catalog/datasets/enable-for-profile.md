---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；啟用資料集
title: 使用API為設定檔和Identity服務啟用資料集
type: Tutorial
description: 本教學課程說明如何使用Adobe Experience Platform API啟用資料集，以便與即時客戶個人檔案和身分識別服務搭配使用。
exl-id: a115e126-6775-466d-ad7e-ee36b0b8b49c
source-git-commit: b80d8349fc54a955ebb3362d67a482d752871420
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 5%

---

# 啟用資料集 [!DNL Profile] 和 [!DNL Identity Service] 使用API

本教學課程涵蓋啟用資料集以用於中的程式 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service]，分為下列步驟：

1. 啟用資料集以用於 [!DNL Real-Time Customer Profile]，使用下列兩個選項之一：
   - [建立新的資料集](#create-a-dataset-enabled-for-profile-and-identity)
   - [設定現有的資料集](#configure-an-existing-dataset)
1. [將資料擷取至資料集](#ingest-data-into-the-dataset)
1. [透過即時客戶個人檔案確認資料擷取](#confirm-data-ingest-by-real-time-customer-profile)
1. [確認由Identity Service擷取的資料](#confirm-data-ingest-by-identity-service)

## 快速入門

若要參閱本教學課程，請先實際瞭解管理已啟用設定檔的資料集所牽涉到的多項Adobe Experience Platform服務。 開始進行本教學課程之前，請先檢閱相關檔案 [!DNL Platform] 服務：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者個人檔案。
- [[!DNL Identity Service]](../../identity-service/home.md)：啟用 [!DNL Real-Time Customer Profile] 透過橋接擷取到的不同資料來源的身分 [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md)：此RESTful API可讓您建立資料集並加以設定，用於 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Platform] 組織客戶體驗資料。

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

## 建立為設定檔和身分啟用的資料集 {#create-a-dataset-enabled-for-profile-and-identity}

您可以在建立資料集後或資料集建立後，立即為即時客戶設定檔和Identity Service啟用資料集。 如果要啟用已建立的資料集，請遵循以下步驟 [設定現有的資料集](#configure-an-existing-dataset) 稍後可在此檔案中找到。

>[!NOTE]
>
>若要建立新的已啟用設定檔的資料集，您必須知道已為設定檔啟用的現有XDM結構描述的ID。 如需如何查詢或建立已啟用設定檔的結構描述的詳細資訊，請參閱以下教學課程： [使用結構描述登入API建立結構描述](../../xdm/tutorials/create-schema-api.md).

若要建立為設定檔啟用的資料集，您可以使用對的POST請求 `/dataSets` 端點。

**API格式**

```http
POST /dataSets
```

**要求**

包含 `unifiedProfile` 和 `unifiedIdentity` 在 `tags` 在請求內文中，資料集將立即啟用 [!DNL Profile] 和 [!DNL Identity Service]，依序輸入。 這些標籤的值必須是包含字串的陣列 `"enabled:true"`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
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
| `schemaRef.id` | 的ID [!DNL Profile]資料集將依據的已啟用結構描述。 |
| `{TENANT_ID}` | 內的名稱空間 [!DNL Schema Registry] 包含屬於您組織的資源。 請參閱 [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) 的區段 [!DNL Schema Registry] 開發人員指南，以取得詳細資訊。 |

**回應**

成功的回應會顯示一個陣列，其中包含以形式建立之資料集的ID `"@/dataSets/{DATASET_ID}"`. 當您成功建立並啟用資料集後，請繼續下列步驟： [上傳資料](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 設定現有的資料集 {#configure-an-existing-dataset}

下列步驟說明如何啟用先前建立的資料集 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service]. 如果您已建立已啟用設定檔的資料集，請繼續的步驟 [擷取資料](#ingest-data-into-the-dataset).

### 檢查資料集是否已啟用 {#check-if-the-dataset-is-enabled}

使用 [!DNL Catalog] API時，您可以檢查現有資料集以判斷是否已啟用它以用於中 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service]. 以下呼叫會依ID擷取資料集的詳細資料。

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
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "5b020a27e7040801dedbf46f",
        "files": "@/dataSetFiles?dataSetId=5b020a27e7040801dedbf46e",
        "schema": "@/xdms/context/experienceevent",
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

在 `tags` 屬性，您會看到 `unifiedProfile` 和 `unifiedIdentity` 都以值呈現 `enabled:true`. 因此， [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service] 已分別為此資料集啟用。

### 啟用資料集 {#enable-the-dataset}

如果現有的資料集尚未啟用 [!DNL Profile] 或 [!DNL Identity Service]，您可使用資料集ID發出PATCH請求來啟用它。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 參數 | 說明 |
|---|---|
| `{DATASET_ID}` | 您要更新之資料集的ID。 |

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

請求內文包含 `path` 兩種型別的標籤， `unifiedProfile` 和 `unifiedIdentity`. 此 `value` 每個都是包含字串的陣列 `enabled:true`.

**回應**

成功的PATCH要求會傳回HTTP狀態200 （確定）以及包含已更新資料集ID的陣列。 此ID應符合PATCH請求中傳送的ID。 此 `unifiedProfile` 和 `unifiedIdentity` 現在已新增標籤，且資料集已啟用供設定檔和身分識別服務使用。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 將資料擷取至資料集 {#ingest-data-into-the-dataset}

兩者 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service] 使用XDM資料，因為它正在被擷取到資料集中。 如需如何將資料上傳到資料集的說明，請參閱上的教學課程 [使用API建立資料集](../../catalog/datasets/create.md). 規劃要傳送哪些資料給您的時 [!DNL Profile] — 啟用的資料集，請考量下列最佳實務：

- 包含您要用來作為分段條件的任何資料。
- 儘可能加入您從設定檔資料中確定的識別碼，以將您的身分圖表最大化。 這允許 [!DNL Identity Service] 跨資料集更有效率地拼接身分。

## 確認資料擷取依據 [!DNL Real-Time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

首次將資料上傳到新資料集時，或作為涉及新ETL或資料來源的程式的一部分，建議仔細檢查資料，以確保資料已按預期上傳。 使用 [!DNL Real-Time Customer Profile] 存取API，您可以在批次資料載入資料集時擷取該資料。 如果您無法擷取任何您期望的實體，您的資料集可能不會啟用 [!DNL Real-Time Customer Profile]. 確認您的資料集已啟用後，請確保來源資料格式和識別碼支援您的期望。 如需如何使用 [!DNL Real-Time Customer Profile] 要存取的API [!DNL Profile] 資料，請參閱 [entities端點指南](../../profile/api/entities.md)，也稱為「[!DNL Profile Access]&quot; API.

## 確認由Identity Service擷取的資料 {#confirm-data-ingest-by-identity-service}

每個內嵌包含多個身分的資料片段，都會在您的私人身分圖形中建立連結。 如需身分圖表和存取身分資料的詳細資訊，請先閱讀 [Identity Service總覽](../../identity-service/home.md).
