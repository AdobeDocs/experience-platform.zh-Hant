---
keywords: Experience Platform；首頁；熱門主題；收集電子商務資料；電子商務資料
solution: Experience Platform
title: 使用流服務API為電子商務源建立資料流
topic-legacy: overview
type: Tutorial
description: 本教學課程涵蓋從協力廠商電子商務系統擷取資料，以及使用來源連接器和API擷取資料至Platform的步驟。
exl-id: 0952f037-5e20-4d84-a2e6-2c9470f168f5
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 1%

---

# 使用建立電子商務源的資料流 [!DNL Flow Service] API

本教學課程涵蓋從電子商務來源擷取資料，以及使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>要建立資料流，您必須已具有具有電子商務源的有效基本連接ID。 如果您沒有此ID，請參閱 [來源概觀](../../../home.md#ecommerce) 以取得您可以建立基礎連線的電子商務來源清單。

## 快速入門

本教學課程需要您妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [結構構成基本概念](../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構註冊表API](../../../../xdm/api/getting-started.md):了解如何成功執行對結構註冊表API的呼叫。 這包括 `{TENANT_ID}`、「容器」的概念，以及提出要求所需的標題（請特別注意「接受」標題及其可能的值）。
* [[!DNL Catalog Service]](../../../../catalog/home.md):目錄是記錄資料位置和內系的系統 [!DNL Experience Platform].
* [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md):批次內嵌API可讓您將資料內嵌至 [!DNL Experience Platform] 作為批處理檔案。
* [[!DNL Sandboxes]](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../landing/api-guide.md).

## 建立源連接 {#source}

您可以透過向 [!DNL Flow Service] API。 源連接由連接ID、源資料檔案的路徑和連接規範ID組成。

要建立源連接，您還必須為資料格式屬性定義枚舉值。

為檔案連接器使用下列列舉值：

| 資料格式 | 列舉值 |
| ----------- | ---------- |
| 分隔 | `delimited` |
| JSON | `json` |
| 鑲木 | `parquet` |

對於所有基於表的連接器，將值設定為 `tabular`.

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
        "name": "Shopify source connection",
        "baseConnectionId": "582f4f8d-71e9-4a5c-a164-9d2056318d6c",
        "description": "Shopify source connection",
        "data": {
            "format": "tabular"
        },
        "params": {
            "tableName": "Shopify.Orders",
            "columns": [
                {
                    "name": "Email",
                    "type": "string"
                },
                {
                    "name": "Phone",
                    "type": "string"
                },
            ]
        },
        "connectionSpec": {
            "id": "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `baseConnectionId` | 您的電子商務來源的連線ID。 |
| `params.path` | 源檔案的路徑。 |
| `connectionSpec.id` | 您的電子商務源的連接規範ID。 |

**回應**

成功的回應會傳回唯一識別碼(`id`)。 在後續步驟中，建立目標連線需要此ID。

```json
{
    "id": "c278ab14-acdf-440b-b67f-1265d15a7655",
    "etag": "\"10007c3f-0000-0200-0000-5fa9be720000\""
}
```

## 建立目標XDM結構 {#target-schema}

為了在Platform中使用來源資料，必須建立目標架構，以根據您的需求來建構來源資料。 然後，目標架構會用來建立包含來源資料的Platform資料集。

您可以透過執行POST要求來建立目標XDM結構 [結構註冊表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

如需建立Target XDM結構的詳細步驟，請參閱 [使用API建立結構](../../../../xdm/api/schemas.md).

## 建立目標資料集 {#target-dataset}

目標資料集的建立方式，是透過對 [目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，提供裝載中目標架構的ID。

如需如何建立目標資料集的詳細步驟，請參閱 [使用API建立資料集](../../../../catalog/api/create-dataset.md).

## 建立目標連線 {#target-connection}

目標連線代表所擷取資料所登陸之目的地的連線。 要建立目標連接，必須提供與Data Lake關聯的固定連接規範ID。 此連接規範ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

您現在擁有目標架構、目標資料集以及資料湖連線規格ID的唯一識別碼。 使用 [!DNL Flow Service] API，您可以指定這些識別碼以及包含傳入來源資料的資料集，以建立目標連線。

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
        "name": "Shopify target connection",
        "description": "Shopify target connection",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/854ddc36ad2c7bd001f66a4392575ed4004f81883328772f",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "dataSetId": "5fa9c083de62e418dd170b42"
        },
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `data.schema.id` | 此 `$id` 目標XDM架構的區段。 |
| `data.schema.version` | 結構的版本。 必須設定此值 `application/vnd.adobe.xed-full+json;version=1`，會傳回結構的最新次要版本。 |
| `params.dataSetId` | 目標資料集的ID。 |
| `connectionSpec.id` | 用於連接到資料湖的連接規範ID。 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**回應**

成功的回應會傳回新目標連線的唯一識別碼(`id`)。 在以後的步驟中需要此值才能建立資料流。

```json
{
    "id": "6c0ba537-a96b-4d74-8c95-450eb88baee8",
    "etag": "\"00005506-0000-0200-0000-5fa9c13c0000\""
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
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/854ddc36ad2c7bd001f66a4392575ed4004f81883328772f",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "personalEmail.address",
                "sourceAttribute": "Email",
                "identity": false,
                "version": 0
            },
            {
                "destinationXdmPath": "mobilePhone.number",
                "sourceAttribute": "Shipping_Address_Phone",
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
    "id": "22922102bffd4369b6209c102a604062",
    "version": 0,
    "createdDate": 1604960750613,
    "modifiedDate": 1604960750613,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 查找資料流規範 {#specs}

資料流負責從源收集資料並將其導入 [!DNL Platform]. 要建立資料流，必須首先通過執行對的GET請求來獲取資料流規範 [!DNL Flow Service] API。 資料流規範負責從電子商務源收集資料。

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

成功的響應返回負責將源資料帶入平台的資料流規範的詳細資訊。 回應包含唯一流量規格 `id` 建立新資料流所需。

>[!NOTE]
>
>以下的JSON回應裝載會隱藏，以便簡潔。 選取「裝載」以查看回應裝載。

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

收集資料的最後一步是建立資料流。 此時，您應準備下列必要值：

* [源連接ID](#source)
* [Target連線ID](#target)
* [對應ID](#mapping)
* [資料流規範ID](#specs)

資料流負責從源中調度和收集資料。 您可以在請求裝載中提供先前提及的值時，執行POST請求以建立資料流。

若要排程擷取，您必須先將開始時間值設為紀元時間（以秒為單位）。 然後，您必須將頻率值設定為以下五個選項之一： `once`, `minute`, `hour`, `day`，或 `week`. 間隔值指定兩個連續擷取之間的期間，並建立一次性擷取不需要設定間隔。 對於所有其他頻率，間隔值必須設定為等於或大於 `15`.

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
        "name": "Test Shopify dataflow",
        "description": "Shopify With mapping ingestion",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "c278ab14-acdf-440b-b67f-1265d15a7655"
        ],
        "targetConnectionIds": [
            "6c0ba537-a96b-4d74-8c95-450eb88baee8"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "22922102bffd4369b6209c102a604062",
                    "mappingVersion": 0
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1604961070",
            "frequency": "once"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `flowSpec.id` | 此 [流規格ID](#specs) 在上一步驟中擷取。 |
| `sourceConnectionIds` | 此 [源連接ID](#source) 在先前步驟中擷取。 |
| `targetConnectionIds` | 此 [目標連線ID](#target-connection) 在先前步驟中擷取。 |
| `transformations.params.mappingId` | 此 [對應ID](#mapping) 在先前步驟中擷取。 |
| `transformations.params.mappingId` | 與您的電子商務來源相關聯的對應ID。 |
| `scheduleParams.startTime` | 資料流的開始時間（以Epoch時間表示）。 |
| `scheduleParams.frequency` | 此 `frequency` 資料流將收集資料。 可接受的值包括： `once`, `minute`, `hour`, `day`，或 `week`. |
| `scheduleParams.interval` | 該間隔指定兩個連續流運行之間的週期。 間隔的值應為非零整數。 若 `frequency` 設為 `once` 且應大於或等於 `15` 其他 `frequency` 值。 |

**回應**

成功的回應會傳回ID `id` 新建立的資料流。

```json
{
    "id": "20c115bc-46e3-40f3-bfe9-fb25abe4ba76",
    "etag": "\"030018cb-0000-0200-0000-5fa9c31a0000\""
}
```

## 監視資料流

建立資料流後，您可以監視正在通過資料流進行內嵌的資料，以查看有關流運行、完成狀態和錯誤的資訊。 有關如何監視資料流的詳細資訊，請參閱 [監控API中的資料流 ](../monitor.md)

## 後續步驟

依照本教學課程，您已建立來源連接器，以排程收集資料電子商務。 下游現在可以使用傳入的資料 [!DNL Platform] 服務，例如 [!DNL Real-Time Customer Profile] 和 [!DNL Data Science Workspace]. 如需詳細資訊，請參閱下列檔案：

* [即時客戶個人檔案概觀](../../../../profile/home.md)
* [Data Science Workspace概觀](../../../../data-science-workspace/home.md)
