---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 透過來源連接器和API，從客戶成功系統收集資料
topic: overview
translation-type: tm+mt
source-git-commit: 84ea3e45a3db749359f3ce4a0ea25429eee8bb66
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 1%

---


# 透過來源連接器和API，從客戶成功系統收集資料

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程涵蓋從客戶成功系統擷取資料並透過來源連接器和API [!DNL Platform] 將其吸收的步驟。

## 快速入門

本教學課程要求您透過有效的連線和您要放入之檔案的相關資訊，包括檔案的路徑和結構，來存取協力廠商 [!DNL Platform]客戶成功系統。 如果您沒有此資訊，請參閱教程，在嘗試本教 [程之前，使用流服務API來探索資料庫或NoSQL系統](../explore/customer-success.md) 。

本教學課程也要求您對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../xdm/home.md): 組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   * [架構構成基礎](../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構註冊開發人員指南](../../../../xdm/api/getting-started.md): 包含您必須知道的重要資訊，以便成功執行對架構註冊表API的呼叫。 這包括您 `{TENANT_ID}`的「容器」概念，以及提出要求所需的標題（請特別注意「接受」標題及其可能的值）。
* [目錄服務](../../../../catalog/home.md): 目錄是記錄資料位置和世系的系統 [!DNL Experience Platform]。
* [批次擷取](../../../../ingestion/batch-ingestion/overview.md): 「批次擷取API」可讓您將資料擷取為 [!DNL Experience Platform] 批次檔案。
* [沙盒](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要瞭解的其他資訊，以便使用 [!DNL Flow Service] API成功連線至客戶成功系統。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* 授權： 生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform]源(包括屬於這些資源 [!DNL Flow Service])都隔離到特定的虛擬沙盒。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* 內容類型： `application/json`

## 建立臨機XDM類別和架構

為了透過來源連接器將 [!DNL Platform] 外部資料匯入，必須為原始來源資料建立臨機XDM類別和架構。

若要建立臨機類別和架構，請依照臨機架構教學課程中 [所述的步驟進行](../../../../xdm/tutorials/ad-hoc.md)。 建立臨機類別時，來源資料中找到的所有欄位都必須在請求內文中說明。

請繼續遵循開發人員指南中所述的步驟，直到您建立臨機架構為止。 臨機架構的唯`$id`一識別碼()是繼續本教學課程的下一步驟的必要項。

## 建立源連接 {#source}

現在，只要建立臨機XDM架構，就可以使用API的POST要求建立來源連 [!DNL Flow Service] 線。 源連接由連接ID、源資料檔案和描述源資料的模式的引用組成。

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
        "name": "Source connection for Customer Success",
        "baseConnectionId": "f1da3694-38a9-403d-9a36-9438a9203d42",
        "description": "Source connection for a Customer Success connector",
        "data": {
            "format": "tabular",
            "schema": {
                "id": "https://ns.adobe.com/adobe_mcdp_connectors_stg/classes/5d032b2230d5495aef49437d04d1c5fac4788b17ae85bf93",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "Account"
        },
        "connectionSpec": {
            "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
            "version": "1.0"
        }
    }}'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `baseConnectionId` | 您存取之協力廠商客戶成功系統的唯一連線ID。 |
