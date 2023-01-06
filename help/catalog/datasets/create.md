---
keywords: Experience Platform；首頁；熱門主題；資料集；資料集；建立資料集；建立資料集
solution: Experience Platform
title: 使用API建立資料集
description: 本檔案提供使用Adobe Experience Platform API建立資料集，以及使用檔案填入資料集的一般步驟。
exl-id: 3a5f48cf-ad05-4b9e-be1d-ff213a26a477
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 1%

---

# 使用API建立資料集

本檔案提供使用Adobe Experience Platform API建立資料集，以及使用檔案填入資料集的一般步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [批次內嵌](../../ingestion/batch-ingestion/overview.md): [!DNL Experience Platform] 可讓您將資料內嵌為批次檔案。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下小節提供您需要知道的其他資訊，以便成功呼叫 [!DNL Platform] API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

若要對 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊，請參閱 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* 內容類型：application/json

## 教學課程

若要建立資料集，必須先定義結構。 結構是一組規則，可協助表示資料。 除了說明資料結構外，結構還提供可套用的限制和期望，當資料在系統之間移動時，可用來驗證資料。

這些標準定義允許一致地解釋資料（無論來源為何），並消除跨應用程式翻譯的需要。 有關合成結構的詳細資訊，請參閱 [綱要構成基本知識](../../xdm/schema/composition.md)

## 查詢資料集結構

本教學課程從 [Schema Registry API教學課程](../../xdm/tutorials/create-schema-api.md) 結束：使用教學課程期間建立的忠誠會員結構。

如果您尚未完成 [!DNL Schema Registry] 教學課程，請從這裡開始，並在您完成必要的架構後，再繼續使用此資料集教學課程。

下列呼叫可用來檢視您在 [!DNL Schema Registry] API教學課程：

**API格式**

```HTTP
GET /tenant/schemas/{schema meta:altId or URL encoded $id URI}
```

**要求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

回應物件的格式取決於要求中傳送的Accept標題。 此響應中的各個屬性已針對空間最小化。

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "properties": {
        "repositoryCreatedBy": {},
        "repositoryLastModifiedBy": {},
        "createdByBatchID": {},
        "modifiedByBatchID": {},
        "_repo": {},
        "identityMap": {},
        "_id": {},
        "timeSeriesEvents": {},
        "person": {},
        "homeAddress": {},
        "personalEmail": {},
        "homePhone": {},
        "mobilePhone": {},
        "faxPhone": {},
        "_{TENANT_ID}": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "loyalty": {
                    "title": "Loyalty",
                    "description": "Loyalty Info",
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "loyaltyPoints": {
                            "title": "Loyalty Points",
                            "type": "integer",
                            "description": "Loyalty points total.",
                            "meta:xdmType": "int"
                        },
                        "memberSince": {
                            "title": "Member Since",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined the Loyalty Program.",
                            "meta:xdmType": "date-time"
                        }
                    }
                }
            }
        }
    },
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.4",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551843052271,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## 建立資料集

現在，只要建立「忠誠會員」結構，您就可以建立參照該結構的資料集。

**API格式**

```HTTP
POST /dataSets
```

**要求**

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| 屬性 | 說明 |
| --- | --- |
| `schemaRef.id` | URI `$id` 資料集所根據之XDM架構的值。 |
| `schemaRef.contentType` | 指示架構的格式和版本。 請參閱 [方案版本設定](../../xdm/api/getting-started.md#versioning) （位於XDM API指南中）以取得詳細資訊。 |

>[!NOTE]
>
>本教學課程使用 [阿帕奇鑲木地板](https://parquet.apache.org/docs/) 檔案格式。 若需使用JSON檔案格式的範例，請參閱 [批次匯入開發人員指南](../../ingestion/batch-ingestion/api-overview.md)

**回應**

成功的回應會傳回HTTP狀態201（已建立），而回應物件則由陣列組成，陣列內含新建立資料集的ID，格式為 `"@/datasets/{DATASET_ID}"`. 資料集ID是唯讀、系統產生的字串，用於在API呼叫中參考資料集。

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## 建立批次

您必須先建立連結至資料集的批次資料，才能將資料新增至資料集。 然後，該批次將用於上傳。

**API格式**

```HTTP
POST /batches
```

**要求**

要求內文包含「datasetId」欄位，其值為 `{DATASET_ID}` 於上一步驟產生。

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

**回應**

成功的回應會傳回HTTP狀態201（已建立），而回應物件會包含新建立批次的詳細資訊，包括其 `id`，此為唯讀、系統產生的字串。

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{ORG_ID}",
    "updated": 1552694873602,
    "status": "loading",
    "created": 1552694873602,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "5c8c3c555033b814b69f947f"
        }
    ],
    "version": "1.0.0",
    "tags": {
        "acp_producer": [
            "{CREATED_CLIENT}"
        ],
        "acp_stagePath": [
            "{CREATED_CLIENT}/stage/5d01230fc78a4e4f8c0c6b387b4b8d1c"
        ],
        "use_plan_b_batch_status": [
            "false"
        ]
    },
    "createdUser": "{CREATED_BY}",
    "updatedUser": "{CREATED_BY}",
    "externalId": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "createdClient": "{CREATED_CLIENT}",
    "inputFormat": {
        "format": "parquet"
    }
}
```

## 上傳檔案至批次

成功建立新批次以供上傳後，您現在可以將檔案上傳至特定資料集。 請務必記住，定義資料集時，已將檔案格式指定為Parquet。 因此，您上傳的檔案必須是該格式。

>[!NOTE]
>
>支援的最大資料上傳檔案為512 MB。 如果資料檔案大於此，則需將其分割為不大於512 MB的區塊，才能一次上傳一個。 您可以對每個檔案重複此步驟，使用相同的批次ID，以相同批次上傳每個檔案。 如果您可以在批次中上傳檔案，則數量沒有限制。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{BATCH_ID}` | 此 `id` 上傳至的批次。 |
| `{DATASET_ID}` | 此 `id` 批次會保存在資料集中。 |
| `{FILE_NAME}` | 您要上傳的檔案名稱。 |

