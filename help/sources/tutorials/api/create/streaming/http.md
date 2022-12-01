---
keywords: Experience Platform；首頁；熱門主題；串流連線；建立串流連線；api指南；教學課程；建立串流連線；串流內嵌；擷取；
title: 使用流程服務API建立HTTP API串流連線
description: 本教學課程提供如何使用Flow Service API為原始和XDM資料使用HTTP API來源建立串流連線的步驟
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: 2b3f8b7b0a19214a95a2ad76c9fecd70ffd91743
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 2%

---


# 使用建立HTTP API串流連線， [!DNL Flow Service] API

流量服務用於收集和集中Adobe Experience Platform中不同來源的客戶資料。 該服務提供用戶介面和RESTful API，所有受支援的源都可從中連接。

本教學課程使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) 引導您完成使用 [!DNL Flow Service] API。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md):標準化框架 [!DNL Platform] 組織體驗資料。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，即時提供統一的消費者設定檔。

此外，建立串流連線需要您具備目標XDM結構和資料集。 若要了解如何建立這些範本，請閱讀 [流記錄資料](../../../../../ingestion/tutorials/streaming-record-data.md) 或 [串流時間序列資料](../../../../../ingestion/tutorials/streaming-time-series-data.md).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基本連接

基本連線會指定來源，並包含讓流程與串流獲取API相容所需的資訊。 建立基本連線時，您可以選擇建立未驗證和已驗證的連線。

### 未驗證的連接

未驗證的連線是您想要將資料串流至Platform時可建立的標準串流連線。

若要建立未驗證的基本連線，請向 `/connections` 端點，同時提供連線名稱、資料類型和HTTP API連線規格ID。 此ID為 `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

**API格式**

```http
POST /flowservice/connections
```

**要求**

下列要求會建立HTTP API的基礎連線。

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "name": "ACME Streaming Connection XDM Data",
    "description": "ACME streaming connection for customer data",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    },
    "auth": {
      "specName": "Streaming Connection",
      "params": {
        "dataType": "xdm"
      }
    }
  }'
```

>[!TAB 原始資料]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "name": "ACME Streaming Connection Raw Data",
    "description": "ACME streaming connection for customer data",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    },
    "auth": {
      "specName": "Streaming Connection",
      "params": {
        "dataType": "raw"
      }
    }
  }'
```

>[!ENDTABS]

| 屬性 | 說明 |
| --- | --- |
| `name` | 基本連接的名稱。 請確定名稱具有描述性，因為您可以使用此名稱來查詢基本連線的資訊。 |
| `description` | （選用）您可以包含的屬性，以提供有關基本連線的詳細資訊。 |
| `connectionSpec.id` | 與HTTP API對應的連線規格ID。 此ID為 `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`. |
| `auth.params.dataType` | 串流連線的資料類型。 支援的值包括： `xdm` 和 `raw`. |
| `auth.params.name` | 您要建立的串流連線名稱。 |

**回應**

成功的回應會傳回HTTP狀態201，並包含新建立連線的詳細資訊，包括其唯一識別碼(`id`)。

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 此 `id` 新建立的基本連接。 |
| `etag` | 分配給連接的標識符，指定基本連接的版本。 |

### 已驗證的連線

當您需要區分來自受信任和不受信任來源的記錄時，應使用已驗證的連線。 想要透過個人識別資訊(PII)傳送資訊的使用者，應在將資訊串流至Platform時建立已驗證的連線。

若要建立已驗證的基本連線，您必須包含 `authenticationRequired` 參數，並將其值指定為 `true`. 在此步驟中，您也可以提供已驗證基本連線的來源ID。 此參數為選用值，且會使用與 `name` 屬性（若未提供）。


**API格式**

```http
POST /flowservice/connections
```

**要求**

下列要求會為HTTP API建立已驗證的基本連線。

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "ACME Streaming Connection XDM Data Authenticated",
     "description": "ACME streaming connection for customer data",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Authenticated XDM streaming connection",
             "dataType": "xdm",
             "name": "Authenticated XDM streaming connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!TAB 原始資料]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "ACME Streaming Connection Raw Data Authenticated",
     "description": "ACME streaming connection for customer data",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Authenticated raw streaming connection",
             "dataType": "raw",
             "name": "Authenticated raw streaming connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!ENDTABS]

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.sourceId` | 建立已驗證的基礎連線時可使用的額外識別碼。 此參數為選用值，且會使用與 `name` 屬性（若未提供）。 |
| `auth.params.authenticationRequired` | 指定已建立串流連接的參數 |

