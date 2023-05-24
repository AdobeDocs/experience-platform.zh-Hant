---
title: 使用流服務API為SugarCRM帳戶和聯繫人建立源連接和資料流
description: 瞭解如何使用流服務API將Adobe Experience Platform與SugarCRM帳戶和聯繫人連接。
exl-id: 2b422b39-5b86-4313-a214-725044d9812c
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '2181'
ht-degree: 1%

---

# (Beta)建立源連接和資料流 [!DNL SugarCRM Accounts & Contacts] 使用流服務API

>[!NOTE]
>
>的 [!DNL SugarCRM Accounts & Contacts] 源為beta。 查看 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

以下教程將指導您完成建立 [!DNL SugarCRM Accounts & Contacts] 源連接並建立資料流，以便 [[!DNL SugarCRM]](https://www.sugarcrm.com/) 帳戶和聯繫人資料，使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對以下Experience Platform元件進行工作理解：

* [源](../../../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了要成功連接到所需的其他資訊 [!DNL SugarCRM] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了連接 [!DNL SugarCRM Accounts & Contacts] 到平台，必須提供以下連接屬性的值：

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| `host` | 源連接到的SugarCRM API終結點。 | `developer.salesfusion.com` |
| `username` | 您的SugarCRM開發人員帳戶用戶名。 | `abc.def@example.com@sugarmarketdemo000.com` |
| `password` | 您的SugarCRM開發人員帳戶密碼。 | `123456789` |

## 連接 [!DNL SugarCRM Accounts & Contacts] 到使用 [!DNL Flow Service] API

下面概述了驗證您的 [!DNL SugarCRM] 源，建立源連接，並建立資料流以將帳戶和聯繫人資料Experience Platform。

### 建立基本連接 {#base-connection}

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL SugarCRM Accounts & Contacts] 身份驗證憑據作為請求正文的一部分。

**API格式**

```https
POST /connections
```

**要求**

以下請求為 [!DNL SugarCRM Accounts & Contacts]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SugarCRM Accounts & Contacts base connection",
      "description": "Create a live inbound connection to your SugarCRM Accounts & Contacts instance, to ingest both historic and scheduled data into Experience Platform",
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
| `{OBJECT}` | 僅當查看特定目錄時才需要此參數。 其值表示要瀏覽的目錄的路徑。 對於此源，值將為 `json`。 |
| `fileType=json` | 要帶到平台的檔案的檔案類型。 目前， `json` 是唯一支援的檔案類型。 |
| `{PREVIEW}` | 一個布爾值，它定義連接的內容是否支援預覽。 |
| `{SOURCE_PARAMS}` | 定義要帶到平台的源檔案的參數。 檢索接受的格式類型 `{SOURCE_PARAMS}`，必須在base64中對整個字串進行編碼。 <br> [!DNL SugarCRM Accounts & Contacts] 支援多個API。 根據您正在利用的對象類型，傳遞以下對象之一： <ul><li>`accounts` :與您的組織有關係的公司。</li><li>`contacts` :與您的組織有既定關係的個人。</li></ul> |

的 [!DNL SugarCRM Accounts & Contacts] 支援多個API。 根據您利用要發送的請求的對象類型，如下所示：

**要求**

>[!BEGINTABS]

>[!TAB 帳戶]

對於 [!DNL SugarCRM] 帳戶API `{SOURCE_PARAMS}` 傳遞為 `{"object_type":"accounts"}`。 當編碼在base64中時，它等於 `eyJvYmplY3RfdHlwZSI6ImFjY291bnRzIn0=` 如下所示。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJvYmplY3RfdHlwZSI6ImFjY291bnRzIn0=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!TAB 聯繫人]

對於 [!DNL SugarCRM] 聯繫人API `{SOURCE_PARAMS}` 傳遞為 `{"object_type":"contacts"}`。 當編碼在base64中時，它等於 `eyJvYmplY3RfdHlwZSI6ImNvbnRhY3RzIn0=` 如下所示。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJvYmplY3RfdHlwZSI6ImNvbnRhY3RzIn0=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!ENDTABS]

