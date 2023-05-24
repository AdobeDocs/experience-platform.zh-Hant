---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；故障排除；API；啟用資料集
title: 使用API為配置檔案和身份服務啟用資料集
type: Tutorial
description: 本教程介紹如何使用Adobe Experience PlatformAPI啟用資料集以與即時客戶配置檔案和身份服務一起使用。
exl-id: a115e126-6775-466d-ad7e-ee36b0b8b49c
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 1%

---

# 為 [!DNL Profile] 和 [!DNL Identity Service] 使用API

本教程介紹啟用資料集以供使用的過程 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service]，分為以下步驟：

1. 啟用資料集以供使用 [!DNL Real-Time Customer Profile]，使用以下兩個選項之一：
   - [建立新資料集](#create-a-dataset-enabled-for-profile-and-identity)
   - [配置現有資料集](#configure-an-existing-dataset)
1. [將資料攝取到資料集](#ingest-data-into-the-dataset)
1. [確認即時客戶配置檔案的資料接收](#confirm-data-ingest-by-real-time-customer-profile)
1. [確認Identity Service接收資料](#confirm-data-ingest-by-identity-service)

## 快速入門

本教程要求對管理啟用Profile的資料集時涉及的幾個Adobe Experience Platform服務進行有效理解。 在開始本教程之前，請查閱相關文檔 [!DNL Platform] 服務：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。
- [[!DNL Identity Service]](../../identity-service/home.md):啟用 [!DNL Real-Time Customer Profile] 通過橋接來自不同資料源的標識來將 [!DNL Platform]。
- [[!DNL Catalog Service]](../../catalog/home.md):一個REST風格的API，允許您建立資料集並為 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service]。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。

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

## 建立為配置檔案和標識啟用的資料集 {#create-a-dataset-enabled-for-profile-and-identity}

您可以在建立時或建立資料集後的任何時間立即為Real-Time Customer Profile和Identity Service啟用資料集。 如果要啟用已建立的資料集，請按照 [配置現有資料集](#configure-an-existing-dataset) 的下一頁。

>[!NOTE]
>
>要建立啟用配置檔案的新資料集，必須知道為配置檔案啟用的現有XDM架構的ID。 有關如何查找或建立啟用配置檔案的架構的資訊，請參見上的教程 [使用架構註冊表API建立架構](../../xdm/tutorials/create-schema-api.md)。

要建立為配置檔案啟用的資料集，可以使用POST請求 `/dataSets` 端點。

**API格式**

```http
POST /dataSets
```

**要求**

通過包括 `unifiedProfile` 和 `unifiedIdentity` 在 `tags` 在請求正文中，將立即為 [!DNL Profile] 和 [!DNL Identity Service]的下界。 這些標籤的值必須是包含字串的陣列 `"enabled:true"`。

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
| `schemaRef.id` | 的ID [!DNL Profile] — 啟用的模式，資料集將基於此模式。 |
| `{TENANT_ID}` | 中的命名空間 [!DNL Schema Registry] 包含屬於您組織的資源。 查看 [租戶ID](../../xdm/api/getting-started.md#know-your-tenant-id) 的下界 [!DNL Schema Registry] 詳細資訊。 |

**回應**

成功的響應顯示一個陣列，該陣列包含以下形式新建立的資料集的ID: `"@/dataSets/{DATASET_ID}"`。 成功建立並啟用資料集後，請繼續執行以下步驟 [上傳資料](#upload-data-to-the-dataset)。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 配置現有資料集 {#configure-an-existing-dataset}

以下步驟介紹如何為 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service]。 如果已建立啟用配置檔案的資料集，請繼續執行 [正在接收資料](#ingest-data-into-the-dataset)。

### 檢查資料集是否已啟用 {#check-if-the-dataset-is-enabled}

使用 [!DNL Catalog] API，您可以檢查現有資料集以確定它是否在 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service]。 以下調用按ID檢索資料集的詳細資訊。

**API格式**

```http
GET /dataSets/{DATASET_ID}
```

| 參數 | 說明 |
|---|---|
| `{DATASET_ID}` | 要檢查的資料集的ID。 |

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

在 `tags` 屬性，你可以看到 `unifiedProfile` 和 `unifiedIdentity` 都有值 `enabled:true`。 所以， [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service] 已分別為此資料集啟用。

### 啟用資料集 {#enable-the-dataset}

如果尚未為 [!DNL Profile] 或 [!DNL Identity Service]，可以通過使用資料集ID發出PATCH請求來啟用它。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 參數 | 說明 |
|---|---|
| `{DATASET_ID}` | 要更新的資料集的ID。 |

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

請求主體包括 `path` 到兩種標籤， `unifiedProfile` 和 `unifiedIdentity`。 的 `value` 每個都是包含字串的陣列 `enabled:true`。

**回應**

成功的PATCH請求返回HTTP狀態200(OK)和包含已更新資料集ID的陣列。 此ID應與在PATCH請求中發送的ID匹配。 的 `unifiedProfile` 和 `unifiedIdentity` 標籤現在已添加，並且資料集已啟用供配置檔案和Identity Services使用。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 將資料攝取到資料集 {#ingest-data-into-the-dataset}

兩者 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service] 在將XDM資料攝取到資料集時使用它。 有關如何將資料上載到資料集的說明，請參閱上面的教程 [使用API建立資料集](../../catalog/datasets/create.md)。 規劃要發送給您的資料時 [!DNL Profile]-enabled dataset，請考慮以下最佳做法：

- 包括要用作分段條件的任何資料。
- 根據配置檔案資料盡可能多地包含標識符，以最大化標識圖。 這允許 [!DNL Identity Service] 以更高效地在資料集上縫合身份。

## 確認資料接收方 [!DNL Real-Time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

首次將資料上載到新資料集時，或作為涉及新ETL或資料源的進程的一部分，建議仔細檢查資料，以確保已按預期上載資料。 使用 [!DNL Real-Time Customer Profile] 訪問API時，可以在批處理資料載入到資料集時檢索它。 如果無法檢索預期的任何實體，則可能未為 [!DNL Real-Time Customer Profile]。 確認已啟用資料集後，請確保源資料格式和標識符支援您的期望值。 有關如何使用的詳細說明 [!DNL Real-Time Customer Profile] 訪問的API [!DNL Profile] 資料，請參閱 [實體端點指南](../../profile/api/entities.md)，也稱為「 」[!DNL Profile Access]» API。

## 確認Identity Service接收資料 {#confirm-data-ingest-by-identity-service}

所攝取的包含多個身份的每個資料片段會在您的私有身份圖中建立一個連結。 有關身份圖和訪問身份資料的詳細資訊，請首先閱讀 [Identity Service概述](../../identity-service/home.md)。
