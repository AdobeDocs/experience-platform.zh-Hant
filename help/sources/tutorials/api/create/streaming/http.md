---
keywords: Experience Platform；首頁；熱門主題；串流連線；建立串流連線；API指南；教學課程；建立串流連線；串流擷取；擷取；
title: 使用流量服務API建立HTTP API串流連線
description: 本教學課程提供如何使用Flow Service API使用HTTP API來源為原始資料和XDM資料建立串流連線的步驟
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 3%

---


# 使用[!DNL Flow Service] API建立HTTP API串流連線

流量服務是用來收集及集中來自Adobe Experience Platform內不同來源的客戶資料。 此服務提供使用者介面和RESTful API，所有支援的來源都可從此API連線。

本教學課程使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)逐步引導您完成使用[!DNL Flow Service] API建立串流連線的步驟。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md)： [!DNL Platform]用來組織體驗資料的標準化架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，即時提供統一的消費者設定檔。

此外，建立串流連線需要您具備目標XDM結構描述和資料集。 若要瞭解如何建立這些資料，請閱讀[串流記錄資料](../../../../../ingestion/tutorials/streaming-record-data.md)的教學課程或[串流時間序列資料](../../../../../ingestion/tutorials/streaming-time-series-data.md)的教學課程。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../../../landing/api-guide.md)的指南。

## 建立基礎連線

基礎連線會指定來源，並包含讓流程與串流獲取API相容所需的資訊。 建立基礎連線時，您可以選擇建立未驗證和已驗證的連線。

### 未驗證的連線

未驗證的連線是標準的串流連線，您可以在想要將資料串流到Platform時建立。

若要建立未驗證的基礎連線，請在提供連線的名稱、資料型別和HTTP API連線規格ID時，向`/connections`端點提出POST要求。 此識別碼為`bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`。

**API格式**

```http
POST /flowservice/connections
```

**要求**

以下請求會建立HTTP API的基本連線。

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
| `name` | 基礎連線的名稱。 請確定名稱是描述性的，因為您可以使用此名稱來查詢基礎連線的資訊。 |
| `description` | （選用）可包含的屬性，可提供基礎連線的詳細資訊。 |
| `connectionSpec.id` | 與HTTP API對應的連線規格ID。 此識別碼為`bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`。 |
| `auth.params.dataType` | 串流連線的資料型別。 支援的值包括： `xdm`和`raw`。 |
| `auth.params.name` | 您要建立的串流連線名稱。 |

**回應**

成功的回應會傳回HTTP狀態201，其中包含新建立連線的詳細資料，包括其唯一識別碼(`id`)。

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 您新建立的基礎連線的`id`。 |
| `etag` | 指定給連線的識別碼，指定基礎連線的版本。 |

### 已驗證的連線

當您需要區分來自受信任與不受信任來源的記錄時，應使用已驗證的連線。 想要傳送個人識別資訊(PII)資訊的使用者，應在將資訊串流至Platform時建立已驗證的連線。

若要建立已驗證的基底連線，您必須在要求中加入`authenticationRequired`引數，並指定其值為`true`。 在此步驟中，您也可以提供已驗證基本連線的來源ID。 此引數為選用引數，若未提供，將使用與`name`屬性相同的值。


**API格式**

```http
POST /flowservice/connections
```

**要求**

以下請求會為HTTP API建立已驗證的基本連線。

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
| `auth.params.sourceId` | 建立已驗證的基礎連線時，可使用的其他識別碼。 此引數為選用引數，若未提供，將使用與`name`屬性相同的值。 |
| `auth.params.authenticationRequired` | 此引數會指定串流連線是否需要驗證。 如果`authenticationRequired`設定為`true`，則必須為串流連線提供驗證。 如果`authenticationRequired`設定為`false`，則不需要驗證。 |

**回應**

成功的回應會傳回HTTP狀態201，其中包含新建立連線的詳細資料，包括其唯一識別碼(`id`)。

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

## 取得串流端點URL

在建立基本連線後，您現在可以擷取串流端點URL。

**API格式**

```http
GET /flowservice/connections/{BASE_CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 您先前建立之連線的`id`值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含請求連線的詳細資訊。 串流端點URL是使用連線自動建立的，並可使用`inletUrl`值擷取。

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

## 建立來源連線 {#source}

若要建立來源連線，請在提供您的基本連線ID時，向`/sourceConnections`端點提出POST要求。

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

成功的回應會傳回HTTP狀態201，其中包含新建立的來源連線的詳細資料，包括其唯一識別碼(`id`)。

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

## 建立目標XDM結構描述 {#target-schema}

為了在Platform中使用來源資料，必須建立目標結構描述，以根據您的需求來建構來源資料。 然後目標結構描述會用來建立包含來源資料的Platform資料集。

可透過對[結構描述登入API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)執行POST要求來建立目標XDM結構描述。

如需有關如何建立目標XDM結構描述的詳細步驟，請參閱有關使用API [建立結構描述的教學課程](../../../../../xdm/api/schemas.md)。

### 建立目標資料集 {#target-dataset}

可以透過對[目錄服務API](https://developer.adobe.com/experience-platform-apis/references/catalog/)執行POST要求，在承載中提供目標結構描述的ID來建立目標資料集。

如需有關如何建立目標資料集的詳細步驟，請參閱有關[使用API建立資料集](../../../../../catalog/api/create-dataset.md)的教學課程。

## 建立目標連線 {#target}

目標連線代表與擷取資料著陸目的地之間的連線。 若要建立目標連線，請在提供目標資料集和目標XDM結構描述的ID時，向`/targetConnections`發出POST要求。 在此步驟中，您也必須提供資料湖連線規格ID。 此識別碼為`c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

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

