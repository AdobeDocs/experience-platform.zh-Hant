---
title: 使用Flow Service API為Pinterest Ads建立來源連線和資料流
description: 瞭解如何使用流量服務API將Adobe Experience Platform連結至Pinterest Ads。
badge: Beta
hide: true
hidefromtoc: true
exl-id: 293a3ec9-38ea-4b71-a923-1f4e28a41236
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2278'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API為[!DNL Pinterest Ads]建立來源連線和資料流

>[!NOTE]
>
>[!DNL Pinterest Ads]來源是測試版。 閱讀[來源概觀](../../../../home.md#terms-and-conditions)，以取得使用測試版標籤之來源的詳細資訊。

下列教學課程會逐步引導您完成建立[!DNL Pinterest Ads]來源連線和資料流的步驟，以使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)將[[!DNL Pinterest Ads]](https://ads.pinterest.com/)資料帶入Adobe Experience Platform。

## 快速入門 {#getting-started}

本指南需要您深入瞭解下列Experience Platform元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL Pinterest Ads]。

### 先決條件 {#prerequisites}

若要將[!DNL Pinterest Ads]連線至Experience Platform，您必須提供下列連線屬性的值：

* [!DNL Pinterest] `accessToken`。
* [!DNL Pinterest] `adAccountId`。
* [!DNL Pinterest] `campaign`、`adGroup`或`ad` ID的其中一個。

