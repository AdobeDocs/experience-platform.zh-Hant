---
keywords: Experience Platform；首頁；熱門主題；串流連線；建立串流連線；api指南；教學課程；建立串流連線；串流內嵌；擷取；
solution: Experience Platform
title: 使用API建立串流連線
topic-legacy: tutorial
type: Tutorial
description: 本教學課程將協助您開始使用Adobe Experience Platform資料擷取服務API中的串流擷取API。
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: b672eab481a8286f92741a971991c7f83102acf7
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 2%

---


# 使用API建立串流連線

流量服務用於收集和集中Adobe Experience Platform內各種不同來源的客戶資料。 該服務提供用戶介面和RESTful API，所有受支援的源都可從中連接。

本教學課程使用[!DNL Flow Service] API來引導您完成使用流程服務API建立串流連線的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md):組織體驗資料的 [!DNL Platform] 標準化架構。
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，即時提供統一的消費者設定檔。

此外，建立串流連線需要您具備目標XDM結構和資料集。 若要了解如何建立這些資料，請閱讀[串流記錄資料](../../../../../ingestion/tutorials/streaming-record-data.md)的教學課程，或閱讀[串流時間序列資料](../../../../../ingestion/tutorials/streaming-time-series-data.md)的教學課程。

以下小節提供您將需要知道的其他資訊，以便成功呼叫串流獲取API。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[authentication tutorial](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有[!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

- 授權：承載`{ACCESS_TOKEN}`
- x-api索引鍵：`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有資源，包括屬於[!DNL Flow Service]的資源，都與特定虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標題，以指定作業將在下列位置進行的沙箱名稱：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../../../../sandboxes/home.md)。

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

若要建立串流連線，必須在POST請求中提供提供者ID和連線規格ID。 提供程式ID為`521eee4d-8cbe-4906-bb48-fb6bd4450033`，連接規範ID為`bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`。

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
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
| `auth.params.dataType` | 串流連線的資料類型。 此值必須為`xdm`。 |
| `auth.params.name` | 您要建立的串流連線名稱。 |
| `connectionSpec.id` | 流連接的連接規範`id`。 |

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
| `id` | 新建立的連接的`id`。 此處稱為`{CONNECTION_ID}`。 |
| `etag` | 分配給連接的標識符，指定連接的修訂。 |

### 已驗證的連線

當您需要區分來自受信任和不受信任來源的記錄時，應使用已驗證的連線。 想要透過個人識別資訊(PII)傳送資訊的使用者，應在將資訊串流至Platform時建立已驗證的連線。

**API格式**

```http
POST /flowservice/connections
```

**要求**

若要建立串流連線，必須在POST請求中提供提供者ID和連線規格ID。 提供程式ID為`521eee4d-8cbe-4906-bb48-fb6bd4450033`，連接規範ID為`bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`。

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
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
| `auth.params.dataType` | 串流連線的資料類型。 此值必須為`xdm`。 |
| `auth.params.name` | 您要建立的串流連線名稱。 |
| `auth.params.authenticationRequired` | 指定已建立串流連接的參數 |
| `connectionSpec.id` | 流連接的連接規範`id`。 |

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
| `id` | 新建立的連接的`id`。 此處稱為`{CONNECTION_ID}`。 |
| `etag` | 分配給連接的標識符，指定連接的修訂。 |

## 取得串流端點URL

建立基本連線後，您現在可以擷取串流端點URL。

**API格式**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 您先前建立之連線的`id`值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含有關所請求連接的詳細資訊。 串流端點URL會透過連線自動建立，且可使用`inletUrl`值加以擷取。

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

## 建立源連接

建立基本連接後，您需要建立源連接。 建立源連接時，將需要建立的基連接中的`id`值。

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

成功的響應返回HTTP狀態201，其中詳細列出了新建的源連接，包括其唯一標識符(`id`)。

```json
{
    "id": "63070871-ec3f-4cb5-af47-cf7abb25e8bb",
    "etag": "\"28000b90-0000-0200-0000-6091b0150000\""
}
```

## 建立目標連線

建立源連接後，可以建立目標連接。 建立目標連線時，您需要先前建立之資料集的`id`值。

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

成功的回應會傳回HTTP狀態201，並包含新建立目標連線的詳細資訊，包括其唯一識別碼(`id`)。

```json
{
    "id": "98a2a72e-a80f-49ae-aaa3-4783cc9404c2",
    "etag": "\"0500b73f-0000-0200-0000-6091b0b90000\""
}
```

## 建立資料流

建立源連接和目標連接後，您現在可以建立資料流。 資料流負責從源中調度和收集資料。 通過向`/flows`端點執行POST請求，可以建立資料流。

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
    "name": "Sample flow",
    "description": "Sample flow description",
    "flowSpec": {
        "id": "d8a6f005-7eaf-4153-983e-e8574508b877",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "{SOURCE_CONNECTION_ID}"
    ],
    "targetConnectionIds": [
        "{TARGET_CONNECTION_ID}"
    ]
}'
```

**回應**

成功的響應返回HTTP狀態201，其中包含新建立的資料流的詳細資訊，包括其唯一標識符(`id`)。

```json
{
    "id": "ab03bde0-86f2-45c7-b6a5-ad8374f7db1f",
    "etag": "\"1200c123-0000-0200-0000-6091b1730000\""
}
```

## 後續步驟

依照本教學課程，您已建立串流HTTP連線，讓您能使用串流端點將資料內嵌至Platform。 有關在UI中建立流連接的說明，請參閱[建立流連接教程](../../../ui/create/streaming/http.md)。

若要了解如何將資料串流至Platform，請參閱[串流時間序列資料](../../../../../ingestion/tutorials/streaming-time-series-data.md)的教學課程，或[串流記錄資料](../../../../../ingestion/tutorials/streaming-record-data.md)的教學課程。

## 附錄

本節提供使用API建立串流連線的補充資訊。

### 傳送訊息至已驗證的串流連線

如果串流連線已啟用驗證，則用戶端需要將`Authorization`標題新增至其要求。

如果`Authorization`標頭不存在，或者發送了無效/過期的訪問令牌，則將返回HTTP 401 Unauthorized響應，響應如下所示：

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

### 將要擷取的原始資料張貼至Platform {#ingest-data}

現在您已建立流程，可以將JSON訊息傳送至先前建立的串流端點。

**API格式**

```http
POST /collection/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 新建立的串流連線的`id`值。 |

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
      "gender": "Male"
      "birthday": {
          "year": 1984
          "month": 6
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
