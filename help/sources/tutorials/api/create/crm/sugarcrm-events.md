---
title: 使用流服務API為SugarCRM事件建立源連接和資料流
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到SugarCRM事件。
exl-id: 12d08010-569c-4111-ba95-697c6ce6f637
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '2009'
ht-degree: 1%

---

# (Beta)建立源連接和資料流 [!DNL SugarCRM Events] 使用流服務API

>[!NOTE]
>
>的 [!DNL SugarCRM Events] 源為beta。 查看 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

以下教程將指導您完成建立 [!DNL SugarCRM Events] 源連接並建立資料流，以便 [[!DNL SugarCRM]](https://www.sugarcrm.com/) 事件資料到Adobe Experience Platform [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對以下Experience Platform元件進行工作理解：

* [源](../../../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了要成功連接到所需的其他資訊 [!DNL SugarCRM] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了連接 [!DNL SugarCRM Events] 到平台，必須提供以下連接屬性的值：

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| `host` | 源連接到的SugarCRM API終結點。 | `developer.salesfusion.com` |
| `username` | 您的SugarCRM開發人員帳戶用戶名。 | `abc.def@example.com@sugarmarketdemo000.com` |
| `password` | 您的SugarCRM開發人員帳戶密碼。 | `123456789` |

## 連接 [!DNL SugarCRM Events] 到使用 [!DNL Flow Service] API

下面概述了驗證您的 [!DNL SugarCRM] 源，建立源連接，並建立資料流以將事件資料Experience Platform。

### 建立基本連接 {#base-connection}

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL SugarCRM Events] 身份驗證憑據作為請求正文的一部分。

**API格式**

```https
POST /connections
```

**要求**

以下請求為 [!DNL SugarCRM Events]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Events base connection",
      "description": "Create a live inbound connection to your SugarCRM Events instance, to ingest both historic and scheduled data into Experience Platform",
      "connectionSpec": {
          "id": "59a4b493-a615-40f9-bd38-f823d0909a2b",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Refresh Code",
          "params": {
              "host": "developer.salesfusion.com",
              "username": "{SUGARCRM_DEVELOPER_ACCOUNT_USERNAME}",
              "password": "{SUGARCRM_DEVELOPER_ACCOUNT_PASSWORD}"
          }
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 基本連接的名稱。 確保基本連接的名稱是描述性的，因為您可以使用此名稱查找有關基本連接的資訊。 |
| `description` | 可以包括的可選值，用於提供有關基本連接的詳細資訊。 |
| `connectionSpec.id` | 源的連接規範ID。 在通過註冊和批准源後，可以檢索此ID [!DNL Flow Service] API。 |
| `auth.specName` | 用於將源驗證到平台的驗證類型。 |
| `auth.params.host` | SugarCRM API主機： *開發者.salesfusion.com* |
| `auth.params.username` | 您的SugarCRM開發人員帳戶用戶名。 |
| `auth.params.password` | 您的SugarCRM開發人員帳戶密碼。 |

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
使用以下調用查找要插入的檔案的路徑 [!DNL Platform]:

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

執行GET請求以瀏覽源的檔案結構和內容時，必須包括下表中列出的查詢參數：

| 參數 | 說明 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 在上一步中生成的基本連接ID。 |
| `objectType=rest` | 要瀏覽的對象的類型。 當前，此值始終設定為 `rest`。 |
| `{OBJECT}` | 僅當查看特定目錄時才需要此參數。 其值表示要瀏覽的目錄的路徑。 對於此源，值將為 `json`。 |
| `fileType=json` | 要帶到平台的檔案的檔案類型。 目前， `json` 是唯一支援的檔案類型。 |
| `{PREVIEW}` | 一個布爾值，它定義連接的內容是否支援預覽。 |
| `{SOURCE_PARAMS}` | 定義要帶到平台的源檔案的參數。 檢索接受的格式類型 `{SOURCE_PARAMS}`，必須在base64中對整個字串進行編碼。 <br> [!DNL SugarCRM Events] 不需要任何負載。 的值 `{SOURCE_PARAMS}` 傳遞為 `{}`，編碼為base64，等於 `e30=` 如下所示。 |

**要求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=e30=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回查詢檔案的結構。 *一些記錄已被刪除，以便能夠更好地演示。*

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "next": {
                "type": "string"
            },
            "page_number": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "previous": {},
            "total_count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "results": {
                "type": "object",
                "properties": {
                    "sessions": {
                        "type": "string"
                    },
                    "description": {
                        "type": "string"
                    },
                    "created_by": {
                        "type": "string"
                    },
                    "event_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "name": {
                        "type": "string"
                    },
                    "updated_by": {
                        "type": "string"
                    },
                    "updated_by_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "updated_date": {
                        "type": "string"
                    },
                    "created_date": {
                        "type": "string"
                    },
                    "created_by_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "event": {
                        "type": "string"
                    },
                    "folder_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "status": {
                        "type": "string"
                    }
                }
            },
            "page_size": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            }
        }
    },
    "data": [
        {
            "next": "https://developer.salesfusion.com/api/2.0/events/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 532,
            "count": 532,
            "results": {
                "event_id": 1,
                "event": "https://developer.salesfusion.com/api/2.0/events/1/",
                "sessions": "https://developer.salesfusion.com/api/2.0/events/1/sessions/",
                "name": "Test",
                "updated_date": "2022-08-30T11:20:11.813Z",
                "updated_by_id": 59,
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "created_date": "2022-08-28T23:40:11Z",
                "created_by_id": 59,
                "created_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "status": "Draft",
                "folder_id": 2
            },
            "page_size": 100
        },
        {
            "next": "https://developer.salesfusion.com/api/2.0/events/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 532,
            "count": 532,
            "results": {
                "event_id": 2,
                "event": "https://developer.salesfusion.com/api/2.0/events/2/",
                "sessions": "https://developer.salesfusion.com/api/2.0/events/2/sessions/",
                "name": "Infy Event",
                "description": "Test Event",
                "updated_date": "2022-09-15T16:26:43.697Z",
                "updated_by_id": 59,
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "created_date": "2022-09-27T23:40:11Z",
                "created_by_id": 59,
                "created_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "status": "Active",
                "folder_id": 2
            },
            "page_size": 100
        },
        {
            "next": "https://developer.salesfusion.com/api/2.0/events/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 532,
            "count": 532,
            "results": {
                "event_id": 3,
                "event": "https://developer.salesfusion.com/api/2.0/events/3/",
                "sessions": "https://developer.salesfusion.com/api/2.0/events/3/sessions/",
                "name": "Infy Workshop 1",
                "updated_date": "2022-10-11T18:12:28.767Z",
                "updated_by_id": 59,
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "created_date": "2022-09-14T23:40:11Z",
                "created_by_id": 59,
                "created_by": "https://developer.salesfusion.com/api/2.0/users/59/",
                "status": "Active",
                "folder_id": 2
            },
            "page_size": 100
        }
    ]
}
```

### 建立源連接 {#source-connection}

您可以通過向POST請求建立源連接 [!DNL Flow Service] API。 源連接由連接ID、源資料檔案的路徑和連接規範ID組成。

**API格式**

```https
POST /sourceConnections
```

**要求**

以下請求為 [!DNL SugarCRM Events]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Source Connection",
      "description": "SugarCRM Source Connection",
      "baseConnectionId": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 源連接的名稱。 確保源連接的名稱是描述性的，因為您可以使用它來查找有關源連接的資訊。 |
| `description` | 可以包括的可選值，用於提供有關源連接的詳細資訊。 |
| `baseConnectionId` | 基本連接ID [!DNL SugarCRM Events]。 此ID是在前一步驟中生成的。 |
| `connectionSpec.id` | 與源對應的連接規範ID。 |
| `data.format` | 格式 [!DNL SugarCRM Events] 要攝取的資料。 目前，唯一支援的資料格式是 `json`。 |

**回應**

成功的響應返回唯一標識符(`id`)。 在後續步驟中建立資料流時需要此ID。

```json
{
    "id": "ffac1ae1-c137-4133-9f8d-0279468c11c9",
    "etag": "\"ed05abc3-0000-0200-0000-6368b3280000\""
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

以下請求為 [!DNL SugarCRM Events]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Target Connection Generic Rest",
      "description": "SugarCRM Target Connection Generic Rest",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/b156e6f818f923e048199173c45e55e20fd2487f5eb03d22",
              "version": "1.22"
          }
      },
      "params": {
          "dataSetId": "6365389d1d37d01c077a81da"
      }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 目標連接的名稱。 確保目標連接的名稱是描述性的，因為您可以使用此名稱查找有關目標連接的資訊。 |