如需這些連線屬性的詳細資訊，請閱讀[[!DNL Pinterest Ads] 總覽](../../../../connectors/advertising/pinterest-ads.md#prerequisites)。

## 使用[!DNL Flow Service] API連線[!DNL Pinterest Ads]至Experience Platform {#connect-platform-to-flow-api}

以下概述將[!DNL Pinterest Ads]連線至Experience Platform所需執行的步驟。

### 建立基礎連線 {#base-connection}

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL Pinterest Ads]驗證認證作為要求內文的一部分時，對`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL Pinterest Ads]的基礎連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Pinterest Ads",
      "description": "Create a live inbound connection to your Pinterest Ads instance, to ingest both historic and scheduled data into Experience Platform",
      "connectionSpec": {
          "id": "f82aae23-91e7-4884-b25f-2d2159d841fd",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Refresh Code",
          "params": {  
              "accessToken": "{PINTEREST_ACCESS_TOKEN}"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 基礎連線的名稱。 確定基本連線的名稱是描述性的，因為您可以使用此名稱來查詢基本連線的資訊。 |
| `description` | 您可以納入的選用值，可提供基礎連線的詳細資訊。 |
| `connectionSpec.id` | 來源的連線規格ID。 在您的來源已透過[!DNL Flow Service] API註冊並核准後，即可擷取此ID。 |
| `auth.specName` | 您用來向Experience Platform驗證來源的驗證型別。 |
| `auth.params.accessToken` | 包含驗證您的來源所需的[!DNL Pinterest]存取權杖值。 |

**回應**

成功的回應會傳回新建立的基礎連線，包括其唯一的連線識別碼(`id`)。 在下一步中探索來源的檔案結構和內容時，需要此ID。

```json
{
    "id": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
    "etag": "\"4d08164f-0000-0200-0000-6368b7bf0000\""
}
```

### 探索您的來源 {#explore}

使用您在上一步中產生的基本連線ID，您可以執行GET要求來探索檔案和目錄。
使用下列呼叫來尋找您要帶入Experience Platform的檔案路徑：

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

執行GET請求以探索來源的檔案結構和內容時，您必須包含下表列出的查詢引數：


| 參數 | 說明 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 在上一步中產生的基本連線ID。 |
| `objectType=rest` | 您要探索的物件型別。 目前，此值一律設為`rest`。 |
| `{OBJECT}` | 只有在檢視特定目錄時才需要此引數。 其值代表您要探索的目錄路徑。 |
| `fileType=json` | 您要帶入Experience Platform的檔案型別。 目前，`json`是唯一受支援的檔案型別。 |
| `{PREVIEW}` | 布林值，定義連線的內容是否支援預覽。 |
| `{SOURCE_PARAMS}` | 為您要帶入Experience Platform的來源檔案定義引數。 若要擷取`{SOURCE_PARAMS}`接受的格式型別，您必須以base64編碼整個`{"ad_account_id":"{PINTEREST_AD_ACCOUNT_ID}","object_ids":"{COMMA_SEPERATED_OBJECT_IDS}","object_type":"{OBJECT_TYPE}}"}`字串。 |

[!DNL Pinterest Ads]支援多個[!DNL Pinterest] Analytics API端點。 根據您運用要傳送的請求的物件型別，如下所示：

**要求**

>[!BEGINTABS]

>[!TAB 行銷活動]

針對[!DNL Pinterest Ads]，當運用Campaign Analytics API時，`{SOURCE_PARAMS}`的值會傳遞為`{"ad_account_id":"123456789000","object_ids":"000123456789","object_type":"campaigns"}`。 以base64編碼時，其等於`YHsiYWRfYWNjb3VudF9pZCI6IjEyMzQ1Njc4OTAwMCIsIm9iamVjdF9pZHMiOiIwMDAxMjM0NTY3ODkiLCJvYmplY3RfdHlwZSI6ImNhbXBhaWducyJ9`，如下所示。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=YHsiYWRfYWNjb3VudF9pZCI6IjEyMzQ1Njc4OTAwMCIsIm9iamVjdF9pZHMiOiIwMDAxMjM0NTY3ODkiLCJvYmplY3RfdHlwZSI6ImNhbXBhaWducyJ9' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!TAB 廣告群組]

針對[!DNL Pinterest Ads]，當使用廣告群組分析API時，`{SOURCE_PARAMS}`的值會傳遞為`{"ad_account_id":"123456789000","object_ids":"000123456789,100123456789","object_type":"ad_groups"}`。 在base64中編碼時，它等於`eyJhZF9hY2NvdW50X2lkIjoiMTIzNDU2Nzg5MDAwIiwib2JqZWN0X2lkcyI6IjAwMDEyMzQ1Njc4OSwxMDAxMjM0NTY3ODkiLCJvYmplY3RfdHlwZSI6ImFkX2dyb3VwcyJ9`，如下所示。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJhZF9hY2NvdW50X2lkIjoiMTIzNDU2Nzg5MDAwIiwib2JqZWN0X2lkcyI6IjAwMDEyMzQ1Njc4OSwxMDAxMjM0NTY3ODkiLCJvYmplY3RfdHlwZSI6ImFkX2dyb3VwcyJ9' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!TAB 廣告]

針對[!DNL Pinterest Ads]，當運用Ads Analytics API時，`{SOURCE_PARAMS}`的值會傳遞為`{"ad_account_id":"123456789000","object_ids":"687247811001,687247811002,687247815005,687247834765","object_type":"ads"}`。 在base64中編碼時，它等於`eyJhZF9hY2NvdW50X2lkIjoiMTIzNDU2Nzg5MDAwIiwib2JqZWN0X2lkcyI6IjY4NzI0NzgxMTAwMSw2ODcyNDc4MTEwMDIsNjg3MjQ3ODE1MDA1LDY4NzI0NzgzNDc2NSIsIm9iamVjdF90eXBlIjoiYWRzIn0=`，如下所示。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJhZF9hY2NvdW50X2lkIjoiMTIzNDU2Nzg5MDAwIiwib2JqZWN0X2lkcyI6IjY4NzI0NzgxMTAwMSw2ODcyNDc4MTEwMDIsNjg3MjQ3ODE1MDA1LDY4NzI0NzgzNDc2NSIsIm9iamVjdF90eXBlIjoiYWRzIn0=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!ENDTABS]

**回應**

>[!NOTE]
>
>部分記錄已截斷，以提供更好的簡報。

>[!BEGINTABS]

>[!TAB 行銷活動]

成功的回應會傳回您呼叫的對應[!DNL Pinterest Ads] API的資料結構。

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "IMPRESSION_1_GROSS": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "DATE": {
                "type": "string"
            },
            "TOTAL_CLICKTHROUGH": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "CAMPAIGN_ID": {
                "type": "string"
            },
            "TOTAL_IMPRESSION_USER": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "REPIN_1": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "TOTAL_ENGAGEMENT": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "ENGAGEMENT_RATE": {
                "type": "number"
            },
            "CAMPAIGN_NAME": {
                "type": "string"
            },
            "ECTR": {
                "type": "number"
            }
        }
    },
    "data": [
        {
            "IMPRESSION_1_GROSS": 355,
            "DATE": "2023-02-10",
            "TOTAL_CLICKTHROUGH": 7,
            "CAMPAIGN_ID": "000123456789",
            "TOTAL_IMPRESSION_USER": 324,
            "REPIN_1": 2,
            "TOTAL_ENGAGEMENT": 10,
            "ENGAGEMENT_RATE": 0.029940119760479042,
            "CAMPAIGN_NAME": "Test Campaign 1",
            "ECTR": 0.020833333333333332
        }
    ]
}
```

