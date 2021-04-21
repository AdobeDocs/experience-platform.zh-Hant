---
keywords: Experience Platform；首頁；熱門主題；雲儲存資料
solution: Experience Platform
title: 使用來源連接器和API收集雲端儲存資料
topic-legacy: overview
type: Tutorial
description: 本教學課程涵蓋從協力廠商雲端儲存空間擷取資料，並使用來源連接器和API將其匯入平台的步驟。
exl-id: 95373c25-24f6-4905-ae6c-5000bf493e6f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 1%

---

# 使用來源連接器和API收集雲端儲存空間資料

本教學課程涵蓋從協力廠商雲端儲存空間擷取資料，並透過來源連接器和[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)將其匯入平台的步驟。

## 快速入門

本教學課程要求您透過有效的連線存取協力廠商雲端儲存空間，並瞭解您要匯入平台的檔案，包括檔案的路徑和結構。 如果您沒有此資訊，請先參閱[教學課程，瞭解如何使用 [!DNL Flow Service] API](../explore/cloud-storage.md)來探索協力廠商雲端儲存空間，然後再嘗試本教學課程。

本教學課程還要求您對Adobe Experience Platform的以下部分有切實的瞭解：

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   - [架構構成基礎](../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   - [架構註冊開發人員指南](../../../../xdm/api/getting-started.md):包含您必須知道的重要資訊，以便成功執行對架構註冊表API的呼叫。這包括您的`{TENANT_ID}`、&quot;containers&quot;的概念，以及提出要求時所需的標題（請特別注意「接受」標題及其可能的值）。
- [[!DNL Catalog Service]](../../../../catalog/home.md):目錄是記錄Experience Platform中資料位置和世系的系統。
- [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md):「批次擷取API」可讓您將資料以批次檔案的形式內嵌至Experience Platform。
- [沙盒](../../../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一平台實例分割為獨立的虛擬環境，以協助開發和發展數位體驗應用程式。以下各節提供您必須知道的其他資訊，以便使用[!DNL Flow Service] API成功連線至雲端儲存空間。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱Experience Platform疑難排解指南中[如何讀取範例API呼叫](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫平台API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有Experience PlatformAPI呼叫中每個必要標題的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Experience Platform中的所有資源（包括屬於[!DNL Flow Service]的資源）都與特定虛擬沙盒隔離。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

- `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要附加的媒體類型標題：

- `Content-Type: application/json`

## 建立源連接{#source}

您可以通過向[!DNL Flow Service] API發出POST請求來建立源連接。 源連接由連接ID、源資料檔案的路徑和連接規範ID組成。

要建立源連接，還必須為資料格式屬性定義枚舉值。

請為檔案來源使用下列列舉值：

| 資料格式 | 列舉值 |
| ----------- | ---------- |
| 分隔字元 | `delimited` |
| JSON | `json` |
| 鑲木 | `parquet` |

對於所有基於表的源，請將值設定為`tabular`。

- [使用自訂分隔檔案建立來源連線](#using-custom-delimited-files)
- [使用壓縮檔案建立源連接](#using-compressed-files)

**API格式**

```http
POST /sourceConnections
```

### 使用自訂分隔檔案{#using-custom-delimited-files}建立來源連線

**要求**

您可以指定`columnDelimiter`為屬性，以自訂分隔字元來內嵌分隔字元的檔案。 任何單一字元值都是允許的欄分隔字元。 如果未提供，則使用逗號`(,)`作為預設值。

下列範例要求會使用Tab分隔值建立分隔檔案類型的來源連線。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cloud storage source connection for delimited files",
        "description": "Cloud storage source connector",
        "baseConnectionId": "9e2541a0-b143-4d23-a541-a0b143dd2301",
        "data": {
            "format": "delimited",
            "columnDelimiter": "\t"
        },
        "params": {
            "path": "/ingestion-demos/leads/tsv_data/*.tsv",
            "recursive": "true"
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `baseConnectionId` | 您所存取之協力廠商雲端儲存系統的唯一連線ID。 |
| `data.format` | 定義資料格式屬性的枚舉值。 |
| `data.columnDelimiter` | 您可以使用任何單一字元欄分隔字元來收集平面檔案。 只有在接收CSV或TSV檔案時，才需要此屬性。 |
| `params.path` | 您正在訪問的源檔案的路徑。 |
| `connectionSpec.id` | 與特定第三方雲端儲存系統關聯的連線規格ID。 有關連接規範ID的清單，請參見[附錄](#appendix)。 |

**回應**

成功的響應返回新建源連接的唯一標識符(`id`)。 在後續步驟中需要此ID才能建立資料流。

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

### 使用壓縮檔案{#using-compressed-files}建立源連接

**要求**

您也可以透過指定壓縮的JSON或分隔檔案`compressionType`為屬性，來內嵌其檔案。 支援的壓縮檔案類型清單包括：

- `bzip2`
- `gzip`
- `deflate`
- `zipDeflate`
- `tarGzip`
- `tar`

以下示例請求使用`gzip`檔案類型為壓縮分隔檔案建立源連接。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cloud storage source connection for compressed files",
        "description": "Cloud storage source connection for compressed files",
        "baseConnectionId": "9e2541a0-b143-4d23-a541-a0b143dd2301",
        "data": {
            "format": "delimited",
            "properties": {
                "compressionType" : "gzip"
            }
        },
        "params": {
            "path": "/compressed/files.gzip"
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
     }'
```

| 屬性 | 說明 |
| --- | --- |
| `data.properties.compressionType` | 決定擷取的壓縮檔案類型。 只有在擷取壓縮的JSON或分隔檔案時，才需要此屬性。 |

**回應**

成功的響應返回新建源連接的唯一標識符(`id`)。 在後續步驟中需要此ID才能建立資料流。

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## 建立目標XDM模式{#target-schema}

為了讓源資料用於平台，必須建立目標模式以根據您的需要來構建源資料。 然後，目標模式用於建立包含源資料的平台資料集。

通過對[方案註冊表API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)執行POST請求，可以建立目標XDM方案。

**API格式**

```http
POST /schemaregistry/tenant/schemas
```

**要求**

以下示例請求建立一個XDM模式，以擴展XDM Individual Profile類。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "type": "object",
        "title": "Target schema for a Cloud Storage connector",
        "description": "Target schema for a Cloud Storage connector",
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
            }
        ],
        "meta:containerId": "tenant",
        "meta:resourceType": "schemas",
        "meta:xdmType": "object",
        "meta:class": "https://ns.adobe.com/xdm/context/profile"
    }'
