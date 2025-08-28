---
title: 建立資料流以將Source資料擷取至Experience Platform
description: 瞭解如何使用流量服務API來建立資料流，並將來源資料擷取到Experience Platform。
hide: true
hidefromtoc: true
source-git-commit: 4e9448170a6c3eb378e003bcd7520cb0e573e408
workflow-type: tm+mt
source-wordcount: '2137'
ht-degree: 2%

---

# 建立資料流以從來源擷取資料

閱讀本指南，瞭解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)建立資料流並將資料擷取到Adobe Experience Platform。

## 快速入門

本指南需要您深入瞭解下列Experience Platform元件：

* [批次擷取](../../../../ingestion/batch-ingestion/overview.md)：探索如何以批次方式有效上傳大量資料。
* [目錄服務](../../../../catalog/datasets/overview.md)：在Experience Platform中組織和追蹤您的資料集。
* [資料準備](../../../../data-prep/home.md)：轉換並對應您的傳入資料，以符合您的結構描述需求。
* [資料流](../../../../dataflows/home.md)：設定並管理將您的資料從來源移至目的地的管道。
* [體驗資料模型(XDM)結構描述](../../../../xdm/home.md)：使用XDM結構描述來建構您的資料，以便在Experience Platform中使用。
* [沙箱](../../../../sandboxes/home.md)：在隔離的環境中安全地測試和開發，不會影響生產資料。
* [來源](../../../home.md)：瞭解如何將外部資料來源連線至Experience Platform。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請閱讀[Experience Platform API快速入門](../../../../landing/api-guide.md)的指南。

### 建立基礎連線

您必須擁有已完整驗證的來源帳戶及其對應的基本連線ID，才能成功為您的來源建立資料流。 如果您沒有此ID，請造訪[來源目錄](../../../home.md)，以取得您可用來建立基礎連線的來源清單。

### 建立目標XDM結構描述 {#target-schema}

Experience Data Model (XDM)結構描述提供一種標準化方式，可在Experience Platform中組織和描述客戶體驗資料。 若要將來源資料內嵌至Experience Platform，您必須先建立目標XDM結構描述，定義您要內嵌的資料結構和型別。 此結構描述可作為您擷取之資料將存放的Experience Platform資料集的藍圖。

可透過對[結構描述登入API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)執行POST要求來建立目標XDM結構描述。 如需建立目標XDM結構描述相關步驟的詳細資訊，請參閱下列指南：

* [使用API建立結構描述](../../../../xdm/api/schemas.md)。
* [使用UI建立結構描述](../../../../xdm/tutorials/create-schema-ui.md)。

建立後，稍後將需要目標XDM結構描述`$id`以用於您的目標資料集和對應。

### 建立目標資料集 {#target-dataset}

資料集是資料集合的儲存和管理結構，通常是包含方案 (欄) 和欄位 (列) 的表格。 成功擷取至Experience Platform的資料會以資料集的形式儲存在資料湖中。 在此步驟中，您可以建立新資料集或使用現有資料集。

