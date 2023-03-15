---
keywords: Experience Platform；首頁；熱門主題；來源；連接器；來源連接器；來源sdk;sdk; SDK
title: （測試版）使用流服務API為Mixpanel建立源連接和資料流
description: 了解如何使用流量服務API將Adobe Experience Platform連線至Mixpanel。
exl-id: 804b876d-6fd5-4a28-b33c-4ecab1ba3333
source-git-commit: 23a6f8ee23fb67290a5bcba2673a87ce74c9e1d3
workflow-type: tm+mt
source-wordcount: '2050'
ht-degree: 1%

---

# （測試版）建立源連接和資料流 [!DNL Mixpanel] 使用 [!DNL Flow Service] API

>[!NOTE]
>
>此 [!DNL Mixpanel] 來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用測試版標籤來源的詳細資訊。

以下教程將逐步引導您完成建立源連接和資料流的步驟 [!DNL Mixpanel] 使用將資料傳送至Adobe Experience Platform [流量服務API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要妥善了解下列Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要了解的其他資訊，以便成功連接到 [!DNL Mixpanel] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了連接 [!DNL Mixpanel] 若要使用Platform，您必須提供下列連線屬性的值：

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| `username` | 與您的 [!DNL Mixpanel] 帳戶。 請參閱 [[!DNL Mixpanel] 服務帳戶檔案](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account) 以取得更多資訊。 | `Test8.6d4ee7.mp-service-account` |
| `password` | 與您的 [!DNL Mixpanel] 帳戶。 | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| `projectId` | 您的 [!DNL Mixpanel] 專案ID。 建立源連接時需要此ID。 請參閱 [[!DNL Mixpanel] 專案設定檔案](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) 和 [[!DNL Mixpanel] 建立和管理項目的指南](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects) 以取得更多資訊。 | `2384945` |
| `timezone` | 與 [!DNL Mixpanel] 專案。 建立源連接需要時區。 請參閱 [Mixpanel專案設定檔案](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) 以取得更多資訊。 | `Pacific Standard Time` |

如需驗證 [!DNL Mixpanel] 來源，請參閱 [[!DNL Mixpanel] 來源概觀](../../../../connectors/analytics/mixpanel.md).

## 建立基本連接 {#base-connection}

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請向 `/connections` 端點提供 [!DNL Mixpanel] 請求內文的驗證憑證。

**API格式**

```https
POST /connections
```

**要求**

下列請求會為 [!DNL Mixpanel]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Mixpanel base connection",
      "description": "Mixpanel base connection to authenticate to Platform",
      "connectionSpec": {
          "id": "fd2c8ff3-1de0-4f6b-8fa8-4264784870eb",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 基本連接的名稱。 請確定基本連線的名稱是描述性的，因為您可以使用此名稱來查詢基本連線的資訊。 |
| `description` | 可包含的選用值，可提供基礎連線的詳細資訊。 |
| `connectionSpec.id` | 源的連接規範ID。 此ID可在您的來源註冊並透過 [!DNL Flow Service] API。 |
| `auth.specName` | 用於向平台驗證源的驗證類型。 |
| `auth.params.` | 包含驗證源所需的憑據。 |
| `auth.params.username` | 與您的 [!DNL Mixpanel] 帳戶。 |
| `auth.params.password` | 與您的 [!DNL Mixpanel] 帳戶。 |

**回應**

成功的響應返回新建的基本連接，包括其唯一連接標識符(`id`)。 在下一步中，瀏覽源的檔案結構和內容時需要此ID。

```json
{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
}
```

## 探索源 {#explore}

使用在上一步中生成的基本連接ID，可以通過執行GET請求來瀏覽檔案和目錄。
使用下列呼叫來尋找您要帶入Experience Platform的檔案路徑：

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

執行GET請求以探索源的檔案結構和內容時，必須包括下表中列出的查詢參數：


| 參數 | 說明 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 上一步驟中產生的基本連線ID。 |
| `objectType=rest` | 要瀏覽的對象類型。 目前，此值一律設為 `rest`. |
| `{OBJECT}` | 只有在查看特定目錄時，才需要此參數。 其值表示要瀏覽的目錄的路徑。 對於此來源，值會是 `json`. |
| `fileType=json` | 要帶入Platform的檔案的檔案類型。 目前， `json` 是唯一支援的檔案類型。 |
| `{PREVIEW}` | 一個布林值，定義連接的內容是否支援預覽。 |
| `{SOURCE_PARAMS}` | 定義要帶入Platform的源檔案的參數。 要檢索接受的格式類型，請執行以下操作 `{SOURCE_PARAMS}`，您必須將整個 `{"projectId":"2671127","timezone":"Pacific Standard Time"}` base64中的字串。 **附註**:在以下範例中， `"{"projectId":"2671127","timezone":"Pacific Standard Time"}"` 在base64等於 `eyJwcm9qZWN0SWQiOiIyNjcxMTI3IiwidGltZXpvbmUiOiJQYWNpZmljIFN0YW5kYXJkIFRpbWUifQ==`. |


**要求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/70383d02-2777-4be7-a309-9dd6eea1b46d/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回查詢的檔案結構。

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "event": {
                "type": "string"
            },
            "properties": {
                "type": "object",
                "properties": {
                    "$mp_api_endpoint": {
                        "type": "string"
                    },
                    "$insert_id": {
                        "type": "string"
                    },
                    "item_id": {
                        "type": "string"
                    },
                    "distinct_id": {
                        "type": "string"
                    },
                    "$mp_api_timestamp_ms": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "item_price": {
                        "type": "string"
                    },
                    "$import": {
                        "type": "boolean"
                    },
                    "item_name": {
                        "type": "string"
                    },
                    "time": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "mp_processing_time_ms": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    }
                }
            }
        }
    },
    "data": [
        {
            "event": "Items purchased",
            "properties": {
                "time": 1652825148,
                "distinct_id": "test@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b70",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1652850348643,
                "item_id": "29066",
                "item_name": "charger",
                "item_price": "800.00",
                "mp_processing_time_ms": 1652850348702
            }
        },
        {
            "event": "Items sold",
            "properties": {
                "time": 1652423938,
                "distinct_id": "test@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b70",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1652449138115,
                "item_id": "29036",
                "item_name": "chair",
                "item_price": "5000.00",
                "mp_processing_time_ms": 1652449138173
            }
        },
        {
            "event": "Items sold",
            "properties": {
                "time": 1652854256,
                "distinct_id": "test@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b70",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1652879456538,
                "item_id": "29066",
                "item_name": "mobile",
                "item_price": "7000.00",
                "mp_processing_time_ms": 1652879456604
            }
        },
        {
            "event": "Sign off",
            "properties": {
                "time": 1648140611,
                "distinct_id": "test@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b75",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1648555709515,
                "item_id": "29073",
                "item_name": "Watch",
                "item_price": "50000.00",
                "mp_processing_time_ms": 1648555710375
            }
        },
        {
            "event": "Items sold",
            "properties": {
                "time": 1648140612,
                "distinct_id": "test@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b75",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1648556481708,
                "item_id": "29073",
                "item_name": "Pen",
                "item_price": "1000.00",
                "mp_processing_time_ms": 1648556481880
            }
        },
        {
            "event": "Sign in",
            "properties": {
                "time": 1648140614,
                "distinct_id": "test1@test.com",
                "$import": true,
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b75",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1648556032401,
                "item_id": "29073",
                "item_name": "Watch",
                "item_price": "50000.00",
                "mp_processing_time_ms": 1648556032462
            }
        },
        {
            "event": "Item Purchased",
            "properties": {
                "time": 1648165814,
                "distinct_id": "test1@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b74",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1648480684785,
                "item_id": "29073",
                "item_name": "Watch",
                "item_price": "50000.00",
                "mp_processing_time_ms": 1648480685058
            }
        },
        {
            "event": "Item Purchased",
            "properties": {
                "time": 1648165814,
                "distinct_id": "test1@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b75",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1648551687866,
                "item_id": "29073",
                "item_name": "Watch",
                "item_price": "50000.00",
                "mp_processing_time_ms": 1648551687922
            }
        },
        {
            "event": "Sign off",
            "properties": {
                "time": 1648530419,
                "distinct_id": "test1@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b75",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1648555619274,
                "item_id": "29073",
                "item_name": "Watch",
                "item_price": "50000.00",
                "mp_processing_time_ms": 1648555619326
            }
        },
        {
            "event": "Items sold",
            "properties": {
                "time": 1648566534,
                "distinct_id": "test1@test.com",
                "$import": true,
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b75",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1648635830114,
                "item_id": "29073",
                "item_name": "Pen",
                "item_price": "1000.00",
                "mp_processing_time_ms": 1648635831010
            }
        }
    ]
}
```

## 建立源連接 {#source-connection}

您可以透過向 [!DNL Flow Service] API。 源連接由連接ID、源資料檔案的路徑和連接規範ID組成。

**API格式**

```https
POST /sourceConnections
```

**要求**

以下請求將建立源連接 [!DNL Mixpanel]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Mixpanel source connection",
      "description": "Mixpanel source connection",
      "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
      "connectionSpec": {
          "id": "fd2c8ff3-1de0-4f6b-8fa8-4264784870eb",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "projectId": "{PROJECT_ID}",
          "timezone": "{TIMEZONE}"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 源連接的名稱。 請確保源連接的名稱是描述性的，因為您可以使用此名稱查找有關源連接的資訊。 |
| `description` | 可包含的選用值，用於提供來源連線的詳細資訊。 |
| `baseConnectionId` | 基本連接ID為 [!DNL Mixpanel]. 此ID是在先前的步驟中產生。 |
| `connectionSpec.id` | 與源對應的連接規範ID。 |
| `data.format` | 格式 [!DNL Mixpanel] 您要擷取的資料。 目前，唯一支援的資料格式是 `json`. |
| `params.projectId` | 您的 [!DNL Mixpanel] 專案ID。 |
| `params.timezone` | 您的 [!DNL Mixpanel] 專案。 |

**回應**

成功的回應會傳回唯一識別碼(`id`)。 在後續步驟中需要此ID才能建立資料流。

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

## 建立目標XDM結構 {#target-schema}

為了在Platform中使用來源資料，必須建立目標架構，以根據您的需求來建構來源資料。 然後，目標架構會用來建立包含來源資料的Platform資料集。

您可以透過執行POST要求來建立目標XDM結構 [結構註冊表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

如需建立Target XDM結構的詳細步驟，請參閱 [使用API建立結構](../../../../../xdm/api/schemas.md).

## 建立目標資料集 {#target-dataset}

目標資料集的建立方式，是透過對 [目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，提供裝載中目標架構的ID。

如需如何建立目標資料集的詳細步驟，請參閱 [使用API建立資料集](../../../../../catalog/api/create-dataset.md).

## 建立目標連線 {#target-connection}

目標連線代表要儲存所擷取資料的目的地連線。 要建立目標連接，必須提供與資料庫對應的固定連接規範ID。 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

您現在擁有目標架構、目標資料集以及資料湖的連線規格ID的唯一識別碼。 使用這些識別碼，您可以使用 [!DNL Flow Service] API，指定包含傳入來源資料的資料集。

**API格式**

```https
POST /targetConnections
```

**要求**

下列請求會為 [!DNL Mixpanel]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{Mixpanel} Target Connection",
        "description": "{Mixpanel} Target Connection",
        "connectionSpec": {
            "id": "fd2c8ff3-1de0-4f6b-8fa8-4264784870eb",
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
| `name` | 目標連接的名稱。 請確定目標連線的名稱是描述性的，因為您可以使用此名稱來查詢目標連線的資訊。 |
| `description` | 可包含的選用值，用於提供目標連線的詳細資訊。 |
| `connectionSpec.id` | 與資料湖對應的連接規範ID。 此固定ID為： `fd2c8ff3-1de0-4f6b-8fa8-4264784870eb`. |
| `data.format` | 格式 [!DNL Mixpanel] 要帶入Platform的資料。 |
| `params.dataSetId` | 上一步驟中擷取的目標資料集ID。 |


**回應**

成功的回應會傳回新目標連線的唯一識別碼(`id`)。 後續步驟需要此ID。

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

## 建立對應 {#mapping}

若要將來源資料內嵌至目標資料集，必須先將其對應至目標資料集所遵守的目標架構。 這是透過執行POST要求來達成 [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) 在要求裝載中定義的資料對應。

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
              "source": "data.distinct_id",
              "destination": "_extconndev.distinct_id",
              "name": "distinct_id",
              "description": "Mixpanel"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.event_name",
              "destination": "_extconndev.event_name"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.import",
              "destination": "_extconndev.import"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.insert_id",
              "destination": "_extconndev.insert_id"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.item_id",
              "destination": "_extconndev.item_id"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.item_name",
              "destination": "_extconndev.item_name"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.item_price",
              "destination": "_extconndev.item_price"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.mp_api_endpoint",
              "destination": "_extconndev.mp_api_endpoint"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.mp_api_timestamp_ms",
              "destination": "_extconndev.mp_api_timestamp_ms"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.mp_processing_time_ms",
              "destination": "_extconndev.mp_processing_time_ms"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.time",
              "destination": "_extconndev.time"
          }
      ]
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `xdmSchema` | 的ID [target XDM結構](#target-schema) 在先前的步驟中產生。 |
| `mappings.destinationXdmPath` | 要映射源屬性的目標XDM路徑。 |
| `mappings.sourceAttribute` | 需要對應至目標XDM路徑的來源屬性。 |
| `mappings.identity` | 一個布林值，用於指定是否要為標籤映射集 [!DNL Identity Service]. |

**回應**

成功的回應會傳回新建立之對應的詳細資訊，包括其唯一識別碼(`id`)。 在以後的步驟中需要此值才能建立資料流。

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 建立流程 {#flow}

將資料從 [!DNL Mixpanel] 到平台是建立資料流。 您現在已準備下列必要值：

* [源連接ID](#source-connection)
* [Target連線ID](#target-connection)
* [對應ID](#mapping)

資料流負責從源中調度和收集資料。 您可以在裝載中提供先前提及的值時，執行POST要求來建立資料流。

若要排程擷取，您必須先將開始時間值設為紀元時間（以秒為單位）。 然後，您必須將頻率值設定為以下五個選項之一： `once`, `minute`, `hour`, `day`，或 `week`. 間隔值會指定兩個連續擷取之間的期間，但建立一次性擷取不需要設定間隔。 對於所有其他頻率，間隔值必須設定為等於或大於 `15`.


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
      "name": "{Mixpanel} dataflow",
      "description": "{Mixpanel} dataflow",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "246d052c-da4a-494a-937f-a0d17b1c6cf5"
      ],
      "targetConnectionIds": [
          "7c96c827-3ffd-460c-a573-e9558f72f263"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
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
| `name` | 資料流的名稱。 請確保資料流的名稱具有描述性，因為您可以使用此名稱查找資料流的資訊。 |
| `description` | 一個可選值，可以包括該值以提供有關資料流的詳細資訊。 |
| `flowSpec.id` | 建立資料流所需的流規範ID。 此固定ID為： `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | 流規範ID的相應版本。 此值預設為 `1.0`. |
| `sourceConnectionIds` | 此 [源連接ID](#source-connection) 在先前的步驟中產生。 |
| `targetConnectionIds` | 此 [目標連線ID](#target-connection) 在先前的步驟中產生。 |
| `transformations` | 此屬性包含需要套用至資料的各種轉換。 將不符合XDM的資料帶入Platform時，此屬性為必要屬性。 |
| `transformations.name` | 指派給轉換的名稱。 |
| `transformations.params.mappingId` | 此 [對應ID](#mapping) 在先前的步驟中產生。 |
| `transformations.params.mappingVersion` | 對應ID的對應版本。 此值預設為 `0`. |
| `scheduleParams.startTime` | 此屬性包含有關資料流獲取調度的資訊。 |
| `scheduleParams.frequency` | 資料流收集資料的頻率。 可接受的值包括： `once`, `minute`, `hour`, `day`，或 `week`. |
| `scheduleParams.interval` | 該間隔指定兩個連續流運行之間的週期。 間隔的值應為非零整數。 頻率設為時不需要間隔 `once` 且應大於或等於 `15` 的其他頻率值。 |

**回應**

成功的回應會傳回ID(`id`)。 您可以使用此ID監視、更新或刪除資料流。

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

## 附錄

以下部分提供了可以監視、更新和刪除資料流的步驟資訊。

### 監視資料流

建立資料流後，您可以監視正在通過資料流進行內嵌的資料，以查看有關流運行、完成狀態和錯誤的資訊。 如需完整的API範例，請參閱 [使用API監控來源資料流](../../monitor.md).

### 更新資料流

通過向發出PATCH請求，更新資料流的詳細資訊（如其名稱和說明），以及其運行計畫和關聯的映射集 `/flows` 端點 [!DNL Flow Service] API，同時提供資料流的ID。 發出PATCH請求時，必須提供資料流的唯一 `etag` 在 `If-Match` 頁首。 如需完整的API範例，請參閱 [使用API更新源資料流](../../update-dataflows.md).

### 更新您的帳戶

通過向執行PATCH請求，更新源帳戶的名稱、說明和憑據 [!DNL Flow Service] API，同時將基本連線ID設為查詢參數。 提出PATCH請求時，您必須提供來源帳戶的唯一 `etag` 在 `If-Match` 頁首。 如需完整的API範例，請參閱 [使用API更新您的來源帳戶](../../update.md).

### 刪除資料流

通過執行DELETE請求以刪除資料流 [!DNL Flow Service] API，同時提供您要在查詢參數中刪除之資料流的ID。 如需完整的API範例，請參閱 [使用API刪除資料流](../../delete-dataflows.md).

### 刪除您的帳戶

對執行DELETE請求以刪除帳戶 [!DNL Flow Service] API，同時提供您要刪除之帳戶的基本連線ID。 如需完整的API範例，請參閱 [使用API刪除您的來源帳戶](../../delete.md).