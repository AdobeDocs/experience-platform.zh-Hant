---
keywords: Experience Platform；首頁；熱門主題；資料庫資料庫；第三方資料庫
solution: Experience Platform
title: 使用流程服務API建立資料庫來源的資料流
type: Tutorial
description: 本教學課程涵蓋從資料庫擷取資料，以及使用來源聯結器和API將其擷取至Experience Platform的步驟。
exl-id: 1e1f9bbe-eb5e-40fb-a03c-52df957cb683
source-git-commit: 104db777446b19fa9e3ea7538ae1dda6f51a00b1
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API建立資料庫來源的資料流

本教學課程涵蓋從資料庫來源擷取資料，以及使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)將這些資料帶到Experience Platform的步驟。

>[!NOTE]
>
>* 為了建立資料流，您必須擁有包含資料庫來源的有效基底連線ID。 如果您沒有此ID，請參閱[來源概觀](../../../home.md#database)，以取得可建立基礎連線的資料庫來源清單。
>* 為了讓Experience Platform擷取資料，所有表格型批次來源的時區都必須設定為UTC。 [[!DNL Snowflake] 來源](../../../connectors/databases/snowflake.md)唯一支援的時間戳記是UTC時間的TIMESTAMP_NTZ。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md)： Experience Platform組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [Schema Registry開發人員指南](../../../../xdm/api/getting-started.md)：包含您成功執行Schema Registry API呼叫所需瞭解的重要資訊。 這包括您的`{TENANT_ID}`、「容器」的概念，以及發出要求所需的標頭（特別注意Accept標頭及其可能的值）。
* [[!DNL Catalog Service]](../../../../catalog/home.md)：目錄是Experience Platform中資料位置和歷程的記錄系統。
* [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md)：批次擷取API可讓您將資料以批次檔案的形式擷取到Experience Platform。
* [沙箱](../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../landing/api-guide.md)指南。

## 建立來源連線 {#source}

您可以對[!DNL Flow Service] API發出POST要求，以建立來源連線。 來源連線由連線ID、來源資料檔案的路徑以及連線規格ID組成。

若要建立來源連線，您也必須定義資料格式屬性的列舉值。

對檔案型聯結器使用下列列舉值：

| 資料格式 | 列舉值 |
| ----------- | ---------- |
| 已分隔 | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

針對所有資料表式聯結器，將值設定為`tabular`。

**API格式**

```http
POST /sourceConnections
```