>[!TAB 廣告群組]

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "IMPRESSION_1_GROSS": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "DATE": {
                "type": "string"
            },
            "TOTAL_CLICKTHROUGH": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "CAMPAIGN_ID": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "TOTAL_IMPRESSION_USER": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "TOTAL_ENGAGEMENT": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "ENGAGEMENT_RATE": {
                "type": "number"
            },
            "CAMPAIGN_NAME": {
                "type": "string"
            },
            "AD_GROUP_ID": {
                "type": "string"
            },
            "ECTR": {
                "type": "number"
            }
        }
    },
    "data": [
        {
            "IMPRESSION_1_GROSS": 164,
            "DATE": "2023-02-13",
            "TOTAL_CLICKTHROUGH": 2,
            "CAMPAIGN_ID": 626747962992,
            "TOTAL_IMPRESSION_USER": 149,
            "TOTAL_ENGAGEMENT": 3,
            "ENGAGEMENT_RATE": 0.01910828025477707,
            "CAMPAIGN_NAME": "Test Campaign 1",
            "AD_GROUP_ID": "000123456789",
            "ECTR": 0.012658227848101266
        },
        {
            "IMPRESSION_1_GROSS": 177,
            "DATE": "2023-02-13",
            "TOTAL_CLICKTHROUGH": 5,
            "CAMPAIGN_ID": 626747962992,
            "TOTAL_IMPRESSION_USER": 167,
            "TOTAL_ENGAGEMENT": 5,
            "ENGAGEMENT_RATE": 0.028901734104046242,
            "CAMPAIGN_NAME": "Test Campaign 1",
            "AD_GROUP_ID": "100123456789",
            "ECTR": 0.028901734104046242
        }
    ]
}
```

>[!TAB 廣告]

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "IMPRESSION_1_GROSS": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "DATE": {
                "type": "string"
            },
            "TOTAL_CLICKTHROUGH": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "CAMPAIGN_ID": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "TOTAL_IMPRESSION_USER": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "AD_ID": {
                "type": "string"
            },
            "TOTAL_ENGAGEMENT": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "ENGAGEMENT_RATE": {
                "type": "number"
            },
            "CAMPAIGN_NAME": {
                "type": "string"
            },
            "AD_GROUP_ID": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "ECTR": {
                "type": "number"
            }
        }
    },
    "data": [
        {
            "IMPRESSION_1_GROSS": 146,
            "DATE": "2023-02-13",
            "TOTAL_CLICKTHROUGH": 2,
            "CAMPAIGN_ID": 100123456789,
            "TOTAL_IMPRESSION_USER": 132,
            "AD_ID": "687247811001",
            "TOTAL_ENGAGEMENT": 3,
            "ENGAGEMENT_RATE": 0.02158273381294964,
            "CAMPAIGN_NAME": "Test Campaign 1",
            "AD_GROUP_ID": 000123456789,
            "ECTR": 0.014285714285714285
        },
        {
            "IMPRESSION_1_GROSS": 19,
            "DATE": "2023-02-13",
            "CAMPAIGN_ID": 100123456789,
            "TOTAL_IMPRESSION_USER": 18,
            "AD_ID": "687247811002",
            "CAMPAIGN_NAME": "Test Campaign 1",
            "AD_GROUP_ID": 000123456789
        },
        {
            "IMPRESSION_1_GROSS": 63,
            "DATE": "2023-02-13",
            "TOTAL_CLICKTHROUGH": 1,
            "CAMPAIGN_ID": 100123456789,
            "TOTAL_IMPRESSION_USER": 57,
            "AD_ID": "687247815005",
            "TOTAL_ENGAGEMENT": 1,
            "ENGAGEMENT_RATE": 0.016129032258064516,
            "CAMPAIGN_NAME": "Test Campaign 1",
            "AD_GROUP_ID": 100123456789,
            "ECTR": 0.016129032258064516
        },
        {
            "IMPRESSION_1_GROSS": 116,
            "DATE": "2023-02-13",
            "TOTAL_CLICKTHROUGH": 4,
            "CAMPAIGN_ID": 100123456789,
            "TOTAL_IMPRESSION_USER": 115,
            "AD_ID": "687247834765",
            "TOTAL_ENGAGEMENT": 4,
            "ENGAGEMENT_RATE": 0.035398230088495575,
            "CAMPAIGN_NAME": "Test Campaign 1",
            "AD_GROUP_ID": 100123456789,
            "ECTR": 0.035398230088495575
        }
    ]
}
```

