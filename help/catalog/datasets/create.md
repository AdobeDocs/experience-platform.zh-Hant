---
keywords: Experience Platform；首頁；熱門主題；資料集；資料集；建立資料集；建立資料集；
solution: Experience Platform
title: 使用API建立資料集
description: 本文檔提供了使用Adobe Experience PlatformAPI建立資料集和使用檔案填充資料集的一般步驟。
exl-id: 3a5f48cf-ad05-4b9e-be1d-ff213a26a477
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 1%

---

# 使用API建立資料集

本文檔提供了使用Adobe Experience PlatformAPI建立資料集和使用檔案填充資料集的一般步驟。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [批量攝取](../../ingestion/batch-ingestion/overview.md): [!DNL Experience Platform] 允許您將資料作為批處理檔案進行接收。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了您需要瞭解的其他資訊，以便成功呼叫 [!DNL Platform] API。

### 讀取示例API調用

本教程提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

### 收集所需標題的值

為了呼叫 [!DNL Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有關中的沙箱的詳細資訊 [!DNL Platform]，請參見 [沙盒概述文檔](../../sandboxes/home.md)。

包含負載(POST、PUT、PATCH)的所有請求都需要附加的標頭：

* 內容類型：應用程式/json

## 教學課程

要建立資料集，必須先定義模式。 架構是一組規則，用於幫助表示資料。 除了描述資料結構外，模式還提供了約束和期望值，這些約束和期望值可以應用並用於在系統之間移動資料時驗證資料。

這些標準定義允許對資料進行一致的解釋，而不管其來源如何，並消除跨應用程式進行翻譯的需要。 有關合成架構的詳細資訊，請參閱 [架構組合基礎](../../xdm/schema/composition.md)

## 查找資料集架構

本教程從 [架構註冊表API教程](../../xdm/tutorials/create-schema-api.md) 結束，使用在本教程中建立的會員成員架構。

如果尚未完成 [!DNL Schema Registry] 教程，請從此開始，並僅在您構建了必要的架構後，才繼續本資料集教程。

以下調用可用於查看在 [!DNL Schema Registry] API教程：

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

響應對象的格式取決於請求中發送的「接受」標頭。 此響應中的各個屬性已最小化為空間。

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

在會員成員架構就位後，您現在可以建立引用該架構的資料集。

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
| `schemaRef.id` | URI `$id` 資料集將基於的XDM模式的值。 |
| `schemaRef.contentType` | 指示架構的格式和版本。 請參閱 [架構版本](../../xdm/api/getting-started.md#versioning) 的子菜單。 |

>[!NOTE]
>
>本教程使用 [阿帕奇鑲木地板](https://parquet.apache.org/docs/) 檔案格式。 在中可找到使用JSON檔案格式的示例 [批量攝取顯影劑指南](../../ingestion/batch-ingestion/api-overview.md)

**回應**

成功的響應返回HTTP狀態201（已建立）和響應對象，該響應對象由包含新建立資料集ID的陣列組成，格式為 `"@/datasets/{DATASET_ID}"`。 資料集ID是只讀的系統生成字串，用於在API調用中引用資料集。

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## 建立批

在向資料集添加資料之前，必須建立連結到該資料集的批處理。 然後，批將用於上載。

**API格式**

```HTTP
POST /batches
```

**要求**

請求正文包括「datasetId」欄位，其值為 `{DATASET_ID}` 生成。

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

成功的響應返回HTTP狀態201（已建立）和包含新建立批的詳細資訊（包括其）的響應對象 `id`，只讀，系統生成的字串。

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

## 將檔案上載到批

成功建立新批以上載後，現在可以將檔案上載到特定資料集。 必須記住，在定義資料集時，將檔案格式指定為Parke。 因此，您上載的檔案必須採用該格式。

>[!NOTE]
>
>支援的最大資料上載檔案為512 MB。 如果資料檔案大於此值，則需要將其分成不大於512 MB的塊，以一次上載一個。 您可以使用相同的批ID對每個檔案重複此步驟，以同一批次上載每個檔案。 如果可以作為批處理的一部分上載檔案，則該數字沒有限制。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{BATCH_ID}` | 的 `id` 上載到的批。 |
| `{DATASET_ID}` | 的 `id` 將保留批處理。 |
| `{FILE_NAME}` | 正在上載的檔案的名稱。 |

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

成功上載的檔案返回空的響應正文和HTTP狀態200（確定）。

## 信號批量完成

將所有資料檔案上載到批後，可以向批發出完成信號。 信令完成導致服務建立 [!DNL Catalog] `DataSetFile` 上載檔案的條目，並將它們與先前生成的批關聯。 的 [!DNL Catalog] 批處理被標籤為成功，這將觸發所有下游流，然後這些流可以處理當前可用的資料。

**API格式**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 參數 | 說明 |
| --- | --- |
| `{BATCH_ID}` | 的 `id` 您標籤為完整的批。 |

**要求**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**回應**

成功完成的批處理返回空的響應正文和HTTP狀態200（確定）。

## 監視攝取

根據資料的大小，批處理需要不同的時間長度才能進行接收。 可以通過附加 `batch` 包含批的ID的請求參數 `GET /batches` 請求。 API將從接收到接收的批處理狀態輪詢資料集 `status` 在響應中表示完成（「成功」或「失敗」）。

**API格式**

```HTTP
GET /batches?batch={BATCH_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{BATCH_ID}` | 的 `id` 要監視的批。 |

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

正響應返回具有其 `status` 包含值的屬性 `success`:

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

負響應返回值為 `"failed"` 在 `"status"` 屬性，並包含任何相關錯誤消息：

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

## 從資料集中讀取資料

使用批ID，您可以使用資料存取API來回讀和驗證上載到批的所有檔案。 響應返回包含檔案ID清單的陣列，每個ID都引用批處理中的檔案。

您還可以使用資料存取API返回名稱、大小（以位元組為單位），以及下載檔案或資料夾的連結。

有關使用資料存取API的詳細步驟，請參見 [資料存取開發人員指南](../../data-access/home.md)。

## 更新資料集架構

您可以添加欄位，並將其他資料添加到已建立的資料集中。 為此，首先需要通過添加定義新資料的附加屬性來更新架構。 這可以使用PATCH和/或PUT操作來更新現有架構。

有關更新架構的詳細資訊，請參見 [《架構註冊API開發人員指南》](../../xdm/api/getting-started.md)。

更新架構後，可以重新執行本教程中的步驟，以接收符合修訂架構的新資料。

必須記住，架構演化純粹是加性的，這意味著一旦將架構保存到註冊表並用於資料接收，就不能對其進行中斷更改。 要瞭解有關構成架構以供Adobe Experience Platform使用的最佳實踐的更多資訊，請參閱 [架構組合基礎](../../xdm/schema/composition.md)。