**回應**

同樣，根據您利用接收的響應的對象類型，如下所示：

>[!NOTE]
>
>某些記錄已被截斷，以便更好地呈現。

>[!BEGINTABS]

>[!TAB 帳戶]

成功的響應將返回如下結構。

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
                    "owner": {
                        "type": "string"
                    },
                    "key_account": {
                        "type": "boolean"
                    },
                    "owner_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "custom_score_field": {
                        "type": "string"
                    },
                    "created_by": {
                        "type": "string"
                    },
                    "billing_city": {
                        "type": "string"
                    },
                    "account_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "phone": {
                        "type": "string"
                    },
                    "account_name": {
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
                    "created_date": {
                        "type": "string"
                    },
                    "updated_date": {
                        "type": "string"
                    },
                    "created_by_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "account_score": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "account": {
                        "type": "string"
                    },
                    "contacts": {
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
            "next": "https://developer.salesfusion.com/api/2.0/accounts/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 101148,
            "count": 101148,
            "results": {
                "account_id": 1,
                "account": "https://developer.salesfusion.com/api/2.0/accounts/1/",
                "account_name": "No Company",
                "owner_id": 1,
                "owner": "https://developer.salesfusion.com/api/2.0/users/1/",
                "created_date": "2022-06-22T23:35:00Z",
                "created_by": "https://developer.salesfusion.com/api/2.0/users/1/",
                "updated_date": "2019-08-29T15:18:00Z",
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/1/",
                "contacts": "https://developer.salesfusion.com/api/2.0/accounts/1/contacts/",
                "created_by_id": 1,
                "updated_by_id": 1,
                "custom_score_field": "0",
                "account_score": 0,
                "key_account": false
            },
            "page_size": 100
        },
        {
            "next": "https://developer.salesfusion.com/api/2.0/accounts/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 101148,
            "count": 101148,
            "results": {
                "account_id": 2,
                "account": "https://developer.salesfusion.com/api/2.0/accounts/2/",
                "account_name": "360 Vacations",
                "owner_id": 45,
                "owner": "https://developer.salesfusion.com/api/2.0/users/45/",
                "phone": "+1 - 384 - 735 - 3844",
                "created_date": "2022-09-22T23:35:00Z",
                "created_by": "https://developer.salesfusion.com/api/2.0/users/45/",
                "updated_date": "2022-02-03T21:55:00Z",
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/45/",
                "billing_city": "New York City",
                "contacts": "https://developer.salesfusion.com/api/2.0/accounts/2/contacts/",
                "created_by_id": 45,
                "updated_by_id": 45,
                "custom_score_field": "0",
                "account_score": 0,
                "key_account": false
            },
            "page_size": 100
        },
        {
            "next": "https://developer.salesfusion.com/api/2.0/accounts/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 101148,
            "count": 101148,
            "results": {
                "account_id": 50,
                "account": "https://developer.salesfusion.com/api/2.0/accounts/50/",
                "account_name": "Waverly Trading House",
                "owner_id": 40,
                "owner": "https://developer.salesfusion.com/api/2.0/users/40/",
                "phone": "+1 - 964 - 226 - 4552",
                "created_date": "2022-09-18T23:35:00Z",
                "created_by": "https://developer.salesfusion.com/api/2.0/users/40/",
                "updated_date": "2022-02-03T21:55:00Z",
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/40/",
                "billing_city": "Minneapolis",
                "contacts": "https://developer.salesfusion.com/api/2.0/accounts/50/contacts/",
                "created_by_id": 40,
                "updated_by_id": 40,
                "custom_score_field": "0",
                "account_score": 0,
                "key_account": false
            },
            "page_size": 100
        }
    ]
}
```

>[!TAB 聯繫人]

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
                    "opt_out": {
                        "type": "string"
                    },
                    "custom_score_field": {
                        "type": "string"
                    },
                    "contact_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "title": {
                        "type": "string"
                    },
                    "deleted_date": {},
                    "contact": {
                        "type": "string"
                    },
                    "account_name": {
                        "type": "string"
                    },
                    "first_name": {
                        "type": "string"
                    },
                    "del_date": {},
                    "email": {
                        "type": "string"
                    },
                    "delivered_date": {},
                    "owner": {
                        "type": "string"
                    },
                    "owner_name": {
                        "type": "string"
                    },
                    "last_name": {
                        "type": "string"
                    },
                    "created_by": {
                        "type": "string"
                    },
                    "account_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "opt_out_date": {},
                    "phone": {
                        "type": "string"
                    },
                    "crm_id": {
                        "type": "string"
                    },
                    "crm_type": {
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
                    "deliverability_status": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "deliverability_message": {},
                    "created_date": {
                        "type": "string"
                    },
                    "updated_date": {
                        "type": "string"
                    },
                    "created_by_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "account": {
                        "type": "string"
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
            "next": "https://developer.salesfusion.com/api/2.0/contacts/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 135704,
            "count": 135704,
            "results": {
                "contact_id": 1,
                "contact": "https://developer.salesfusion.com/api/2.0/contacts/1/",
                "first_name": "Cynthia",
                "last_name": "Rose",
                "phone": "+1 - 000 - 000 - 000",
                "email": "test.user@hotmail.com",
                "account_id": 10,
                "account_name": "Sunyvale Reporting Ltd",
                "account": "https://developer.salesfusion.com/api/2.0/accounts/10/",
                "owner_name": "Sarah Smith",
                "owner": "https://developer.salesfusion.com/api/2.0/users/41/",
                "created_date": "2022-06-23T23:35:00Z",
                "created_by": "https://developer.salesfusion.com/api/2.0/users/41/",
                "updated_date": "2022-02-03T21:55:00Z",
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/41/",
                "created_by_id": 41,
                "updated_by_id": 41,
                "crm_id": "f53c3982-84ea-11ec-874a-06a1e215b98e",
                "opt_out": "N",
                "crm_type": "Lead",
                "status": "Assigned",
                "title": "Director Operations",
                "custom_score_field": "0",
                "deliverability_status": 0
            },
            "page_size": 100
        },
        {
            "next": "https://developer.salesfusion.com/api/2.0/contacts/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 135704,
            "count": 135704,
            "results": {
                "contact_id": 2,
                "contact": "https://developer.salesfusion.com/api/2.0/contacts/2/",
                "email": "test.user@outlook.com",
                "created_date": "2022-06-21T23:35:00Z",
                "updated_date": "2022-02-03T21:55:00Z",
                "opt_out": "N",
                "crm_type": "Contact",
                "deliverability_status": 0
            },
            "page_size": 100
        },
        {
            "next": "https://developer.salesfusion.com/api/2.0/contacts/?date_field=updated_date&page=2",
            "page_number": 1,
            "total_count": 135704,
            "count": 135704,
            "results": {
                "contact_id": 3,
                "contact": "https://developer.salesfusion.com/api/2.0/contacts/3/",
                "first_name": "Jonathan",
                "last_name": "Ryan",
                "phone": "+1 - 000 - 000 - 0000",
                "email": "test.user@yahoo.com",
                "account_id": 52,
                "account_name": "Q3 ARVRO III PR",
                "account": "https://developer.salesfusion.com/api/2.0/accounts/52/",
                "owner_name": "Max Jensen",
                "owner": "https://developer.salesfusion.com/api/2.0/users/45/",
                "created_date": "2022-07-02T23:35:00Z",
                "created_by": "https://developer.salesfusion.com/api/2.0/users/45/",
                "updated_date": "2022-02-03T21:55:00Z",
                "updated_by": "https://developer.salesfusion.com/api/2.0/users/45/",
                "created_by_id": 45,
                "updated_by_id": 45,
                "crm_id": "f54a1840-84ea-11ec-9546-06a1e215b98e",
                "opt_out": "N",
                "crm_type": "Lead",
                "status": "New",
                "title": "Director Sales",
                "custom_score_field": "0",
                "deliverability_status": 0
            },
            "page_size": 100
    ]
}
```