>[!ENDTABS]

### 建立來源連線 {#source-connection}

您可以對[!DNL Flow Service] API發出POST要求，以建立來源連線。 來源連線由基礎連線ID、來源資料檔案的路徑以及連線規格ID組成。

**API格式**

```https
POST /sourceConnections
```

**要求**

[!DNL Pinterest Ads]來源支援多個[!DNL Pinterest] Analytics API端點。 根據您運用下列請求建立的物件型別，會建立來源連線：

>[!BEGINTABS]

>[!TAB 行銷活動]

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Pinterest Ads Source Connection",
        "description": "Pinterest Ads Source Connection",
        "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
        "connectionSpec": {
            "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "ad_account_id": "123456789000",
            "object_type": "campaigns",
            "object_ids": "2680074532641"
        }
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 來源連線的名稱。 確保來源連線的名稱是描述性的，因為您可以使用此名稱來查詢來源連線的資訊。 |
| `description` | 您可以納入的選用值，可提供來源連線的詳細資訊。 |
| `baseConnectionId` | [!DNL Pinterest Ads]的基本連線識別碼。 此ID是在先前步驟中產生的。 |
| `connectionSpec.id` | 與您的來源對應的連線規格ID。 |
| `data.format` | 您要擷取的[!DNL Pinterest Ads]資料格式。 目前唯一支援的資料格式為`json`。 |
| `params.ad_account_id` | [!DNL Pinterest] `Ad account ID`。 |
| `params.object_type` | 由於[!DNL Pinterest] Campaign Analytics API端點為必要項，因此值為`campaigns`。 |
| `params.object_ids` | [!DNL Pinterest]行銷活動ID的逗號分隔清單。 |