您可以對[目錄服務API](https://developer.adobe.com/experience-platform-apis/references/catalog/)發出POST要求，同時在承載中提供目標結構描述的ID，藉此建立目標資料集。 如需如何建立目標資料集的詳細步驟，請參閱[使用API建立資料集](../../../../catalog/api/create-dataset.md)的指南。

>[!TIP]
>
>如果您想要將資料內嵌至即時客戶設定檔，則必須確保已為設定檔啟用目標XDM結構描述和目標資料集。

+++選取以檢視範例

**API格式**

```HTTP
POST /dataSets
```

**要求**

以下範例說明如何建立已啟用即時客戶設定檔擷取的目標資料集。 在此請求中，`unifiedProfile`屬性設定為`true` （在`tags`物件下），以告知Experience Platform將此資料集納入即時客戶設定檔中。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Target Dataset",
    "schemaRef": {
      "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
      "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "tags": {
      "unifiedProfile": [
        "enabled: true"
      ]
    }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 目標資料集的描述性名稱。 使用清晰且唯一的名稱，以便在未來操作中更容易識別和管理您的資料集。 |
| `schemaRef.id` | 目標XDM結構描述的ID。 |
| `tags.unifiedProfile` | 布林值，通知Experience Platform資料是否應擷取至即時客戶個人檔案。 |

**回應**

成功回應會傳回您的目標資料集ID。 稍後需要此ID才能建立目標連線。

```json
[
    "@/dataSets/6889f4f89b982b2b90bc1207"
]
```

+++

## 建立來源連線

來源連線會定義如何將資料從外部來源帶入Experience Platform。 它同時指定來源系統和傳入資料的格式，並且會參考包含驗證詳細資訊的基礎連線。 每個來源連線都是您組織專屬的。

* 對於檔案型來源（例如雲端儲存空間），來源連線可以包含欄分隔符號、編碼型別、壓縮型別、檔案選取的規則運算式，以及是否要以遞回方式擷取檔案等設定。
* 對於以表格為基礎的來源（例如資料庫、CRM和行銷自動化提供者），來源連線可以指定詳細資訊，例如表格名稱和欄對應。

若要建立來源連線，請向`/sourceConnections` API的[!DNL Flow Service]端點發出POST要求，並提供您的基本連線ID、連線規格ID以及來源資料檔案的路徑。

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
    "name": "ACME source connection",
    "baseConnectionId": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "description": "A source connection for ACME contact data",
    "data": {
      "format": "tabular"
    },
    "params": {
      "tableName": "Contact",
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
      ],
      "cdcEnabled": true
    },
    "connectionSpec": {
      "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
      "version": "1.0"
    }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 來源連線的描述性名稱。 使用清晰且唯一的名稱，以便在未來操作中更容易識別和管理您的連線。 |
| `description` | 選用的說明，您可以新增此說明，以提供來源連線的其他資訊。 |
| `baseConnectionId` | 您的基礎連線的`id`。 您可以使用[!DNL Flow Service] API向Experience Platform驗證您的來源以擷取此ID。 |
| `data.format` | 資料的格式。 針對以資料表為基礎的來源（例如資料庫、CRM和行銷自動化提供者），將此值設定為`tabular`。 |
| `params.tableName` | 來源帳戶中您要擷取至Experience Platform的表格名稱。 |
| `params.columns` | 您要擷取至Experience Platform的特定資料表欄。 |
| `params.cdcEnabled` | 表示是否啟用變更記錄擷取的布林值。 下列資料庫來源支援此屬性： <ul><li>[!DNL Azure Databricks]</li><li>[!DNL Google BigQuery]</li><li>[!DNL Snowflake]</li></ul> 如需詳細資訊，請閱讀在來源[中使用](../change-data-capture.md)變更資料擷取的指南。 |
| `connectionSpec.id` | 您使用之來源的連線規格ID。 |

**回應**

成功的回應會傳回來源連線的ID。 需要此ID才能建立資料流並內嵌您的資料。

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## 建立目標連線 {#target-connection}

目標連線代表與擷取資料著陸目的地之間的連線。 若要建立目標連線，您必須提供與Data Lake相關聯的固定連線規格ID。 此連線規格識別碼為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

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
      "name": "ACME target connection",
      "description": "ACME target connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6889f4f89b982b2b90bc1207"
      },
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 目標連線的描述性名稱。 使用清晰且唯一的名稱，以便在未來操作中更容易識別和管理您的連線。 |
| `description` | 選用的說明，您可將其新增以提供目標連線的其他資訊。 |
| `data.schema.id` | 目標XDM結構描述的ID。 |
| `params.dataSetId` | 目標資料集的ID。 |
| `connectionSpec.id` | 資料湖的連線規格ID。 此ID已修正： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |

## 對應 {#mapping}

