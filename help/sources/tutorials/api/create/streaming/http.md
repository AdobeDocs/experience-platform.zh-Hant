---
keywords: Experience Platform；首頁；熱門主題；流連接；建立流連接；api指南；教程；建立流連接；流接收；接收；
solution: Experience Platform
title: 使用API建立HTTP API流連接
topic-legacy: tutorial
type: Tutorial
description: 本教程將幫助您開始使用流接收API，這是Adobe Experience Platform資料接收服務API的一部分。
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 2%

---


# 建立 [!DNL HTTP API] 使用API的流連接

Flow Service用於收集和集中Adobe Experience Platform內各種不同來源的客戶資料。 該服務提供了用戶介面和REST風格的API，所有支援的源都可從中連接。

本教程使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) 引導您完成使用流服務API建立流連接的步驟。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md):標準化框架 [!DNL Platform] 組織經驗資料。
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個源的聚合資料即時提供統一的消費者配置檔案。

此外，建立流連接需要您具有目標XDM架構和資料集。 要瞭解如何建立這些元件，請閱讀上的教程 [流記錄資料](../../../../../ingestion/tutorials/streaming-record-data.md) 或教程 [流時間序列資料](../../../../../ingestion/tutorials/streaming-time-series-data.md)。

以下各節提供了需要瞭解的其他資訊，以便成功調用流接收API。

### 讀取示例API調用

本指南提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

### 收集所需標題的值

為了呼叫 [!DNL Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

- 授權：持 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform]包括那些 [!DNL Flow Service]，與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有關中的沙箱的詳細資訊 [!DNL Platform]，請參見 [沙盒概述文檔](../../../../../sandboxes/home.md)。

包含負載(POST、PUT、PATCH)的所有請求都需要附加的標頭：

- 內容類型：應用程式/json

## 建立基本連接

基本連接指定源並包含使流與流接收API相容所需的資訊。 建立基本連接時，您可以選擇建立未經驗證的連接和經過驗證的連接。

### 未驗證連接

非驗證連接是在要將資料流入平台時可以建立的標準流連接。

**API格式**

```http
POST /flowservice/connections
```

**要求**

為了建立流連接，必須將提供程式ID和連接規範ID作為POST請求的一部分提供。 提供程式ID為 `521eee4d-8cbe-4906-bb48-fb6bd4450033` 連接規範ID為 `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`。

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.sourceId` | 要建立的流連接的ID。 |
| `auth.params.dataType` | 流連接的資料類型。 此值必須為 `xdm`。 |
| `auth.params.name` | 要建立的流連接的名稱。 |
| `connectionSpec.id` | 連接規範 `id` 流連接。 |

**回應**

成功的響應返回HTTP狀態201，其中包含新建立的連接的詳細資訊，包括其唯一標識符(`id`)。

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 的 `id` 新建的連接。 此處稱為 `{CONNECTION_ID}`。 |
| `etag` | 分配給連接的標識符，指定連接的修訂版本。 |

### 已驗證的連接

在需要區分來自受信任源和不受信任源的記錄時，應使用經過身份驗證的連接。 希望使用個人身份資訊(PII)發送資訊的用戶應在將資訊流式傳輸到平台時建立經過身份驗證的連接。

**API格式**

```http
POST /flowservice/connections
```

**要求**

為了建立流連接，必須將提供程式ID和連接規範ID作為POST請求的一部分提供。 提供程式ID為 `521eee4d-8cbe-4906-bb48-fb6bd4450033` 連接規範ID為 `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`。

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.sourceId` | 要建立的流連接的ID。 |
| `auth.params.dataType` | 流連接的資料類型。 此值必須為 `xdm`。 |
| `auth.params.name` | 要建立的流連接的名稱。 |
| `auth.params.authenticationRequired` | 指定建立的流連接的參數 |
| `connectionSpec.id` | 連接規範 `id` 流連接。 |

**回應**

成功的響應返回HTTP狀態201，其中包含新建立的連接的詳細資訊，包括其唯一標識符(`id`)。

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 的 `id` 新建的連接。 此處稱為 `{CONNECTION_ID}`。 |
| `etag` | 分配給連接的標識符，指定連接的修訂版本。 |

## 獲取流終結點URL

建立基本連接後，現在可以檢索流終結點URL。

**API格式**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 的 `id` 先前建立的連接的值。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
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

建立基本連接後，需要建立源連接。 建立源連接時，您需要 `id` 值。

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

成功的響應返回HTTP狀態201，其中詳細列出了新建立的源連接，包括其唯一標識符(`id`)。

```json
{
    "id": "63070871-ec3f-4cb5-af47-cf7abb25e8bb",
    "etag": "\"28000b90-0000-0200-0000-6091b0150000\""
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

目標連接表示到所接收資料所在目的地的連接。 要建立目標連接，必須提供與資料湖關聯的固定連接規範ID。 此連接規範ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

您現在將唯一標識符作為目標模式、目標資料集和到資料湖的連接規範ID。 使用這些標識符，可以使用 [!DNL Flow Service] API，用於指定將包含入站源資料的資料集。

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

成功的響應返回HTTP狀態201，其中包含新建立的目標連接的詳細資訊，包括其唯一標識符(`id`)。

```json
{
    "id": "98a2a72e-a80f-49ae-aaa3-4783cc9404c2",
    "etag": "\"0500b73f-0000-0200-0000-6091b0b90000\""
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
| `xdmSchema` | 的 `$id` 目標XDM架構。 |

**回應**

成功的響應返回新建立的映射的詳細資訊，包括其唯一標識符(`id`)。 在後續步驟中建立資料流時需要此ID。

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

建立源連接和目標連接後，您現在可以建立資料流。 資料流負責調度和收集來自源的資料。 通過對執行POST請求，可以建立資料流 `/flows` 端點。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `flowSpec.id` | 流規範ID [!DNL HTTP API]。 此ID為： `c1a19761-d2c7-4702-b9fa-fe91f0613e81`。 |
| `sourceConnectionIds` | 的 [源連接ID](#source) 在較早的步驟中檢索。 |
| `targetConnectionIds` | 的 [目標連接ID](#target) 在較早的步驟中檢索。 |
| `transformations.params.mappingId` | 的 [映射ID](#mapping) 在較早的步驟中檢索。 |

**回應**

成功的響應返回HTTP狀態201，其中包含新建立的資料流的詳細資訊，包括其唯一標識符(`id`)。

```json
{
    "id": "ab03bde0-86f2-45c7-b6a5-ad8374f7db1f",
    "etag": "\"1200c123-0000-0200-0000-6091b1730000\""
}
```

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

### 將要接收的原始資料發佈到平台 {#ingest-data}

現在，您已建立流，您可以將JSON消息發送到先前建立的流終結點。

**API格式**

```http
POST /collection/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 的 `id` 新建立的流連接的值。 |

**要求**

該示例請求將原始資料接收到以前建立的流終結點。

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

成功響應返回HTTP狀態200，並返回新接收資訊的詳細資訊。

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 先前建立的流連接的ID。 |
| `xactionId` | 為您剛發送的記錄生成的唯一標識符伺服器端。 此ID有助於Adobe通過各種系統和調試跟蹤此記錄的生命週期。 |
| `receivedTimeMs` | 顯示接收請求的時間的時間戳（以毫秒為單位）。 |
