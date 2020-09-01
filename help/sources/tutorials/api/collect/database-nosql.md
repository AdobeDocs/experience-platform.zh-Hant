---
keywords: Experience Platform;home;popular topics;third-party database;third party database
solution: Experience Platform
title: 透過來源連接器和API，從協力廠商資料庫收集資料
topic: overview
description: 本教學課程涵蓋從協力廠商資料庫擷取資料，並透過來源連接器和API將其匯入平台的步驟。
translation-type: tm+mt
source-git-commit: 6f4714561c2946a084eed4e89d3148df5b8044f5
workflow-type: tm+mt
source-wordcount: '1650'
ht-degree: 1%

---


# 透過來源連接器和API，從協力廠商資料庫收集資料

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程涵蓋從協力廠商資料庫擷取資料，並透過來源連接器 [!DNL Platform] 和 [[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) API將其內嵌至其中的步驟。

## 快速入門

本教學課程要求您必須與第三方資料庫建立有效的連線，以及您要放入之檔案的相關資訊 [!DNL Platform] （包括檔案的路徑和結構）。 如果您沒有此資訊，請先參閱教學課程， [在嘗試本教學課程之前，使用Flow Service API探索資料庫](../explore/database-nosql.md) 。

本教學課程也要求您對Adobe Experience Platform的下列元件有正確的認識：

* [[!DNL體驗資料模型(XDM)系統]](../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構註冊開發人員指南](../../../../xdm/api/getting-started.md):包含您必須知道的重要資訊，以便成功執行對架構註冊表API的呼叫。 這包括您 `{TENANT_ID}`的「容器」概念，以及提出要求所需的標題（請特別注意「接受」標題及其可能的值）。
* [[!DNL目錄服務]](../../../../catalog/home.md):目錄是記錄資料位置和世系的系統 [!DNL Experience Platform]。
* [[!DNL批處理提取]](../../../../ingestion/batch-ingestion/overview.md):「批次擷取API」可讓您將資料擷取為 [!DNL Experience Platform] 批次檔案。
* [沙盒](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用 [[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) API成功連線至協力廠商資料庫。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

中的所有資 [!DNL Experience Platform]源(包括屬於這些資源 [!DNL Flow Service])都隔離到特定的虛擬沙盒。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* `Content-Type: application/json`

## 建立源連接 {#source}

您可以對 [!DNL Flow Service] API提出POST要求，以建立來源連線。 源連接由連接ID、源資料檔案的路徑和連接規範ID組成。

要建立源連接，還必須為資料格式屬性定義枚舉值。

對基於檔案的連接器使 **用下列枚舉值**:

| Data.format | 列舉值 |
| ----------- | ---------- |
| 分隔檔案 | `delimited` |
| JSON檔案 | `json` |
| 拼花檔案 | `parquet` |

對於所 **有基於表的連接器** ，請使用枚舉值： `tabular`.

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
        "name": "Database Source Connector",
        "baseConnectionId": "d5cbb5bc-44cc-41a2-8bb5-bc44ccf1a2fb",
        "description": "A test source connector for a third-party database",
        "data": {
            "format": "tabular",
        },
        "params": {
            "path": "ADMIN.E2E"
        },
        "connectionSpec": {
            "id": "d6b52d86-f0f8-475f-89d4-ce54c8527328",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `baseConnectionId` | 第三方資料庫源的連接ID。 |
| `params.path` | 源檔案的路徑。 |
| `connectionSpec.id` | 第三方資料庫源的連接規範ID。 有關資料庫 [規範ID的清單](#appendix) ，請參見附錄。 |

**回應**

成功的響應返回新建立的源連`id`接的唯一標識符()。 在後續步驟中需要此ID才能建立目標連線。

```json
{
    "id": "2f7356d9-a866-47ea-b356-d9a86687ea7a",
    "etag": "\"c8006055-0000-0200-0000-5ecd79520000\""
}
```

## 建立目標XDM模式 {#target-schema}

在之前的步驟中，會建立臨機XDM架構來結構來源資料。 為了使用源資料，還必須創 [!DNL Platform]建目標模式，以根據您的需要構建源資料。 然後，目標模式用於建立包含 [!DNL Platform] 源資料的資料集。 此目標XDM模式還擴展了 [!DNL XDM Individual Profile] 類。

通過對方案註冊表API執行POST請求，可以建立目標XDM [方案](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)。 如果希望在中使用用戶介面 [!DNL Experience Platform], [](../../../../xdm/tutorials/create-schema-ui.md) Schema Editor教程將提供在Schema Editor中執行類似操作的逐步說明。

**API格式**

```http
POST /tenant/schemas
```

**請求**

以下示例請求建立了擴展XDM類的XDM [!DNL Individual Profile] 架構。

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
        "title": "Database Source Connector Target Schema",
        "description": "Target schema for a third-party database",
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

成功的回應會傳回新建立之架構的詳細資料，包括其唯一識別碼(`$id`)。 在後續步驟中需要此ID，才能建立目標資料集、對應和資料流。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/c44dd18673370dbf16243ba6e6fd9ae62c7916ec10477727",
    "meta:altId": "_{TENANT_ID}.schemas.c44dd18673370dbf16243ba6e6fd9ae62c7916ec10477727",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for an Oracle connector 5/26/20",
    "type": "object",
    "description": "Target schema for Database",
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
        "repo:createdDate": 1590523478581,
        "repo:lastModifiedDate": 1590523478581,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "34fdf36fc3029999a07270c4e7719d8a627f7e93e2fbc13888b3c11fb08983c0",
        "meta:globalLibVersion": "1.10.2.1"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
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
        "name": "Target dataset for a third-party database source connector",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c44dd18673370dbf16243ba6e6fd9ae62c7916ec10477727",
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
    "@/dataSets/5ecd766e4bab17191b78e892"
]
```

## 建立目標連接 {#target-connection}

您現在擁有資料集基本連線、目標架構和目標資料集的唯一識別碼。 使用這些標識符，可以使用 [[!DNL流服務]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) API建立目標連接，以指定將包含入站源資料的資料集。

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
        "name": "Target Connection for a third-party database source connector",
        "description": "Target Connection for a third-party database source connector",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c44dd18673370dbf16243ba6e6fd9ae62c7916ec10477727",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5ecd766e4bab17191b78e892"
        },
            "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `data.schema.id` | 目 `$id` 標XDM模式的。 |
| `params.dataSetId` | 在上一步驟中收集的目標資料集的ID。 |
| `connectionSpec.id` | 資料湖的固定連接規範ID。 此連接規範ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**回應**

成功的回應會傳回新目標連線的唯一識別碼(`id`)。 在後續步驟中需要此值才能建立資料流。

```json
{
    "id": "e66fdb22-06df-48ac-afdb-2206dff8ac10",
    "etag": "\"7e03773a-0000-0200-0000-5ecd768d0000\""
}
```

## 建立對應 {#mapping}

為了將源資料引入目標資料集，必須首先將其映射到目標資料集所遵守的目標模式。 這是透過對API執行POST請求，並在請求裝載中 [!DNL Conversion Service] 定義資料映射來實現的。

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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c44dd18673370dbf16243ba6e6fd9ae62c7916ec10477727",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "person.name.fullName",
                "sourceAttribute": "NAME",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_repo.createDate",
                "sourceAttribute": "DOB",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "ID",
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
    "id": "d9d94124417d4df48ea3d00e28eb4327",
    "version": 0,
    "createdDate": 1590523552440,
    "modifiedDate": 1590523552440,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 檢索資料流規範 {#specs}

資料流負責從源收集資料並將其引入 [!DNL Platform]。 要建立資料流，必須首先通過對 [[!DNL流服務]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) API執行GET請求來獲取資料流規範。 資料流規範負責從外部資料庫或NoSQL系統收集資料。

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

成功的響應返回負責將資料從資料庫或NoSQL系統帶入資料的資料流規範的詳細資訊 [!DNL Platform]。 在下一步中需要此ID才能建立新的資料流。

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

若要排程擷取，您必須先將開始時間值設定為以秒為單位的紀元時間。 然後，您必須將頻率值設為以下五個選項之一： `once`、 `minute`、 `hour`、 `day`或 `week`。 間隔值指定兩個連續的提取之間的期間，並且建立一次性提取不需要設定間隔。 對於所有其它頻率，間隔值必須設定為等於或大於 `15`。

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
        "name": "Dataflow for a third-party database and Platform,
        "description": "collecting ADMIN.E2E",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "89cf81c9-47b4-463a-8f81-c947b4863afb"
        ],
        "targetConnectionIds": [
            "e66fdb22-06df-48ac-afdb-2206dff8ac10"
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
                    "mappingId": "d9d94124417d4df48ea3d00e28eb4327",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1590523836",
            "frequency":"minute",
            "interval":"15",
            "backfill": "true"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `flowSpec.id` | 在上 [一步驟中檢索的流式規範ID](#specs) 。 |
| `sourceConnectionIds` | 在先 [前步驟中擷取的來源連線ID](#source) 。 |
| `targetConnectionIds` | 在先 [前步驟中擷取的目標連線ID](#target-connection) 。 |
| `transformations.params.mappingId` | 在先 [前步驟中擷取](#mapping) 的對應ID。 |
| `transformations.params.deltaColum` | 用於區分新資料和現有資料的指定欄。 增量資料將根據選取欄的時間戳記進行擷取。 支援的日期格 `deltaColumn` 式 `yyyy-MM-dd HH:mm:ss`為。 如果您使用Azure表格儲存，則支援的格 `deltaColumn` 式為 `yyyy-MM-ddTHH:mm:ssZ`。 |
| `transformations.params.mappingId` | 與資料庫關聯的映射ID。 |
| `scheduleParams.startTime` | 資料流在時代時間中的開始時間。 |
| `scheduleParams.frequency` | 資料流收集資料的頻率。 可接受的值包括： `once`、 `minute`、 `hour`、 `day`或 `week`。 |
| `scheduleParams.interval` | 該間隔用於指定兩個連續流運行之間的期間。 間隔的值應為非零整數。 當頻率設為且應大於或等於其 `once` 他頻率值時，不需要 `15` 間隔。 |

**回應**

成功的響應返回新創`id`建的資料流的ID()。

```json
{
    "id": "e0bd8463-0913-4ca1-bd84-6309134ca1f6",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## 監控資料流

建立資料流後，您可以監視通過其接收的資料，以查看有關流運行、完成狀態和錯誤的資訊。 有關如何監視資料流的詳細資訊，請參見API中有關監 [視資料流的教程 ](../monitor.md)


## 後續步驟

在本教學課程中，您已建立來源連接器，以依排程從協力廠商資料庫收集資料。 現在，下游服務（例如和）可 [!DNL Platform] 以使用傳入 [!DNL Real-time Customer Profile] 的資料 [!DNL Data Science Workspace]。 如需詳細資訊，請參閱下列檔案：

* [即時客戶個人檔案總覽](../../../../profile/home.md)
* [資料科學工作區概觀](../../../../data-science-workspace/home.md)

## 附錄

下節列出不同的雲儲存源連接器及其連接規範。

### 連接規範

| 連接器名稱 | 連接規範ID |
| -------------- | --------------- |
| [!DNL Amazon Redshift] | `3416976c-a9ca-4bba-901a-1f08f66978ff` |
| [!DNL Apache Hive] on [!DNL Azure HDInsights] | `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f` |
| [!DNL Apache Spark] on [!DNL Azure HDInsights] | `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |
| [!DNL Azure Data Explorer] | `0479cc14-7651-4354-b233-7480606c2ac3` |
| [!DNL Azure Synapse Analytics] | `a49bcc7d-8038-43af-b1e4-5a7a089a7d79` |
| [!DNL Azure Table Storage] | `ecde33f2-c56f-46cc-bdea-ad151c16cd69` |
| [!DNL CouchBase] | `1fe283f6-9bec-11ea-bb37-0242ac130002` |
| [!DNL Google BigQuery] | `3c9b37f8-13a6-43d8-bad3-b863b941fedd` |
| [!DNL IBM DB2] | `09182899-b429-40c9-a15a-bf3ddbc8ced7` |
| [!DNL MariaDB] | `000eb99-cd47-43f3-827c-43caf170f015` |
| [!DNL Microsoft SQL Server] | `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec` |
| [!DNL MySQL] | `26d738e0-8963-47ea-aadf-c60de735468a` |
| [!DNL Oracle] | `d6b52d86-f0f8-475f-89d4-ce54c8527328` |
| [!DNL Phoenix] | `102706fb-a5cd-42ee-afe0-bc42f017ff43` |
| [!DNL PostgreSQL] | `74a1c565-4e59-48d7-9d67-7c03b8a13137` |