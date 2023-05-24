---
keywords: Experience Platform；首頁；熱門主題；流連接；建立流連接；api指南；教程；建立流連接；流接收；接收；
title: 使用流服務API建立HTTP API流連接
description: 本教程提供了如何使用流服務API為原始和XDM資料使用HTTP API源建立流連接的步驟
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: 7ff297973f951d7bfd940983bf4fa39dcc9f1542
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 2%

---


# 使用 [!DNL Flow Service] API

Flow Service用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供了用戶介面和REST風格的API，所有支援的源都可從中連接。

本教程使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) 引導您完成使用 [!DNL Flow Service] API。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md):標準化框架 [!DNL Platform] 組織經驗資料。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根據來自多個源的聚合資料即時提供統一的消費者配置檔案。

此外，建立流連接需要您具有目標XDM架構和資料集。 要瞭解如何建立這些元件，請閱讀上的教程 [流記錄資料](../../../../../ingestion/tutorials/streaming-record-data.md) 或教程 [流時間序列資料](../../../../../ingestion/tutorials/streaming-time-series-data.md)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接指定源並包含使流與流接收API相容所需的資訊。 建立基本連接時，您可以選擇建立未經驗證的連接和經過驗證的連接。

### 未驗證連接

非驗證連接是在要將資料流入平台時可以建立的標準流連接。

要建立未經身份驗證的基連接，請向 `/connections` 終結點，同時為連接、資料類型和HTTP API連接規範ID提供名稱。 此ID為 `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`。

**API格式**

```http
POST /flowservice/connections
```

**要求**

以下請求為HTTP API建立基連接。

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
| `name` | 基本連接的名稱。 請確保名稱是描述性的，因為您可以使用此名稱查找有關基本連接的資訊。 |
| `description` | （可選）可包含的屬性，用於提供有關基本連接的詳細資訊。 |
| `connectionSpec.id` | 與HTTP API對應的連接規範ID。 此ID為 `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`。 |
| `auth.params.dataType` | 流連接的資料類型。 支援的值包括： `xdm` 和 `raw`。 |
| `auth.params.name` | 要建立的流連接的名稱。 |

**回應**

成功的響應返回HTTP狀態201，其中包含新建立的連接的詳細資訊，包括其唯一標識符(`id`)。

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 的 `id` 新建的基本連接。 |
| `etag` | 分配給連接的標識符，指定基本連接的版本。 |

### 已驗證的連接

在需要區分來自受信任源和不受信任源的記錄時，應使用經過身份驗證的連接。 希望使用個人身份資訊(PII)發送資訊的用戶應在將資訊流式傳輸到平台時建立經過身份驗證的連接。

要建立經過驗證的基連接，必須包括 `authenticationRequired` 參數，將其值指定為 `true`。 在此步驟中，您還可以為經過身份驗證的基本連接提供源ID。 此參數是可選的，將使用與 `name` 屬性。


**API格式**

```http
POST /flowservice/connections
```

**要求**

以下請求為HTTP API建立經過驗證的基連接。

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
| `auth.params.sourceId` | 可在建立經過驗證的基連接時使用的附加標識符。 此參數是可選的，將使用與 `name` 屬性。 |
| `auth.params.authenticationRequired` | 此參數指定流連接是否需要身份驗證。 如果 `authenticationRequired` 設定為 `true` 則必須為流連接提供身份驗證。 如果 `authenticationRequired` 設定為 `false` 則不需要驗證。 |

**回應**

成功的響應返回HTTP狀態201，其中包含新建立的連接的詳細資訊，包括其唯一標識符(`id`)。

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

## 獲取流終結點URL

建立基本連接後，現在可以檢索流終結點URL。

**API格式**

```http
GET /flowservice/connections/{BASE_CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 的 `id` 先前建立的連接的值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含有關所請求連接的詳細資訊。 流終結點URL是通過連接自動建立的，並且可以使用 `inletUrl` 值。

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

要建立源連接，請向 `/sourceConnections` 提供基本連接ID時的終結點。

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

成功的響應返回HTTP狀態201，其中詳細列出了新建立的源連接，包括其唯一標識符(`id`)。

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

## 建立目標XDM架構 {#target-schema}

為了在平台中使用源資料，必須建立目標架構以根據您的需要來構造源資料。 然後使用目標模式建立包含源資料的平台資料集。

通過執行對目標XDM的POST請求，可以建立目標XDM模式 [架構註冊表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)。

有關如何建立目標XDM架構的詳細步驟，請參見上的教程 [使用API建立架構](../../../../../xdm/api/schemas.md)。

### 建立目標資料集 {#target-dataset}

通過對目標資料集執行POST請求，可以建立目標資料集 [目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，提供負載內目標架構的ID。

有關如何建立目標資料集的詳細步驟，請參見上的教程 [使用API建立資料集](../../../../../catalog/api/create-dataset.md)。

## 建立目標連接 {#target}

目標連接表示到所接收資料所在目的地的連接。 要建立目標連接，請將POST請求 `/targetConnections` 為目標資料集和目標XDM架構提供ID。 在此步驟中，還必須提供資料湖連接規範ID。 此ID為 `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

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

