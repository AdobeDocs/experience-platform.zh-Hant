---
keywords: Experience Platform；首頁；熱門主題；雲端儲存資料
solution: Experience Platform
title: 使用流量服務API為雲端儲存空間來源建立資料流
type: Tutorial
description: 本教學課程涵蓋從第三方雲端儲存空間擷取資料，以及使用來源聯結器和API將資料帶入Experience Platform的步驟。
exl-id: 95373c25-24f6-4905-ae6c-5000bf493e6f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1756'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API為雲端儲存空間來源建立資料流

本教學課程涵蓋從雲端儲存空間來源擷取資料，以及使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)將資料帶到Experience Platform的步驟。

>[!NOTE]
>
>為了建立資料流，您必須擁有與雲端儲存空間來源之間的有效基本連線ID。 如果您沒有此ID，請參閱[來源概觀](../../../home.md#cloud-storage)，以取得您可以用來建立基礎連線的雲端儲存空間來源清單。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md)： Experience Platform組織客戶體驗資料的標準化架構。
   - [結構描述組合的基本概念](../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   - [Schema Registry開發人員指南](../../../../xdm/api/getting-started.md)：包含您成功執行Schema Registry API呼叫所需瞭解的重要資訊。 這包括您的`{TENANT_ID}`、「容器」的概念，以及發出要求所需的標頭（特別注意Accept標頭及其可能的值）。
- [[!DNL Catalog Service]](../../../../catalog/home.md)：目錄是Experience Platform中資料位置和歷程的記錄系統。
- [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md)：批次擷取API可讓您將資料以批次檔案的形式擷取到Experience Platform。
- [沙箱](../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../landing/api-guide.md)指南。

## 建立來源連線 {#source}

您可以透過向[!DNL Flow Service] API的`sourceConnections`端點發出POST要求來建立來源連線，同時提供您的基本連線ID、您要擷取的來源檔案的路徑，以及來源對應的連線規格ID。

建立來源連線時，您還必須定義資料格式屬性的列舉值。

對檔案型來源使用下列列舉值：

| 資料格式 | 列舉值 |
| ----------- | ---------- |
| 已分隔 | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

對於所有以資料表為基礎的來源，將值設定為`tabular`。

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
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited",
          "properties": {
              "columnDelimiter": "{COLUMN_DELIMITER}",
              "encoding": "{ENCODING}",
              "compressionType": "{COMPRESSION_TYPE}"
          }
      },
      "params": {
          "path": "/acme/summerCampaign/account.csv",
          "type": "file"
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `baseConnectionId` | 您的雲端儲存空間來源的基本連線ID。 |
| `data.format` | 您要帶入Experience Platform的資料格式。 支援的值為： `delimited`、`JSON`和`parquet`。 |
| `data.properties` | （選用）一組屬性，可在建立來源連線時套用至資料。 |
| `data.properties.columnDelimiter` | （選擇性）收集一般檔案時可指定的單一字元欄分隔符號。 任何單一字元值都是允許的欄分隔符號。 如果未提供，則使用逗號(`,`)作為預設值。 **注意**： `columnDelimiter`屬性只能在擷取分隔檔案時使用。 |
| `data.properties.encoding` | （選用）屬性，定義將資料擷取至Experience Platform時使用的編碼型別。 支援的編碼型別為： `UTF-8`和`ISO-8859-1`。 **注意**： `encoding`引數僅在擷取分隔的CSV檔案時可用。 將使用預設編碼`UTF-8`擷取其他檔案型別。 |
| `data.properties.compressionType` | （選用）定義要擷取的壓縮檔案型別的屬性。 支援的壓縮檔案型別為： `bzip2`、`gzip`、`deflate`、`zipDeflate`、`tarGzip`和`tar`。 **注意**： `compressionType`屬性只能在擷取分隔檔案或JSON檔案時使用。 |
| `params.path` | 您存取之來源檔案的路徑。 此引數指向個別檔案或整個資料夾。  **注意**：您可以使用星號來取代檔案名稱，以指定整個資料夾的擷取。 例如： `/acme/summerCampaign/*.csv`將會內嵌整個`/acme/summerCampaign/`資料夾。 |
| `params.type` | 您正在擷取的來源資料檔案的檔案型別。 使用型別`file`來擷取個別檔案，並使用型別`folder`來擷取整個資料夾。 |
| `connectionSpec.id` | 與您特定的雲端儲存空間來源相關聯的連線規格ID。 如需連線規格ID的清單，請參閱[附錄](#appendix)。 |

**回應**

成功的回應會傳回新建立的來源連線的唯一識別碼(`id`)。 在後續步驟中需要此ID才能建立資料流。

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

### 使用規則運算式來選取要擷取的特定檔案集 {#regex}

建立來源連線時，您可以使用規則運算式從來源擷取特定一組檔案至Experience Platform。

**API格式**

```http
POST /sourceConnections
```

**要求**

在以下範例中，檔案路徑中使用規則運算式，以指定擷取名稱中有`premium`的所有CSV檔案。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited"
      },
      "params": {
          "path": "/acme/summerCampaign/*premium*.csv",
          "type": "folder"
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

### 設定來源連線以遞回方式擷取資料

建立來源連線時，您可以使用`recursive`引數從深層巢狀資料夾擷取資料。

**API格式**

```http
POST /sourceConnections
```

**要求**

在下列範例中，`recursive: true`引數會通知[!DNL Flow Service]在擷取程式期間以遞回方式讀取所有子資料夾。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Cloud Storage source connection",
      "description: "Source connection for a cloud storage source with recursive ingestion",
      "baseConnectionId": "1f164d1b-debe-4b39-b4a9-df767f7d6f7c",
      "data": {
          "format": "delimited"
      },
      "params": {
          "path": "/acme/summerCampaign/customers/premium/buyers/recursive",
          "type": "folder",
          "recursive": true
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

## 建立目標XDM結構描述 {#target-schema}

為了在Experience Platform中使用來源資料，必須建立目標結構描述，以根據您的需求建構來源資料。 然後使用目標結構描述來建立包含來源資料的Experience Platform資料集。

可透過對[結構描述登入API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)執行POST要求來建立目標XDM結構描述。

如需有關如何建立目標XDM結構描述的詳細步驟，請參閱有關使用API [建立結構描述的教學課程](../../../../xdm/api/schemas.md)。

## 建立目標資料集 {#target-dataset}

可透過對[目錄服務API](https://developer.adobe.com/experience-platform-apis/references/catalog/)執行POST要求，在承載中提供目標結構描述的ID，來建立目標資料集。

如需有關如何建立目標資料集的詳細步驟，請參閱有關[使用API建立資料集](../../../../catalog/api/create-dataset.md)的教學課程。

## 建立目標連線 {#target-connection}

目標連線代表與擷取資料著陸目的地之間的連線。 若要建立目標連線，您必須提供與Data Lake相關聯的固定連線規格ID。 此連線規格識別碼為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

您現在具有目標結構描述、目標資料集和到資料湖的連線規格ID的唯一識別碼。 使用這些識別碼，您可以使用[!DNL Flow Service] API建立目標連線，以指定將包含傳入來源資料的資料集。

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
        "name": "Target Connection for a Cloud Storage connector",
        "description": "Target Connection for a Cloud Storage connector",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5f3c3cedb2805c194ff0b69a"
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

成功的回應會傳回新目標連線的唯一識別碼(`id`)。 此ID在後續步驟中是必要的。

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 建立對應 {#mapping}

為了將來源資料擷取到目標資料集中，必須首先將其對應到目標資料集所堅持的目標結構描述。

若要建立對應集，請在提供您的目標XDM結構描述`$id`和您要建立的對應集詳細資料時，對[[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/)的`mappingSets`端點提出POST要求。

>[!TIP]
>
>您可以使用雲端儲存空間來源聯結器來對應複雜的資料型別，例如JSON檔案中的陣列。

**API格式**

```http
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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
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
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "FirstName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "LastName",
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

成功的回應會傳回新建立的對應詳細資料，包括其唯一識別碼(`id`)。 在後續步驟中需要此值，才能建立資料流。

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 擷取資料流規格 {#specs}

資料流負責從來源收集資料，並將資料匯入Experience Platform。 為了建立資料流，您必須先取得負責收集雲端儲存空間資料的資料流規格。

**API格式**

```http
GET /flowSpecs?property=name=="CloudStorageToAEP"
```

**要求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!NOTE]
>
>為了簡單起見，會隱藏下列JSON回應裝載。 選取「裝載」以檢視回應裝載。

+++ 檢視裝載

**回應**

成功的回應會傳回負責將資料從來源帶入Experience Platform的資料流規格的詳細資料。 回應包含建立新資料流所需的唯一流程規格`id`。

```json
{
  "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
  "name": "CloudStorageToAEP",
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
    "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
    "ecadc60c-7455-4d87-84dc-2a0e293d997b",
    "b7829c2f-2eb0-4f49-a6ee-55e33008b629",
    "4c10e202-c428-4796-9208-5f1f5732b1cf",
    "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
    "32e8f412-cdf7-464c-9885-78184cb113fd",
    "b7bf2577-4520-42c9-bae9-cad01560f7bc",
    "998b8ae3-cec0-43b7-8abe-40b1eb4ee069",
    "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
    "54e221aa-d342-4707-bcff-7a4bceef0001",
    "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
    "26f526f2-58f4-4712-961d-e41bf1ccc0e8"
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
            "description": "An integer that defines the end time of the window against which data is to be pulled.  The value is represented in Unix epoch time."
          }
        },
        "required": [
          "startTime",
          "windowStartTime",
          "windowEndTime"
        ]
      }
    }
}
```

+++

## 建立資料流

收集雲端儲存空間資料的最後一步是建立資料流。 到現在為止，您已準備下列必要值：

- [Source連線ID](#source)
- [目標連線ID](#target)
- [對應 ID](#mapping)
- [資料流規格ID](#specs)

資料流負責從來源排程及收集資料。 您可以執行POST要求，同時在裝載中提供先前提及的值來建立資料流。

>[!NOTE]
>
>對於批次擷取，每個後續資料流會根據其&#x200B;**上次修改時間**&#x200B;時間戳記，選取要從您的來源擷取的檔案。 這表示批次資料流會從來源選取新的或自上次資料流執行以來經過修改的檔案。

若要排程內嵌，您必須先將開始時間值設為以秒為單位的epoch時間。 然後，您必須將頻率值設定為下列五個選項之一： `once`、`minute`、`hour`、`day`或`week`。 間隔值會指定兩個連續擷取之間的期間，而建立一次性擷取不需要設定間隔。 對於所有其他頻率，間隔值必須設定為等於或大於`15`。

>[!IMPORTANT]
>
>強烈建議在使用[FTP聯結器](../../../connectors/cloud-storage/ftp.md)時，排程您的資料流以進行一次性擷取。

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
        "name": "Cloud Storage flow to Experience Platform",
        "description": "Cloud Storage flow to Experience Platform",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "26b53912-1005-49f0-b539-12100559f0e2"
        ],
        "targetConnectionIds": [
            "f7eb08fa-5f04-4e45-ab08-fa5f046e45ee"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                    "mappingVersion": 0
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1597784298",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `flowSpec.id` | 在上一步中擷取的[流程規格識別碼](#specs)。 |
| `sourceConnectionIds` | 已在先前步驟中擷取的[來源連線識別碼](#source)。 |
| `targetConnectionIds` | 已在先前步驟中擷取的[目標連線識別碼](#target-connection)。 |
| `transformations.params.mappingId` | 已在先前步驟中擷取的[對應ID](#mapping)。 |
| `scheduleParams.startTime` | 資料流的開始時間（以Epoch時間計）。 |
| `scheduleParams.frequency` | 資料流收集資料的頻率。 可接受的值包括： `once`、`minute`、`hour`、`day`或`week`。 |
| `scheduleParams.interval` | 間隔會指定兩個連續資料流執行之間的期間。 間隔的值應為非零整數。 每個頻率的最小接受間隔值如下：<ul><li>**一次**：不適用</li><li>**分鐘**： 15</li><li>**小時**： 1</li><li>**天**： 1</li><li>**周**： 1</li></ul> |

**回應**

成功的回應會傳回新建立的資料流識別碼(`id`)。

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 監視資料流

建立資料流後，您可以監視透過該資料流擷取的資料，以檢視有關資料流執行、完成狀態和錯誤的資訊。 如需如何監視資料流程的詳細資訊，請參閱有關API中[監視資料流程的教學課程](../monitor.md)

## 後續步驟

依照本教學課程所述，您已建立來源聯結器，以排程方式從雲端儲存空間收集資料。 下游Experience Platform服務（例如[!DNL Real-Time Customer Profile]和[!DNL Data Science Workspace]）現在可以使用內送資料。 如需更多詳細資訊，請參閱下列檔案：

- [即時客戶輪廓概觀](../../../../profile/home.md)
- [資料科學工作區總覽](../../../../data-science-workspace/home.md)

## 附錄 {#appendix}

下節列出不同的雲端儲存空間來源聯結器及其連線規格。

### 連線規格

| 聯結器名稱 | 連線規格 |
| -------------- | --------------- |
| [!DNL Amazon S3] (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| [!DNL Amazon Kinesis] (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| [!DNL Azure Blob] (Blob) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) | `b3ba5556-48be-44b7-8b85-ff2b69b46dc4` |
| [!DNL Azure Event Hubs] （事件中樞） | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| [!DNL Azure File Storage] | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| [!DNL Google Cloud Storage] | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| [!DNL HDFS] | `54e221aa-d342-4707-bcff-7a4bceef0001` |
| [!DNL Oracle Object Storage] | `c85f9425-fb21-426c-ad0b-405e9bd8a46c` |
| [!DNL SFTP] | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |
