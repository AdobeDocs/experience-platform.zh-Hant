---
keywords: Experience Platform；首頁；熱門主題；雲端儲存資料；串流資料；串流
solution: Experience Platform
title: 使用流服務API為原始資料建立流資料流
type: Tutorial
description: 本教學課程涵蓋擷取串流資料，以及使用來源連接器和API將其匯入Platform的步驟。
exl-id: 898df7fe-37a9-4495-ac05-30029258a6f4
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 2%

---

# 使用為原始資料建立流資料流 [!DNL Flow Service] API

本教學課程涵蓋從串流來源連接器擷取原始資料，並使用Experience Platform [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本教學課程需要您妥善了解下列Adobe Experience Platform元件：

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   - [結構構成基本概念](../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   - [Schema Registry開發人員指南](../../../../xdm/api/getting-started.md):包括您必須知道的重要資訊，才能成功執行對結構註冊表API的呼叫。 這包括 `{TENANT_ID}`、「容器」的概念，以及提出要求所需的標題（請特別注意「接受」標題及其可能的值）。
- [[!DNL Catalog Service]](../../../../catalog/home.md):目錄是記錄Experience Platform內資料位置和世系的系統。
- [[!DNL Streaming ingestion]](../../../../ingestion/streaming-ingestion/overview.md):Platform的串流內嵌為使用者提供了一種方法，可即時從用戶端和伺服器端裝置傳送資料至Experience Platform。
- [沙箱](../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../landing/api-guide.md).

### 建立源連接 {#source}

本教學課程也要求您具備串流連接器的有效來源連線ID。 如果您沒有此資訊，請在嘗試本教學課程之前，先參閱下列有關建立串流來源連線的教學課程：

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

## 建立目標XDM結構 {#target-schema}

為了在Platform中使用來源資料，必須建立目標架構，以根據您的需求來建構來源資料。 然後，目標架構會用來建立包含來源資料的Platform資料集。 此目標XDM架構也可擴充XDM [!DNL Individual Profile] 類別。

若要建立目標XDM結構，請向 `/schemas` 端點 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

**API格式**

```http
POST /tenant/schemas
```

**要求**

下列範例要求會建立可擴充XDM的XDM架構 [!DNL Individual Profile] 類別。

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

成功的回應會傳回新建立架構的詳細資訊，包括其唯一識別碼(`$id`)。 在後續步驟中，需要此ID才能建立目標資料集、對應和資料流。

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

建立目標XDM架構及其唯一 `$id` 您現在可以建立目標資料集來包含來源資料。 若要建立目標資料集，請向 `dataSets` 端點 [目錄服務API](https://www.adobe.io/experience-platform-apis/references/catalog/)，同時在裝載中提供目標架構的ID。

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
| `name` | 要建立的資料集名稱。 |
| `schemaRef.id` | URI `$id` 針對XDM結構，資料集將以為基礎。 |
| `schemaRef.contentType` | 結構的版本。 此值必須設為 `application/vnd.adobe.xed-full-notext+json;version=1`，會傳回結構的最新次要版本。 請參閱 [方案版本設定](../../../../xdm/api/getting-started.md#versioning) （位於XDM API指南中）以取得詳細資訊。 |

**回應**

成功的回應會傳回一個陣列，內含以格式建立之新資料集的ID `"@/datasets/{DATASET_ID}"`. 資料集ID是唯讀、系統產生的字串，用於在API呼叫中參考資料集。 後續步驟需要目標資料集ID，才能建立目標連線和資料流。

```json
[
    "@/dataSets/5f7187bac6d00f194fb937c0"
]
```

## 建立目標連線 {#target-connection}

Target連線會建立和管理到Platform或傳輸資料將著陸的任何位置的目的地連線。 目標連接包含有關資料目標、資料格式以及建立資料流所需的目標連接ID的資訊。 Target連線例項是租用戶和IMS組織專屬的。

若要建立目標連線，請向 `/targetConnections` 端點 [!DNL Flow Service] API。 在請求中，您必須提供資料格式，即 `dataSetId` 在前一步驟中檢索到，並且固定連接規範ID與 [!DNL Data Lake]. 此ID為 `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

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
| `connectionSpec.id` | 用於連接到的連接規範ID [!DNL Data Lake]. 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | 您要帶入的指定資料格式 [!DNL Data Lake]. |
| `params.dataSetId` | 上一步驟中擷取的目標資料集ID。 |

**回應**

成功的回應會傳回新目標連線的唯一識別碼(`id`)。 後續步驟需要此ID。

```json
{
    "id": "d9300194-6a82-4163-b001-946a821163b8",
    "etag": "\"4006d3e4-0000-0200-0000-5f7189220000\""
}
```

## 建立對應 {#mapping}

若要將來源資料內嵌至目標資料集，必須先將其對應至目標資料集所遵守的目標架構。

若要建立對應集，請向 `mappingSets` 端點 [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) 提供目標XDM架構時 `$id` 以及您要建立之對應集的詳細資訊。

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
| `xdmSchema` | 此 `$id` 目標XDM架構的區段。 |

**回應**

成功的回應會傳回新建立之對應的詳細資訊，包括其唯一識別碼(`id`)。 在後續步驟中需要此ID才能建立資料流。

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

資料流負責從源收集資料並將其導入Platform。 要建立資料流，必須首先通過執行對的GET請求來獲取資料流規範 [!DNL Flow Service] API。

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

成功的響應返回資料流規範的清單。 使用以下任一項建立資料流時需要檢索的資料流規範ID [!DNL Amazon Kinesis], [!DNL Azure Event Hubs]，或  [!DNL Google PubSub]，即 `d69717ba-71b4-4313-b654-49f9cf126d7a`.

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

收集串流資料的最後一步是建立資料流。 您現在已準備下列必要值：

- [源連接ID](#source)
- [Target連線ID](#target)
- [對應ID](#mapping)
- [資料流規範ID](#specs)

資料流負責從源中調度和收集資料。 您可以在裝載中提供先前提及的值時，執行POST要求來建立資料流。

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
| `flowSpec.id` | 此 [流規格ID](#specs) 在上一步驟中擷取。 |
| `sourceConnectionIds` | 此 [源連接ID](#source) 在先前步驟中擷取。 |
| `targetConnectionIds` | 此 [目標連線ID](#target-connection) 在先前步驟中擷取。 |
| `transformations.params.mappingId` | 此 [對應ID](#mapping) 在先前步驟中擷取。 |

**回應**

成功的回應會傳回ID(`id`)。

```json
{
    "id": "1f086c23-2ea8-4d06-886c-232ea8bd061d",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 後續步驟

依照本教學課程，您已建立資料流，以從串流連接器收集串流資料。 下游Platform服務(例如 [!DNL Real-Time Customer Profile] 和 [!DNL Data Science Workspace]. 如需詳細資訊，請參閱下列檔案：

- [即時客戶個人檔案概觀](../../../../profile/home.md)
- [Data Science Workspace概觀](../../../../data-science-workspace/home.md)