| `description` | 可以包括的可選值，用於提供有關目標連接的詳細資訊。 |
| `connectionSpec.id` | 與資料湖對應的連接規範ID。 此固定ID為： `6b137bf6-d2a0-48c8-914b-d50f4942eb85`。 |
| `data.format` | 格式 [!DNL SugarCRM Events] 要攝取的資料。 |
| `params.dataSetId` | 在上一步中檢索到的目標資料集ID。 |

**回應**

成功的響應返回新目標連接的唯一標識符(`id`)。 後續步驟中需要此ID。

```json
{
    "id": "dfe9113e-be98-4d63-80a9-f41761721049",
    "etag": "\"84050267-0000-0200-0000-6368b3640000\""
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
      "outputSchema": {
          "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/b156e6f818f923e048199173c45e55e20fd2487f5eb03d22",
              "contentType": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "mappings": [
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.created_by",
          "destination": "_extconndev.created_by"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.created_by_id",
          "destination": "_extconndev.created_by_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.created_date",
          "destination": "_extconndev.created_date"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.name",
          "destination": "_extconndev.name_event"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.event_id",
          "destination": "_extconndev.id_event"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.event_id",
          "destination": "_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.sessions",
          "destination": "_extconndev.sessions"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.updated_by",
          "destination": "_extconndev.updated_by"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.updated_by_id",
          "destination": "_extconndev.updated_by_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.updated_date",
          "destination": "_extconndev.updated_date"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.updated_date",
          "destination": "timestamp"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.event",
          "destination": "_extconndev.event"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.description",
          "destination": "_extconndev.description"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.folder_id",
          "destination": "_extconndev.folder_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.status",
          "destination": "_extconndev.status"
      }
      ]
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
    "id": "d3845beaceeb49669228973f5f937f89",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### 建立流 {#flow}

向從 [!DNL SugarCRM Events] 平台是建立資料流。 現在，您準備了以下必需值：

* [源連接ID](#source-connection)
* [目標連接ID](#target-connection)
* [對應 ID](#mapping)

資料流負責從源調度和收集資料。 通過在負載中提供先前提到的值的同時執行POST請求，可以建立資料流。

要計畫攝取，必須首先將開始時間值設定為劃時代（秒）。 然後，必須將頻率值設定為 `hour` 或 `day`。 間隔值指定兩個連續接收之間的期間。 間隔值應設定為 `1` 或 `24` 取決於 `scheduleParams.frequency` 選擇 `hour` 或 `day`。

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
      "name": "SugarCRM Connector Description Flow Generic Rest",
      "description": "SugarCRM Connector Description Flow Generic Rest",
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
                  "mappingId": "d3845beaceeb49669228973f5f937f89",
                  "mappingVersion": "0"
              }
          }
      ],
      "scheduleParams": {
          "startTime": "1625040887",
          "frequency": "hour",
          "interval": 1
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
| `scheduleParams.frequency` | 資料流收集資料的頻率。 可接受值包括： `hour` 或 `day`。 |
| `scheduleParams.interval` | 該間隔指定兩個連續流運行之間的期間。 間隔的值應為非零整數。 間隔值應設定為 `1` 或 `24` 取決於 `scheduleParams.frequency` 選擇 `hour` 或 `day`。 |

**回應**

成功的響應返回ID(`id`)。 您可以使用此ID監視、更新或刪除資料流。

```json
{
     "id": "fcd16140-81b4-422a-8f9a-eaa92796c4f4",
     "etag": "\"9200a171-0000-0200-0000-6368c1da0000\""
}
```

## 附錄

以下部分提供了有關可以監視、更新和刪除資料流的步驟的資訊。

### 監視資料流

建立資料流後，您可以監視正在通過其接收的資料，以查看有關流運行、完成狀態和錯誤的資訊。 有關完整的API示例，請閱讀上的指南 [使用API監視源資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html)。

### 更新資料流

通過向發出PATCH請求來更新資料流的詳細資訊，如其名稱和說明，以及其運行計畫和關聯映射集 `/flows` 端點 [!DNL Flow Service] API，同時提供資料流的ID。 發出PATCH請求時，必須提供資料流的唯一性 `etag` 的 `If-Match` 標題。 有關完整的API示例，請閱讀上的指南 [使用API更新源資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### 更新帳戶

通過執行對的PATCH請求，更新源帳戶的名稱、說明和憑據 [!DNL Flow Service] API，同時將基本連接ID作為查詢參數提供。 發出PATCH請求時，必須提供源帳戶的唯一 `etag` 的 `If-Match` 標題。 有關完整的API示例，請閱讀上的指南 [使用API更新源帳戶](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html)。

### 刪除資料流

通過執行DELETE請求刪除資料流 [!DNL Flow Service] API，同時提供要作為查詢參數一部分刪除的資料流的ID。 有關完整的API示例，請閱讀上的指南 [使用API刪除資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html)。

### 刪除帳戶

通過執行DELETE請求刪除帳戶 [!DNL Flow Service] API，同時提供要刪除的帳戶的基本連接ID。 有關完整的API示例，請閱讀上的指南 [使用API刪除源帳戶](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html)。
