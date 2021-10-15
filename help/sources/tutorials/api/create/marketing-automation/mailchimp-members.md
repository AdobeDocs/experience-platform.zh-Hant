---
keywords: Experience Platform;home;popular topics;sources;connectors;source connectors;sources sdk;sdk;SDK
solution: Experience Platform
title: 使用流服務API為MailChimp成員建立資料流
topic-legacy: tutorial
description: 了解如何使用Flow Service API將Adobe Experience Platform連線至MailChimp成員。
source-git-commit: c8d94af6185785a0e4bfce9889c04405ed223b1f
workflow-type: tm+mt
source-wordcount: '2500'
ht-degree: 2%

---

# Create a dataflow for [!DNL MailChimp Members] using the Flow Service API

The following tutorial walks you through the steps to create a source connection and a dataflow to bring [!DNL MailChimp Members] data to Platform using the [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 先決條件

您必須先為[!DNL MailChimp.]擷取存取權杖，才能使用OAuth 2重新整理程式碼將[!DNL MailChimp]連線至Adobe Experience Platform。請參閱[[!DNL MailChimp] OAuth 2指南](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/)以取得尋找存取權杖的詳細指示。

## 建立基本連接 {#base-connection}

檢索到[!DNL MailChimp]身份驗證憑據後，您現在可以開始建立資料流以將[!DNL MailChimp Members]資料帶到Platform的過程。 建立資料流的第一步是建立基本連接。

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

[!DNL MailChimp] 支援基本驗證和OAuth 2重新整理程式碼。如需如何使用任一驗證類型進行驗證的指引，請參閱下列範例。

### 使用基本身份驗證建立[!DNL MailChimp]基本連接

要使用基本身份驗證建立[!DNL MailChimp]基本連接，請在提供`host`、`authorizationTestUrl`、`username`和`password`的憑據的同時向[!DNL Flow Service] API的`/connections`端點發出POST請求。

**API格式**

```https
POST /connections
```

**要求**

以下請求會為[!DNL MailChimp]建立基本連線：

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp base connection with basic authentication",
      "description": "MailChimp Members base connection with basic authentication",
      "connectionSpec": {
          "id": "2e8580db-6489-4726-96de-e33f5f60295f",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "authorizationTestUrl": "https://login.mailchimp.com/oauth2/metadata",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 基本連接的名稱。 請確定基本連線的名稱是描述性的，因為您可以使用此名稱來查詢基本連線的資訊。 |
| `description` | （選用）您可以包含的屬性，以提供有關基本連線的詳細資訊。 |
| `connectionSpec.id` | 源的連接規範ID。 透過[!DNL Flow Service] API註冊並核准您的來源後，即可擷取此ID。 |
| `auth.specName` | 用於將源連接到平台的驗證類型。 |
| `auth.params.host` | 用來連線至[!DNL MailChimp] API的根URL。 根URL的格式為`https://{DC}.api.mailchimp.com`，其中`{DC}`代表與您的帳戶對應的資料中心。 |
| `auth.params.authorizationTestUrl` | （可選）建立基本連線時，授權測試URL用於驗證憑證。 如果未提供，則在建立源連接步驟期間將自動檢查憑據。 |
| `auth.params.username` | 與您的[!DNL MailChimp]帳戶對應的使用者名稱。 This is required for basic authentication. |
| `auth.params.password` | 與您的[!DNL MailChimp]帳戶對應的密碼。 這是基本驗證的必要條件。 |

**回應**

成功的響應返回新建的基本連接，包括其唯一連接標識符(`id`)。 在下一步中，瀏覽源的檔案結構和內容時需要此ID。

```json
{
    "id": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
    "etag": "\"4000cff7-0000-0200-0000-6154bad60000\""
}
```

### 使用OAuth 2重新整理程式碼建立[!DNL MailChimp]基本連線

若要使用OAuth 2重新整理程式碼建立[!DNL MailChimp]基本連線，請在提供`host`、`authorizationTestUrl`和`accessToken`的認證時，向`/connections`端點提出POST要求。

**API format**

```https
POST /connections
```

**要求**

The following request creates a base connection for [!DNL MailChimp] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp base connection with OAuth 2 refresh code",
      "description": "MailChimp Members base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "2e8580db-6489-4726-96de-e33f5f60295f",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
              "host": "{HOST}",
              "authorizationTestUrl": "https://login.mailchimp.com/oauth2/metadata",
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 基本連接的名稱。 請確定基本連線的名稱是描述性的，因為您可以使用此名稱來查詢基本連線的資訊。 |
| `description` | （選用）您可以包含的屬性，以提供有關基本連線的詳細資訊。 |
| `connectionSpec.id` | 源的連接規範ID。 使用[!DNL Flow Service] API註冊您的源後，可以檢索此ID。 |
| `auth.specName` | 用於向平台驗證源的驗證類型。 |
| `auth.params.host` | 用來連線至[!DNL MailChimp] API的根URL。 根URL的格式為`https://{DC}.api.mailchimp.com`，其中`{DC}`代表與您的帳戶對應的資料中心。 |
| `auth.params.authorizationTestUrl` | （可選）建立基本連線時，授權測試URL用於驗證憑證。 如果未提供，則在建立源連接步驟期間將自動檢查憑據。 |
| `auth.params.accessToken` | 用於驗證源的相應訪問令牌。 這是OAuth型驗證的必要項目。 |

**回應**

成功的響應返回新建的基本連接，包括其唯一連接標識符(`id`)。 在下一步中，瀏覽源的檔案結構和內容時需要此ID。

```json
{
    "id": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
    "etag": "\"4000cff7-0000-0200-0000-6154bad60000\""
}
```

## 探索源 {#explore}

使用在上一步中生成的基本連接ID，可以通過執行GET請求來瀏覽檔案和目錄。

>[!TIP]
>
>若要擷取`{SOURCE_PARAMS}`接受的格式類型，您必須以base64對整個`list_id`字串進行編碼。 For example, `"list_id": "10c097ca71"` encoded in base64 equates to `eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=`.

**API format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

執行GET請求以探索源的檔案結構和內容時，必須包括下表中列出的查詢參數：

| 參數 | 說明 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 上一步驟中產生的基本連線ID。 |
| `{OBJECT_TYPE}` | 要瀏覽的對象的類型。 For REST sources, this value defaults to `rest`. |
| `{OBJECT}` | 您要探索的物件。 |
| `{FILE_TYPE}` | 只有在查看特定目錄時，才需要此參數。 其值表示要瀏覽的目錄的路徑。 |
| `{PREVIEW}` | 一個布林值，定義連接的內容是否支援預覽。 |
| `{SOURCE_PARAMS}` | `list_id`的base64編碼字串。 |

**要求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/05c595e5-edc3-45c8-90bb-fcf556b57c4b/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回查詢的檔案結構。

```json
{ 
"data": [
    {
        "list_id": "10c097ca71",
        "_links": [
            {
                "rel": "self",
                "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
                "method": "GET",
                "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/CollectionResponse.json",
                "schema": "https://us6.api.mailchimp.com/schema/3.0/Paths/Lists/Members/Collection.json"
            },
            {
                "rel": "parent",
                "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71",
                "method": "GET",
                "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
            },
            {
                "rel": "create",
                "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
                "method": "POST",
                "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json",
                "schema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/POST.json"
            }
        ],
        "members": [
            {
                "id": "cff65fb4c5f5828666ad846443720efd",
                "email_address": "kendallt2134@gmail.com",
                "unique_email_id": "72c758cbf1",
                "contact_id": "874a0d6e9ddb89d8b4a31e416ead2d6f",
                "full_name": "Kendall Roy",
                "web_id": 547094062,
                "email_type": "html",
                "status": "subscribed",
                "consents_to_one_to_one_messaging": true,
                "merge_fields": {
                    "FNAME": "Kendall",
                    "LNAME": "Roy",
                    "ADDRESS": {
                        "country": "US"
                    }
                },
                "stats": {
                    "avg_open_rate": 0,
                    "avg_click_rate": 0
                },
                "ip_opt": "103.43.112.97",
                "timestamp_opt": "2021-06-01T15:31:36+00:00",
                "member_rating": 2,
                "last_changed": "2021-06-01T15:31:36+00:00",
                "vip": false,
                "location": {
                    "latitude": 0,
                    "longitude": 0,
                    "gmtoff": 0,
                    "dstoff": 0
                },
                "source": "Admin Add",
                "tags_count": 0,
                "list_id": "10c097ca71",
                "_links": [
                        {
                            "rel": "self",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
                        },
                        {
                            "rel": "parent",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/CollectionResponse.json",
                            "schema": "https://us6.api.mailchimp.com/schema/3.0/Paths/Lists/Members/Collection.json"
                        },
                        {
                            "rel": "update",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "PATCH",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json",
                            "schema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/PATCH.json"
                        },
                        {
                            "rel": "upsert",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "PUT",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json",
                            "schema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/PUT.json"
                        },
                        {
                            "rel": "delete",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd",
                            "method": "DELETE"
                        },
                        {
                            "rel": "activity",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/activity",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Activity/Response.json"
                        },
                        {
                            "rel": "goals",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/goals",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Goals/Response.json"
                        },
                        {
                            "rel": "notes",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/notes",
                            "method": "GET",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Notes/CollectionResponse.json"
                        },
                        {
                            "rel": "events",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/events",
                            "method": "POST",
                            "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Events/POST.json"
                        },
                        {
                            "rel": "delete_permanent",
                            "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members/cff65fb4c5f5828666ad846443720efd/actions/delete-permanent",
                            "method": "POST"
                        }
                    ]
                }
            ]  
        }
    ]
}
```

## 建立源連接 {#source-connection}

您可以向[!DNL Flow Service] API發出POST請求，以建立來源連線。 源連接由連接ID、源資料檔案的路徑和連接規範ID組成。

要建立源連接，您還必須為資料格式屬性定義枚舉值。

為檔案型來源使用下列列舉值：

| 資料格式 | 列舉值 |
| ----------- | ---------- |
| 分隔 | `delimited` |
| JSON | `json` |
| 鑲木 | `parquet` |

對於所有基於表的源，將值設定為`tabular`。

**API格式**

```https
POST /sourceConnections
```

**要求**

以下請求為[!DNL MailChimp]建立源連接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp source connection to ingest listId",
      "description": "MailChimp Members source connection to ingest listId",
      "baseConnectionId": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
      "connectionSpec": {
          "id": "2e8580db-6489-4726-96de-e33f5f60295f",
          "version": "1.0"
      },
      "data": {
          "format": "json",
      },
      "params": {
          "listId": "10c097ca71"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 源連接的名稱。 請確保源連接的名稱是描述性的，因為您可以使用此名稱查找有關源連接的資訊。 |
| `description` | （選用）您可以包含的屬性，以提供來源連線的詳細資訊。 |
| `baseConnectionId` | 基本連接ID [!DNL MailChimp]。 此ID是在先前的步驟中產生。 |
| `connectionSpec.id` | 與源對應的連接規範ID。 |
| `data.format` | 您要擷取的[!DNL MailChimp]資料格式。 |
| `params.listId` | [!DNL MailChimp]清單ID也稱為受眾ID，可將受眾資料傳輸至其他整合。 |

**回應**

成功的響應返回新建源連接的唯一標識符(`id`)。 在後續步驟中需要此ID才能建立資料流。

```json
{
    "id": "a51e4cf6-65ef-45f4-b4bf-4f03da5f01cc",
    "etag": "\"6b02b65d-0000-0200-0000-6154bfbe0000\""
}
```

## 建立目標XDM結構 {#target-schema}

為了在Platform中使用來源資料，必須建立目標架構，以根據您的需求來建構來源資料。 然後，目標架構會用來建立包含來源資料的Platform資料集。

通過對[Schema Registry API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)執行POST請求，可以建立目標XDM架構。

如需如何建立目標XDM架構的詳細步驟，請參閱有關使用API](../../../../../xdm/api/schemas.md)建立架構的[教學課程。

### 建立目標資料集 {#target-dataset}

目標資料集的建立方式，是對[目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)執行POST請求，提供裝載內目標架構的ID。

如需如何建立目標資料集的詳細步驟，請參閱有關使用API](../../../../../catalog/api/create-dataset.md)建立資料集的[教學課程。

## 建立目標連線 {#target-connection}

目標連線代表所擷取資料所登陸之目的地的連線。 要建立目標連接，必須提供與[!DNL Data Lake]對應的固定連接規範ID。 此ID為：`c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

目標架構中的目標資料集和[!DNL Data Lake]的連接規範ID現在具有唯一標識符。 使用這些識別碼，您可以使用[!DNL Flow Service] API建立目標連線，以指定將包含傳入來源資料的資料集。

**API格式**

```https
POST /targetConnections
```

**要求**

下列請求會為[!DNL MailChimp]建立目標連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp target connection",
      "description": "MailChimp Members target connection",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/570630b91eb9d5cf5db0436756abb110d02912917a67da2d",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6155e3a9bd13651949515f14"
      }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 目標連接的名稱。 請確定目標連線的名稱是描述性的，因為您可以使用此名稱來查詢目標連線的資訊。 |
| `description` | （選用）您可以包含的屬性，用於提供目標連線的詳細資訊。 |
| `connectionSpec.id` | 與[!DNL Data Lake]對應的連接規範ID。 此固定ID為：`c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |
| `data.format` | 要帶入Platform的[!DNL MailChimp]資料格式。 |
| `params.dataSetId` | 上一步驟中擷取的目標資料集ID。 |


**回應**

A successful response returns the new target connection&#39;s unique identifier (`id`). 後續步驟需要此ID。

```json
{
    "id": "8db5fb4a-6ce8-4370-afc0-1765e39535a5",
    "etag": "\"960093ce-0000-0200-0000-6154da3e0000\""
}
```

## 建立對應 {#mapping}

若要將來源資料內嵌至目標資料集，必須先將其對應至目標資料集所遵守的目標架構。 這是透過對[[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/)執行POST要求，並在要求裝載中定義資料對應而達成。

**API format**

```http
POST /conversion/mappingSets
```

**要求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "version": 0,
      "xdmSchema": "_{TENANT_ID}.schemas.570630b91eb9d5cf5db0436756abb110d02912917a67da2d",
      "xdmVersion": "1.0",
      "mappings": [
      {
        "destinationXdmPath": "person.name.firstName",
        "sourceAttribute": "merge_fields.FNAME",
        "identity": false,
        "version": 0
      },
      {
        "destinationXdmPath": "person.name.lastName",
        "sourceAttribute": "merge_fields.LNAME",
        "identity": false,
        "version": 0
      }
    ]
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `xdmSchema` | 先前步驟中產生的[目標XDM架構](#target-schema)的ID。 |
| `mappings.destinationXdmPath` | 要映射源屬性的目標XDM路徑。 |
| `mappings.sourceAttribute` | 需要對應至目標XDM路徑的來源屬性。 |
| `mappings.identity` | 一個布爾值，用於指定是否為[!DNL Identity Service]標籤映射集。 |

**回應**

成功的響應返回新建立的映射的詳細資訊，包括其唯一標識符(`id`)。 在以後的步驟中需要此值才能建立資料流。

```json
{
    "id": "5a365b23962d4653b9d9be25832ee5b4",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 建立流程 {#flow}

將[!DNL MailChimp]資料帶入Platform的最後一步是建立資料流。 您現在已準備下列必要值：

* [源連接ID](#source-connection)
* [Target連線ID](#target-connection)
* [對應ID](#mapping)

資料流負責從源中調度和收集資料。 您可以在裝載中提供先前提及的值時，執行POST要求來建立資料流。

若要排程擷取，您必須先將開始時間值設為紀元時間（以秒為單位）。 然後，您必須將頻率值設定為以下五個選項之一：`once`、`minute`、`hour`、`day`或`week`。 間隔值指定兩個連續擷取之間的期間，並建立一次性擷取不需要設定間隔。 對於所有其他頻率，間隔值必須設定為等於或大於`15`。


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
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "MailChimp Members dataflow",
      "description": "MailChimp Members dataflow",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "a51e4cf6-65ef-45f4-b4bf-4f03da5f01cc"
      ],
      "targetConnectionIds": [
          "8db5fb4a-6ce8-4370-afc0-1765e39535a5"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "5a365b23962d4653b9d9be25832ee5b4",
                  "mappingVersion": 0
              }
          }
      ],
      "scheduleParams": {
          "startTime": "1632809759",
          "frequency": "minute",
          "interval": 15
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 資料流的名稱。 請確保資料流的名稱具有描述性，因為您可以使用此名稱查找資料流的資訊。 |
| `description` | （可選）可以包括的屬性，用於提供有關資料流的更多資訊。 |
| `flowSpec.id` | 建立資料流所需的流規範ID。 此固定ID為：`6499120c-0b15-42dc-936e-847ea3c24d72`。 |
| `flowSpec.version` | 流規範ID的相應版本。 此值預設為`1.0`。 |
| `sourceConnectionIds` | 先前步驟中產生的[源連接ID](#source-connection)。 |
| `targetConnectionIds` | 先前步驟中產生的[目標連線ID](#target-connection)。 |
| `transformations` | 此屬性包含需要套用至資料的各種轉換。 將不符合XDM的資料帶入Platform時，此屬性為必要項目。 |
| `transformations.name` | 指派給轉換的名稱。 |
| `transformations.params.mappingId` | 先前步驟中產生的[對應ID](#mapping)。 |
| `transformations.params.mappingVersion` | 對應ID的對應版本。 此值預設為`0`。 |
| `scheduleParams.startTime` | 資料首次擷取開始時的指定開始時間。 |
| `scheduleParams.frequency` | 資料流收集資料的頻率。 可接受的值包括：`once`、`minute`、`hour`、`day`或`week`。 |
| `scheduleParams.interval` | 該間隔指定兩個連續流運行之間的週期。 間隔的值應為非零整數。 當頻率設定為`once`且對於其他頻率值應大於或等於`15`時，不需要間隔。 |

**回應**

成功的響應返回新建立的資料流的ID(`id`)。 您可以使用此ID監視、更新或刪除資料流。

```json
{
    "id": "209812ad-7bef-430c-b5b2-a648aae72094",
    "etag": "\"2e01f11d-0000-0200-0000-615649660000\""
}
```

## 監視資料流

建立資料流後，您可以監視正在通過資料流進行內嵌的資料，以查看有關流運行、完成狀態和錯誤的資訊。

**API格式**

```http
GET /runs?property=flowId=={FLOW_ID}
```

**要求**

以下請求將檢索現有資料流的規範。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回關於流程執行的詳細資訊，包括關於其建立日期、來源和目標連線的資訊，以及流程執行的唯一識別碼(`id`)。

```json
{
    "items": [
        {
            "id": "209812ad-7bef-430c-b5b2-a648aae72094",
            "createdAt": 1633044829955,
            "updatedAt": 1633044838006,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{IMS_ORG}",
            "name": "MailChimp Members dataflow",
            "description": "MailChimp Members dataflow",
            "flowSpec": {
                "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"2e01f11d-0000-0200-0000-615649660000\"",
            "etag": "\"2e01f11d-0000-0200-0000-615649660000\"",
            "sourceConnectionIds": [
                "e70d2773-711f-43ee-b956-9a1a5da03dd8"
            ],
            "targetConnectionIds": [
                "43e141f6-6385-4d80-a4e4-c0fb59abbd43"
            ],
            "inheritedAttributes": {
                "sourceConnections": [
                    {
                        "id": "e70d2773-711f-43ee-b956-9a1a5da03dd8",
                        "connectionSpec": {
                            "id": "2e8580db-6489-4726-96de-e33f5f60295f",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "05c595e5-edc3-45c8-90bb-fcf556b57c4b",
                            "connectionSpec": {
                                "id": "2e8580db-6489-4726-96de-e33f5f60295f",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "43e141f6-6385-4d80-a4e4-c0fb59abbd43",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "scheduleParams": {
                "startTime": "1633044818",
                "frequency": "minute",
                "interval": 15
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingId": "5a365b23962d4653b9d9be25832ee5b4",
                        "mappingVersion": 0
                    }
                }
            ],
            "runs": "/flows/209812ad-7bef-430c-b5b2-a648aae72094/runs",
            "lastOperation": {
                "started": 1633044829988,
                "updated": 0,
                "operation": "create"
            }
        }
    ]
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `items` | 包含與您特定流程執行相關聯的中繼資料的單一裝載。 |
| `id` | 顯示與資料流對應的ID。 |
| `state` | 顯示資料流的當前狀態。 |
| `inheritedAttributes` | Contains the attributes that define your flow, such as IDs for its corresponding base, source, and target connection. |
| `scheduleParams` | 包含資料流的獲取調度的資訊，如其開始時間（以紀元時間）、頻率和間隔。 |
| `transformations` | 包含有關應用於資料流的轉換屬性的資訊。 |
| `runs` | Displays your flow&#39;s corresponding run ID. 您可以使用此ID來監控特定的流程執行。 |

## 更新資料流

要更新資料流的運行計畫、名稱和說明，請對[!DNL Flow Service] API執行PATCH請求，同時提供您的流ID、版本和要使用的新計畫。

>[!IMPORTANT]
>
>提出PATCH請求時需要`If-Match`標題。 The value for this header is the unique version of the connection you want to update.

**API format**

```http
PATCH /flows/{FLOW_ID}
```

**要求**

以下請求會更新流程運行計畫以及資料流的名稱和說明。

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/209812ad-7bef-430c-b5b2-a648aae72094' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: "2e01f11d-0000-0200-0000-615649660000"' \
  -d '[
          {
              "op": "replace",
              "path": "/scheduleParams/frequency",
              "value": "day"
          },
          {
              "op": "replace",
              "path": "/name",
              "value": "MailChimp Members Dataflow 2.0"
          },
          {
              "op": "replace",
              "path": "/description",
              "value": "MailChimp Members Dataflow Updated"
          }
      ]'
```

| 參數 | 說明 |
| --------- | ----------- |
| `op` | 用於定義更新資料流所需操作的操作調用。 操作包括：`add`、`replace`和`remove`。 |
| `path` | 要更新的參數的路徑。 |
| `value` | 您要用更新參數的新值。 |

**回應**

成功的回應會傳回您的流程ID和更新的etag。 您可以在提供流程ID時，向[!DNL Flow Service] API提出GET要求，以驗證更新。

```json
{
    "id": "209812ad-7bef-430c-b5b2-a648aae72094",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 刪除資料流

使用現有流ID，可以通過對[!DNL Flow Service] API執行DELETE請求來刪除資料流。

**API格式**

```http
DELETE /flows/{FLOW_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{FLOW_ID}` | 要刪除的資料流的唯一`id`值。 |

**要求**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/flows/209812ad-7bef-430c-b5b2-a648aae72094' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204（無內容）和空白內文。 您可以嘗試對資料流執行查閱(GET)請求以確認刪除。 API會傳回HTTP 404（找不到）錯誤，指出資料流已刪除。

## 更新您的連線

要更新連接的名稱、說明和憑據，請對[!DNL Flow Service] API執行PATCH請求，同時提供您的基本連接ID、版本和要使用的新資訊。

>[!IMPORTANT]
>
>提出PATCH請求時需要`If-Match`標題。 此標題的值是您要更新的連線的唯一版本。

**API格式**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 要更新的連接的唯一`id`值。 |

**要求**

以下請求會提供新名稱和說明，以及一組新的憑證，以更新您的連線。

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/connections/4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: 4000cff7-0000-0200-0000-6154bad60000' \
  -d '[
      {
          "op": "replace",
          "path": "/auth/params",
          "value": {
              "username": "mailchimp-member-activity-user",
              "password": "{NEW_PASSWORD}"
          }
      },
      {
          "op": "replace",
          "path": "/name",
          "value": "MailChimp Members Connection 2.0"
      },
      {
          "op": "add",
          "path": "/description",
          "value": "Updated MailChimp Members Connection"
      }
  ]'
```

| 參數 | 說明 |
| --------- | ----------- |
| `op` | 用來定義更新連線所需動作的操作呼叫。 操作包括：`add`、`replace`和`remove`。 |
| `path` | 要更新的參數的路徑。 |
| `value` | 您要用更新參數的新值。 |

**回應**

成功的回應會傳回基本連線ID和更新的etag。 您可以在提供連線ID時，向[!DNL Flow Service] API提出GET要求，以驗證更新。

```json
{
    "id": "4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## 刪除您的連線

擁有現有基本連線ID後，請對[!DNL Flow Service] API執行DELETE請求。

**API格式**

```http
DELETE /connections/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 要刪除的基本連接的唯一`id`值。 |

**要求**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/flowservice/connections/4cea039f-f1cc-4fa5-9136-db8dd4c7fbfa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態204（無內容）和空白內文。

您可以嘗試對連線進行查詢(GET)以確認刪除。