```

**回應**

成功的響應返回新建立的架構的詳細資訊，包括其唯一標識符(`$id`)。 在後續步驟中需要此ID，才能建立目標資料集、對應和資料流。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
    "meta:altId": "_{TENANT_ID}.schemas.995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema cloud storage",
    "type": "object",
    "description": "Target schema for cloud storage",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "imsOrg": "{IMS_ORG}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1597783248870,
        "repo:lastModifiedDate": 1597783248870,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "596661ec6c7a9c6ae530676e98290a4a58ca29540ed92489cf4478b2bf013a65",
        "meta:globalLibVersion": "1.13.3"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "{TENANT_ID}"
}
```

## 建立目標資料集

通過對[目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)執行POST請求，提供裝載內目標方案的ID，可以建立目標資料集。

**API格式**

```http
POST /catalog/dataSets
```

**要求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Target dataset for cloud storage",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `schemaRef.id` | 目標XDM架構的ID。 |
| `schemaRef.contentType` | 架構的版本。 此值必須設定為`application/vnd.adobe.xed-full-notext+json;version=1` ，以返回方案的最新次要版本。 |

**回應**

成功的響應返回一個陣列，該陣列包含以`"@/datasets/{DATASET_ID}"`格式新建立的資料集的ID。 資料集ID是唯讀、系統產生的字串，用於在API呼叫中參考資料集。 在後續步驟中需要目標資料集ID才能建立目標連接和資料流。

