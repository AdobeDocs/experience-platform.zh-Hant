---
keywords: Experience Platform;home；熱門主題；dataset;Dataset；建立資料集；建立資料集
solution: Experience Platform
title: 使用API建立資料集
topic: datasets
description: 本檔案提供使用Adobe Experience PlatformAPI建立資料集，以及使用檔案填入資料集的一般步驟。
exl-id: 3a5f48cf-ad05-4b9e-be1d-ff213a26a477
translation-type: tm+mt
source-git-commit: 727c9dbd87bacfd0094ca29157a2d0283c530969
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 1%

---

# 使用API建立資料集

本檔案提供使用Adobe Experience PlatformAPI建立資料集，以及使用檔案填入資料集的一般步驟。

## 快速入門

本指南需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

* [批次擷取](../../ingestion/batch-ingestion/overview.md): [!DNL Experience Platform] 可讓您將資料內嵌為批次檔案。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，才能成功呼叫[!DNL Platform] API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙盒的詳細資訊，請參閱[沙盒概述檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* 內容類型：application/json

## 教學課程

要建立資料集，必須先定義模式。 架構是一組規則，可協助表示資料。 除了描述資料結構外，結構描述還提供可套用並用於驗證在系統間移動資料的約束和期望。

這些標準定義允許一致地解釋資料，而不論其來源為何，並消除跨應用程式翻譯的需要。 有關合成方案的詳細資訊，請參見[架構合成基礎指南](../../xdm/schema/composition.md)

## 查找資料集模式

本教程從[方案註冊表API教程](../../xdm/tutorials/create-schema-api.md)結束的位置開始，使用在該教程中建立的忠誠成員方案。

如果您尚未完成[!DNL Schema Registry]教學課程，請從這裡開始，並只有在完成必要的架構後，才繼續使用此資料集教學課程。

以下呼叫可用於查看在[!DNL Schema Registry] API教程中建立的忠誠成員方案：

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

回應物件的格式取決於請求中傳送的「接受」標題。 此響應中的各個屬性已最小化為空間。

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

現在，您可以在「忠誠成員」結構模式就位後，建立參照結構的資料集。

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
| `schemaRef.id` | 資料集將基於的XDM模式的URI `$id`值。 |
| `schemaRef.contentType` | 指示方案的格式和版本。 如需詳細資訊，請參閱XDM API指南中有關[架構版本控制](../../xdm/api/getting-started.md#versioning)的章節。 |

>[!NOTE]
>
>本教程的所有示例都使用[Apache Parce](https://parquet.apache.org/documentation/latest/)檔案格式。 使用JSON檔案格式的範例可在[批次擷取開發人員指南](../../ingestion/batch-ingestion/api-overview.md)中找到

**回應**

成功的響應返回HTTP狀態201（已建立）和一個響應對象，該響應對象由一個陣列組成，該陣列包含以`"@/datasets/{DATASET_ID}"`格式新建立的資料集的ID。 資料集ID是唯讀、系統產生的字串，用於在API呼叫中參考資料集。

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## 建立批次

您必須先建立連結至資料集的批次，才能將資料新增至資料集。 然後，該批次將用於上載。

**API格式**

```HTTP
POST /batches
```

**要求**

請求內文包含「datasetId」欄位，其值為上一步驟中產生的`{DATASET_ID}`。

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

成功的響應返回HTTP狀態201（已建立）和包含新建立批的詳細資訊的響應對象，包括其`id`（只讀，系統生成的字串）。

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

## 將檔案上傳至批次

成功建立新批次以上傳後，您現在可以將檔案上傳至特定資料集。 請務必記住，當您定義資料集時，將檔案格式指定為Parce。 因此，您上傳的檔案必須是該格式。

>[!NOTE]
>
>支援的最大資料上傳檔案為512 MB。 如果您的資料檔案大於此，則需要將它分割為不大於512 MB的區塊，以一次上傳一個。 您可以對每個檔案重複此步驟，使用相同的批次ID，以相同批次上傳每個檔案。 如果您可以在批次中上傳檔案，則數目沒有限制。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{BATCH_ID}` | 您要上傳至的批次的`id`。 |
| `{DATASET_ID}` | 批次將保留的資料集的`id`。 |
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

成功上傳的檔案會傳回空白的回應正文和HTTP狀態200（確定）。

## 信號批次完成

將所有資料檔案上傳至批次後，您可以向批次發出完成訊號。 信令完成使服務為已上載檔案建立[!DNL Catalog] `DataSetFile`條目，並將它們與先前生成的批關聯。 [!DNL Catalog]批次已標示為成功，這會觸發任何下游流，然後可處理現有可用資料。

**API格式**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 參數 | 說明 |
| --- | --- |
| `{BATCH_ID}` | 您標籤為完成的批的`id`。 |

**要求**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**回應**

成功完成的批返回空白響應主體和HTTP狀態200（確定）。

## 螢幕擷取

批處理需要不同的時間長度才能進行收錄，這取決於資料的大小。 您可以將包含批ID的`batch`請求參數附加到`GET /batches`請求，以監控批的狀態。 API會從擷取到回應中的`status`指出完成（「成功」或「失敗」），輪詢資料集以找出批次的狀態。

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

正向響應返回其`status`屬性包含`success`值的對象：

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

負響應返回其`"status"`屬性中值`"failed"`的對象，並包含任何相關錯誤消息：

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

使用批次ID，您可以使用資料存取API來回讀及驗證上傳至批次的所有檔案。 響應返回包含檔案ID清單的陣列，每個ID都引用批中的檔案。

您也可以使用資料存取API傳回名稱、大小（以位元組為單位），以及下載檔案或資料夾的連結。

有關使用Data Access API的詳細步驟，請參閱[Data Access開發人員指南](../../data-access/home.md)。

## 更新資料集結構

您可以新增欄位，並將其他資料內嵌至您建立的資料集。 為此，您首先需要通過添加定義新資料的其他屬性來更新方案。 這可以使用PATCH和／或PUT操作來更新現有模式。

有關更新方案的詳細資訊，請參閱[方案註冊表API開發人員指南](../../xdm/api/getting-started.md)。

更新架構後，您可以重新遵循本教學課程中的步驟，以便新增符合修訂架構的資料。

請務必記住，模式演化純粹是可加性的，這表示一旦將模式保存到註冊表並用於資料提取，您就不能對模式引入中斷更改。 要瞭解有關構成方案以用於Adobe Experience Platform的最佳實踐，請參見[架構構成基礎](../../xdm/schema/composition.md)的指南。