**要求**

```SHELL
curl -X PUT 'https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c/datasets/5c8c3c555033b814b69f947f/files/loyaltyData.parquet' \
  -H 'content-type: application/octet-stream' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  --data-binary '@{FILE_PATH_AND_NAME}.parquet'
```

**回應**

成功上傳的檔案會傳回空白回應內文，並傳回HTTP狀態200（確定）。

## 信號批完成

將所有資料檔案上傳至批次後，您可以發出批次訊號以完成。 信令完成導致服務建立 [!DNL Catalog] `DataSetFile` 上傳檔案的項目，並將它們與先前產生的批次建立關聯。 此 [!DNL Catalog] 批次會標示為成功，這會觸發任何下游流程，而這些流程隨後可對現在可用的資料運作。

**API格式**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 參數 | 說明 |
| --- | --- |
| `{BATCH_ID}` | 此 `id` 標籤為已完成的批。 |

**要求**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**回應**

成功完成的批處理返回空白響應正文和HTTP狀態200（確定）。

## 監視擷取

批處理需要不同的時間才能進行內嵌，具體取決於資料的大小。 您可以附加 `batch` 包含批次ID的請求參數 `GET /batches` 請求。 API會從擷取到擷取，輪詢資料集的批次狀態 `status` 在回應中表示完成（「success」或「failure」）。

**API格式**

```HTTP
GET /batches?batch={BATCH_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{BATCH_ID}` | 此 `id` 要監視的批次。 |

**要求**

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?batch=5d01230fc78a4e4f8c0c6b387b4b8d1c' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**回應**

正面回應會傳回物件及其 `status` 包含值的屬性 `success`:

```JSON
{
    "5b7129a879323401ef2a6486": {
        "imsOrg": "{ORG_ID}",
        "created": 1534142888068,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1534142955152,
        "replay": {},
        "status": "success",
        "errors": [],
        "version": "1.0.3",
        "availableDates": {},
        "relatedObjects": [
            {
                "type": "batch",
                "id": "29285e08378f4a41827e7e70fb7cb8f0"
            }
        ],
        "metrics": {
            "startTime": 1534142943819,
            "endTime": 1534142951760,
            "recordsRead": 108,
            "recordsWritten": 108
        }
    }
}
```

負回應會傳回物件，其值為 `"failed"` 在 `"status"` 屬性，並包含任何相關錯誤訊息：

```JSON
{
    "5b96ce65badcf701e51f075d": {
        "imsOrg": "{ORG_ID}",
        "status": "failed",
        "relatedObjects": [
            {
                "type": "batch",
                "id": "29285e08378f4a41827e7e70fb7cb8f0"
            }
        ],
        "replay": {},
        "availableDates": {},
        "metrics": {
            "startTime": 1536610322329,
            "endTime": 1536610438083,
            "recordsRead": 4004,
            "recordsWritten": 4004,
            "failureReason": "Job aborted due to stage failure: Task 0 in stage 1.0 failed 4 times,:"
        },
        "errors": [
            {
                "code": "0070000017",
                "description": "Unknown error occurred."
            },
            {
                "code": "unknown",
                "description": "Job aborted."
            }
        ],
        "created": 1536609893629,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1536610442814,
        "version": "1.0.5"
    }
}
```

>[!NOTE]
>
>建議的輪詢間隔為2分鐘。

## 從資料集讀取資料

透過批次ID，您可以使用資料存取API來回讀及驗證上傳至批次的所有檔案。 回應會傳回包含檔案ID清單的陣列，每個ID都會參考批次中的檔案。

您也可以使用資料存取API來傳回名稱、大小（以位元組為單位），以及下載檔案或資料夾的連結。

若需使用資料存取API的詳細步驟，請參閱 [資料存取開發人員指南](../../data-access/home.md).

## 更新資料集結構

您可以新增欄位，並將其他資料內嵌至已建立的資料集。 若要這麼做，您必須先新增定義新資料的其他屬性，以更新結構。 您可以使用PATCH和/或PUT操作來更新現有架構。

如需更新結構的詳細資訊，請參閱 [Schema Registry API開發人員指南](../../xdm/api/getting-started.md).

更新結構後，您可以依照本教學課程中的步驟，擷取符合修訂結構的新資料。

請務必記住，架構演化純粹是可加進的，這表示一旦將架構儲存至註冊表並用於資料擷取，便無法對架構進行中斷變更。 若要進一步了解合成結構以搭配Adobe Experience Platform使用的最佳實務，請參閱 [綱要構成基本知識](../../xdm/schema/composition.md).