接下來，您必須將來源資料對應至目標資料集所固定的目標結構描述。 若要建立對應，請向`mappingSets`API[[!DNL Data Prep] 的](https://developer.adobe.com/experience-platform-apis/references/data-prep/)端點發出POST要求，提供您的目標XDM結構描述ID以及您要建立之對應集的詳細資料。

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
    "id": "93ddfa69c4864d978832b1e5ef6ec3b9",
    "version": 0,
    "createdDate": 1612309018666,
    "modifiedDate": 1612309018666,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 擷取資料流規格

建立資料流之前，必須先擷取與來源對應的資料流規格。 若要擷取此資訊，請向`/flowSpecs` API的[!DNL Flow Service]端點提出GET要求。

**API格式**

```http
GET /flowSpecs?property=name=="{NAME}"
```

| 查詢引數 | 說明 |
| --- | --- |
| `property=name=="{NAME}"` | 資料流規格的名稱。 <ul><li>針對檔案型來源（例如雲端儲存空間），將此值設定為`CloudStorageToAEP`。</li><li>對於以資料表為基礎的來源（例如資料庫、CRM和行銷自動化提供者），請將此值設定為`CRMToAEP`。</li></ul> |

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

為確保您使用正確的資料流規格，請檢查回應中的`items.sourceConnectionSpecIds`陣列。 確認您來源的連線規格ID包含在此清單中。

+++選取以檢視

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
                "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
                "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
                "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
                "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
                "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
                "09182899-b429-40c9-a15a-bf3ddbc8ced7",
                "0479cc14-7651-4354-b233-7480606c2ac3",
                "d6b52d86-f0f8-475f-89d4-ce54c8527328",
                "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
                "fcad62f3-09b0-41d3-be11-449d5a621b69",
                "ea1c2a08-b722-11eb-8529-0242ac130003",
                "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
                "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
                "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
                "2fa8af9c-2d1a-43ea-a253-f00a00c74412",
                "e9d7ec6b-0873-4e57-ad21-b3a7c65e310b"
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
            },
            "attributes": {
                "recordTypeEnabled": true,
                "defaultRecordType": "profile",
                "isSourceFlow": true,
                "flacValidationSupported": true,
                "isDraftModeSupported": true,
                "frequency": "batch",
                "notification": {
                    "category": "sources",
                    "flowRun": {
                        "enabled": true
                    }
                }
            },
            "permissionsInfo": {
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ],
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ]
            }
        }
    ]
}
```

+++

## 建立資料流

資料流是已設定的管道，可跨Experience Platform服務傳輸資料。 它定義如何從外部來源（例如資料庫、雲端儲存空間或API）擷取、處理資料，以及將其路由到目標資料集。 然後，身分服務、即時客戶個人檔案和目的地等服務會使用這些資料集來啟用和分析。

若要建立資料流，您必須擁有下列專案的值：

* Source連線ID
* 目標連線ID
* 對應 ID
* 資料流規格ID

在此步驟中，您可以在`scheduleParams`中使用下列引數來設定資料流程的擷取排程：

| 排程引數 | 說明 |
| --- | --- |
| `startTime` | 資料流應該開始的Epoch時間（以秒為單位）。 |
| `frequency` | 擷取頻率。 設定頻率以指出資料流執行的頻率。 您可以將頻率設為： <ul><li>`once`：將頻率設為`once`以建立一次性內嵌。 建立一次性擷取資料流時，無法使用間隔和回填的設定。 依預設，排程頻率會設定為一次。</li><li>`minute`：將頻率設為`minute`，排程您的資料流以每分鐘擷取資料。</li><li>`hour`：將頻率設為`hour`，排程您的資料流以每小時擷取資料。</li><li>`day`：將頻率設為`day`，排程您的資料流每天擷取資料。</li><li>`week`：將頻率設為`week`，排程資料流每週擷取資料。</li></ul> |
| `interval` | 連續內嵌之間的間隔（除`once`外的所有頻率均需要）。 設定間隔設定，以建立每次擷取之間的時間範圍。 例如，如果您將頻率設為「天」，並將間隔設為15，則您的資料流將每隔15天執行一次。 您不能將間隔設定為零。 每個頻率的最小接受間隔值如下：<ul><li>`once`：不適用</li><li>`minute`： 15</li><li>`hour`: 1</li><li>`day`: 1</li><li>`week`: 1</li></ul> |
| `backfill` | 指示是否要擷取`startTime`之前的歷史資料。 |

{style="table-layout:auto"}


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
      "name": "ACME Contact Dataflow",
      "description": "A dataflow for ACME contact data",
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
                  "mappingId": "93ddfa69c4864d978832b1e5ef6ec3b9",
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

| 屬性 | 說明 |
| --- | --- |
| `name` | 資料流程的描述性名稱。 使用清楚且獨一無二的名稱，以便日後作業中更輕鬆地識別及管理您的資料流。 |
| `description` | 選擇性說明，您可新增以提供其他資訊給資料流。 |
| `flowSpec.id` | 與來源對應的流程規格ID。 |
| `sourceConnectionIds` | 先前步驟中產生的來源連線ID。 |
| `targetConnectionIds` | 先前步驟中產生的目標連線ID。 |
| `transformations.params.deltaColum` | 用來區分新資料和現有資料的指定欄。 將根據所選欄的時間戳記擷取增量資料。 `deltaColumn`支援的格式為`yyyy-MM-dd HH:mm:ss`。 對於[!DNL Microsoft Dynamics]，`deltaColumn`支援的格式為`yyyy-MM-ddTHH:mm:ssZ`。 |
| `transformations.params.deltaColumn.dateFormat` | 差異欄要遵循的日期格式。 |
| `transformations.params.deltaColumn.timeZone` | 解譯delta欄中的值時要使用的時區。 |
| `transformations.params.mappingId` | 在先前步驟中產生的對應ID。 |
| `scheduleParams.startTime` | 資料流的開始時間（以Epoch時間表示） （自Unix Epoch以來的秒數）。 決定資料流何時開始其首次執行。 |
| `scheduleParams.frequency` | 資料流執行的頻率。 可接受的值包括： `once`、`minute`、`hour`、`day`或`week`。 |
| `scheduleParams.interval` | 根據選取的頻率，連續資料流執行之間的間隔。 必須是非零整數。 例如，間隔`15`的頻率`minute`表示資料流每15分鐘執行一次。 |
| `scheduleParams.backfill` | 布林值（`true`或`false`），可決定是否要在首次建立資料流時擷取歷史資料（回填）。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回新建立的資料流識別碼(`id`)。

```json
{
    "id": "ae0a9777-b322-4ac1-b0ed-48ae9e497c7e",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

### 使用UI驗證API工作流程

您可以使用Experience Platform使用者介面來驗證資料流的建立。 導覽至Experience Platform UI中的&#x200B;*[!UICONTROL 來源]*&#x200B;目錄，然後從標題標籤中選取&#x200B;**[!UICONTROL 資料流程]**。 接下來，使用[!UICONTROL 資料流名稱]欄，並找出您使用[!DNL Flow Service] API建立的資料流。

![Experience Platform UI中來源工作區的資料流介面](../../../images/tutorials/validations/dataflows-interface.png)

您可以透過[!UICONTROL 資料流活動]介面進一步驗證資料流。 使用右邊欄檢視資料流的[!UICONTROL API使用狀況]資訊。 此區段會顯示在[!DNL Flow Service]中資料流建立程式期間產生的相同資料流ID、資料集ID和對應ID。

![來源工作區的資料流檢視頁面。](../../../images/tutorials/validations/api-usage.png)

## 後續步驟

本教學課程將引導您完成使用[!DNL Flow Service] API在Experience Platform中建立資料流的程式。 您已瞭解如何建立及設定必要的元件，包括目標XDM結構、資料集、來源連線、目標連線和資料流本身。 按照這些步驟，您可以將來自外部來源的資料擷取到Experience Platform中自動化，讓下游服務（例如即時客戶個人資料和目的地）將擷取的資料用於進階使用案例。

### 監視資料流

建立資料流後，您可以監視透過它擷取的資料，以檢視擷取率、成功和錯誤的資訊。 如需如何監視資料流的詳細資訊，請瀏覽有關[監視帳戶和資料流](../../../../dataflows/ui/monitor-sources.md)的教學課程。

### 更新您的資料流

若要更新資料流排程、對應和一般資訊的設定，請瀏覽有關[更新來源資料流](../../api/update-dataflows.md)的教學課程。

## 刪除您的資料流

您可以刪除不再需要的資料流，或使用&#x200B;**[!UICONTROL 資料流]**&#x200B;工作區中可用的&#x200B;**[!UICONTROL 刪除]**&#x200B;功能建立錯誤的資料流。 如需有關如何刪除資料流程的詳細資訊，請瀏覽有關[刪除資料流程](../../api/delete.md)的教學課程。