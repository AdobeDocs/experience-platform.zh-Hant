---
keywords: Experience Platform；首頁；熱門主題；資料集；資料集；建立資料集；建立資料集
solution: Experience Platform
title: 使用API建立資料集
description: 本檔案提供使用Adobe Experience Platform API建立資料集以及使用檔案填入資料集的一般步驟。
exl-id: 3a5f48cf-ad05-4b9e-be1d-ff213a26a477
source-git-commit: e2f16f532b98e6948ffd7f331e630137b3972f0f
workflow-type: tm+mt
source-wordcount: '1302'
ht-degree: 6%

---

# 使用API建立資料集

本檔案提供使用Adobe Experience Platform API建立資料集以及使用檔案填入資料集的一般步驟。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [批次內嵌](../../ingestion/batch-ingestion/overview.md)： [!DNL Experience Platform]可讓您將資料內嵌為批次檔案。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
* [[!DNL Sandboxes]](../../sandboxes/home.md)： [!DNL Experience Platform]提供的虛擬沙箱可將單一[!DNL Platform]執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能成功呼叫[!DNL Platform] API。

### 讀取範例 API 呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集所需標頭的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

[!DNL Experience Platform]中的所有資源都與特定的虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標頭，以指定將在其中執行作業的沙箱名稱：

* x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的要求都需要額外`Content-Type: application/json`標題。 若為JSON+PATCH要求，`Content-Type`應為`application/json-patch+json`。

## 教學課程

若要建立資料集，必須先定義結構描述。 結構是一組規則，可協助表示資料。 除了說明資料結構外，結構描述還會提供一些限制和期望，可用於在系統之間行動資料時驗證資料。

這些標準定義可讓資料以一致方式解譯，無論其來源為何，並移除跨應用程式翻譯的需求。 如需構成結構描述的詳細資訊，請參閱結構描述構成的[基本概念指南](../../xdm/schema/composition.md)

## 查詢資料集結構

此教學課程從[結構描述登入API教學課程](../../xdm/tutorials/create-schema-api.md)的結尾處開始，並會使用該教學課程期間建立的忠誠會員結構描述。

如果您尚未完成[!DNL Schema Registry]教學課程，請從這裡開始，並在撰寫必要的結構描述後繼續此資料集教學課程。

下列呼叫可用來檢視您在[!DNL Schema Registry] API教學課程中建立的熟客方案會員結構描述：

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

回應物件的格式取決於請求中傳送的Accept標頭。 此回應中的個別屬性已最小化空間。

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

備妥熟客方案後，您現在可以建立參考該方案的資料集。

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
| `schemaRef.id` | 資料集將依據的XDM結構描述的URI `$id`值。 |
| `schemaRef.contentType` | 表示結構描述的格式和版本。 如需詳細資訊，請參閱XDM API指南中[架構版本設定](../../xdm/api/getting-started.md#versioning)的相關章節。 |

>[!NOTE]
>
>本教學課程的所有範例都使用[Apache Parquet](https://parquet.apache.org/docs/)檔案格式。 您可以在[批次擷取開發人員指南](../../ingestion/batch-ingestion/api-overview.md)中找到使用JSON檔案格式的範例

**回應**

成功的回應會傳回HTTP狀態201 （已建立）和一個回應物件，該回應物件包含一個陣列，其中包含以`"@/datasets/{DATASET_ID}"`格式建立的新資料集識別碼。 資料集ID是系統產生的唯讀字串，用來參考API呼叫中的資料集。

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## 建立批次

您必須先建立連結至資料集的批次，才能將資料新增到資料集。 該批次隨後將用於上傳。

**API格式**

```HTTP
POST /batches
```

**要求**

請求內文包含「datasetId」欄位，其值是上一步驟產生的`{DATASET_ID}`。

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

成功的回應會傳回HTTP狀態201 （已建立）和回應物件。 回應物件由陣列組成，該陣列包含新建立批次的識別碼，格式為`"@/batches/{BATCH_ID}"`。 批次ID是系統產生的唯讀字串，用來參考API呼叫中的批次。

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

## 將檔案上傳到批次

成功建立要上傳的新批次後，您現在可以將檔案上傳到特定資料集。 請務必記住，定義資料集時，已將檔案格式指定為Parquet。 因此，您上傳的檔案必須採用該格式。

>[!NOTE]
>
>支援的最大資料上傳檔案為512 MB。 如果您的資料檔案大於此值，則需要將其分成不大於512 MB的區塊，以便一次上傳一個。 您可以對每個檔案重複此步驟，使用相同的批次ID，將每個檔案上傳到相同的批次中。 如果檔案可作為批次的一部分上傳，則數量沒有限制。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{BATCH_ID}` | 您正在上傳的批次的`id`。 |
| `{DATASET_ID}` | 批次將保留在的資料集`id`。 |
| `{FILE_NAME}` | 您正在上傳的檔案名稱。 |

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

成功上傳的檔案會傳回空白的回應本文和HTTP狀態200 （確定）。

## 訊號批次完成

將所有資料檔案上傳至批次後，您可以發出完成批次的訊號。 訊號完成會導致服務為上傳的檔案建立[!DNL Catalog] `DataSetFile`專案，並將這些專案與先前產生的批次建立關聯。 [!DNL Catalog]批次標籤為成功，這會觸發任何下游流程，這些流程隨後可用於現在可用的資料。

**API格式**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 參數 | 說明 |
| --- | --- |
| `{BATCH_ID}` | 您標示為完成的批次`id`。 |

**要求**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**回應**

成功完成的批次會傳回空白的回應本文和HTTP狀態200 （確定）。

## 監視內嵌

根據資料的大小，批次擷取的時間長度不一。 您可以將批次的ID附加至`GET /batches`請求，藉此監控批次的狀態。

**API格式**

```HTTP
GET /batches/{BATCH_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{BATCH_ID}` | 您要監視之批次的`id`。 |

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

正面回應傳回物件，其`status`屬性包含`success`的值：

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

負回應傳回物件的`"status"`屬性值為`"failed"`，並包含任何相關的錯誤訊息：

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
>建議的輪詢間隔為兩分鐘。

## 從資料集讀取資料

使用批次ID，您可以使用資料存取API來讀取及驗證上傳至批次的所有檔案。 回應會傳回一個陣列，其中包含檔案ID清單，每個檔案ID都會參照批次中的檔案。

您也可以使用資料存取API來傳回名稱、大小（位元組），以及下載檔案或資料夾的連結。

您可以在[資料存取開發人員指南](../../data-access/home.md)中找到使用資料存取API的詳細步驟。

## 更新資料集結構

您可以新增欄位，並將其他資料擷取到您建立的資料集中。 若要這麼做，您首先需要透過新增定義新資料的其他屬性來更新結構。 這可以使用PATCH和/或PUT操作來更新現有結構描述來完成。

如需更新結構描述的詳細資訊，請參閱[結構描述登入API開發人員指南](../../xdm/api/getting-started.md)。

更新結構描述後，您可以依照本教學課程中的步驟重新進行，以擷取符合修訂後結構描述的新資料。

請務必記住，結構描述演化是完全相加的，這表示一旦結構描述儲存至登入並用於資料內嵌，您就無法引進重大變更給結構描述。 若要進一步瞭解構成結構描述以與Adobe Experience Platform搭配使用的最佳實務，請參閱結構描述構成的[基本概念指南](../../xdm/schema/composition.md)。