>[!TAB 廣告群組]

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Pinterest Ads Source Connection",
        "description": "Pinterest Ads Source Connection",
        "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
        "connectionSpec": {
            "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "ad_account_id": "123456789000",
            "object_type": "ad_groups",
            "object_ids": "2680074532641,2680074533547"
        }
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 來源連線的名稱。 確保來源連線的名稱是描述性的，因為您可以使用此名稱來查詢來源連線的資訊。 |
| `description` | 您可以納入的選用值，可提供來源連線的詳細資訊。 |
| `baseConnectionId` | [!DNL Pinterest Ads]的基本連線識別碼。 此ID是在先前步驟中產生的。 |
| `connectionSpec.id` | 與您的來源對應的連線規格ID。 |
| `data.format` | 您要擷取的[!DNL Pinterest Ads]資料格式。 目前唯一支援的資料格式為`json`。 |
| `params.ad_account_id` | [!DNL Pinterest] `Ad account ID`。 |
| `params.object_type` | 由於[!DNL Pinterest]廣告群組Analytics API端點為必要項，因此值為`ad_groups`。 |
| `params.object_ids` | [!DNL Pinterest]個廣告群組ID的逗號分隔清單。 |

>[!TAB 廣告]

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Pinterest Ads Source Connection",
        "description": "Pinterest Ads Source Connection",
        "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
        "connectionSpec": {
            "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "ad_account_id": "123456789000",
            "object_type": "ads",
            "object_ids": "687247811001,687247811002,687247815005,687247834765"
        }
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 來源連線的名稱。 確保來源連線的名稱是描述性的，因為您可以使用此名稱來查詢來源連線的資訊。 |
| `description` | 您可以納入的選用值，可提供來源連線的詳細資訊。 |
| `baseConnectionId` | [!DNL Pinterest Ads]的基本連線識別碼。 此ID是在先前步驟中產生的。 |
| `connectionSpec.id` | 與您的來源對應的連線規格ID。 |
| `data.format` | 您要擷取的[!DNL Pinterest Ads]資料格式。 目前唯一支援的資料格式為`json`。 |
| `params.ad_account_id` | [!DNL Pinterest] `Ad account ID`。 |
| `params.object_type` | 由於[!DNL Pinterest] Ad Analytics API端點為必要項，因此值為`ads`。 |
| `params.object_ids` | [!DNL Pinterest]個廣告ID的逗號分隔清單。 |

>[!ENDTABS]

**回應**

成功的回應會傳回新建立的來源連線的唯一識別碼(`id`)。 在後續步驟中需要此ID才能建立資料流。

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

### 建立目標XDM結構描述 {#target-schema}

為了在Experience Platform中使用來源資料，必須建立目標結構描述，以根據您的需求建構來源資料。 然後使用目標結構描述來建立包含來源資料的Experience Platform資料集。

可透過對[結構描述登入API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)執行POST要求來建立目標XDM結構描述。

