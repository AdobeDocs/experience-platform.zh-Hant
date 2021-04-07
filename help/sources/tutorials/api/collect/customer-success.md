---
keywords: Experience Platform；首頁；熱門主題；收集客戶成功；客戶成功
solution: Experience Platform
title: 使用來源連接器和API從客戶成功系統收集資料
topic: 概述
type: 教學課程
description: 本教學課程涵蓋從客戶成功系統擷取資料，並使用來源連接器和API將其匯入平台的步驟。
exl-id: 0fae04d0-164b-4113-a274-09677f4bbde5
translation-type: tm+mt
source-git-commit: 610ce5c6dca5e7375b941e7d6f550382da10ca27
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 1%

---

# 使用來源連接器和API從客戶成功系統收集資料

本教學課程涵蓋從協力廠商客戶成功系統擷取資料，並透過來源連接器和[[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) API將其內嵌至[!DNL Platform]的步驟。

## 快速入門

本教學課程要求您透過有效的連線和您要匯入[!DNL Platform]之檔案的相關資訊（包括檔案的路徑和結構），存取協力廠商客戶成功系統。 如果您沒有此資訊，請先參閱有關[使用流服務API](../explore/customer-success.md)瀏覽資料庫或NoSQL系統的教程，然後再嘗試本教程。

本教學課程還要求您對Adobe Experience Platform的以下部分有切實的瞭解：

* [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構註冊開發人員指南](../../../../xdm/api/getting-started.md):包含您必須知道的重要資訊，以便成功執行對架構註冊表API的呼叫。這包括您的`{TENANT_ID}`、&quot;containers&quot;的概念，以及提出要求時所需的標題（請特別注意「接受」標題及其可能的值）。
* [[!DNL Catalog Service]](../../../../catalog/home.md):目錄是記錄資料位置和世系的系統 [!DNL Experience Platform]。
* [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md):「批次擷取API」可讓您將資料以批次檔 [!DNL Experience Platform] 案的形式擷取。
* [沙盒](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要瞭解的其他資訊，以便使用[!DNL Flow Service] API成功連線至客戶成功系統。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要附加的媒體類型標題：

* `Content-Type: application/json`

## 建立源連接{#source}

您可以通過向[!DNL Flow Service] API發出POST請求來建立源連接。 源連接由連接ID、源資料檔案的路徑和連接規範ID組成。

要建立源連接，還必須為資料格式屬性定義枚舉值。

對基於檔案的連接器使用以下枚舉值：

| 資料格式 | 列舉值 |
| ----------- | ---------- |
| 分隔字元 | `delimited` |
| JSON | `json` |
| 鑲木 | `parquet` |

對於所有基於表的連接器，請設定值`tabular`。

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
        "name": "Source connection for Customer Success",
        "baseConnectionId": "f1da3694-38a9-403d-9a36-9438a9203d42",
        "description": "Source connection for a Customer Success connector",
        "data": {
            "format": "tabular",
        },
        "params": {
            "tableName": "Account",
            "columns": [
                {
                    "name": "Id",
                    "type": "string",
                    "xdm": {
                        "type": "string"
                    }
                },
                {
                    "name": "Name",
                    "type": "string",
                    "xdm": {
                        "type": "string"
                    }
                },
                {
                    "name": "Phone",
                    "type": "string",
                    "xdm": {
                        "type": "string"
                    }
                },
                {
                    "name": "CreatedDate",
                    "type": "string",
                    "meta:xdmType": "date-time",
                    "xdm": {
                        "type": "string",
                        "format": "date-time"
                    }
                }
            ]
        },
        "connectionSpec": {
            "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `baseConnectionId` | 您存取之協力廠商客戶成功系統的唯一連線ID。 |
| `params.path` | 源檔案的路徑。 |
| `connectionSpec.id` | 與特定第三方客戶成功系統關聯的連接規範ID。 有關連接規範ID的清單，請參見[附錄](#appendix)。 |

**回應**

成功的響應返回新建源連接的唯一標識符(`id`)。 在後續步驟中需要此ID才能建立目標連線。

```json
{
    "id": "17faf955-2cf8-4b15-baf9-552cf88b1540",
    "etag": "\"2900a761-0000-0200-0000-5ed18cea0000\""
}
```

## 建立目標XDM模式{#target-schema}

為了讓源資料用於平台，必須建立目標模式以根據您的需要來構建源資料。 然後，目標模式用於建立包含源資料的平台資料集。

通過對[方案註冊表API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)執行POST請求，可以建立目標XDM方案。

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
        "title": "Target schema for a Customer Success connector",
        "description": "Target schema for a customer success connector",
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
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/b750bd161fef405bc324d0c8809b02c494d73e60e7ae9b3e",
    "meta:altId": "_{TENANT_ID}.schemas.b750bd161fef405bc324d0c8809b02c494d73e60e7ae9b3e",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for a Customer Success connector",
    "type": "object",
    "description": "Target schema for a customer success connector",
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
        "repo:createdDate": 1590791550228,
        "repo:lastModifiedDate": 1590791550228,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "d730441903b95425145d9c742647ab4426d86549159182913e5f99cc904be5b1",
        "meta:globalLibVersion": "1.10.4.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 建立目標資料集

通過對[目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)執行POST請求，提供裝載內目標方案的ID，可以建立目標資料集。

**API格式**

```http
POST catalog/dataSets
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
        "name": "Target dataset for a Customer Success connector",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/b750bd161fef405bc324d0c8809b02c494d73e60e7ae9b3e",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `schemaRef.id` | 目標XDM架構的`$id`。 |
| `schemaRef.contentType` | 架構的版本。 此值必須設定為`application/vnd.adobe.xed-full-notext+json;version=1` ，以返回方案的最新次要版本。 |

**回應**

成功的響應返回一個陣列，該陣列包含以`"@/datasets/{DATASET_ID}"`格式新建立的資料集的ID。 資料集ID是唯讀、系統產生的字串，用於在API呼叫中參考資料集。 在後續步驟中，依需要儲存目標資料集ID以建立目標連線和資料流。

```json
[
    "@/dataSets/5ed18e0f4f90b719196f44a9"
]
```

## 建立目標連接{#target-connection}

目標連接表示到所收錄資料所在目的地的連接。 要建立目標連接，必須提供與「資料湖」關聯的固定連接規範ID。 此連接規範ID為：`c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

您現在擁有目標資料集的唯一識別碼、目標模式，以及與資料湖的連線規範ID。 使用[!DNL Flow Service] API，您可以指定這些識別碼以及包含傳入來源資料的資料集來建立目標連線。

**API格式**

```http
POST /targetConnections
```

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Target Connection for a customer success connector",
        "description": "Target Connection for a customer success connector",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/deb3e1096c35d8311b5d80868c4bd5b3cdfd4b3150e7345f",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5e543e8a60b15218ad44b95f"
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
| `connectionSpec.id` | 用於連接到資料湖的連接規範ID。 此ID為：`c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |

**回應**

成功的響應返回新目標連接的唯一標識符(`id`)。 在後續步驟中需要此值才能建立資料流。

```json
{
    "id": "1f5af99c-f1ef-4076-9af9-9cf1ef507678",
    "etag": "\"530013e2-0000-0200-0000-5ebc4c110000\""
}
```

## 建立映射{#mapping}

為了將源資料引入目標資料集，必須首先將其映射到目標資料集所遵守的目標模式。 這是透過對[!DNL Conversion Service] API執行POST請求，並在請求裝載中定義資料映射來實現的。

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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/b750bd161fef405bc324d0c8809b02c494d73e60e7ae9b3e",
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
                "destinationXdmPath": "person.name.fullName",
                "sourceAttribute": "Name",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_repo.createDate",
                "sourceAttribute": "CreatedDate",
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
| `xdmSchema` | 目標XDM架構的`$id`。 |

**回應**

成功的響應返回新建立映射的詳細資訊，包括其唯一標識符(`id`)。 在後續步驟中需要此ID才能建立資料流。

```json
{
    "id": "7c3547d3cfc14f568a51c32b4c0ed739",
    "version": 0,
    "createdDate": 1590792069173,
    "modifiedDate": 1590792069173,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 檢索資料流規範{#specs}

資料流負責從源收集資料並將其引入平台。 要建立資料流，必須首先通過對流服務API執行GET請求來獲取資料流規範。 資料流規範負責從第三方客戶成功系統收集資料。

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

成功的響應返回負責將源資料帶入平台的資料流規範的詳細資訊。 響應包括建立新資料流所需的唯一流規範`id`。

```json
{
    "items": [
        {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "name": "CRMToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "3416976c-a9ca-4bba-901a-1f08f66978ff",
                "38ad80fe-8b06-4938-94f4-d4ee80266b07",
                "d771e9c1-4f26-40dc-8617-ce58c4b53702",
                "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
                "3000eb99-cd47-43f3-827c-43caf170f015",
                "26d738e0-8963-47ea-aadf-c60de735468a",
                "74a1c565-4e59-48d7-9d67-7c03b8a13137",
                "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
                "cb66ab34-8619-49cb-96d1-39b37ede86ea",
                "eb13cb25-47ab-407f-ba89-c0125281c563",
                "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
                "37b6bf40-d318-4655-90be-5cd6f65d334b",
                "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
                "221c7626-58f6-4eec-8ee2-042b0226f03b",
                "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
                "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
                "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
                "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
                "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
                "102706fb-a5cd-42ee-afe0-bc42f017ff43",
                "09182899-b429-40c9-a15a-bf3ddbc8ced7",
                "0479cc14-7651-4354-b233-7480606c2ac3",
                "d6b52d86-f0f8-475f-89d4-ce54c8527328",
                "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
                "1fe283f6-9bec-11ea-bb37-0242ac130002"
            ],
            "targetConnectionSpecIds": [
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
            ],
            "optionSpec": {
                "name": "OptionSpec",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "errorDiagnosticsEnabled": {
                            "title": "Error diagnostics.",
                            "description": "Flag to enable detailed and sample error diagnostics summary.",
                            "type": "boolean",
                            "default": false
                        },
                        "partialIngestionPercent": {
                            "title": "Partial ingestion threshold.",
                            "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
                            "type": "number",
                            "exclusiveMinimum": 0
                        }
                    }
                }
            },
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
                        "frequency": {
                            "type": "string",
                            "enum": [
                                "once",
                                "minute",
                                "hour",
                                "day",
                                "week"
                            ]
                        },
                        "interval": {
                            "type": "integer"
                        },
                        "backfill": {
                            "type": "boolean",
                            "default": true
                        }
                    },
                    "required": [
                        "startTime",
                        "frequency"
                    ],
                    "if": {
                        "properties": {
                            "frequency": {
                                "const": "once"
                            }
                        }
                    },
                    "then": {
                        "allOf": [
                            {
                                "not": {
                                    "required": [
                                        "interval"
                                    ]
                                }
                            },
                            {
                                "not": {
                                    "required": [
                                        "backfill"
                                    ]
                                }
                            }
                        ]
                    },
                    "else": {
                        "required": [
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
            },
            "attributes": {
                "notification": {
                    "category": "sources",
                    "flowRun": {
                        "enabled": true
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

收集資料的最後一步是建立資料流。 此時，您應準備下列必要值：

* [源連接ID](#source)
* [目標連線ID](#target)
* [對應ID](#mapping)
* [資料流規範ID](#specs)

若要排程擷取，您必須先將開始時間值設定為以秒為單位的紀元時間。 然後，您必須將頻率值設為以下五個選項之一：`once`、`minute`、`hour`、`day`或`week`。 間隔值指定兩個連續的提取之間的期間，並且建立一次性提取不需要設定間隔。 對於所有其它頻率，間隔值必須設定為等於或大於`15`。

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
        "name": "Creating a dataflow for a Customer Success connector",
        "description": "Creating a dataflow for a Customer Success connector",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "17faf955-2cf8-4b15-baf9-552cf88b1540"
        ],
        "targetConnectionIds": [
            "bc36ecd6-3b04-4067-b6ec-d63b04b0673d"
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
                    "mappingId": "7c3547d3cfc14f568a51c32b4c0ed739",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1590792316",
            "frequency": "minute",
            "interval": "15",
            "backfill": "true"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `flowSpec.id` | 在上一步驟中檢索的[流規範ID](#specs)。 |
| `sourceConnectionIds` | 在先前步驟中檢索的[源連接ID](#source)。 |
| `targetConnectionIds` | 在先前步驟中擷取的[目標連線ID](#target-connection)。 |
| `transformations.params.mappingId` | 在先前步驟中檢索的[映射ID](#mapping)。 |
| `transformations.params.deltaColum` | 用於區分新資料和現有資料的指定欄。 增量資料將根據選取欄的時間戳記進行擷取。 `deltaColumn`支援的日期格式為`yyyy-MM-dd HH:mm:ss`。 |
| `transformations.params.mappingId` | 與資料庫關聯的映射ID。 |
| `scheduleParams.startTime` | 資料流在時代時間中的開始時間。 |
| `scheduleParams.frequency` | 資料流收集資料的頻率。 可接受的值包括：`once`、`minute`、`hour`、`day`或`week`。 |
| `scheduleParams.interval` | 該間隔用於指定兩個連續流運行之間的期間。 間隔的值應為非零整數。 當頻率設為`once`時，不需要間隔，對於其他頻率值，應大於或等於`15`。 |

**回應**

成功的響應返回新建立的資料流的ID `id`。

```json
{
    "id": "e0bd8463-0913-4ca1-bd84-6309134ca1f6",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## 監控資料流

建立資料流後，您可以監視通過其接收的資料，以查看有關流運行、完成狀態和錯誤的資訊。 有關如何監視資料流的詳細資訊，請參見API ](../monitor.md)中有關[監視資料流的教程

## 後續步驟

在本教學課程中，您已建立來源連接器，以依計畫從客戶成功系統收集資料。 現在，下游[!DNL Platform]服務（例如[!DNL Real-time Customer Profile]和[!DNL Data Science Workspace]）可以使用傳入的資料。 如需詳細資訊，請參閱下列檔案：

* [即時客戶個人檔案總覽](../../../../profile/home.md)
* [資料科學工作區概觀](../../../../data-science-workspace/home.md)

## 附錄

下節列出不同的雲儲存源連接器及其連接規範。

### 連接規範

| 連接器名稱 | 連接規範 |
| -------------- | --------------- |
| [!DNL Salesforce Service Cloud] | `cb66ab34-8619-49cb-96d1-39b37ede86ea` |
| [!DNL ServiceNow] | `eb13cb25-47ab-407f-ba89-c0125281c563` |
