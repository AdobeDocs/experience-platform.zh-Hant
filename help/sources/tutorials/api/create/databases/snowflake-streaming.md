---
title: 將您的Snowflake串流帳戶連線至Adobe Experience Platform
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連結至Snowflake串流。
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 2%

---

# 串流 [!DNL Snowflake] 使用進行Experience Platform的資料 [!DNL Flow Service] API

>[!IMPORTANT]
>
>* 此 [!DNL Snowflake] 串流來源為測試版。 請閱讀 [來源概觀](../../../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。
>* 此 [!DNL Snowflake] 已購買Real-Time CDP Ultimate的客戶可在來源目錄中取得串流來源。


本教學課程提供如何連線並串流資料的步驟。 [!DNL Snowflake] Adobe Experience Platform帳戶，使用 [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## 快速入門

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

如需先決條件設定及相關資訊，請參閱 [!DNL Snowflake] 串流來源。 請閱讀 [[!DNL Snowflake] 串流來源概觀](../../../../connectors/databases/snowflake-streaming.md).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線 {#create-a-base-connection}

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL Snowflake] 要求內文中的驗證認證。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立 [!DNL Snowflake]：

>[!TIP]
>
>此 `auth.specName` 輸入的值必須與下面的範例完全相同，包括空格。

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
| `auth.params.account` | 您的名稱 [!DNL Snowflake] 串流帳戶。 |
| `auth.params.database` | 您的名稱 [!DNL Snowflake] 從中提取資料的資料庫。 |
| `auth.params.warehouse` | 您的名稱 [!DNL Snowflake] 倉儲。 此 [!DNL Snowflake] warehouse會管理應用程式的查詢執行程式。 每個倉儲彼此獨立，且在將資料帶到Platform時必須個別存取。 |
| `auth.params.username` | 您的使用者名稱 [!DNL Snowflake] 串流帳戶。 |
| `auth.params.schema` | （選用）與下列專案關聯的資料庫結構： [!DNL Snowflake] 串流帳戶。 |
| `auth.params.password` | 您的密碼 [!DNL Snowflake] 串流帳戶。 |
| `auth.params.role` | （選用）此專案的使用者角色 [!DNL Snowflake] 連線。 如果未提供，則此值預設為 `public`. |
| `connectionSpec.id` | 此 [!DNL Snowflake] 連線規格ID： `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

**回應**

成功回應會傳回新建立的基本連線及其對應的電子標籤。

```json
{
    "id": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## 探索您的資料表格 {#explore-your-data-tables}

接下來，使用基本連線ID透過向以下專案發出GET請求，以探索並瀏覽來源的資料表： `/connections/{BASE_CONNECTION_ID}/explore?objectType=root` 端點時，將基本連線ID作為引數提供。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 您的的基本連線ID [!DNL Snowflake] 串流來源。 |


**要求**

以下請求會擷取您的結構和內容 [!DNL Snowflake] 串流帳戶。

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
| `items.names` | 表格的名稱。 |

## 建立來源連線 {#create-a-source-connection}

來源連線會建立和管理與擷取資料之外部來源的連線。

POST若要建立來源連線，請向 `/sourceConnections` 的端點 [!DNL Flow Service] API。

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
          "backfill": "true"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `baseConnectionId` | 貴機構的已驗證基本連線ID [!DNL Snowflake] 串流來源。 此ID是在先前的步驟中產生的。 |
| `connectionSpec.id` | 的連線規格ID [!DNL Snowflake] 串流來源。 |
| `params.tableName` | 中的表格名稱 [!DNL Snowflake] 要帶到Platform的資料庫。 |
| `params.timestampColumn` | 用於擷取增量值的時間戳記資料行名稱。 |
| `params.backfill` | 布林值旗標，可判斷資料是從開始（0紀元時間）擷取，還是從來源起始時間擷取。 如需此值的詳細資訊，請閱讀 [[!DNL Snowflake] 串流來源概觀](../../../../connectors/databases/snowflake-streaming.md). |

**回應**

成功的回應會傳回您的來源連線ID及其對應的etag。 來源連線ID將用於後續步驟以建立資料流。

```json
{
    "id": "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## 建立資料流

若要建立資料流以串流瀏覽的資料 [!DNL Snowflake] 帳戶至平台，您必須向以下網站發出POST請求： `/flows` 端點，並提供下列值：

>[!TIP]
>
>請依照下列連結取得如何擷取下列ID的逐步指南。

* [來源連線ID](#create-a-source-connection)
* [目標連線ID](../../collect/database-nosql.md#create-a-target-connection)
* [流量規格ID](../../collect/database-nosql.md#retrieve-dataflow-specifications)
* [對應 ID](../../collect/database-nosql.md#create-a-mapping)

**API格式**

```http
POST /flows
```

**要求**

以下請求會為您的建立串流資料流 [!DNL Snowflake] 帳戶。

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
| `sourceConnectionIds` | 您的來源連線ID [!DNL Snowflake] 串流來源。 |
| `targetConnectionIds` | 您的目標連線ID [!DNL Snowflake] 串流來源。 |
| `flowSpec.id` | 為建立資料流的流程規格ID [!DNL Snowflake] 串流來源。 此流程規格ID可讓您使用對應轉換建立串流資料流。 此ID已修正，且為： `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. |
| `transformations.params.mappingId` | 資料流的對應ID。 |

**回應**

成功回應會傳回您的流量ID及其對應的etag。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

## 後續步驟

依照本教學課程所述，您已為您的建立串流資料流 [!DNL Snowflake] 資料使用 [!DNL Flow Service] API。 如需Adobe Experience Platform來源的其他資訊，請瀏覽下列檔案：

* [來源概觀](../../../../home.md)
* [使用API監控資料流](../../monitor.md)