**回應**

成功的回應會傳回HTTP狀態201，並包含新建立連線的詳細資訊，包括其唯一識別碼(`id`)。

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

## 取得串流端點URL

建立基本連線後，您現在可以擷取串流端點URL。

**API格式**

```http
GET /flowservice/connections/{BASE_CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 此 `id` 先前建立之連線的值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含有關所請求連接的詳細資訊。 串流端點URL會透過連線自動建立，且可使用 `inletUrl` 值。

```json
{
  "items": [
    {
      "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
      "createdAt": 1669238699119,
      "updatedAt": 1669238699119,
      "createdBy": "acme@AdobeID",
      "updatedBy": "acme@AdobeID",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "ACME Streaming Connection XDM Data",
      "description": "ACME streaming connection for customer data",
      "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "Streaming Connection",
        "params": {
          "sourceId": "ACME Streaming Connection XDM Data",
          "inletUrl": "https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec",
          "authenticationRequired": false,
          "inletId": "667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec",
          "dataType": "xdm",
          "name": "ACME Streaming Connection XDM Data"
        }
      },
      "version": "\"f50185ed-0000-0200-0000-637e8fad0000\"",
      "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
    }
  ]
}
```

## 建立源連接 {#source}

若要建立來源連線，請向 `/sourceConnections` 端點，同時提供基本連線ID。

**API格式**

```http
POST /flowservice/sourceConnections
```

**要求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Source Connection for Customer Data",
      "description": "A streaming source connection for ACME XDM Customer Data",
      "baseConnectionId": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
      "connectionSpec": {
          "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
          "version": "1.0"
      }
    }'
```

**回應**

成功的回應會傳回HTTP狀態201，並詳細說明新建立的來源連線，包括其唯一識別碼(`id`)。

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

## 建立目標XDM結構 {#target-schema}

為了在Platform中使用來源資料，必須建立目標架構，以根據您的需求來建構來源資料。 然後，目標架構會用來建立包含來源資料的Platform資料集。