| `data.schema.id` | 臨 `$id` 機XDM架構。 |
| `params.path` | 源檔案的路徑。 |
| `connectionSpec.id` | 與特定第三方客戶成功系統關聯的連接規範ID。 有關連 [接規範](#appendix) ID的清單，請參見附錄。 |

**回應**

成功的響應返回新建立的源連`id`接的唯一標識符()。 在後續步驟中需要此ID才能建立目標連線。

```json
{
    "id": "17faf955-2cf8-4b15-baf9-552cf88b1540",
    "etag": "\"2900a761-0000-0200-0000-5ed18cea0000\""
}
```

## 建立目標XDM模式 {#target}

在之前的步驟中，會建立臨機XDM架構來結構來源資料。 為了使用源資料，還必須創 [!DNL Platform]建目標模式，以根據您的需要構建源資料。 然後，目標模式用於建立包含 [!DNL Platform] 源資料的資料集。 此目標XDM模式還擴展了XDM Individual Profile類。

通過對方案註冊表API執行POST請求，可以建立目標XDM [方案](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)。

如果希望在中使用用戶介面 [!DNL Experience Platform], [](../../../../xdm/tutorials/create-schema-ui.md) Schema Editor教程將提供在Schema Editor中執行類似操作的逐步說明。

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
        "description": "Target schema for Database",
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
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/b750bd161fef405bc324d0c8809b02c494d73e60e7ae9b3e",
    "meta:altId": "_{TENANT_ID}.schemas.b750bd161fef405bc324d0c8809b02c494d73e60e7ae9b3e",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for a Customer Success connector",
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

目標資料集可以通過對目錄服務 [API執行POST請求](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，提供裝載內目標方案的ID來建立。

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
| `schemaRef.id` | 目 `$id` 標XDM模式的。 |

**回應**

成功的回應會傳回包含新建立資料集ID的陣列，格式為 `"@/datasets/{DATASET_ID}"`。 資料集ID是唯讀、系統產生的字串，用於在API呼叫中參考資料集。 在後續步驟中，依需要儲存目標資料集ID以建立目標連線和資料流。

```json
[
    "@/dataSets/5ed18e0f4f90b719196f44a9"
]
```

## 建立目標連接

目標連接表示到所收錄資料所在目的地的連接。 要建立目標連接，必須提供與資料庫關聯的固定連接規範ID。 此連接規範ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

您現在擁有目標資料集的目標模式及與資料湖的連線規格ID作為唯一識別碼。 使用這些識別碼，您可以使用 [!DNL Flow Service] API建立目標連線，以指定將包含傳入來源資料的資料集。

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
        "baseConnectionId": "d6c3988d-14ef-4000-8398-8d14ef000021",
        "name": "Target Connection for CS",
        "description": "Target Connection for CS",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}}/schemas/deb3e1096c35d8311b5d80868c4bd5b3cdfd4b3150e7345f",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5e543e8a60b15218ad44b95f"
        },
            "connectionSpec": {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `data.schema.id` | 目 `$id` 標XDM模式的。 |
| `params.dataSetId` | 目標資料集的ID。 |
| `connectionSpec.id` | 已修正連接規範ID到資料湖。 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**回應**

成功的回應會傳回新目標連線的唯一識別碼(`id`)。 在後續步驟中需要此值才能建立資料流。

```json
{
    "id": "1f5af99c-f1ef-4076-9af9-9cf1ef507678",
    "etag": "\"530013e2-0000-0200-0000-5ebc4c110000\""
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
| `xdmSchema` | 目 `$id` 標XDM模式的。 |

**回應**

成功的回應會傳回新建立之對應的詳細資訊，包括其唯一識別碼(`id`)。 在後續步驟中需要此ID才能建立資料流。

```json
{
    "id": "7c3547d3cfc14f568a51c32b4c0ed739",
    "version": 0,
    "createdDate": 1590792069173,
    "modifiedDate": 1590792069173,
    "createdBy": "28AF22BA5DE6B0B40A494036@AdobeID",
    "modifiedBy": "28AF22BA5DE6B0B40A494036@AdobeID"
}
```

## 檢索資料流規範 {#specs}

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

成功的響應返回負責將客戶成功系統中的資料帶入資料流規範的詳細資訊 [!DNL Platform]。 在下一步中需要此ID才能建立新的資料流。

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
                        "name": "date-time"
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

**回應**

成功的響應返回新創 `id` 建的資料流的ID。

```json
{
    "id": "e0bd8463-0913-4ca1-bd84-6309134ca1f6",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

| 屬性 | 說明 |
| --- | --- |
| `flowSpec.id` | 在上一步中檢索的流規範ID。 |
| `sourceConnectionIds` | 在先前步驟中擷取的來源連線ID。 |
| `targetConnectionIds` | 在先前步驟中擷取的目標連線ID。 |
| `transformations.params.mappingId` | 在先前步驟中擷取的對應ID。 |
| `scheduleParams.startTime` | 資料流的開始時間（以秒為單位）。 |
| `scheduleParams.frequency` | 可選頻率值包括： `once`、 `minute`、 `hour`、 `day`或 `week`。 |
| `scheduleParams.interval` | 該間隔用於指定兩個連續流運行之間的期間。 間隔的值應為非零整數。 當頻率設為且應大於或等於其 `once` 他頻率值時，不需要 `15` 間隔。 |

## 後續步驟

在本教學課程中，您已建立來源連接器，以依計畫從客戶成功系統收集資料。 現在，下游服務（例如和）可 [!DNL Platform] 以使用傳入 [!DNL Real-time Customer Profile] 的資料 [!DNL Data Science Workspace]。 如需詳細資訊，請參閱下列檔案：

* [即時客戶個人檔案總覽](../../../../profile/home.md)
* [資料科學工作區概觀](../../../../data-science-workspace/home.md)

## 附錄

下節列出不同的雲儲存源連接器及其連接規範。

### 連接規範

| 連接器名稱 | 連接規範 |
| -------------- | --------------- |
| [!DNL Salesforce Service Cloud] | `cb66ab34-8619-49cb-96d1-39b37ede86ea` |
| [!DNL ServiceNow] | `eb13cb25-47ab-407f-ba89-c0125281c563` |