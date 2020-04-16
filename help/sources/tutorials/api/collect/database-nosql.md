---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 透過來源連接器和API，從外部資料庫或NoSQL系統收集資料
topic: overview
translation-type: tm+mt
source-git-commit: 00764a59629eb8a5a06ac28ad446084b0bdb2293

---


# 透過來源連接器和API，從外部資料庫或NoSQL系統收集資料

Flow Service用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教程介紹從資料庫或NoSQL系統檢索資料並通過源連接器和API將其導入平台的步驟。

## 快速入門

本教程要求您通過有效的基本連接和要引入平台的檔案（包括檔案的路徑和結構）訪問第三方資料庫或NoSQL系統。 如果您沒有此資訊，請參閱教程，在嘗試本教 [程之前，使用流服務API來探索資料庫或NoSQL系統](../explore/database-nosql.md) 。

本教學課程也要求您對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構註冊開發人員指南](../../../../xdm/api/getting-started.md):包含您必須知道的重要資訊，以便成功執行對架構註冊表API的呼叫。 這包括您 `{TENANT_ID}`的「容器」概念，以及提出要求所需的標題（請特別注意「接受」標題及其可能的值）。
* [目錄服務](../../../../catalog/home.md):目錄是Experience Platform中資料位置和世系的記錄系統。
* [批次擷取](../../../../ingestion/batch-ingestion/overview.md):批次擷取API可讓您將資料以批次檔案的形式內嵌至Experience Platform。
* [沙盒](../../../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用流服務API成功連接到資料庫或NoSQL系統。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集必要標題的值

若要呼叫平台API，您必須先完成驗證教 [學課程](../../../../tutorials/authentication.md)。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

* 授權：生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源（包括屬於Flow Service的資源）都隔離至特定的虛擬沙盒。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* 內容類型： `application/json`

## 建立臨機XDM類別和架構

為了透過來源連接器將外部資料匯入平台，必須為原始來源資料建立臨機XDM類別和架構。

若要建立臨機類別和架構，請依照臨機架構教學課程中 [所述的步驟進行](../../../../xdm/tutorials/ad-hoc.md)。 建立臨機類別時，來源資料中找到的所有欄位都必須在請求內文中說明。

請繼續遵循開發人員指南中所述的步驟，直到您建立臨機架構為止。 取得並儲存臨機結構的唯一識別碼(`$id`)，然後繼續本教學課程的下一步。

## 建立源連接 {#source}

現在，只要建立臨機XDM架構，就可以使用Flow Service API的POST要求建立來源連線。 源連接由基本連接、源資料檔案和描述源資料的模式的引用組成。

**API格式**

```http
POST /sourceConnections
```

**請求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Source Connection for database or NoSQL",
        "baseConnectionId": "54c22133-3a01-4d3b-8221-333a01bd3b03",
        "description": "Source Connection for database or NoSQL to ingest test1.Mytable",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c8c2b32d6f6a53d5ffc7212c37b3a9369282404a7bd551e8",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "test1.Mytable"
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
}'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `baseConnectionId` | 資料庫或NoSQL系統的基本連接的ID。 |
| `data.schema.id` | 臨 `$id` 機XDM架構。 |
| `params.path` | 源檔案的路徑。 |
| `connectionSpec.id` | 資料庫或NoSQL系統的連接規範ID。 |

**回應**

成功的響應返回新建立的源連`id`接的唯一標識符()。 在後續步驟中需要此ID才能建立目標連線。

```json
{
    "id": "beefc650-f2dc-45e2-afc6-50f2dcc5e2b8",
    "etag": "\"1600f153-0000-0200-0000-5e4710880000\""
}
```

## 建立目標XDM模式 {#target}

在之前的步驟中，會建立臨機XDM架構來結構來源資料。 為了讓源資料用於平台，還必須建立目標模式以根據您的需求來構建源資料。 然後，目標模式用於建立包含源資料的平台資料集。 此目標XDM模式還擴展了XDM Individual Profile類。

通過對方案註冊表API執行POST請求，可以建立目標XDM [方案](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)。 如果您想要在Experience Platform中使用使用者介面， [](../../../../xdm/tutorials/create-schema-ui.md) Schema Editor教學課程會提供在Schema Editor中執行類似動作的逐步指示。

**API格式**

```http
POST /tenant/schemas
```

