---
keywords: Experience Platform；首頁；熱門主題；串流連線；建立串流連線；api指南；教學課程；建立串流連線；串流內嵌；擷取；
solution: Experience Platform
title: 使用API建立HTTP API串流連線
topic-legacy: tutorial
type: Tutorial
description: 本教學課程將協助您開始使用Adobe Experience Platform資料擷取服務API中的串流擷取API。
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: d39cdeaa57a221f10c975353a54d3ff7c88239d6
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 2%

---


# 建立 [!DNL HTTP API] 使用API串流連線

流量服務用於收集和集中Adobe Experience Platform內各種不同來源的客戶資料。 該服務提供用戶介面和RESTful API，所有受支援的源都可從中連接。

本教學課程使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) 引導您完成使用流量服務API建立串流連線的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md):標準化框架 [!DNL Platform] 組織體驗資料。
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，即時提供統一的消費者設定檔。

此外，建立串流連線需要您具備目標XDM結構和資料集。 若要了解如何建立這些範本，請閱讀 [流記錄資料](../../../../../ingestion/tutorials/streaming-record-data.md) 或 [串流時間序列資料](../../../../../ingestion/tutorials/streaming-time-series-data.md).

以下小節提供您將需要知道的其他資訊，以便成功呼叫串流獲取API。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

若要對 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

- 授權：承載 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有資源 [!DNL Experience Platform]，包括 [!DNL Flow Service]，會與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊，請參閱 [!DNL Platform]，請參閱 [沙箱概述檔案](../../../../../sandboxes/home.md).

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

## 建立基本連接

基本連線會指定來源，並包含讓流程與串流獲取API相容所需的資訊。 建立基本連線時，您可以選擇建立未驗證和已驗證的連線。

### 未驗證的連接

未驗證的連線是您想要將資料串流至Platform時可建立的標準串流連線。

**API格式**

```http
POST /flowservice/connections
```

**要求**

若要建立串流連線，必須在POST請求中提供提供者ID和連線規格ID。 提供者ID為 `521eee4d-8cbe-4906-bb48-fb6bd4450033` 連接規範ID為 `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.sourceId` | 您要建立的串流連線ID。 |
| `auth.params.dataType` | 串流連線的資料類型。 此值必須是 `xdm`. |
| `auth.params.name` | 您要建立的串流連線名稱。 |
| `connectionSpec.id` | 連接規範 `id` 用於串流連線。 |

**回應**

成功的回應會傳回HTTP狀態201，並包含新建立連線的詳細資訊，包括其唯一識別碼(`id`)。

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 此 `id` 新建立的連接。 此處稱為 `{CONNECTION_ID}`. |
| `etag` | 分配給連接的標識符，指定連接的修訂。 |

### 已驗證的連線

當您需要區分來自受信任和不受信任來源的記錄時，應使用已驗證的連線。 想要透過個人識別資訊(PII)傳送資訊的使用者，應在將資訊串流至Platform時建立已驗證的連線。

**API格式**

```http
POST /flowservice/connections
```

**要求**

若要建立串流連線，必須在POST請求中提供提供者ID和連線規格ID。 提供者ID為 `521eee4d-8cbe-4906-bb48-fb6bd4450033` 連接規範ID為 `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection",
             "authenticationRequired": true
         }
     }
 }
```


| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.sourceId` | 您要建立的串流連線ID。 |
| `auth.params.dataType` | 串流連線的資料類型。 此值必須是 `xdm`. |
| `auth.params.name` | 您要建立的串流連線名稱。 |
| `auth.params.authenticationRequired` | 指定已建立串流連接的參數 |
| `connectionSpec.id` | 連接規範 `id` 用於串流連線。 |

**回應**

成功的回應會傳回HTTP狀態201，並包含新建立連線的詳細資訊，包括其唯一識別碼(`id`)。

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 此 `id` 新建立的連接。 此處稱為 `{CONNECTION_ID}`. |
| `etag` | 分配給連接的標識符，指定連接的修訂。 |

## 取得串流端點URL

建立基本連線後，您現在可以擷取串流端點URL。

**API格式**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 此 `id` 先前建立之連線的值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含有關所請求連接的詳細資訊。 串流端點URL會透過連線自動建立，且可使用 `inletUrl` 值。

```json
{
    "items": [
        {
            "createdAt": 1583971856947,
            "updatedAt": 1583971856947,
            "createdBy": "{API_KEY}",
            "updatedBy": "{API_KEY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "id": "77a05521-91d6-451c-a055-2191d6851c34",
            "name": "Another new sample connection (Experience Event)",
            "description": "Sample description",
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Streaming Connection",
                "params": {
                    "sourceId": "Sample connection (ExperienceEvent)",
                    "inletUrl": "https://dcs.adobedc.net/collection/a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "inletId": "a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "dataType": "xdm",
                    "name": "Sample connection (ExperienceEvent)"
                }
            },
            "version": "\"56008aee-0000-0200-0000-5e697e150000\"",
            "etag": "\"56008aee-0000-0200-0000-5e697e150000\""
        }
    ]
}
```

## 建立源連接 {#source}

建立基本連接後，您需要建立源連接。 建立來源連線時，您需要 `id` 值。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Sample source connection",
    "description": "Sample source connection description",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
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
    "id": "63070871-ec3f-4cb5-af47-cf7abb25e8bb",
    "etag": "\"28000b90-0000-0200-0000-6091b0150000\""
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

目標連線代表所擷取資料所登陸之目的地的連線。 要建立目標連接，必須提供與Data Lake關聯的固定連接規範ID。 此連接規範ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

您現在擁有目標結構的唯一識別碼、目標資料集，以及Data Lake的連線規格ID。 使用這些識別碼，您可以使用 [!DNL Flow Service] API，指定包含傳入來源資料的資料集。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Sample target connection",
    "description": "Sample target connection description",
    "connectionSpec": {
        "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
        "version": "1.0"
    },
    "data": {
        "format": "parquet_xdm"
    },
    "params": {
        "dataSetId": "{DATASET_ID}"
    }
}'
```

**回應**

成功的回應會傳回HTTP狀態201，並包含新建立之目標連線的詳細資訊，包括其唯一識別碼(`id`)。

```json
{
    "id": "98a2a72e-a80f-49ae-aaa3-4783cc9404c2",
    "etag": "\"0500b73f-0000-0200-0000-6091b0b90000\""
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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

## 建立資料流

建立源連接和目標連接後，您現在可以建立資料流。 資料流負責從源中調度和收集資料。 您可以透過對 `/flows` 端點。

**API格式**

```http
POST /flows
```

**要求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "HTTP API streaming dataflow",
        "description": "HTTP API streaming dataflow",
        "flowSpec": {
            "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "63070871-ec3f-4cb5-af47-cf7abb25e8bb"
        ],
        "targetConnectionIds": [
            "98a2a72e-a80f-49ae-aaa3-4783cc9404c2"
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
| `flowSpec.id` | 的流規範ID [!DNL HTTP API]. 此ID為： `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. |
| `sourceConnectionIds` | 此 [源連接ID](#source) 在先前步驟中擷取。 |
| `targetConnectionIds` | 此 [目標連線ID](#target) 在先前步驟中擷取。 |
| `transformations.params.mappingId` | 此 [對應ID](#mapping) 在先前步驟中擷取。 |

**回應**

成功的響應返回HTTP狀態201，其中包含新建立的資料流的詳細資訊，包括其唯一標識符(`id`)。

```json
{
    "id": "ab03bde0-86f2-45c7-b6a5-ad8374f7db1f",
    "etag": "\"1200c123-0000-0200-0000-6091b1730000\""
}
```

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

### 張貼要擷取的原始資料至Platform {#ingest-data}

現在您已建立流程，可以將JSON訊息傳送至先前建立的串流端點。

**API格式**

```http
POST /collection/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 此 `id` 新建立串流連線的值。 |

**要求**

範例要求會將原始資料內嵌至先前建立的串流端點。

```shell
curl -X POST https://dcs.adobedc.net/collection/2301a1f761f6d7bf62c5312c535e1076bbc7f14d728e63cdfd37ecbb4344425b \
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

**回應**

成功的回應會傳回HTTP狀態200，並包含新擷取資訊的詳細資訊。

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 先前建立的串流連線ID。 |
| `xactionId` | 在伺服器端為您剛傳送的記錄產生唯一識別碼。 此ID有助於Adobe通過各種系統和調試跟蹤此記錄的生命週期。 |
| `receivedTimeMs` | 顯示接收請求的時間的時間戳記（以毫秒為單位）。 |
