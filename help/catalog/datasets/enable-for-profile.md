---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；啟用資料集
title: 使用API為設定檔和Identity服務啟用資料集
type: Tutorial
description: 本教學課程說明如何使用Adobe Experience Platform API啟用資料集，以便與即時客戶個人檔案和身分識別服務搭配使用。
exl-id: a115e126-6775-466d-ad7e-ee36b0b8b49c
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 5%

---

# 使用API為[!DNL Profile]和[!DNL Identity Service]啟用資料集

本教學課程涵蓋啟用資料集以在[!DNL Real-Time Customer Profile]和[!DNL Identity Service]中使用的程式，並細分為下列步驟：

1. 使用下列兩個選項之一，啟用資料集以用於[!DNL Real-Time Customer Profile]：
   - [建立新的資料集](#create-a-dataset-enabled-for-profile-and-identity)
   - [設定現有的資料集](#configure-an-existing-dataset)
1. [將資料內嵌至資料集](#ingest-data-into-the-dataset)
1. [透過即時客戶個人檔案確認資料擷取](#confirm-data-ingest-by-real-time-customer-profile)
1. [確認Identity服務擷取的資料](#confirm-data-ingest-by-identity-service)

## 快速入門

若要參閱本教學課程，請先實際瞭解管理已啟用設定檔的資料集所牽涉到的多項Adobe Experience Platform服務。 在開始本教學課程之前，請先檢閱這些相關[!DNL Experience Platform]服務的檔案：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
- [[!DNL Identity Service]](../../identity-service/home.md)：透過橋接擷取到[!DNL Experience Platform]中的不同資料來源的身分來啟用[!DNL Real-Time Customer Profile]。
- [[!DNL Catalog Service]](../../catalog/home.md)： RESTful API可讓您建立資料集並為[!DNL Real-Time Customer Profile]和[!DNL Identity Service]設定資料集。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。

以下章節提供您需瞭解的其他資訊，才能成功呼叫Experience Platform API。

### 讀取範例 API 呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集所需標頭的值

若要呼叫[!DNL Experience Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

所有包含裝載(POST、PUT、PATCH)的要求都需要額外`Content-Type`標題。 必要時，此標頭的正確值會顯示在範例要求中。

[!DNL Experience Platform]中的所有資源都與特定的虛擬沙箱隔離。 對[!DNL Experience Platform] API的所有請求都需要`x-sandbox-name`標頭，以指定將在其中執行操作的沙箱名稱。 如需[!DNL Experience Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

## 建立為設定檔和身分啟用的資料集 {#create-a-dataset-enabled-for-profile-and-identity}

您可以在建立資料集後或資料集建立後，立即為即時客戶設定檔和Identity Service啟用資料集。 如果要啟用已建立的資料集，請依照本檔案稍後所提供的[設定現有資料集](#configure-an-existing-dataset)的步驟操作。

>[!NOTE]
>
>若要建立新的已啟用設定檔的資料集，您必須知道已為設定檔啟用的現有XDM結構描述的ID。 如需如何查閱或建立啟用設定檔的結構描述的相關資訊，請參閱有關使用結構描述登入API建立結構描述[的教學課程](../../xdm/tutorials/create-schema-api.md)。

若要建立為設定檔啟用的資料集，您可以使用POST要求至`/dataSets`端點。

**API格式**

```http
POST /dataSets
```

**要求**

藉由在要求內文中的`tags`下包含`unifiedProfile`和`unifiedIdentity`，資料集將分別立即啟用[!DNL Profile]和[!DNL Identity Service]。 這些標籤的值必須是包含字串`"enabled:true"`的陣列。

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
| `schemaRef.id` | 資料集將依據已啟用[!DNL Profile]的結構描述識別碼。 |
| `{TENANT_ID}` | [!DNL Schema Registry]內的名稱空間，其中包含屬於您組織的資源。 如需詳細資訊，請參閱[!DNL Schema Registry]開發人員指南的[TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id)一節。 |

**回應**

成功的回應會顯示一個陣列，其中包含`"@/dataSets/{DATASET_ID}"`形式的新建立資料集識別碼。 當您成功建立並啟用資料集後，請繼續進行[上傳資料](#upload-data-to-the-dataset)的步驟。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 設定現有的資料集 {#configure-an-existing-dataset}

下列步驟說明如何為[!DNL Real-Time Customer Profile]和[!DNL Identity Service]啟用先前建立的資料集。 如果您已建立已啟用設定檔的資料集，請繼續進行[擷取資料](#ingest-data-into-the-dataset)的步驟。

### 檢查資料集是否已啟用 {#check-if-the-dataset-is-enabled}

您可以使用[!DNL Catalog] API檢查現有的資料集，以判斷是否已啟用它以用於[!DNL Real-Time Customer Profile]和[!DNL Identity Service]。 以下呼叫會依ID擷取資料集的詳細資料。

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

在`tags`屬性下，您可以看到`unifiedProfile`和`unifiedIdentity`都以值`enabled:true`存在。 因此，已分別為此資料集啟用[!DNL Real-Time Customer Profile]和[!DNL Identity Service]。

### 啟用資料集 {#enable-the-dataset}

如果尚未為[!DNL Profile]或[!DNL Identity Service]啟用現有的資料集，您可以使用資料集ID發出PATCH請求來啟用它。

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

要求內文包含`path`到兩種型別的標籤： `unifiedProfile`和`unifiedIdentity`。 每個的`value`都是包含字串`enabled:true`的陣列。

**回應**

成功的PATCH要求會傳回HTTP狀態200 （確定）以及包含已更新資料集ID的陣列。 此ID應符合PATCH請求中傳送的ID。 `unifiedProfile`和`unifiedIdentity`標籤現已新增，且資料集已啟用供設定檔和身分識別服務使用。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 將資料擷取至資料集 {#ingest-data-into-the-dataset}

[!DNL Real-Time Customer Profile]和[!DNL Identity Service]都會使用XDM資料，因為它正在擷取到資料集中。 如需如何將資料上傳到資料集的說明，請參閱有關[使用API建立資料集](../../catalog/datasets/create.md)的教學課程。 規劃要傳送至已啟用[!DNL Profile]之資料集的資料時，請考慮下列最佳實務：

- 包含您要用來作為分段條件的任何資料。
- 儘可能加入您從設定檔資料中確定的識別碼，以將您的身分圖表最大化。 這可讓[!DNL Identity Service]更有效率地拼接資料集中的身分。

## 確認由[!DNL Real-Time Customer Profile]擷取的資料 {#confirm-data-ingest-by-real-time-customer-profile}

首次將資料上傳到新資料集時，或作為涉及新ETL或資料來源的程式的一部分，建議仔細檢查資料，以確保資料已按預期上傳。 使用[!DNL Real-Time Customer Profile] Access API，您可以在批次資料載入資料集時擷取該資料。 如果您無法擷取任何您期望的實體，您的資料集可能無法啟用[!DNL Real-Time Customer Profile]。 確認您的資料集已啟用後，請確保來源資料格式和識別碼支援您的期望。 如需有關如何使用[!DNL Real-Time Customer Profile] API存取[!DNL Profile]資料的詳細指示，請參閱[entities端點指南](../../profile/api/entities.md)，也稱為&quot;[!DNL Profile Access]&quot; API。

## 確認由Identity Service擷取的資料 {#confirm-data-ingest-by-identity-service}

每個內嵌包含多個身分的資料片段，都會在您的私人身分圖形中建立連結。 如需身分圖表和存取身分資料的詳細資訊，請先閱讀[身分識別服務概觀](../../identity-service/home.md)。