成功的響應返回HTTP狀態201，其中包含新建立的目標連接的詳細資訊，包括其唯一標識符(`id`)。

```json
{
  "id": "07f2f6ff-1da5-4704-916a-c615b873cba9",
  "etag": "\"340680f7-0000-0200-0000-637eb8730000\""
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
| `xdmSchema` | 的 `$id` 目標XDM架構。 |

**回應**

成功的響應返回新建立的映射的詳細資訊，包括其唯一標識符(`id`)。 在後續步驟中建立資料流時需要此ID。

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

建立源連接和目標連接後，您現在可以建立資料流。 資料流負責調度和收集來自源的資料。 通過對執行POST請求，可以建立資料流 `/flows` 端點。

**API格式**

```http
POST /flows
```

**要求**

>[!BEGINTABS]

>[!TAB 不轉換]

以下請求為HTTP API建立不進行資料轉換的流資料流。

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

>[!TAB 具有轉換]

以下請求為HTTP API建立流資料流，並將映射轉換應用到您的資料。

建立具有轉換的資料流時， `name` 無法更改參數。 此值必須始終設定為 `Mapping`。

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
| `name` | 資料流的名稱。 確保資料流的名稱是描述性的，因為您可以使用此名稱查找有關資料流的資訊。 |
| `description` | （可選）可包含的屬性，用於提供有關資料流的詳細資訊。 |
| `flowSpec.id` | 流規範ID [!DNL HTTP API]。 要建立具有轉換的資料流，必須使用  `c1a19761-d2c7-4702-b9fa-fe91f0613e81`。 要建立不進行轉換的資料流，請使用 `d8a6f005-7eaf-4153-983e-e8574508b877`。 |
| `sourceConnectionIds` | 的 [源連接ID](#source) 在較早的步驟中檢索。 |
| `targetConnectionIds` | 的 [目標連接ID](#target) 在較早的步驟中檢索。 |
| `transformations.params.mappingId` | 的 [映射ID](#mapping) 在較早的步驟中檢索。 |

**回應**

成功的響應返回HTTP狀態201，其中包含新建立的資料流的詳細資訊，包括其唯一標識符(`id`)。

```json
{
  "id": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
  "etag": "\"dc0459ae-0000-0200-0000-637ebaec0000\""
}
```


## 將資料上傳到平台 {#ingest-data}

現在，您已建立流，您可以將JSON消息發送到先前建立的流終結點。

**API格式**

```http
POST /collection/{INLET_URL}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{INLET_URL}` | 流終結點URL。 您可以通過向URL發出GET請求來檢索此URL `/connections` 提供基本連接ID時的終結點。 |

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

成功響應返回HTTP狀態200，並返回新接收資訊的詳細資訊。

```json
{
    "inletId": "{BASE_CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{BASE_CONNECTION_ID}` | 先前建立的流連接的ID。 |
| `xactionId` | 為您剛發送的記錄生成的唯一標識符伺服器端。 此ID有助於Adobe通過各種系統和調試跟蹤此記錄的生命週期。 |
| `receivedTimeMs` | 顯示接收請求的時間的時間戳（以毫秒為單位）。 |


## 後續步驟

按照本教程，您建立了流式HTTP連接，使您能夠使用流終結點將資料接收到平台。 有關在UI中建立流連接的說明，請閱讀 [建立流連接教程](../../../ui/create/streaming/http.md)。

要瞭解如何將資料流傳輸到平台，請閱讀上的教程 [流時序資料](../../../../../ingestion/tutorials/streaming-time-series-data.md) 或教程 [流記錄資料](../../../../../ingestion/tutorials/streaming-record-data.md)。

## 附錄

本節提供有關使用API建立流連接的補充資訊。

### 將消息發送到經過驗證的流連接

如果流連接已啟用身份驗證，則需要客戶端添加 `Authorization` 他們的請求。

如果 `Authorization` 標頭不存在，或者發送了無效/過期的訪問令牌，將返回HTTP 401未授權響應，響應類似如下：

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