您可以透過執行POST要求來建立目標XDM結構 [結構註冊表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

如需建立Target XDM結構的詳細步驟，請參閱 [使用API建立結構](../../../../../xdm/api/schemas.md).

### 建立目標資料集 {#target-dataset}

目標資料集的建立方式，是透過對 [目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，提供裝載中目標架構的ID。

如需如何建立目標資料集的詳細步驟，請參閱 [使用API建立資料集](../../../../../catalog/api/create-dataset.md).

## 建立目標連線 {#target}

目標連線代表所擷取資料所登陸之目的地的連線。 若要建立目標連線，請向發出POST要求 `/targetConnections` 同時為目標資料集和目標XDM結構提供ID。 在此步驟中，您還必須提供資料湖連接規範ID。 此ID為 `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

**API格式**

```http
POST /flowservice/targetConnections
```

**要求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Target Connection",
      "description": "ACME Streaming Target Connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
              "version": "application/vnd.adobe.xed-full+json;version=1.0"
          }
      },
      "params": {
          "dataSetId": "637eb7fadc8a211b6312b65b"
      },
          "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
  }'
```

**回應**

成功的回應會傳回HTTP狀態201，並包含新建立之目標連線的詳細資訊，包括其唯一識別碼(`id`)。

```json
{
  "id": "07f2f6ff-1da5-4704-916a-c615b873cba9",
  "etag": "\"340680f7-0000-0200-0000-637eb8730000\""
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
      "xdmSchema": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
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
  "id": "79a623960d3f4969835c9e00dc90c8df",
  "version": 0,
  "createdDate": 1669249214031,
  "modifiedDate": 1669249214031,
  "createdBy": "acme@AdobeID",
  "modifiedBy": "acme@AdobeID"
}
```

| 屬性 | 說明 |
| --- | --- |

## 建立資料流

建立源連接和目標連接後，您現在可以建立資料流。 資料流負責從源中調度和收集資料。 您可以透過對 `/flows` 端點。

**API格式**

```http
POST /flows
```

**要求**

>[!BEGINTABS]

>[!TAB 無需轉換]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Dataflow",
      "description": "ACME streaming dataflow for customer data",
      "flowSpec": {
        "id": "d8a6f005-7eaf-4153-983e-e8574508b877",
        "version": "1.0"
      },
      "sourceConnectionIds": [
        "34ece231-294d-416c-ad2a-5a5dfb2bc69f"
      ],
      "targetConnectionIds": [
        "07f2f6ff-1da5-4704-916a-c615b873cba9"
      ]
    }'
```

>[!TAB 轉換]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "<name>",
      "description": "<description>",
      "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
      },
      "sourceConnectionIds": [
        "34ece231-294d-416c-ad2a-5a5dfb2bc69f"
      ],
      "targetConnectionIds": [
        "07f2f6ff-1da5-4704-916a-c615b873cba9"
      ],
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingId": "79a623960d3f4969835c9e00dc90c8df",
            "mappingVersion": 0
          }
        }
      ]
    }'
```

>[!ENDTABS]

| 屬性 | 說明 |
| --- | --- |
| `name` | 資料流的名稱。 請確保資料流的名稱具有描述性，因為您可以使用此名稱查找資料流的資訊。 |
| `description` | （可選）可以包括的屬性，用於提供有關資料流的更多資訊。 |
| `flowSpec.id` | 的流規範ID [!DNL HTTP API]. 要使用轉換建立資料流，必須使用  `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. 要建立不進行轉換的資料流，請使用 `d8a6f005-7eaf-4153-983e-e8574508b877`. |
| `sourceConnectionIds` | 此 [源連接ID](#source) 在先前步驟中擷取。 |
| `targetConnectionIds` | 此 [目標連線ID](#target) 在先前步驟中擷取。 |
| `transformations.params.mappingId` | 此 [對應ID](#mapping) 在先前步驟中擷取。 |

**回應**

成功的響應返回HTTP狀態201，其中包含新建立的資料流的詳細資訊，包括其唯一標識符(`id`)。

```json
{
  "id": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
  "etag": "\"dc0459ae-0000-0200-0000-637ebaec0000\""
}
```


## 要擷取的貼文資料至Platform {#ingest-data}

現在您已建立流程，可以將JSON訊息傳送至先前建立的串流端點。

**API格式**

```http
POST /collection/{INLET_URL}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{INLET_URL}` | 您的串流端點URL。 您可以向 `/connections` 端點，同時提供基本連線ID。 |

**要求**

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2' \
  -d '{
        "header": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
          },
          "flowId": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
          "datasetId": "604a18a3bae67d18db6d258c"
        },
        "body": {
          "xdmMeta": {
            "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
              "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
            }
          },
          "xdmEntity": {
            "_id": "http-source-connector-acme-01",
            "person": {
              "name": {
                "firstName": "suman",
                "lastName": "nolan"
              }
            },
            "workEmail": {
              "primary": true,
              "address": "suman@acme.com",
              "type": "work",
              "status": "active"
            }
          }
        }
      }'
```

>[!TAB 原始資料]

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: 1f086c23-2ea8-4d06-886c-232ea8bd061d' \
  -d '{
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

>[!ENDTABS]

**回應**

成功的回應會傳回HTTP狀態200，並包含新擷取資訊的詳細資訊。

```json
{
    "inletId": "{BASE_CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BASE_CONNECTION_ID}` | 先前建立的串流連線ID。 |
| `xactionId` | 在伺服器端為您剛傳送的記錄產生唯一識別碼。 此ID有助於Adobe通過各種系統和調試跟蹤此記錄的生命週期。 |
| `receivedTimeMs` | 顯示接收請求的時間的時間戳記（以毫秒為單位）。 |


## 後續步驟

依照本教學課程，您已建立串流HTTP連線，讓您能使用串流端點將資料內嵌至Platform。 如需在UI中建立串流連線的指示，請參閱 [建立串流連線教學課程](../../../ui/create/streaming/http.md).

若要了解如何將資料串流至Platform，請閱讀以下任一教學課程： [串流時間序列資料](../../../../../ingestion/tutorials/streaming-time-series-data.md) 或 [流記錄資料](../../../../../ingestion/tutorials/streaming-record-data.md).

## 附錄

本節提供使用API建立串流連線的補充資訊。

### 傳送訊息至已驗證的串流連線

如果串流連線已啟用驗證，則用戶端必須新增 `Authorization` 標題。

若 `Authorization` 標頭不存在，或者已傳送無效/過期的存取權杖，將會傳回HTTP 401未授權回應，並有類似的回應，如下所示：

**回應**

```json
{
    "type": "https://ns.adobe.com/adobecloud/problem/data-collection-service-authorization",
    "status": "401",
    "title": "Authorization",
    "report": {
        "message": "[id] Ims service token is empty"
    }
}
```