>[!ENDTABS]

### 建立源連接 {#source-connection}

您可以通過向POST請求建立源連接 [!DNL Flow Service] API。 源連接由連接ID、源資料檔案的路徑和連接規範ID組成。

**API格式**

```https
POST /sourceConnections
```

**要求**

以下請求為 [!DNL SugarCRM Accounts & Contacts]:

根據您正在利用的對象類型，從下面的頁籤中選擇：

>[!BEGINTABS]

>[!TAB 帳戶]

對於 [!DNL SugarCRM] 帳戶API `object_type` 屬性值應 `accounts`。

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
          "object_type": "accounts",
          "path": "accounts"
      }
  }'
```

>[!TAB 聯繫人]

對於 [!DNL SugarCRM] 聯繫API `object_type` 屬性值應 `contacts`。

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
          "object_type": "contacts",
          "path": "contacts"
      }
  }'
```

>[!ENDTABS]

| 屬性 | 說明 |
| --- | --- |
| `name` | 源連接的名稱。 確保源連接的名稱是描述性的，因為您可以使用它來查找有關源連接的資訊。 |
| `description` | 可以包括的可選值，用於提供有關源連接的詳細資訊。 |
| `baseConnectionId` | 基本連接ID [!DNL SugarCRM Accounts & Contacts]。 此ID是在前一步驟中生成的。 |
| `connectionSpec.id` | 與源對應的連接規範ID。 |
| `data.format` | 格式 [!DNL SugarCRM Accounts & Contacts] 要攝取的資料。 目前，唯一支援的資料格式是 `json`。 |
| `object_type` | [!DNL SugarCRM Accounts & Contacts] 支援多個API。 根據您正在利用的對象類型，傳遞以下對象之一： <ul><li>`accounts` :與您的組織有關係的公司。</li><li>`contacts` :與您的組織有既定關係的個人。</li></ul> |
| `path` | 此值與您為其選擇的值相同 *`object_type`*。 |