**要求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Database source connection",
        "baseConnectionId": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
        "description": "Database source connection",
        "data": {
            "format": "tabular"
        },
        "params": {
            "tableName": "test1.Mytable",
            "columns": [
                {
                    "name": "TestID",
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
                    "name": "Datefield",
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
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `baseConnectionId` | 資料庫來源的連線ID。 |
| `params.path` | 來源檔案的路徑。 |
| `connectionSpec.id` | 資料庫來源的連線規格ID。 如需資料庫規格ID的清單，請參閱[附錄](#appendix)。 |

**回應**

成功的回應會傳回新建立的來源連線的唯一識別碼(`id`)。 在後續步驟中，建立目標連線時需要此ID。

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## 建立目標XDM結構描述 {#target-schema}

為了在Experience Platform中使用來源資料，必須建立目標結構描述，以根據您的需求建構來源資料。 然後使用目標結構描述來建立包含來源資料的Experience Platform資料集。

可透過對[結構描述登入API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)執行POST要求來建立目標XDM結構描述。

如需有關如何建立目標XDM結構描述的詳細步驟，請參閱有關使用API [建立結構描述的教學課程](../../../../xdm/api/schemas.md)。

## 建立目標資料集 {#target-dataset}

可透過對[目錄服務API](https://developer.adobe.com/experience-platform-apis/references/catalog/)執行POST要求，在承載中提供目標結構描述的ID，來建立目標資料集。

如需有關如何建立目標資料集的詳細步驟，請參閱有關[使用API建立資料集](../../../../catalog/api/create-dataset.md)的教學課程。

## 建立目標連線 {#target-connection}

目標連線代表與擷取資料著陸目的地之間的連線。 若要建立目標連線，您必須提供與資料湖相關聯的固定連線規格ID。 此連線規格識別碼為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

您現在具有目標結構描述、目標資料集和到資料湖的連線規格ID的唯一識別碼。 使用[!DNL Flow Service] API，您可以指定這些識別碼以及將包含傳入來源資料的資料集，以建立目標連線。

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
        "name": "Database target connection",
        "description": "Database target connection",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "6019e0e7c5dcf718db5ebc71"
        },
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `data.schema.id` | 目標XDM結構的`$id`。 |
| `data.schema.version` | 結構描述的版本。 此值必須設定為`application/vnd.adobe.xed-full+json;version=1`，這會傳回結構描述的最新次要版本。 |
| `params.dataSetId` | 上一步中產生的目標資料集的ID。 **注意**：建立目標連線時，您必須提供有效的資料集識別碼。 無效的資料集ID將會導致錯誤。 |
| `connectionSpec.id` | 用來連線至Data Lake的連線規格ID。 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |

**回應**

成功的回應會傳回新目標連線的唯一識別碼(`id`)。 在後續步驟中需要此值，才能建立資料流。

```json
{
    "id": "320f119a-5ac1-4ab1-88ea-eb19e674ea2e",
    "etag": "\"c0038936-0000-0200-0000-6019e1190000\""
}
```

## 建立對應 {#mapping}

為了將來源資料擷取到目標資料集中，必須首先將其對應到目標資料集所堅持的目標結構描述。

若要建立對應集，請在提供您的目標XDM結構描述`$id`和您要建立的對應集詳細資料時，對[[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/)的`mappingSets`端點提出POST要求。

**API格式**

```http
POST /mappingSets
```

**要求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "TestID",
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
                "destinationXdmPath": "person.birthDate",
                "sourceAttribute": "Datefield",
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
| `xdmSchema` | 目標XDM結構的`$id`。 |

**回應**

成功的回應會傳回新建立的對應詳細資料，包括其唯一識別碼(`id`)。 在後續步驟中需要此ID才能建立資料流。

```json
{
    "id": "0b090130b58b4819afc78b6dc98b484d",
    "version": 0,
    "createdDate": 1612309018666,
    "modifiedDate": 1612309018666,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 擷取資料流規格 {#specs}

資料流負責從來源收集資料，並將這些資料匯入Experience Platform。 若要建立資料流，您必須先對[!DNL Flow Service] API執行GET要求，以取得資料流規格。 資料流規格負責從外部資料庫或NoSQL系統收集資料。

**API格式**

```http
GET /flowSpecs?property=name=="CRMToAEP"
```

**要求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="CRMToAEP"' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回負責將資料從來源帶入Experience Platform的資料流規格的詳細資料。 回應包含建立新資料流所需的唯一流程規格`id`。

>[!NOTE]
>
>為了簡單起見，會隱藏下列JSON回應裝載。 選取「裝載」以檢視回應裝載。

+++ 檢視裝載

```json
{
  "id": "14518937-270c-4525-bdec-c2ba7cce3860",
  "name": "CRMToAEP",
  "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
  "version": "1.0",
  "attributes": {
    "isSourceFlow": true,
    "flacValidationSupported": true,
    "frequency": "batch",
    "notification": {
      "category": "sources",
      "flowRun": {
        "enabled": true
      }
    }
  },
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
    "1fe283f6-9bec-11ea-bb37-0242ac130002",
    "fcad62f3-09b0-41d3-be11-449d5a621b69",
    "ea1c2a08-b722-11eb-8529-0242ac130003",
    "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
    "ff4274f2-c9a9-11eb-b8bc-0242ac130003",
    "ba5126ec-c9ac-11eb-b8bc-0242ac130003",
    "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
    "929e4450-0237-4ed2-9404-b7e1e0a00309",
    "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
    "2fa8af9c-2d1a-43ea-a253-f00a00c74412"
  ],
  "targetConnectionSpecIds": [
    "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
  ],
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
  },
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
  "transformationSpec": [
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
  "runSpec": {
      "name": "ProviderParams",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines various params required for creating flow run.",
        "properties": {
          "startTime": {
            "type": "integer",
            "description": "An integer that defines the start time of the run. The value is represented in Unix epoch time."
          },
          "windowStartTime": {
            "type": "integer",
            "description": "An integer that defines the start time of the window against which data is to be pulled. The value is represented in Unix epoch time."
          },
          "windowEndTime": {
            "type": "integer",
            "description": "An integer that defines the end time of the window against which data is to be pulled. The value is represented in Unix epoch time."
          },
          "deltaColumn": {
            "type": "object",
            "description": "The delta column is required to partition the data and separate newly ingested data from historic data.",
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
          "startTime",
          "windowStartTime",
          "windowEndTime",
          "deltaColumn"
        ]
      }
    }
}
```

+++

## 建立資料流

收集資料的最後一步是建立資料流。 此時，您應該已準備下列必要值：

* [Source連線ID](#source)
* [目標連線ID](#target)
* [對應 ID](#mapping)
* [資料流規格ID](#specs)

資料流負責從來源排程及收集資料。 您可以執行POST要求來建立資料流，同時在要求裝載中提供先前提到的值。

若要排程內嵌，您必須先將開始時間值設為以秒為單位的epoch時間。 然後，您必須將頻率值設定為下列五個選項之一： `once`、`minute`、`hour`、`day`或`week`。 間隔值會指定兩個連續擷取之間的期間，而建立一次性擷取不需要設定間隔。 對於所有其他頻率，間隔值必須設定為等於或大於`15`。

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
        "name": "Database dataflow using BigQuery",
        "description": "collecting test1.Mytable",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "b7581b59-c603-4df1-a689-d23d7ac440f3"
        ],
        "targetConnectionIds": [
            "320f119a-5ac1-4ab1-88ea-eb19e674ea2e"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "deltaColumn": {
                        "name": "Datefield",
                        "dateFormat": "YYYY-MM-DD",
                        "timezone": "UTC"
                    }
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "0b090130b58b4819afc78b6dc98b484d",
                    "mappingVersion": 0
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1612310466",
            "frequency":"minute",
            "interval":"15",
            "backfill": "true"
        }
    }'
```

+++

| 屬性 | 說明 |
| -------- | ----------- |
| `flowSpec.id` | 在上一步中擷取的[流程規格識別碼](#specs)。 |
| `sourceConnectionIds` | 已在先前步驟中擷取的[來源連線識別碼](#source)。 |
| `targetConnectionIds` | 已在先前步驟中擷取的[目標連線識別碼](#target-connection)。 |
| `transformations.params.mappingId` | 已在先前步驟中擷取的[對應ID](#mapping)。 |
| `transformations.params.deltaColum` | 用來區分新資料和現有資料的指定欄。 將根據所選欄的時間戳記擷取增量資料。 `deltaColumn`支援的日期格式為`yyyy-MM-dd HH:mm:ss`。 如果您使用Azure資料表儲存體，`deltaColumn`支援的格式為`yyyy-MM-ddTHH:mm:ssZ`。 |
| `transformations.params.mappingId` | 與資料庫關聯的對應ID。 |
| `scheduleParams.startTime` | 資料流的開始時間（以Epoch時間計）。 |
| `scheduleParams.frequency` | 資料流收集資料的頻率。 可接受的值包括： `once`、`minute`、`hour`、`day`或`week`。 |
| `scheduleParams.interval` | 間隔會指定兩個連續資料流執行之間的期間。 間隔的值應為非零整數。 每個頻率的最小接受間隔值如下：<ul><li>**一次**：不適用</li><li>**分鐘**： 15</li><li>**小時**： 1</li><li>**天**： 1</li><li>**周**： 1</li></ul> |

**回應**

成功的回應會傳回新建立的資料流識別碼(`id`)。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

## 監視資料流

建立資料流後，您可以監視透過該資料流擷取的資料，以檢視有關資料流執行、完成狀態和錯誤的資訊。 如需如何監視資料流程的詳細資訊，請參閱有關API中[監視資料流程的教學課程](../monitor.md)

## 後續步驟

依照本教學課程中的指示，您已建立來源聯結器，以根據排程從資料庫收集資料。 下游Experience Platform服務（例如[!DNL Real-Time Customer Profile]和[!DNL Data Science Workspace]）現在可以使用內送資料。 如需更多詳細資訊，請參閱下列檔案：

* [即時客戶輪廓概觀](../../../../profile/home.md)
* [資料科學工作區概觀](../../../../data-science-workspace/home.md)

## 附錄

下節列出不同的雲端儲存空間來源聯結器及其連線規格。

### 連線規格

| 聯結器名稱 | 連線規格ID |
| -------------- | --------------- |
| [!DNL Amazon Redshift] | `3416976c-a9ca-4bba-901a-1f08f66978ff` |
| [!DNL Azure HDInsights]上的[!DNL Apache Hive] | `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f` |
| [!DNL Azure HDInsights]上的[!DNL Apache Spark] | `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |
| [!DNL Azure Data Explorer] | `0479cc14-7651-4354-b233-7480606c2ac3` |
| [!DNL Azure Synapse Analytics] | `a49bcc7d-8038-43af-b1e4-5a7a089a7d79` |
| [!DNL Azure Table Storage] | `ecde33f2-c56f-46cc-bdea-ad151c16cd69` |
| [!DNL Google BigQuery] | `3c9b37f8-13a6-43d8-bad3-b863b941fedd` |
| [!DNL Greenplum] | `37b6bf40-d318-4655-90be-5cd6f65d334b` |
| [!DNL IBM DB2] | `09182899-b429-40c9-a15a-bf3ddbc8ced7` |
| [!DNL MariaDB] | `000eb99-cd47-43f3-827c-43caf170f015` |
| [!DNL Microsoft SQL Server] | `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec` |
| [!DNL MySQL] | `26d738e0-8963-47ea-aadf-c60de735468a` |
| [!DNL Oracle] | `d6b52d86-f0f8-475f-89d4-ce54c8527328` |
| [!DNL PostgreSQL] | `74a1c565-4e59-48d7-9d67-7c03b8a13137` |
