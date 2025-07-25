---
title: 將您的Snowflake串流帳戶連線至Adobe Experience Platform
description: 瞭解如何使用流量服務API將Adobe Experience Platform連線至Snowflake串流。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3fc225a4-746c-4a91-aa77-bbeb091ec364
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API將[!DNL Snowflake]資料串流到Experience Platform

>[!IMPORTANT]
>
>
> 已購買Real-Time Customer Data Platform Ultimate的使用者可在API中使用[!DNL Snowflake]串流來源。

本教學課程提供如何使用[[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>)將資料從您的[!DNL Snowflake]帳戶連線並串流到Adobe Experience Platform的步驟。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

有關[!DNL Snowflake]串流來源的先決條件設定和資訊。 請閱讀[[!DNL Snowflake] 串流來源概觀](../../../../connectors/databases/snowflake-streaming.md)。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

## 建立基礎連線 {#create-a-base-connection}

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL Snowflake]驗證認證作為要求內文的一部分時，對`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL Snowflake]的基礎連線：

>[!TIP]
>
>必須完全依照以下範例輸入`auth.specName`值，包括空格。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "Snowflake base connection",
      "auth": {
          "specName": "Basic Authentication for Snowflake",
          "params": {
              "account": "wixnnnd-ui60793.snowflakecomputing.com",
              "database": "ACME_DB",
              "warehouse": "ACME_WH",
              "username": "nikola15",
              "schema": "PUBLIC",
              "password": "xxxx",
              "role": "ACCOUNTADMIN"
          }
      },
      "connectionSpec": {
          "id": "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `auth.params.account` | 您的[!DNL Snowflake]串流帳戶的名稱。 |
| `auth.params.database` | 將從其中提取資料的[!DNL Snowflake]資料庫名稱。 |
| `auth.params.warehouse` | [!DNL Snowflake]倉儲的名稱。 [!DNL Snowflake]倉儲管理應用程式的查詢執行程式。 每個倉儲彼此獨立，將資料帶入Experience Platform時必須個別存取。 |
| `auth.params.username` | 您[!DNL Snowflake]串流帳戶的使用者名稱。 |
| `auth.params.schema` | （選用）與您的[!DNL Snowflake]串流帳戶關聯的資料庫結構描述。 |
| `auth.params.password` | 您的[!DNL Snowflake]串流帳戶的密碼。 |
| `auth.params.role` | （選用）此[!DNL Snowflake]連線的使用者角色。 如果未提供，此值會預設為`public`。 |
| `connectionSpec.id` | [!DNL Snowflake]連線規格識別碼： `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`。 |

**回應**

成功的回應會傳回新建立的基本連線及其對應的標籤。

```json
{
    "id": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## 探索您的資料表 {#explore-your-data-tables}

接下來，使用基底連線ID來探索並導覽您來源的資料表，方法是在提供基底連線ID作為引數的同時，對`/connections/{BASE_CONNECTION_ID}/explore?objectType=root`端點發出GET請求。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | [!DNL Snowflake]串流來源的基本連線識別碼。 |


**要求**

下列要求會擷取[!DNL Snowflake]串流帳戶的結構和內容。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/1b614dc0-b76e-41e1-b25f-09f4a9d3f111/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會在根層級傳回來源資料的結構和內容。

```json
{
    "items": [
        {
            "type": "table",
            "name": "ACME"
        }
    ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `items.type` | 表格的型別。 |
| `items.names` | 資料表的名稱。 |

## 建立來源連線 {#create-a-source-connection}

來源連線會建立和管理與擷取資料的外部來源的連線。

若要建立來源連線，請對[!DNL Flow Service] API的`/sourceConnections`端點提出POST要求。

**API格式**

```http
POST /sourceConnections
```

**要求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Snowflake Streaming Source Connection",
      "description": "A source connection for Snowflake Streaming data",
      "baseConnectionId": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
      "connectionSpec": {
          "id": "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
          "version": "1.0"
      },
      "params": {
          "tableName": "ACME",
          "timestampColumn": "dOb",
          "backfill": "true",
          "timezoneValue": "PST"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `baseConnectionId` | 您[!DNL Snowflake]串流來源的已驗證基本連線識別碼。 此ID是在先前步驟中產生的。 |
| `connectionSpec.id` | [!DNL Snowflake]串流來源的連線規格ID。 |
| `params.tableName` | [!DNL Snowflake]資料庫中要帶至Experience Platform的資料表名稱。 |
| `params.timestampColumn` | 用於擷取增量值的時間戳記資料行的名稱。 |
| `params.backfill` | 布林值旗標，可判斷資料是從開始（0紀元時間）擷取，還是從來源起始時間擷取。 如需此值的詳細資訊，請閱讀[[!DNL Snowflake] 串流來源概觀](../../../../connectors/databases/snowflake-streaming.md)。 |
| `params.timezoneValue` | 時區值表示在查詢[!DNL Snowflake]資料庫時，應該擷取哪個時區的目前時間。 如果設定的時間戳記資料行設為`TIMESTAMP_NTZ`，則應提供此引數。 如果未提供，`timezoneValue`會預設為UTC。 |

**回應**

成功的回應會傳回來源連線ID及其對應的電子標籤。 來源連線ID將用於稍後步驟中建立資料流。

```json
{
    "id": "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## 建立資料流

>[!NOTE]
>
>在您建立或更新串流資料流後，需要短暫暫停資料擷取5分鐘，以防止任何可能的資料遺失或資料中斷情況。

若要建立資料流以將資料從導覽[!DNL Snowflake]帳戶串流到Experience Platform，您必須在提供下列值時對`/flows`端點進行POST要求：

>[!TIP]
>
>請依照下列連結取得如何擷取下列ID的逐步指南。

* [Source連線ID](#create-a-source-connection)
* [目標連線ID](../../collect/database-nosql.md#create-a-target-connection)
* [流量規格ID](../../collect/database-nosql.md#retrieve-dataflow-specifications)
* [對應 ID](../../collect/database-nosql.md#create-a-mapping)

**API格式**

```http
POST /flows
```

**要求**

以下請求會為您的[!DNL Snowflake]帳戶建立串流資料流。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake Streaming Dataflow",
      "description": "A dataflow for Snowflake streaming data",
      "sourceConnectionIds": [
        "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6"
      ],
      "targetConnectionIds": [
        "78f41c31-3652-4a5e-b264-74331226dcf3"
      ],
      "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
      },
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingId": "44d42ed27c46499a80eb0c0705c38cbd",
            "mappingVersion": 0
          }
        }
      ]
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `sourceConnectionIds` | 您[!DNL Snowflake]串流來源的來源連線識別碼。 |
| `targetConnectionIds` | 您的[!DNL Snowflake]串流來源的目標連線識別碼。 |
| `flowSpec.id` | 用於為[!DNL Snowflake]串流來源建立資料流的流程規格ID。 此流程規格ID可讓您透過對應轉換建立串流資料流。 此ID已修正且為： `c1a19761-d2c7-4702-b9fa-fe91f0613e81`。 |
| `transformations.params.mappingId` | 資料流的對應ID。 |

**回應**

成功的回應會傳回您的流程ID及其對應的標籤。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API為[!DNL Snowflake]資料建立串流資料流。 如需Adobe Experience Platform來源的其他資訊，請瀏覽下列檔案：

* [來源概觀](../../../../home.md)
* [使用API監視您的資料流](../../monitor.md)