如需有關如何建立目標XDM結構描述的詳細步驟，請參閱有關使用API [建立結構描述的教學課程](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html?lang=zh-Hant#create)。

### 建立目標資料集 {#target-dataset}

可透過對[目錄服務API](https://developer.adobe.com/experience-platform-apis/references/catalog/)執行POST要求，在承載中提供目標結構描述的ID，來建立目標資料集。

如需有關如何建立目標資料集的詳細步驟，請參閱有關[使用API建立資料集](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html?lang=zh-Hant)的教學課程。

### 建立目標連線 {#target-connection}

目標連線代表與要儲存所擷取資料的目的地之間的連線。 若要建立目標連線，您必須提供對應至資料湖的固定連線規格ID。 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

您現在具有目標結構描述、目標資料集和到資料湖的連線規格ID的唯一識別碼。 使用這些識別碼，您可以使用[!DNL Flow Service] API建立目標連線，以指定將包含傳入來源資料的資料集。

**API格式**

```https
POST /targetConnections
```

**要求**

下列要求會建立[!DNL Pinterest Ads]的目標連線：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Pinterest Ads Target Connection",
        "description": "Pinterest Ads Target Connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "dataSetId": "5ef4551c52e054191a61a99f"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 目標連線的名稱。 請確定目標連線的名稱是描述性的，因為您可以使用此名稱來查詢目標連線的資訊。 |
| `description` | 您可以納入的選用值，可提供目標連線的詳細資訊。 |
| `connectionSpec.id` | 對應至[!DNL Data Lake]的連線規格識別碼。 此固定ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |
| `data.format` | 您要帶入Experience Platform的[!DNL Pinterest Ads]資料格式。 |
| `params.dataSetId` | 在上一步中擷取的目標資料集ID。 |

**回應**

成功的回應會傳回新目標連線的唯一識別碼(`id`)。 此ID在後續步驟中是必要的。

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

### 建立對應 {#mapping}

為了將來源資料擷取到目標資料集中，必須首先將其對應到目標資料集所堅持的目標結構描述。 這是透過使用在要求裝載中定義的資料對應對[[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/)執行POST要求來達成。

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
            "sourceType": "ATTRIBUTE",
            "source": "CAMPAIGN_ID",
            "destination": "_extconndev.ID_CAMPAIGN"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "CAMPAIGN_NAME",
            "destination": "_extconndev.NAME_CAMPAIGN"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "AD_GROUP_ID",
            "destination": "_extconndev.AD_GROUP_ID"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "AD_ID",
            "destination": "_extconndev.AD_ID"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "DATE",
            "destination": "_extconndev.DATE"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "ECTR",
            "destination": "_extconndev.ECTR"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "ENGAGEMENT_RATE",
            "destination": "_extconndev. ENGAGEMENT_RATE"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "IMPRESSION_1_GROSS",
            "destination": "_extconndev. IMPRESSION_1_GROSS"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "REPIN_1",
            "destination": "_extconndev. REPIN_1"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "TOTAL_CLICKTHROUGH",
            "destination": "_extconndev. TOTAL_CLICKTHROUGH"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "TOTAL_ENGAGEMENT",
            "destination": "_extconndev. TOTAL_ENGAGEMENT"
            },
            {
            "sourceType": "ATTRIBUTE",
            "source": "TOTAL_IMPRESSION_USER",
            "destination": "_extconndev. TOTAL_IMPRESSION_USER"
            }
        ],
        "outputSchema": {
            "schemaRef": {
            "id": "{{schemaId}}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        }
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `outputSchema.schemaRef.id` | 在先前步驟中產生的[目標XDM結構描述](#target-schema)識別碼。 |
| `mappings.sourceType` | 正在對應的來源屬性型別。 |
| `mappings.source` | 需要對映至目的地XDM路徑的來源屬性。 |
| `mappings.destination` | 來源屬性對應到的目的地XDM路徑。 |

**回應**

成功的回應會傳回新建立的對應詳細資料，包括其唯一識別碼(`id`)。 在後續步驟中需要此值，才能建立資料流。

```json
{
    "id": "059c69f7207b4d7e9b48c47e2fd966a6",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### 建立流程 {#flow}

將資料從[!DNL Pinterest Ads]引進Experience Platform的最後一步是建立資料流。 到現在為止，您已準備下列必要值：

* [Source連線ID](#source-connection)
* [目標連線ID](#target-connection)
* [對應 ID](#mapping)

資料流負責從來源排程及收集資料。 您可以執行POST要求，同時在裝載中提供先前提及的值來建立資料流。

若要排程內嵌，您必須先將開始時間值設為以秒為單位的epoch時間。 然後，您必須將頻率值設定為下列五個選項之一： `once`、`minute`、`hour`、`day`或`week`。 間隔值會指定兩個連續擷取之間的期間，不過，建立一次性擷取不需要設定間隔。 對於所有其他頻率，間隔值必須設定為等於或大於`15`。

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
        "name": "Pinterest Ads dataflow",
        "description": "Pinterest Ads dataflow",
        "flowSpec": {
            "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "8f1fc72a-f562-4a1d-8597-85b5ca1b1cd3"
        ],
        "targetConnectionIds": [
            "6b137bf6-d2a0-48c8-914b-d50f4942eb85"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "059c69f7207b4d7e9b48c47e2fd966a6",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1625040887",
            "frequency": "minute",
            "interval": 15
        }
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 資料流的名稱。 確保資料流的名稱是描述性的，因為您可以使用此名稱來查閱資料流上的資訊。 |
| `description` | 您可以納入的選用值，可提供資料流的詳細資訊。 |
| `flowSpec.id` | 建立資料流所需的流量規格ID。 此固定ID為： `6499120c-0b15-42dc-936e-847ea3c24d72`。 |
| `flowSpec.version` | 流程規格ID的對應版本。 此值預設為`1.0`。 |
| `sourceConnectionIds` | 在先前步驟中產生的[來源連線識別碼](#source-connection)。 |
| `targetConnectionIds` | 在先前步驟中產生的[目標連線識別碼](#target-connection)。 |
| `transformations` | 此屬性包含套用至資料所需的各種轉換。 將非XDM相容的資料引進Experience Platform時，需要此屬性。 |
| `transformations.name` | 指定給轉換的名稱。 |
| `transformations.params.mappingId` | 在先前步驟中產生的[對應ID](#mapping)。 |
| `transformations.params.mappingVersion` | 對應ID的對應版本。 此值預設為`0`。 |
| `scheduleParams.startTime` | 此屬性包含資料流擷取排程的相關資訊。 |
| `scheduleParams.frequency` | 資料流收集資料的頻率。 可接受的值包括： `once`、`minute`、`hour`、`day`或`week`。 |
| `scheduleParams.interval` | 間隔會指定兩個連續資料流執行之間的期間。 間隔的值應為非零整數。 當頻率設定為`once`時不需要間隔，其他頻率值應該大於或等於`15`。 |

**回應**

成功的回應會傳回新建立的資料流識別碼(`id`)。 您可以使用此ID來監視、更新或刪除資料流。

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

## 附錄 {#appendix}

下節提供監視、更新和刪除資料流的步驟相關資訊。

### 監視資料流 {#monitor-dataflow}

建立資料流後，您可以監視透過該資料流擷取的資料，以檢視有關資料流執行、完成狀態和錯誤的資訊。 如需完整的API範例，請閱讀[使用API監視您的來源資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html?lang=zh-Hant)的指南。

### 更新您的資料流 {#update-dataflow}

提供資料流的ID時，透過向[!DNL Flow Service] API的`/flows`端點發出PATCH要求，更新資料流的詳細資訊，例如其名稱和說明，以及其執行排程和相關聯的對應集。 發出PATCH請求時，您必須在`If-Match`標頭中提供資料流的唯一`etag`。 如需完整的API範例，請閱讀[使用API更新來源資料流的指南](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html?lang=zh-Hant)

### 更新您的帳戶 {#update-account}

在提供您的基本連線ID作為查詢引數的同時，透過對[!DNL Flow Service] API執行PATCH請求來更新來源帳戶的名稱、說明和認證。 發出PATCH請求時，您必須在`If-Match`標頭中提供來源帳戶的唯一`etag`。 如需完整的API範例，請閱讀[使用API更新來源帳戶的指南](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html?lang=zh-Hant)。

### 刪除您的資料流 {#delete-dataflow}

提供您要刪除之資料流的ID做為查詢引數的一部分，同時對[!DNL Flow Service] API執行DELETE要求，以刪除您的資料流。 如需完整的API範例，請閱讀[使用API刪除資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html?lang=zh-Hant)的指南。

### 刪除您的帳戶 {#delete-account}

在提供您要刪除之帳戶的基本連線ID時，對[!DNL Flow Service] API執行DELETE要求，以刪除您的帳戶。 如需完整的API範例，請閱讀[使用API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html?lang=zh-Hant)刪除來源帳戶的指南。