```json
[
    "@/dataSets/5f3c3cedb2805c194ff0b69a"
]
```

## 建立目標連接{#target-connection}

目標連接表示到所收錄資料所在目的地的連接。 要建立目標連接，必須提供與「資料湖」關聯的固定連接規範ID。 此連接規範ID為：`c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

您現在擁有目標資料集的唯一識別碼、目標模式和至資料湖的連線規格ID。 使用這些標識符，可以使用[!DNL Flow Service] API建立目標連接，以指定將包含入站源資料的資料集。

**API格式**

```http
POST /targetConnections
```

**要求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Target Connection for a Cloud Storage connector",
        "description": "Target Connection for a Cloud Storage connector",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5f3c3cedb2805c194ff0b69a"
        },
            "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `data.schema.id` | 目標XDM架構的`$id`。 |
| `data.schema.version` | 架構的版本。 此值必須設定為`application/vnd.adobe.xed-full+json;version=1` ，以返回方案的最新次要版本。 |
| `params.dataSetId` | 目標資料集的ID。 |
| `connectionSpec.id` | 已修正資料湖的連線規格ID。 此ID為：`c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |

**回應**

成功的響應返回新目標連接的唯一標識符(`id`)。 後續步驟需要此ID。

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 建立映射{#mapping}

為了將源資料引入目標資料集，必須首先將其映射到目標資料集所遵守的目標模式。 這是透過對轉換服務執行POST請求，並在請求裝載中定義資料映射來實現的。

>[!TIP]
>
>您可以使用雲端儲存來源連接器來對應複雜的資料類型，例如JSON檔案中的陣列。

**API格式**

```http
POST /conversion/mappingSets
```

**要求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "FirstName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "LastName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `xdmSchema` | 目標XDM架構的ID。 |

**回應**

成功的響應返回新建立映射的詳細資訊，包括其唯一標識符(`id`)。 在後續步驟中需要此值才能建立資料流。

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 檢索資料流規範{#specs}

資料流負責從源收集資料，並將其引入平台。 要建立資料流，必須首先獲得負責收集雲儲存資料的資料流規範。

**API格式**

```http
GET /flowSpecs?property=name=="CloudStorageToAEP"
```

**要求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回負責將源資料帶入平台的資料流規範的詳細資訊。 響應包括建立新資料流所需的唯一流規範`id`。

```json
{
    "items": [
        {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "name": "CloudStorageToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
                "ecadc60c-7455-4d87-84dc-2a0e293d997b",
                "b7829c2f-2eb0-4f49-a6ee-55e33008b629",
                "4c10e202-c428-4796-9208-5f1f5732b1cf",
                "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
                "32e8f412-cdf7-464c-9885-78184cb113fd",
                "b7bf2577-4520-42c9-bae9-cad01560f7bc",
                "998b8ae3-cec0-43b7-8abe-40b1eb4ee069",
                "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8"
            ],
            "targetConnectionSpecIds": [
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
            ],
            "transformationSpecs": [
                {
                    "name": "Mapping",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines various params required for different mapping from source to target",
                        "properties": {
                            "mappingId": {
                                "type": "string"
                            },
                            "mappingVersion": {
                                "type": "string"
                            }
                        }
                    }
                }
            ],
            "scheduleSpec": {
                "name": "PeriodicSchedule",
                "type": "Periodic",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "startTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "endTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "interval": {
                            "type": "integer"
                        },
                        "frequency": {
                            "type": "string",
                            "enum": [
                                "minute",
                                "hour",
                                "day",
                                "week"
                            ]
                        },
                        "backfill": {
                            "type": "boolean",
                            "default": true
                        }
                    },
                    "required": [
                        "startTime",
                        "frequency",
                        "interval"
                    ],
                    "if": {
                        "properties": {
                            "frequency": {
                                "const": "minute"
                            }
                        }
                    },
                    "then": {
                        "properties": {
                            "interval": {
                                "minimum": 15
                            }
                        }
                    },
                    "else": {
                        "properties": {
                            "interval": {
                                "minimum": 1
                            }
                        }
                    }
                }
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        }
    ]
}
```

## 建立資料流

收集雲端儲存資料的最後一步是建立資料流。 目前，您已準備好下列必要值：

- [源連接ID](#source)
- [目標連線ID](#target)
- [對應ID](#mapping)
- [資料流規範ID](#specs)

資料流負責調度和收集源中的資料。 您可以通過執行POST請求，同時在裝載中提供先前提到的值來建立資料流。

若要排程擷取，您必須先將開始時間值設定為以秒為單位的紀元時間。 然後，您必須將頻率值設為以下五個選項之一：`once`、`minute`、`hour`、`day`或`week`。 間隔值指定兩個連續的提取之間的期間，並且建立一次性提取不需要設定間隔。 對於所有其它頻率，間隔值必須設定為等於或大於`15`。

>[!IMPORTANT]
>
>強烈建議在使用[FTP連接器](../../../connectors/cloud-storage/ftp.md)時，安排資料流進行一次性提取。

**API格式**

```http
POST /flows
```

**要求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cloud Storage flow to Platform",
        "description": "Cloud Storage flow to Platform",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "26b53912-1005-49f0-b539-12100559f0e2"
        ],
        "targetConnectionIds": [
            "f7eb08fa-5f04-4e45-ab08-fa5f046e45ee"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1597784298",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `flowSpec.id` | 在上一步驟中檢索的[流規範ID](#specs)。 |
| `sourceConnectionIds` | 在先前步驟中檢索的[源連接ID](#source)。 |
| `targetConnectionIds` | 在先前步驟中擷取的[目標連線ID](#target-connection)。 |
| `transformations.params.mappingId` | 在先前步驟中檢索的[映射ID](#mapping)。 |
| `scheduleParams.startTime` | 資料流在時代時間中的開始時間。 |
| `scheduleParams.frequency` | 資料流收集資料的頻率。 可接受的值包括：`once`、`minute`、`hour`、`day`或`week`。 |
| `scheduleParams.interval` | 該間隔用於指定兩個連續流運行之間的期間。 間隔的值應為非零整數。 當頻率設為`once`時，不需要間隔，對於其他頻率值，應大於或等於`15`。 |

**回應**

成功的響應返回新建立的資料流的ID(`id`)。

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 監控資料流

建立資料流後，您可以監視通過其接收的資料，以查看有關流運行、完成狀態和錯誤的資訊。 有關如何監視資料流的詳細資訊，請參見API](../monitor.md)中有關[監視資料流的教程

## 後續步驟

在本教學課程中，您已建立來源連接器，以依計畫從雲端儲存空間收集資料。 現在，下游平台服務（如[!DNL Real-time Customer Profile]和[!DNL Data Science Workspace]）可以使用傳入的資料。 如需詳細資訊，請參閱下列檔案：

- [即時客戶個人檔案總覽](../../../../profile/home.md)
- [資料科學工作區概觀](../../../../data-science-workspace/home.md)

## 附錄 {#appendix}

下節列出不同的雲儲存源連接器及其連接規範。

### 連接規範

| 連接器名稱 | 連接規範 |
| -------------- | --------------- |
| [!DNL Amazon S3] (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| [!DNL Amazon Kinesis] (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| [!DNL Azure Blob] （點滴） | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| [!DNL Azure Data Lake Storage Gen2] （ADLS第2代） | `0ed90a81-07f4-4586-8190-b40eccef1c5a` |
| [!DNL Azure Event Hubs] （事件集線器） | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| [!DNL Azure File Storage] | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| [!DNL Google Cloud Storage] | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| [!DNL HDFS] | `54e221aa-d342-4707-bcff-7a4bceef0001` |
| [!DNL Oracle Object Storage] | `c85f9425-fb21-426c-ad0b-405e9bd8a46c` |
| [!DNL SFTP] | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |
