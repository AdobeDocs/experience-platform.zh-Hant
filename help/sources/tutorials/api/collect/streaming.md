---
keywords: Experience Platform；首頁；熱門主題；雲端儲存資料；串流資料；串流
solution: Experience Platform
title: 使用流量服務API為原始資料建立串流資料流
type: Tutorial
description: 本教學課程涵蓋擷取串流資料，以及使用來源聯結器和API將其帶入Platform的步驟。
exl-id: 898df7fe-37a9-4495-ac05-30029258a6f4
source-git-commit: 39b5a2b76c28033b9e98dcefc4cdcaa9964f4d2e
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API為原始資料建立串流資料流

本教學課程涵蓋從串流來源聯結器擷取原始資料，以及使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)將資料帶入Experience Platform的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   - [結構描述組合的基本概念](../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   - [Schema Registry開發人員指南](../../../../xdm/api/getting-started.md)：包含您成功執行Schema Registry API呼叫所需瞭解的重要資訊。 這包括您的`{TENANT_ID}`、「容器」的概念，以及發出要求所需的標頭（特別注意Accept標頭及其可能的值）。
- [[!DNL Catalog Service]](../../../../catalog/home.md)：目錄是Experience Platform中資料位置和歷程的記錄系統。
- [[!DNL Streaming ingestion]](../../../../ingestion/streaming-ingestion/overview.md)： Platform的串流擷取為使用者提供從使用者端和伺服器端裝置傳送資料以即時Experience Platform的方法。
- [沙箱](../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../../landing/api-guide.md)的指南。

### 建立來源連線 {#source}

本教學課程也要求您具備串流聯結器的有效來源連線ID。 如果您沒有這項資訊，請先參閱下列有關建立串流來源連線的教學課程，然後再嘗試進行本教學課程：

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

## 建立目標XDM結構描述 {#target-schema}

為了在Platform中使用來源資料，必須建立目標結構描述，以根據您的需求來建構來源資料。 然後目標結構描述會用來建立包含來源資料的Platform資料集。 此目標XDM結構描述也會擴充XDM [!DNL Individual Profile]類別。

若要建立目標XDM結構描述，請向[[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)的`/schemas`端點提出POST要求。

**API格式**

```http
POST /tenant/schemas
```

**要求**

以下範例請求會建立擴充XDM [!DNL Individual Profile]類別的XDM結構描述。

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

成功的回應會傳回新建立之結構描述的詳細資料，包括其唯一識別碼(`$id`)。 在後續步驟中，建立目標資料集、對應和資料流時需要此ID。

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

在建立目標XDM結構描述及其唯一`$id`後，您現在可以建立目標資料集以包含來源資料。 若要建立目標資料集，請向[目錄服務API](https://www.adobe.io/experience-platform-apis/references/catalog/)的`dataSets`端點提出POST要求，同時在承載中提供目標結構描述的ID。

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
| `schemaRef.id` | 資料集將依據的XDM結構描述的URI `$id`。 |
| `schemaRef.contentType` | 結構描述的版本。 此值必須設定為`application/vnd.adobe.xed-full-notext+json;version=1`，這會傳回結構描述的最新次要版本。 如需詳細資訊，請參閱XDM API指南中[架構版本設定](../../../../xdm/api/getting-started.md#versioning)的相關章節。 |

**回應**

成功的回應會傳回陣列，其中包含以`"@/datasets/{DATASET_ID}"`格式建立之新資料集的識別碼。 資料集ID是系統產生的唯讀字串，用來參考API呼叫中的資料集。 在後續步驟中，需要目標資料集ID才能建立目標連線和資料流。

```json
[
    "@/dataSets/5f7187bac6d00f194fb937c0"
]
```

## 建立目標連線 {#target-connection}

Target連線會建立並管理與Platform或任何已傳輸資料著陸位置的目的地連線。 目標連線包含有關資料目的地、資料格式以及建立資料流所需的目標連線ID的資訊。 Target連線例項是租使用者和組織專屬的。

若要建立目標連線，請向[!DNL Flow Service] API的`/targetConnections`端點發出POST要求。 作為要求的一部分，您必須提供資料格式、上一步驟中擷取的`dataSetId`以及繫結至[!DNL Data Lake]的固定連線規格識別碼。 此識別碼為`c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

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
| `data.format` | 您要帶到Data Lake的資料指定格式。 |
| `params.dataSetId` | 上一步中產生的目標資料集的ID。 **注意**：建立目標連線時，您必須提供有效的資料集識別碼。 無效的資料集ID將會導致錯誤。 |
| `connectionSpec.id` | 用來連線至Data Lake的連線規格ID。 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |

**回應**

成功的回應會傳回新目標連線的唯一識別碼(`id`)。 此ID在後續步驟中是必要的。

```json
{
    "id": "d9300194-6a82-4163-b001-946a821163b8",
    "etag": "\"4006d3e4-0000-0200-0000-5f7189220000\""
}
```

## 建立對應 {#mapping}

為了將來源資料擷取到目標資料集中，必須首先將其對應到目標資料集所堅持的目標結構描述。

若要建立對應集，請在提供您的目標XDM結構描述`$id`和您要建立的對應集詳細資料時，向[[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml)的`mappingSets`端點提出POST要求。

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
| `xdmSchema` | 目標XDM結構的`$id`。 |

**回應**

成功的回應會傳回新建立的對應詳細資料，包括其唯一識別碼(`id`)。 在後續步驟中需要此ID才能建立資料流。

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

## 擷取資料流規格清單 {#specs}

資料流負責從來源收集資料，並將這些資料匯入Platform。 若要建立資料流，您必須先對[!DNL Flow Service] API執行GET要求，以取得資料流規格。

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

成功的回應會傳回資料流規格的清單。 您需要擷取的資料流規格ID是使用[!DNL Amazon Kinesis]、[!DNL Azure Event Hubs]或[!DNL Google PubSub]的任何一個來建立資料流，是`d69717ba-71b4-4313-b654-49f9cf126d7a`。

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

收集串流資料的最後一步是建立資料流。 到現在為止，您已準備下列必要值：

- [Source連線ID](#source)
- [目標連線ID](#target)
- [對應 ID](#mapping)
- [資料流規格ID](#specs)

資料流負責從來源排程及收集資料。 您可以執行POST要求，同時在裝載中提供先前提到的值，藉此建立資料流。

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
| `flowSpec.id` | 在上一步中擷取的[流程規格識別碼](#specs)。 |
| `sourceConnectionIds` | 已在先前步驟中擷取的[來源連線識別碼](#source)。 |
| `targetConnectionIds` | 已在先前步驟中擷取的[目標連線識別碼](#target-connection)。 |
| `transformations.params.mappingId` | 已在先前步驟中擷取的[對應ID](#mapping)。 |

**回應**

成功的回應會傳回新建立的資料流識別碼(`id`)。

```json
{
    "id": "1f086c23-2ea8-4d06-886c-232ea8bd061d",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 用於內嵌的Post資料

檢視下列裝載範例，以取得您可傳送以進行內嵌的原始或XDM相容JSON範例。

>[!NOTE]
>
>在建立資料流與擷取任何串流資料之間，您必須增加至少約5分鐘的延遲。 這可讓資料流在擷取任何資料之前完全啟用。

下列範例適用於所有：

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

>[!BEGINTABS]

>[!TAB 原始資料]

```json
'{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male",
      "birthday": {
          "year": 1984,
          "month": 6,
          "day": 9
      }
  }'
```

>[!TAB XDM資料]

```json
{
  "header": {
    "schemaRef": {
      "id": "https://ns.adobe.com/aepstreamingservicesint/schemas/73cae7e6db06ebca535cd973e3ece85e66253962f504e7d8",
      "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
    }
  },
  "body": {
    "xdmMeta": {
      "schemaRef": {
        "id": "https://ns.adobe.com/aepstreamingservicesint/schemas/73cae7e6db06ebca535cd973e3ece85e66253962f504e7d8",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
      }
    },
    "xdmEntity": {
      "_id": "acme",
      "workEmail": {
        "address": "mike@acme.com",
        "primary": true,
        "type": "work",
        "status": "active"
      },
      "person": {
        "gender": "male",
        "name": {
          "firstName": "Mike",
          "lastName": "Wazowski"
        },
        "birthDate": "1985-01-01"
      },
      "identityMap": {
        "ecid": [
          {
            "id": "01262118050522051420082102000000000000"
          }
        ]
      }
    }
  }
}
```

>[!ENDTABS]

## 後續步驟

依照本教學課程指示，您已建立資料流以從串流聯結器收集串流資料。 下游Platform服務（例如[!DNL Real-Time Customer Profile]和[!DNL Data Science Workspace]）現在可以使用傳入的資料。 如需更多詳細資訊，請參閱下列檔案：

- [即時客戶輪廓概觀](../../../../profile/home.md)
- [資料科學工作區總覽](../../../../data-science-workspace/home.md)