**回應**

成功的響應返回唯一標識符(`id`)。 在後續步驟中建立資料流時需要此ID。

```json
{
    "id": "8f1fc72a-f562-4a1d-8597-85b5ca1b1cd3",
    "etag": "\"ed05f1e1-0000-0200-0000-6368b8710000\""
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

以下請求為 [!DNL SugarCRM Accounts & Contacts]:

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
| `data.format` | 格式 [!DNL SugarCRM Accounts & Contacts] 要攝取的資料。 |
| `params.dataSetId` | 在上一步中檢索到的目標資料集ID。 |

**回應**

成功的響應返回新目標連接的唯一標識符(`id`)。 後續步驟中需要此ID。

```json
{
    "id": "6b137bf6-d2a0-48c8-914b-d50f4942eb85",
    "etag": "\"8405a268-0000-0200-0000-6368b8c30000\""
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
          "source": "results.account",
          "destination": "_extconndev.account"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.account_id",
          "destination": "_extconndev.account_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.acount_name",
          "destination": "_extconndev.account_name"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.account_score",
          "destination": "_extconndev.account_score"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.billing_city",
          "destination": "_extconndev.billing_city"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.contacts",
          "destination": "_extconndev.contacts"
      },
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
          "source": "results.custom_score_field",
          "destination": "_extconndev.custom_score_field"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.key_account",
          "destination": "_extconndev.key_account"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.owner",
          "destination": "_extconndev.owner"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.owner_id",
          "destination": "_extconndev.owner_id"
      },
      {
          "sourceType": "ATTRIBUTE",
          "source": "results.phone",
          "destination": "_extconndev.phone_no"
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
    "id": "059c69f7207b4d7e9b48c47e2fd966a6",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### 建立流 {#flow}

向從 [!DNL SugarCRM Accounts & Contacts] 平台是建立資料流。 現在，您準備了以下必需值：

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
                  "mappingId": "059c69f7207b4d7e9b48c47e2fd966a6",
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
