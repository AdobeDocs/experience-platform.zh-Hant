---
keywords: Experience Platform；主題；熱門主題；雲儲存資料；流資料；流
solution: Experience Platform
title: 使用流服務API為原始資料建立流資料流
type: Tutorial
description: 本教程介紹了使用源連接器和API檢索流資料並將其引入平台的步驟。
exl-id: 898df7fe-37a9-4495-ac05-30029258a6f4
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 2%

---

# 使用 [!DNL Flow Service] API

本教程介紹從流源連接器檢索原始資料並使用Experience Platform [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本教程要求您對以下Adobe Experience Platform元件有一定的瞭解：

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化框架。
   - [架構組合的基礎](../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   - [架構註冊表開發人員指南](../../../../xdm/api/getting-started.md):包括成功執行對架構註冊表API的調用所需要瞭解的重要資訊。 這包括您 `{TENANT_ID}`、「容器」的概念和發出請求所需的標頭（特別要注意「接受」標頭及其可能值）。
- [[!DNL Catalog Service]](../../../../catalog/home.md):目錄是記錄Experience Platform中資料位置和沿襲的系統。
- [[!DNL Streaming ingestion]](../../../../ingestion/streaming-ingestion/overview.md):平台的流接收為用戶提供了一種從客戶端和伺服器端設備向Experience Platform即時發送資料的方法。
- [沙箱](../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../landing/api-guide.md)。

### 建立源連接 {#source}

本教程還要求您具有流連接器的有效源連接ID。 如果您沒有此資訊，請在嘗試本教程之前參閱以下有關建立流源連接的教程：

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

## 建立目標XDM架構 {#target-schema}

為了在平台中使用源資料，必須建立目標架構以根據您的需要來構造源資料。 然後使用目標模式建立包含源資料的平台資料集。 此目標XDM架構還擴展了XDM [!DNL Individual Profile] 類。

要建立目標XDM架構，請向 `/schemas` 端點 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)。

**API格式**

```http
POST /tenant/schemas
```

**要求**

以下示例請求建立擴展XDM的XDM架構 [!DNL Individual Profile] 類。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "type": "object",
        "title": "Sample schema for a streaming connector",
        "description": "Sample schema for a streaming connector",
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

成功的響應返回新建立的架構的詳細資訊，包括其唯一標識符(`$id`)。 在後續步驟中，建立目標資料集、映射和資料流時需要此ID。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
    "meta:altId": "_{TENANT_ID}.schemas.e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Sample schema for a streaming connector",
    "type": "object",
    "description": "Sample schema for a streaming connector",
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
    "imsOrg": "{ORG_ID}",
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
        "repo:createdDate": 1604960074752,
        "repo:lastModifiedDate": 1604960074752,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{MODIFIED_USER_ID}",
        "eTag": "8522a151effd974429518ed90c3eaf6efc9bf6ffb6644087a85c6d4455dcd045",
        "meta:globalLibVersion": "1.16.1"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "{SANDBOX_ID}",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 建立目標資料集

建立目標XDM架構及其唯一性 `$id` 您現在可以建立目標資料集以包含源資料。 要建立目標資料集，請向 `dataSets` 端點 [目錄服務API](https://www.adobe.io/experience-platform-apis/references/catalog/)，同時在負載中提供目標架構的ID。

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test streaming dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags": {
            "identity": [
            "enabled:true"
            ],
            "profile": [
            "enabled:true"
            ]
        }
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 要建立的資料集的名稱。 |
| `schemaRef.id` | URI `$id` 對於XDM模式，資料集將基於。 |
| `schemaRef.contentType` | 架構的版本。 此值必須設定為 `application/vnd.adobe.xed-full-notext+json;version=1`，返回架構的最新次版本。 請參閱 [架構版本](../../../../xdm/api/getting-started.md#versioning) 的子菜單。 |

**回應**

成功的響應將返回一個陣列，該陣列包含以格式新建立的資料集的ID `"@/datasets/{DATASET_ID}"`。 資料集ID是只讀的系統生成字串，用於在API調用中引用資料集。 在後續步驟中需要目標資料集ID才能建立目標連接和資料流。

```json
[
    "@/dataSets/5f7187bac6d00f194fb937c0"
]
```

## 建立目標連接 {#target-connection}

目標連接建立並管理到平台或傳輸資料將降落的任何位置的目標連接。 目標連接包含有關建立資料流所需的資料目標、資料格式和目標連接ID的資訊。 目標連接實例特定於租戶和組織。

要建立目標連接，請向 `/targetConnections` 端點 [!DNL Flow Service] API。 作為請求的一部分，必須提供資料格式， `dataSetId` 在上一步中檢索，並且固定連接規範ID與 [!DNL Data Lake]。 此ID為 `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Streaming target connection",
        "description": "Streaming target connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5f7187bac6d00f194fb937c0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `connectionSpec.id` | 用於連接到的連接規範ID [!DNL Data Lake]。 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |
| `data.format` | 您要帶到的資料的指定格式 [!DNL Data Lake]。 |
| `params.dataSetId` | 在上一步中檢索的目標資料集的ID。 |

**回應**

成功的響應返回新目標連接的唯一標識符(`id`)。 後續步驟中需要此ID。

```json
{
    "id": "d9300194-6a82-4163-b001-946a821163b8",
    "etag": "\"4006d3e4-0000-0200-0000-5f7189220000\""
}
```

## 建立映射 {#mapping}

為了將源資料攝取到目標資料集中，必須首先將其映射到目標資料集所遵循的目標模式。

要建立映射集，請向 `mappingSets` 端點 [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) 提供目標XDM架構時 `$id` 以及要建立的映射集的詳細資訊。

**API格式**

```http
POST /mappingSets
```

**要求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "_{TENANT_ID}.schemas.e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
        "xdmVersion": "1.0",
        "mappings": [
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "firstName",
                "identity": false,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "lastName",
                "identity": false,
                "version": 0
            }
        ]
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `xdmSchema` | 的 `$id` 目標XDM架構。 |

**回應**

成功的響應返回新建立的映射的詳細資訊，包括其唯一標識符(`id`)。 在後續步驟中建立資料流時需要此ID。

```json
{
    "id": "380b032b445a46008e77585e046efe5e",
    "version": 0,
    "createdDate": 1604960750613,
    "modifiedDate": 1604960750613,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 檢索資料流規範清單 {#specs}

資料流負責從源收集資料並將其引入平台。 要建立資料流，必須首先通過向 [!DNL Flow Service] API。

**API格式**

```http
GET /flowSpecs
```

**要求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回資料流規範的清單。 需要檢索的資料流規範ID，以使用以下任一項建立資料流 [!DNL Amazon Kinesis]。 [!DNL Azure Event Hubs]或  [!DNL Google PubSub]的 `d69717ba-71b4-4313-b654-49f9cf126d7a`。

```json
{
    "items": [
        {
            "id": "d69717ba-71b4-4313-b654-49f9cf126d7a",
            "name": "Stream data with optional transformation",
            "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
                "86043421-563b-46ec-8e6c-e23184711bf6",
                "70116022-a743-464a-bbfe-e226a7f8210c"
            ],
            "targetConnectionSpecIds": [
                "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                "db4fe783-ef79-4a12-bda9-32b2b1bc3b2c"
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
                            }
                        }
                    }
                }
            ],
            "attributes": {
                "uiAttributes": {
                    "apiFeatures": {
                        "flowRunsSupported": false
                    }
                }
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "StreamingSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "StreamingSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        },
    ]
}
```

## 建立資料流

收集流資料的最後一步是建立資料流。 現在，您準備了以下必需值：

- [源連接ID](#source)
- [目標連接ID](#target)
- [對應 ID](#mapping)
- [資料流規範ID](#specs)

資料流負責從源調度和收集資料。 通過在負載中提供先前提到的值的同時執行POST請求，可以建立資料流。

**API格式**

```http
POST /flows
```

**要求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Streaming dataflow",
        "description": "Streaming dataflow",
        "flowSpec": {
            "id": "d69717ba-71b4-4313-b654-49f9cf126d7a",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "e96d6135-4b50-446e-922c-6dd66672b6b2"
        ],
        "targetConnectionIds": [
            "723222e2-6ab9-4b0b-b222-e26ab9bb0bc2"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "380b032b445a46008e77585e046efe5e",
                    "mappingVersion": 0
                }
            }
        ]
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `flowSpec.id` | 的 [流規範ID](#specs) 在上一步中檢索。 |
| `sourceConnectionIds` | 的 [源連接ID](#source) 在較早的步驟中檢索。 |
| `targetConnectionIds` | 的 [目標連接ID](#target-connection) 在較早的步驟中檢索。 |
| `transformations.params.mappingId` | 的 [映射ID](#mapping) 在較早的步驟中檢索。 |

**回應**

成功的響應返回ID(`id`)。

```json
{
    "id": "1f086c23-2ea8-4d06-886c-232ea8bd061d",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 後續步驟

按照本教程，您建立了一個資料流以從流連接器收集流資料。 現在，下游平台服務(如 [!DNL Real-Time Customer Profile] 和 [!DNL Data Science Workspace]。 有關詳細資訊，請參閱以下文檔：

- [即時客戶概要資訊概述](../../../../profile/home.md)
- [資料科學工作區概述](../../../../data-science-workspace/home.md)
