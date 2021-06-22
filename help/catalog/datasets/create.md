---
keywords: Experience Platform；首頁；熱門主題；資料集；資料集；建立資料集；建立資料集
solution: Experience Platform
title: 使用API建立資料集
topic-legacy: datasets
description: 本檔案提供使用Adobe Experience Platform API建立資料集，以及使用檔案填入資料集的一般步驟。
exl-id: 3a5f48cf-ad05-4b9e-be1d-ff213a26a477
source-git-commit: e4bf5bb77ac4186b24580329699d74d653310d93
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 1%

---

# 使用API建立資料集

本檔案提供使用Adobe Experience Platform API建立資料集，以及使用檔案填入資料集的一般步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [批次內嵌](../../ingestion/batch-ingestion/overview.md): [!DNL Experience Platform] 可讓您將資料內嵌為批次檔案。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要了解的其他資訊，以便成功呼叫[!DNL Platform] API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[authentication tutorial](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有[!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源都與特定虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標題，以指定作業將在下列位置進行的沙箱名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* 內容類型：application/json

## 教學課程

若要建立資料集，必須先定義結構。 結構是一組規則，可協助表示資料。 除了說明資料結構外，結構還提供可套用的限制和期望，當資料在系統之間移動時，可用來驗證資料。

這些標準定義允許一致地解釋資料（無論來源為何），並消除跨應用程式翻譯的需要。 有關合成架構的詳細資訊，請參閱[架構合成基礎](../../xdm/schema/composition.md)的指南

## 查詢資料集結構

本教學課程從[Schema Registry API教學課程](../../xdm/tutorials/create-schema-api.md)結束的位置開始，其中會使用在本教學課程中建立的忠誠會員架構。

如果您尚未完成[!DNL Schema Registry]教學課程，請從該處開始，並僅在您構建了必要的架構後繼續使用此資料集教學課程。

以下呼叫可用來檢視您在[!DNL Schema Registry] API教學課程期間建立的忠誠會員架構：

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrg": "{IMS_ORG}",
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `schemaRef.id` | 資料集將基於的XDM架構的URI `$id`值。 |
| `schemaRef.contentType` | 指示架構的格式和版本。 如需詳細資訊，請參閱XDM API指南中[架構版本設定](../../xdm/api/getting-started.md#versioning)的相關章節。 |

>[!NOTE]
>
>本教學課程的所有範例都使用[Apache Parquet](https://parquet.apache.org/documentation/latest/)檔案格式。 若需使用JSON檔案格式的範例，請參閱[批次內嵌開發人員指南](../../ingestion/batch-ingestion/api-overview.md)

**回應**

成功的回應會傳回HTTP狀態201（已建立），而回應物件則包含陣列，內含以`"@/datasets/{DATASET_ID}"`格式建立之新資料集的ID。 資料集ID是唯讀、系統產生的字串，用於在API呼叫中參考資料集。

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

要求內文包含「datasetId」欄位，其值為上一步驟中產生的`{DATASET_ID}`。

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

**回應**

成功的響應返回HTTP狀態201（已建立）和包含新建立批的詳細資訊的響應對象，包括其`id`（只讀、系統生成的字串）。

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{IMS_ORG}",
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
| `{BATCH_ID}` | 要上載到的批的`id`。 |
| `{DATASET_ID}` | 批次資料集的`id`將持續存在。 |
| `{FILE_NAME}` | 您要上傳的檔案名稱。 |

**要求**

```SHELL
curl -X PUT 'https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c/datasets/5c8c3c555033b814b69f947f/files/loyaltyData.parquet' \
  -H 'content-type: application/octet-stream' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  --data-binary '@{FILE_PATH_AND_NAME}.parquet'
```

**回應**

成功上傳的檔案會傳回空白回應內文，並傳回HTTP狀態200（確定）。

## 信號批完成

將所有資料檔案上傳至批次後，您可以發出批次訊號以完成。 信令完成使服務為上載的檔案建立[!DNL Catalog] `DataSetFile`條目，並將它們與以前生成的批處理關聯。 [!DNL Catalog]批次會標示為成功，這會觸發任何下游流程，而這些流程隨後可用於目前可用的資料。

**API格式**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 參數 | 說明 |
| --- | --- |
| `{BATCH_ID}` | 要標籤為完成的批的`id`。 |

**要求**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**回應**

成功完成的批處理返回空白響應正文和HTTP狀態200（確定）。

## 監視擷取

批處理需要不同的時間才能進行內嵌，具體取決於資料的大小。 您可以將包含批次ID的`batch`請求參數附加至`GET /batches`請求，借此監控批次的狀態。 API會從擷取到回應中的`status`，對資料集進行輪詢，以找出批次狀態，指出完成（&quot;success&quot;或&quot;failure&quot;）。

**API格式**

```HTTP
GET /batches?batch={BATCH_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{BATCH_ID}` | 要監視的批的`id`。 |

**要求**

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?batch=5d01230fc78a4e4f8c0c6b387b4b8d1c' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**回應**

正向響應返回具有`status`屬性的對象，該屬性包含`success`的值：

```JSON
{
    "5b7129a879323401ef2a6486": {
        "imsOrg": "{IMS_ORG}",
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

負響應在其`"status"`屬性中返回值為`"failed"`的對象，並包括任何相關錯誤消息：

```JSON
{
    "5b96ce65badcf701e51f075d": {
        "imsOrg": "{IMS_ORG}",
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

若需使用資料存取API的詳細步驟，請參閱[資料存取開發人員指南](../../data-access/home.md)。

## 更新資料集結構

您可以新增欄位，並將其他資料內嵌至已建立的資料集。 若要這麼做，您必須先新增定義新資料的其他屬性，以更新結構。 您可以使用PATCH和/或PUT操作來更新現有架構。

如需更新結構的詳細資訊，請參閱[Schema Registry API開發人員指南](../../xdm/api/getting-started.md)。

更新結構後，您可以依照本教學課程中的步驟，擷取符合修訂結構的新資料。

請務必記住，架構演化純粹是可加進的，這表示一旦將架構儲存至註冊表並用於資料擷取，便無法對架構進行中斷變更。 若要進一步了解合成架構以與Adobe Experience Platform搭配使用的最佳實務，請參閱架構合成[基本概念](../../xdm/schema/composition.md)上的指南。
