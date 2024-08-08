---
keywords: Experience Platform；首頁；熱門主題；行銷自動化系統；收集行銷自動化資料
solution: Experience Platform
title: 使用流量服務API建立Marketing Automation來源的資料流
type: Tutorial
description: 本教學課程涵蓋從行銷自動化系統擷取資料，以及使用來源聯結器和API將資料引進Adobe Experience Platform的步驟。
exl-id: f3754bd0-ed31-4bf2-8f97-975bf6a9b076
source-git-commit: 48aef63cffbdc52a6a96ef69e5db4f54274144b6
workflow-type: tm+mt
source-wordcount: '1350'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API建立行銷自動化來源的資料流

本教學課程涵蓋從行銷自動化來源擷取資料，以及使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)將資料帶到Platform的步驟。

>[!NOTE]
>
>* 為了建立資料流，您必須擁有有效的基底連線ID以及行銷自動化來源。 如果您沒有此ID，請參閱[來源概觀](../../../home.md#marketing-automation)，以取得您可建立基礎連線的行銷自動化來源清單。
>* 為了讓Experience Platform擷取資料，所有以表格為基礎的批次來源的時區都必須設定為UTC。

## 快速入門

本教學課程也要求您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [Schema Registry開發人員指南](../../../../xdm/api/getting-started.md)：包含您成功執行Schema Registry API呼叫所需瞭解的重要資訊。 這包括您的`{TENANT_ID}`、「容器」的概念，以及發出要求所需的標頭（特別注意Accept標頭及其可能的值）。
* [[!DNL Catalog Service]](../../../../catalog/home.md)：目錄是Experience Platform中資料位置和歷程的記錄系統。
* [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md)：批次擷取API可讓您將資料以批次檔案的形式擷取到Experience Platform中。
* [沙箱](../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../../landing/api-guide.md)的指南。

## 建立來源連線 {#source}

您可以向[!DNL Flow Service] API發出POST要求，以建立來源連線。 來源連線由連線ID、來源資料檔案的路徑以及連線規格ID組成。

若要建立來源連線，您也必須定義資料格式屬性的列舉值。

對檔案型聯結器使用下列列舉值：

| 資料格式 | 列舉值 |
| ----------- | ---------- |
| 已分隔 | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

針對所有資料表式聯結器，將值設定為`tabular`。

**API格式**

```https
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
        "name": "HubSpot source connection",
        "baseConnectionId": "c6d4ee17-6752-4e83-94ee-1767522e83fa",
        "description": "HubSpot source connection",
        "data": {
            "format": "tabular",
        },
        "params": {
            "path": "Hubspot.Contacts"
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `baseConnectionId` | 您存取之協力廠商行銷自動化系統的唯一連線ID。 |
| `params.path` | 您存取之來源檔案的路徑。 |
| `connectionSpec.id` | 行銷自動化系統的連線規格ID。 |

**回應**

成功的回應會傳回新建立的來源連線的唯一識別碼(`id`)。 將此值儲存為稍後建立目標連線時所需的值。

```json
{
    "id": "f44dbef2-a4f0-4978-8dbe-f2a4f0e978cf",
    "etag": "\"5f00fba7-0000-0200-0000-5ed560520000\""
}
```

## 建立目標XDM結構描述 {#target-schema}

為了在Platform中使用來源資料，必須建立目標結構描述，以根據您的需求來建構來源資料。 然後目標結構描述會用來建立包含來源資料的Platform資料集。

可透過對[結構描述登入API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)執行POST要求來建立目標XDM結構描述。

如需有關如何建立目標XDM結構描述的詳細步驟，請參閱有關使用API [建立結構描述的教學課程](../../../../xdm/api/schemas.md)。

## 建立目標資料集 {#target-dataset}

可以透過對[目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)執行POST要求，在承載中提供目標結構描述的ID來建立目標資料集。

如需有關如何建立目標資料集的詳細步驟，請參閱有關[使用API建立資料集](../../../../catalog/api/create-dataset.md)的教學課程。

## 建立目標連線 {#target-connection}

目標連線代表與擷取資料著陸目的地之間的連線。 若要建立目標連線，您必須提供與Data Lake相關聯的固定連線規格ID。 此連線規格識別碼為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

您現在具有目標結構描述、目標資料集和到資料湖的連線規格ID的唯一識別碼。 使用[!DNL Flow Service] API，您可以指定這些識別碼以及將包含傳入來源資料的資料集，以建立目標連線。

**API格式**

```https
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
        "name": "HubSpot target connection",
        "description": "HubSpot target connection",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/da411446eec78026c28d9fafd9e406e304b771d55b07b91b",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5ed5639d798a22191b6987b2"
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

```json
{
    "id": "4b3d05d8-b7aa-40de-bd05-d8b7aa80de65",
    "etag": "\"dd00a1a2-0000-0200-0000-5ed564850000\""
}
```

## 建立對應 {#mapping}

為了將來源資料擷取到目標資料集中，必須首先將其對應到目標資料集所堅持的目標結構描述。

若要建立對應集，請在提供您的目標XDM結構描述`$id`和您要建立的對應集詳細資料時，向[[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml)的`mappingSets`端點提出POST要求。

**API格式**

```https
POST /conversion/mappingSets
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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/da411446eec78026c28d9fafd9e406e304b771d55b07b91b",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Vid",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "Properties_Firstname_Value",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_repo.createDate",
                "sourceAttribute": "Added_At",
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
| `xdmSchema` | 目標XDM結構的ID。 |

**回應**

成功的回應會傳回新建立的對應詳細資料，包括其唯一識別碼(`id`)。 儲存此值，因為建立資料流時需要此值。

```json
{
    "id": "500a9b747fcf4908a21917d49bd61780",
    "version": 0,
    "createdDate": 1591043336298,
    "modifiedDate": 1591043336298,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 查詢資料流規格 {#specs}

資料流負責從來源收集資料，並將這些資料匯入Platform。 為了建立資料流，您必須先取得負責收集行銷自動化資料的資料流規格。

**API格式**

```https
GET /flowSpecs?property=name=="CRMToAEP"
```

**要求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CRMToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回負責將資料從來源帶入Platform的資料流規格的詳細資料。 回應包含建立新資料流所需的唯一流程規格`id`。

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

收集行銷自動化資料的最後一步是建立資料流。 到現在為止，您已準備下列必要值：

* [Source連線ID](#source)
* [目標連線ID](#target)
* [對應 ID](#mapping)
* [資料流規格ID](#specs)

資料流負責從來源排程及收集資料。 您可以執行POST要求，同時在裝載中提供先前提到的值，藉此建立資料流。

若要排程內嵌，您必須先將開始時間值設為以秒為單位的epoch時間。 然後，您必須將頻率值設定為下列五個選項之一： `once`、`minute`、`hour`、`day`或`week`。 間隔值會指定兩個連續擷取之間的期間，而建立一次性擷取不需要設定間隔。 對於所有其他頻率，間隔值必須設定為等於或大於`15`。

**API格式**

```https
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
        "name": "HubSpot dataflow",
        "description": "collecting Hubspot.Contacts",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "f44dbef2-a4f0-4978-8dbe-f2a4f0e978cf"
        ],
        "targetConnectionIds": [
            "4b3d05d8-b7aa-40de-bd05-d8b7aa80de65"
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
                    "mappingId": "500a9b747fcf4908a21917d49bd61780",
                    "mappingVersion": 0
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1591043454",
            "frequency":"once",
            "interval":"15"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `flowSpec.id` | 在上一步中擷取的[流程規格識別碼](#specs)。 |
| `sourceConnectionIds` | 已在先前步驟中擷取的[來源連線識別碼](#source)。 |
| `targetConnectionIds` | 已在先前步驟中擷取的[目標連線識別碼](#target-connection)。 |
| `transformations.params.mappingId` | 已在先前步驟中擷取的[對應ID](#mapping)。 |
| `transformations.params.deltaColum` | 用來區分新資料和現有資料的指定欄。 將根據所選欄的時間戳記擷取增量資料。 `deltaColumn`支援的日期格式為`yyyy-MM-dd HH:mm:ss`。 |
| `transformations.params.mappingId` | 與資料庫關聯的對應ID。 |
| `scheduleParams.startTime` | 資料流的開始時間（以Epoch時間計）。 |
| `scheduleParams.frequency` | 資料流收集資料的頻率。 可接受的值包括： `once`、`minute`、`hour`、`day`或`week`。 |
| `scheduleParams.interval` | 間隔會指定兩個連續資料流執行之間的期間。 間隔的值應為非零整數。 每個頻率的最小接受間隔值如下：<ul><li>**一次**：不適用</li><li>**分鐘**： 15</li><li>**小時**： 1</li><li>**天**： 1</li><li>**周**： 1</li></ul> |

**回應**

成功的回應會傳回新建立的資料流識別碼(`id`)。

```json
{
    "id": "e0bd8463-0913-4ca1-bd84-6309134ca1f6",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## 監視資料流

建立資料流後，您可以監視透過該資料流擷取的資料，以檢視有關資料流執行、完成狀態和錯誤的資訊。 如需如何監視資料流程的詳細資訊，請參閱有關API中[監視資料流程的教學課程](../monitor.md)

## 後續步驟

依照本教學課程所述，您已建立來源聯結器，以排程方式從行銷自動化系統收集資料。 下游Platform服務（例如[!DNL Real-Time Customer Profile]和[!DNL Data Science Workspace]）現在可以使用傳入的資料。 如需更多詳細資訊，請參閱下列檔案：

* [即時客戶輪廓概觀](../../../../profile/home.md)
* [資料科學工作區總覽](../../../../data-science-workspace/home.md)
