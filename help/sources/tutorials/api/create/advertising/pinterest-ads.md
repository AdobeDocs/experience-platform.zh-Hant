---
title: 使用流服務API為Pinterest廣告建立源連接和資料流
description: 瞭解如何使用流服務API將Adobe Experience Platform與Pinterest廣告連接。
badge: β
hide: true
hidefromtoc: true
exl-id: 293a3ec9-38ea-4b71-a923-1f4e28a41236
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '2333'
ht-degree: 1%

---

# 建立源連接和資料流 [!DNL Pinterest Ads] 使用 [!DNL Flow Service] API

>[!NOTE]
>
>的 [!DNL Pinterest Ads] 源為beta。 閱讀 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

以下教程將指導您完成建立 [!DNL Pinterest Ads] 源連接和資料流 [[!DNL Pinterest Ads]](https://ads.pinterest.com/) 資料到Adobe Experience Platform [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門 {#getting-started}

本指南要求對以下Experience Platform元件進行工作理解：

* [源](../../../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了要成功連接到所需的其他資訊 [!DNL Pinterest Ads] 使用 [!DNL Flow Service] API。

### 先決條件 {#prerequisites}

為了連接 [!DNL Pinterest Ads] 要Experience Platform，必須為以下連接屬性提供值：

* 此 [!DNL Pinterest] `accessToken`.
* 此 [!DNL Pinterest] `adAccountId`.
* 其中之一 [!DNL Pinterest] `campaign`。 `adGroup` 或 `ad` ID根據需要。

有關這些連接屬性的詳細資訊，請閱讀 [[!DNL Pinterest Ads] 概述](../../../../connectors/advertising/pinterest-ads.md#prerequisites)。

## 連接 [!DNL Pinterest Ads] 到使用 [!DNL Flow Service] API {#connect-platform-to-flow-api}

以下概述了要連接的步驟 [!DNL Pinterest Ads] Experience Platform。

### 建立基本連接 {#base-connection}

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL Pinterest Ads] 身份驗證憑據作為請求正文的一部分。

**API格式**

```https
POST /connections
```

**要求**

以下請求為 [!DNL Pinterest Ads]:

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
| `name` | 基本連接的名稱。 確保基本連接的名稱是描述性的，因為您可以使用此名稱查找有關基本連接的資訊。 |
| `description` | 可以包括的可選值，用於提供有關基本連接的詳細資訊。 |
| `connectionSpec.id` | 源的連接規範ID。 在通過註冊和批准源後，可以檢索此ID [!DNL Flow Service] API。 |
| `auth.specName` | 用於將源驗證到平台的驗證類型。 |
| `auth.params.accessToken` | 包含 [!DNL Pinterest] 驗證源所需的訪問令牌值。 |

**回應**

成功的響應返回新建立的基本連接，包括其唯一連接標識符(`id`)。 在下一步中瀏覽源的檔案結構和內容需要此ID。

```json
{
    "id": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
    "etag": "\"4d08164f-0000-0200-0000-6368b7bf0000\""
}
```

### 瀏覽源 {#explore}

使用上一步中生成的基本連接ID，可以通過執行GET請求來瀏覽檔案和目錄。
使用以下調用查找要引入平台的檔案路徑：

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

執行GET請求以瀏覽源的檔案結構和內容時，必須包括下表中列出的查詢參數：


| 參數 | 說明 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 在上一步中生成的基本連接ID。 |
| `objectType=rest` | 要瀏覽的對象的類型。 當前，此值始終設定為 `rest`。 |
| `{OBJECT}` | 僅當查看特定目錄時才需要此參數。 其值表示要瀏覽的目錄的路徑。 |
| `fileType=json` | 要帶到平台的檔案的檔案類型。 目前， `json` 是唯一支援的檔案類型。 |
| `{PREVIEW}` | 一個布爾值，它定義連接的內容是否支援預覽。 |
| `{SOURCE_PARAMS}` | 定義要帶到平台的源檔案的參數。 檢索接受的格式類型 `{SOURCE_PARAMS}`，您必須對整個 `{"ad_account_id":"{PINTEREST_AD_ACCOUNT_ID}","object_ids":"{COMMA_SEPERATED_OBJECT_IDS}","object_type":"{OBJECT_TYPE}}"}` base64中的字串。 |

[!DNL Pinterest Ads] 支援多個 [!DNL Pinterest] 分析API終結點。 根據您利用要發送的請求的對象類型，如下所示：

**要求**

>[!BEGINTABS]

>[!TAB 行銷活動]

對於 [!DNL Pinterest Ads]，在利用市場活動分析API時， `{SOURCE_PARAMS}` 傳遞為 `{"ad_account_id":"123456789000","object_ids":"000123456789","object_type":"campaigns"}`。 當編碼在base64中時，它等於 `YHsiYWRfYWNjb3VudF9pZCI6IjEyMzQ1Njc4OTAwMCIsIm9iamVjdF9pZHMiOiIwMDAxMjM0NTY3ODkiLCJvYmplY3RfdHlwZSI6ImNhbXBhaWducyJ9` 如下所示。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=YHsiYWRfYWNjb3VudF9pZCI6IjEyMzQ1Njc4OTAwMCIsIm9iamVjdF9pZHMiOiIwMDAxMjM0NTY3ODkiLCJvYmplY3RfdHlwZSI6ImNhbXBhaWducyJ9' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!TAB 廣告組]

對於 [!DNL Pinterest Ads]，在利用Ad Groups Analytics API時， `{SOURCE_PARAMS}` 傳遞為 `{"ad_account_id":"123456789000","object_ids":"000123456789,100123456789","object_type":"ad_groups"}`。 當編碼在base64中時，它等於 `eyJhZF9hY2NvdW50X2lkIjoiMTIzNDU2Nzg5MDAwIiwib2JqZWN0X2lkcyI6IjAwMDEyMzQ1Njc4OSwxMDAxMjM0NTY3ODkiLCJvYmplY3RfdHlwZSI6ImFkX2dyb3VwcyJ9` 如下所示。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJhZF9hY2NvdW50X2lkIjoiMTIzNDU2Nzg5MDAwIiwib2JqZWN0X2lkcyI6IjAwMDEyMzQ1Njc4OSwxMDAxMjM0NTY3ODkiLCJvYmplY3RfdHlwZSI6ImFkX2dyb3VwcyJ9' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!TAB 廣告]

對於 [!DNL Pinterest Ads]，在利用Ads Analytics API時， `{SOURCE_PARAMS}` 傳遞為 `{"ad_account_id":"123456789000","object_ids":"687247811001,687247811002,687247815005,687247834765","object_type":"ads"}`。 當編碼在base64中時，它等於 `eyJhZF9hY2NvdW50X2lkIjoiMTIzNDU2Nzg5MDAwIiwib2JqZWN0X2lkcyI6IjY4NzI0NzgxMTAwMSw2ODcyNDc4MTEwMDIsNjg3MjQ3ODE1MDA1LDY4NzI0NzgzNDc2NSIsIm9iamVjdF90eXBlIjoiYWRzIn0=` 如下所示。

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
>某些記錄已被截斷，以便更好地呈現。

>[!BEGINTABS]

>[!TAB 行銷活動]

成功的響應返回相應的 [!DNL Pinterest Ads] 你調用的API。

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

>[!TAB 廣告組]

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

### 建立源連接 {#source-connection}

您可以通過向POST請求建立源連接 [!DNL Flow Service] API。 源連接由基本連接ID、源資料檔案路徑和連接規範ID組成。

**API格式**

```https
POST /sourceConnections
```

**要求**

的 [!DNL Pinterest Ads] 源支援多個 [!DNL Pinterest] 分析API終結點。 根據您利用以下請求的對象類型建立源連接：

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
| `name` | 源連接的名稱。 確保源連接的名稱是描述性的，因為您可以使用它來查找有關源連接的資訊。 |
| `description` | 可以包括的可選值，用於提供有關源連接的詳細資訊。 |
| `baseConnectionId` | 基本連接ID [!DNL Pinterest Ads]。 此ID是在前一步驟中生成的。 |
| `connectionSpec.id` | 與源對應的連接規範ID。 |
| `data.format` | 格式 [!DNL Pinterest Ads] 要攝取的資料。 目前，唯一支援的資料格式是 `json`。 |
| `params.ad_account_id` | 此 [!DNL Pinterest] `Ad account ID`. |
| `params.object_type` | 作為 [!DNL Pinterest] 市場活動分析API終結點是必需的，該值將為 `campaigns`。 |
| `params.object_ids` | 以逗號分隔的清單 [!DNL Pinterest] 市場活動ID |

>[!TAB 廣告組]

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
| `name` | 源連接的名稱。 確保源連接的名稱是描述性的，因為您可以使用它來查找有關源連接的資訊。 |
| `description` | 可以包括的可選值，用於提供有關源連接的詳細資訊。 |
| `baseConnectionId` | 基本連接ID [!DNL Pinterest Ads]。 此ID是在前一步驟中生成的。 |
| `connectionSpec.id` | 與源對應的連接規範ID。 |
| `data.format` | 格式 [!DNL Pinterest Ads] 要攝取的資料。 目前，唯一支援的資料格式是 `json`。 |
| `params.ad_account_id` | 此 [!DNL Pinterest] `Ad account ID`. |
| `params.object_type` | 作為 [!DNL Pinterest] 需要Ad Groups Analytics API終結點，該值將為 `ad_groups`。 |
| `params.object_ids` | 以逗號分隔的清單 [!DNL Pinterest] 廣告組ID |

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
| `name` | 源連接的名稱。 確保源連接的名稱是描述性的，因為您可以使用它來查找有關源連接的資訊。 |
| `description` | 可以包括的可選值，用於提供有關源連接的詳細資訊。 |
| `baseConnectionId` | 基本連接ID [!DNL Pinterest Ads]。 此ID是在前一步驟中生成的。 |
| `connectionSpec.id` | 與源對應的連接規範ID。 |
| `data.format` | 格式 [!DNL Pinterest Ads] 要攝取的資料。 目前，唯一支援的資料格式是 `json`。 |
| `params.ad_account_id` | 此 [!DNL Pinterest] `Ad account ID`. |
| `params.object_type` | 作為 [!DNL Pinterest] 需要Ad Analytics API終結點，該值應為 `ads`。 |
| `params.object_ids` | 以逗號分隔的清單 [!DNL Pinterest] 廣告ID。 |

>[!ENDTABS]

**回應**

成功的響應返回唯一標識符(`id`)。 在後續步驟中建立資料流時需要此ID。

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

### 建立目標XDM架構 {#target-schema}

為了在平台中使用源資料，必須建立目標架構以根據您的需要來構造源資料。 然後使用目標模式建立包含源資料的平台資料集。

通過執行對目標XDM的POST請求，可以建立目標XDM模式 [架構註冊表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)。

有關如何建立目標XDM架構的詳細步驟，請參見上的教程 [使用API建立架構](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html?lang=en#create)。

### 建立目標資料集 {#target-dataset}

通過對目標資料集執行POST請求，可以建立目標資料集 [目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，提供負載內目標架構的ID。

有關如何建立目標資料集的詳細步驟，請參見上的教程 [使用API建立資料集](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html?lang=en)。

### 建立目標連接 {#target-connection}

目標連接表示到要儲存所攝取資料的目的地的連接。 要建立目標連接，必須提供與資料湖相對應的固定連接規範ID。 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

您現在將唯一標識符作為目標模式、目標資料集和到資料湖的連接規範ID。 使用這些標識符，可以使用 [!DNL Flow Service] API，用於指定將包含入站源資料的資料集。

**API格式**

```https
POST /targetConnections
```

**要求**

以下請求為 [!DNL Pinterest Ads]:

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
| `name` | 目標連接的名稱。 確保目標連接的名稱是描述性的，因為您可以使用此名稱查找有關目標連接的資訊。 |
| `description` | 可以包括的可選值，用於提供有關目標連接的詳細資訊。 |
| `connectionSpec.id` | 與 [!DNL Data Lake]。 此固定ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |
| `data.format` | 格式 [!DNL Pinterest Ads] 要帶到平台的資料。 |
| `params.dataSetId` | 在上一步中檢索到的目標資料集ID。 |

**回應**

成功的響應返回新目標連接的唯一標識符(`id`)。 後續步驟中需要此ID。

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

### 建立映射 {#mapping}

為了將源資料攝取到目標資料集中，必須首先將其映射到目標資料集所遵循的目標模式。 這通過執行POST請求來實現 [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) 在請求負載中定義資料映射。

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
| `outputSchema.schemaRef.id` | 的ID [目標XDM架構](#target-schema) 生成。 |
| `mappings.sourceType` | 正在映射的源屬性類型。 |
| `mappings.source` | 需要映射到目標XDM路徑的源屬性。 |
| `mappings.destination` | 要映射源屬性的目標XDM路徑。 |

**回應**

成功的響應返回新建立的映射的詳細資訊，包括其唯一標識符(`id`)。 在後續步驟中建立資料流時需要此值。

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

### 建立流 {#flow}

向從 [!DNL Pinterest Ads] 平台是建立資料流。 現在，您準備了以下必需值：

* [源連接ID](#source-connection)
* [目標連接ID](#target-connection)
* [對應 ID](#mapping)

資料流負責從源調度和收集資料。 通過在負載中提供先前提到的值的同時執行POST請求，可以建立資料流。

要計畫攝取，必須首先將開始時間值設定為劃時代（秒）。 然後，必須將頻率值設定為以下五個選項之一： `once`。 `minute`。 `hour`。 `day`或 `week`。 該間隔值指定兩個連續接收之間的期間，但建立一次性接收不需要設定間隔。 對於所有其它頻率，間隔值必須設定為等於或大於 `15`。

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
| `name` | 資料流的名稱。 確保資料流的名稱是描述性的，因為您可以使用此名稱查找有關資料流的資訊。 |
| `description` | 可以包括的可選值，用於提供有關資料流的詳細資訊。 |
| `flowSpec.id` | 建立資料流所需的流規範ID。 此固定ID為： `6499120c-0b15-42dc-936e-847ea3c24d72`。 |
| `flowSpec.version` | 流規範ID的相應版本。 此值預設為 `1.0`。 |
| `sourceConnectionIds` | 的 [源連接ID](#source-connection) 生成。 |
| `targetConnectionIds` | 的 [目標連接ID](#target-connection) 生成。 |
| `transformations` | 此屬性包含需要應用於資料的各種轉換。 將不符合XDM的資料帶入平台時需要此屬性。 |
| `transformations.name` | 分配給轉換的名稱。 |
| `transformations.params.mappingId` | 的 [映射ID](#mapping) 生成。 |
| `transformations.params.mappingVersion` | 映射ID的相應版本。 此值預設為 `0`。 |
| `scheduleParams.startTime` | 此屬性包含有關資料流的接收調度的資訊。 |
| `scheduleParams.frequency` | 資料流收集資料的頻率。 可接受值包括： `once`。 `minute`。 `hour`。 `day`或 `week`。 |
| `scheduleParams.interval` | 該間隔指定兩個連續流運行之間的期間。 間隔的值應為非零整數。 頻率設定為時不需要間隔 `once` 應大於或等於 `15` 其他頻率值。 |

**回應**

成功的響應返回ID(`id`)。 您可以使用此ID監視、更新或刪除資料流。

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

## 附錄 {#appendix}

以下部分提供了有關可以監視、更新和刪除資料流的步驟的資訊。

### 監視資料流 {#monitor-dataflow}

建立資料流後，您可以監視正在通過其接收的資料，以查看有關流運行、完成狀態和錯誤的資訊。 有關完整的API示例，請閱讀上的指南 [使用API監視源資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html)。

### 更新資料流 {#update-dataflow}

通過向發出PATCH請求來更新資料流的詳細資訊，如其名稱和說明，以及其運行計畫和關聯映射集 `/flows` 端點 [!DNL Flow Service] API，同時提供資料流的ID。 發出PATCH請求時，必須提供資料流的唯一性 `etag` 的 `If-Match` 標題。 有關完整的API示例，請閱讀上的指南 [使用API更新源資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### 更新帳戶 {#update-account}

通過執行對的PATCH請求，更新源帳戶的名稱、說明和憑據 [!DNL Flow Service] API，同時將基本連接ID作為查詢參數提供。 發出PATCH請求時，必須提供源帳戶的唯一 `etag` 的 `If-Match` 標題。 有關完整的API示例，請閱讀上的指南 [使用API更新源帳戶](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html)。

### 刪除資料流 {#delete-dataflow}

通過執行DELETE請求刪除資料流 [!DNL Flow Service] API，同時提供要作為查詢參數一部分刪除的資料流的ID。 有關完整的API示例，請閱讀上的指南 [使用API刪除資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html)。

### 刪除帳戶 {#delete-account}

通過執行DELETE請求刪除帳戶 [!DNL Flow Service] API，同時提供要刪除的帳戶的基本連接ID。 有關完整的API示例，請閱讀上的指南 [使用API刪除源帳戶](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html)。