成功的回應會傳回HTTP狀態201，其中包含新建立的目標連線的詳細資料，包括其唯一識別碼(`id`)。

```json
{
  "id": "07f2f6ff-1da5-4704-916a-c615b873cba9",
  "etag": "\"340680f7-0000-0200-0000-637eb8730000\""
}
```

## 建立對應 {#mapping}

為了將來源資料擷取到目標資料集中，必須首先將其對應到目標資料集所堅持的目標結構描述。

若要建立對應集，請在提供您的目標XDM結構描述`$id`和您要建立的對應集詳細資料時，向[[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/)的`mappingSets`端點提出POST要求。

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
| `xdmSchema` | 目標XDM結構的`$id`。 |

**回應**

成功的回應會傳回新建立的對應詳細資料，包括其唯一識別碼(`id`)。 在後續步驟中需要此ID才能建立資料流。

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

## 建立資料流

建立來源和目標連線後，您現在可以建立資料流。 資料流負責從來源排程及收集資料。 您可以對`/flows`端點執行POST要求，以建立資料流。

**API格式**

```http
POST /flows
```

**要求**

>[!BEGINTABS]

>[!TAB XDM]

以下請求會為XDM資料建立串流資料流。

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

>[!TAB 原始]

以下請求會建立原始資料的串流資料流。

使用轉換建立資料流時，無法變更`name`引數。 此值必須一律設定為`Mapping`。

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
| `name` | 資料流的名稱。 確保資料流的名稱是描述性的，因為您可以使用此名稱來查閱資料流上的資訊。 |
| `description` | （選用）可包含的屬性，可提供資料流的詳細資訊。 |
| `flowSpec.id` | [!DNL HTTP API]的流程規格識別碼。 若要建立包含轉換的資料流，您必須使用`c1a19761-d2c7-4702-b9fa-fe91f0613e81`。 若要在不轉換的情況下建立資料流，請使用`d8a6f005-7eaf-4153-983e-e8574508b877`。 |
| `sourceConnectionIds` | 已在先前步驟中擷取的[來源連線識別碼](#source)。 |
| `targetConnectionIds` | 已在先前步驟中擷取的[目標連線識別碼](#target)。 |
| `transformations.params.mappingId` | 已在先前步驟中擷取的[對應ID](#mapping)。 |

**回應**

成功的回應會傳回HTTP狀態201，其中包含您新建立的資料流詳細資料，包括其唯一識別碼(`id`)。

```json
{
  "id": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
  "etag": "\"dc0459ae-0000-0200-0000-637ebaec0000\""
}
```

## 張貼要擷取至平台的資料 {#ingest-data}

>[!NOTE]
>
>在建立資料流與擷取任何串流資料之間，您必須增加至少約5分鐘的延遲。 這可讓資料流在擷取任何資料之前完全啟用。

現在您已建立流程，可以將JSON訊息傳送至您先前建立的串流端點。

**API格式**

```http
POST /collection/{INLET_URL}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{INLET_URL}` | 您的串流端點網址。 您可以在提供基本連線ID時，透過向`/connections`端點發出GET要求來擷取此URL。 |
| `{FLOW_ID}` | HTTP API串流資料流的ID。 XDM和RAW資料都需要此ID。 |

**要求**

>[!BEGINTABS]

>[!TAB 傳送XDM資料]

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' \
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

>[!TAB 以流程識別碼傳送原始資料做為HTTP標頭]

傳送原始資料時，您可以將流量ID指定為查詢引數或HTTP標頭的一部分。 下列範例會將流量ID指定為HTTP標題。

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' 
  -H 'x-adobe-flow-id=f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2' \
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

>[!TAB 以流程識別碼傳送原始資料作為查詢引數]

傳送原始資料時，您可以將流量ID指定為查詢引數或HTTP標題。 下列範例會將流量ID指定為查詢引數。

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec?x-adobe-flow-id=f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2 \
  -H 'Content-Type: application/json' \
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

成功的回應會傳回HTTP狀態200以及新擷取的資訊詳細資訊。

```json
{
    "inletId": "{BASE_CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BASE_CONNECTION_ID}` | 先前建立串流連線的ID。 |
| `xactionId` | 在伺服器端為您剛傳送的記錄產生的唯一識別碼。 此ID可協助Adobe透過各種系統和偵錯追蹤此記錄的生命週期。 |
| `receivedTimeMs` | 顯示收到要求的時間戳記（紀元單位：毫秒）。 |


## 後續步驟

依照本教學課程指示，您已建立串流HTTP連線，讓您能夠使用串流端點將資料擷取到Platform。 如需在UI中建立串流連線的指示，請參閱[建立串流連線教學課程](../../../ui/create/streaming/http.md)。

若要瞭解如何將資料串流到Platform，請閱讀[串流時間序列資料](../../../../../ingestion/tutorials/streaming-time-series-data.md)的教學課程或[串流記錄資料](../../../../../ingestion/tutorials/streaming-record-data.md)的教學課程。

## 附錄

本節提供有關使用API建立串流連線的補充資訊。

### 傳送訊息至已驗證的串流連線

如果串流連線已啟用驗證，使用者端必須將`Authorization`標頭新增至其要求。

如果`Authorization`標頭不存在，或傳送了無效/過期的存取Token，則會傳回HTTP 401未經授權的回應，其回應類似如下：

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