**請求**

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
        "title": "Target schema for database or NoSQL",
        "description": "Target schema for database or NoSQL",
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
            }
        ],
    }'
```

**回應**

成功的回應會傳回新建立之架構的詳細資料，包括其唯一識別碼(`$id`)。 在後續步驟中需要此ID，才能建立目標資料集、對應和資料流。

```json
{
    "$id": "https://ns.adobe.com/{TENANT}/schemas/a9d63c5e3fab2687e064577959d0b91e274823f91f2f578e",
    "meta:altId": "_{TENANT}.schemas.a9d63c5e3fab2687e064577959d0b91e274823f91f2f578e",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for database or NoSQL",
    "type": "object",
    "description": "Target schema for database or NoSQL",
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
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/common/extensible"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1581716110281,
        "repo:lastModifiedDate": 1581716110281,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "6360f2175b40462ff25ec8735dc93a7e3af6a8faadd80a1cc500a59721e1a424"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "{TENANT_ID}"
}
```

## 建立目標資料集

目標資料集可以通過對目錄服務 [API執行POST請求](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，提供裝載內目標方案的ID來建立。

**API格式**

```http
POST /dataSets
```

**請求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Target Dataset for database or NoSQL",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/a9d63c5e3fab2687e064577959d0b91e274823f91f2f578e",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `schemaRef.id` | 目標XDM架構的ID。 |

**回應**

成功的回應會傳回包含新建立資料集ID的陣列，格式為 `"@/datasets/{DATASET_ID}"`。 資料集ID是唯讀、系統產生的字串，用於在API呼叫中參考資料集。 在後續步驟中，依需要儲存目標資料集ID以建立目標連線和資料流。

```json
[
    "@/dataSets/5e47161fa49bb818ad7f47bd"
]
```

## 建立資料集基礎連線

為了將外部資料收入Platform，必須先取得Experience Platform資料集基本連線。

要建立資料集基礎連接，請遵循資料集基礎連接教 [程中介紹的步驟](../create-dataset-base-connection.md)。

請繼續遵循開發人員指南中所述的步驟，直到您建立資料集基本連線為止。 取得並儲存唯一識別碼(`$id`)，並繼續在下個步驟中，將它當做基本連線ID來建立目標連線。

## 建立目標連接

您現在擁有資料集基本連線、目標架構和目標資料集的唯一識別碼。 使用這些識別碼，您可以使用Flow Service API建立目標連線，以指定將包含傳入來源資料的資料集。

**API格式**

```http
POST /targetConnections
```

**請求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "baseConnectionId": "d6c3988d-14ef-4000-8398-8d14ef000021",
        "name": "Target Connection for database or NoSQL",
        "description": "Target Connection for database or NoSQL",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/a9d63c5e3fab2687e064577959d0b91e274823f91f2f578e",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5e47161fa49bb818ad7f47bd"
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `baseConnectionId` | 資料集基礎連線的ID。 |
| `data.schema.id` | 目 `$id` 標XDM模式的。 |
| `params.dataSetId` | 目標資料集的ID。 |
| `connectionSpec.id` | 第三方資料庫的連接規範ID。 |

>[!NOTE] 建立目標連線時，請務必針對基本連線使用資料集基本連線值，而非 `id` 使用協力廠商來源連線的基本連線。

**回應**

成功的回應會傳回新目標連線的唯一識別碼(`id`)。 在後續步驟中需要此值才能建立資料流。

```json
{
    "id": "4f3845b6-87d9-4702-b845-b687d9270297",
    "etag": "\"2a007aa8-0000-0200-0000-5e597aaf0000\""
}
```

## 建立對應 {#mapping}

為了將源資料引入目標資料集，必須首先將其映射到目標資料集所遵守的目標模式。 這是透過對轉換服務API執行POST請求，並在請求裝載中定義資料映射來實現的。

**API格式**

```http
POST /mappingSets
```

**請求**

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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/a9d63c5e3fab2687e064577959d0b91e274823f91f2f578e",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "person.name",
                "sourceAttribute": "Name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "mobilePhone.number",
                "sourceAttribute": "Phone",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "personalEmail.address",
                "sourceAttribute": "email",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `xdmSchema` | 目 `$id` 標XDM模式的。 |

**回應**

成功的回應會傳回新建立之對應的詳細資訊，包括其唯一識別碼(`id`)。 在後續步驟中需要此ID才能建立資料流。

```json
{
    "id": "ab91c736-1f3d-4b09-8424-311d3d3e3cea",
    "version": 1,
    "createdDate": 1568047685000,
    "modifiedDate": 1568047703000,
    "inputSchemaRef": {
        "id": null,
        "contentType": null
    },
    "outputSchemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/efea012ad5deefcdf51afd23ceb3583f",
        "contentType": "1.0"
    },
    "mappings": [
        {
            "id": "7bbea5c0f0ef498aa20aa2e2e5c22290",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "Id",
            "destination": "_id",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "Id",
            "destinationXdmPath": "_id"
        },
        {
            "id": "def7fd7db2244f618d072e8315f59c05",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "FirstName",
            "destination": "person.name.firstName",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "FirstName",
            "destinationXdmPath": "person.name.firstName"
        },
        {
            "id": "e974986b28c74ed8837570f421d0b2f4",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "LastName",
            "destination": "person.name.lastName",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "LastName",
            "destinationXdmPath": "person.name.lastName"
        }
    ],
    "status": "PUBLISHED",
    "xdmVersion": "1.0",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2574494fdb01fa14c25b52d717ccb828",
        "contentType": "1.0"
    },
    "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2574494fdb01fa14c25b52d717ccb828"
}
```

## 查找資料流規範 {#specs}

資料流負責從源收集資料並將其引入平台。 要建立資料流，必須首先通過對流服務API執行GET請求來獲取資料流規範。 資料流規範負責從外部資料庫或NoSQL系統收集資料。

**API格式**

```http
GET /flowSpecs?property=name=="CRMToAEP"
```

**請求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="CRMToAEP"' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回負責將資料從資料庫或NoSQL系統帶入平台的資料流規範的詳細資訊。 在下一步中需要此ID才能建立新的資料流。

```json
{
    "items": [
        {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "name": "CRMToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "transformationSpecs": [
                {
                    "name": "Copy",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "properties": {
                            "deltaColumn": {
                                "type": "object",
                                "properties": {
                                    "name": {
                                        "type": "string"
                                    },
                                    "dateFormat": {
                                        "type": "string"
                                    },
                                    "timezone": {
                                        "type": "string"
                                    }
                                },
                                "required": [
                                    "name"
                                ]
                            }
                        },
                        "required": [
                            "deltaColumn"
                        ]
                    }
                },
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
            }
        }
    ]
}
```

## 建立資料流

收集資料的最後一步是建立資料流。 此時，您應準備下列必要值：

* [源連接ID](#source)
* [目標連線ID](#target)
* [對應ID](#mapping)
* [資料流規範ID](#specs)

資料流負責調度和收集源中的資料。 您可以通過執行POST請求來建立資料流，同時在裝載中提供先前提到的值。

**API格式**

```http
POST /flows
```

**請求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dataflow between database or NoSQL Platform",
        "description": "Inbound data to Platform",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "beefc650-f2dc-45e2-afc6-50f2dcc5e2b8"
        ],
        "targetConnectionIds": [
            "4f3845b6-87d9-4702-b845-b687d9270297"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "deltaColumn": {
                        "name": "updatedAt",
                        "dateFormat": "YYYY-MM-DD",
                        "timezone": "UTC"
                    }
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "ab91c736-1f3d-4b09-8424-311d3d3e3cea",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1567411548",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `flowSpec.id` | 與資料庫或NoSQL系統關聯的資料流規範ID。 |
| `sourceConnectionIds` | 與資料庫或NoSQL系統關聯的源連接ID。 |
| `targetConnectionIds` | 與資料庫或NoSQL系統關聯的目標連接ID。 |
| `transformations.params.mappingId` | 與資料庫或NoSQL系統關聯的映射ID。 |

**回應**

成功的響應返回新創`id`建的資料流的ID()。

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```

## 後續步驟

在本教程中，您建立了源連接器，以按計畫從資料庫或NoSQL系統收集資料。 現在，下游平台服務（例如即時客戶個人檔案和資料科學工作區）可以使用傳入的資料。 如需詳細資訊，請參閱下列檔案：

* [即時客戶個人檔案總覽](../../../../profile/home.md)
* [資料科學工作區概觀](../../../../data-science-workspace/home.md)