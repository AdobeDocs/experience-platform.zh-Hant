---
title: 使用流量服務API為Oracle NetSuite實體建立來源連線和資料流
description: 瞭解如何使用流量服務API建立來源連線和資料流，將Oracle NetSuite聯絡人和客戶資料匯入Experience Platform。
hide: true
hidefromtoc: true
badge: Beta
exl-id: ddbb413e-a6ca-49df-b68d-37c9d2aab61b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2177'
ht-degree: 1%

---

# 使用Flow Service API為[!DNL Oracle NetSuite Entities]建立來源連線和資料流

>[!NOTE]
>
>[!DNL Oracle NetSuite Entities]來源是測試版。 如需使用Beta版標示來源的相關資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

閱讀下列教學課程，瞭解如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)將連絡人和客戶資料從您的[!DNL Oracle NetSuite Activities Entities]帳戶帶入Adobe Experience Platform。

## 快速入門

本指南需要您深入瞭解下列Experience Platform元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL Oracle NetSuite Entities]。

### Authentication

請閱讀[[!DNL Oracle NetSuite] 總覽](../../../../connectors/marketing-automation/oracle-netsuite.md)，瞭解如何擷取您的驗證認證的相關資訊。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

## 使用[!DNL Flow Service] API連線[!DNL Oracle NetSuite Entities]至Experience Platform

以下概述驗證[!DNL Oracle NetSuite Entities]來源、建立來源連線，以及建立資料流以將客戶和連絡人資料匯入Experience Platform所需執行的步驟。

### 建立基礎連線 {#base-connection}

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL Oracle NetSuite Entities]驗證認證作為要求內文的一部分時，對`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL Oracle NetSuite Entities]的基礎連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NetSuite Entities base connection",
      "description": "Authenticated base connection for Oracle NetSuite Entities",
      "connectionSpec": {
          "id": "fdf850b4-5a8d-4a5a-9ce8-4caef9abb2a8",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params": {
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
              "accessTokenUrl": "{ACCESS_TOKEN_URL}",
              "accessToken": "{ACCESS_TOKEN_URL}"
          }
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 基礎連線的名稱。 確定基本連線的名稱是描述性的，因為您可以使用此名稱來查詢基本連線的資訊。 |
| `description` | 您可以納入的選用值，可提供基礎連線的詳細資訊。 |
| `connectionSpec.id` | 來源的連線規格ID。 在您的來源已透過[!DNL Flow Service] API註冊並核准後，即可擷取此ID。 |
| `auth.specName` | 您用來向Experience Platform驗證來源的驗證型別。 |
| `auth.params.clientId` | 建立整合記錄時的使用者端ID值。 您可以在[這裡](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981)找到建立互動記錄的程式。 值是類似於`7fce.....b42f`的64個字元字串。 |
| `auth.params.clientSecret` | 建立整合記錄時的使用者端ID值。 您可以在[這裡](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981)找到建立互動記錄的程式。 值是類似於`5c98.....1b46`的64個字元字串。 |
| `auth.params.accessTokenUrl` | [!DNL NetSuite]存取權杖URL，類似`https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/auth/oauth2/v1/token`，您會將ACCOUNT_ID取代為[!DNL NetSuite]帳戶識別碼。 |
| `auth.params.accessToken` | 在[OAuth 2.0授權代碼授予流程](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow)教學課程的[步驟二](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint)的結尾產生存取權杖值。 存取權杖的有效期限僅為60分鐘。 此值是格式為JSON Web權杖(JWT)的1024字元字串，類似於`eyJr......f4V0`。 |

**回應**

成功的回應會傳回新建立的基礎連線，包括其唯一的連線識別碼(`id`)。 在下一步中探索來源的檔案結構和內容時，需要此ID。

```json
{
    "id": "60c81023-99b4-4aae-9c31-472397576dd2",
    "etag": "\"fa003785-0000-0200-0000-6555c5310000\""
}
```

### 探索您的來源 {#explore}

取得基礎連線ID後，您現在可以透過對`/connections`端點執行GET要求，同時提供基礎連線ID作為查詢引數，以探索來源資料的內容和結構。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

**要求**

執行GET請求以探索來源的檔案結構和內容時，您必須包含下表列出的查詢引數：

| 參數 | 說明 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 在上一步中產生的基本連線ID。 |
| `objectType=rest` | 您要探索的物件型別。 目前，此值一律設為`rest`。 |
| `{OBJECT}` | 只有在檢視特定目錄時才需要此引數。 其值代表您要探索的目錄路徑。 對於此來源，值為`json`。 |
| `fileType=json` | 您要帶入Experience Platform的檔案型別。 目前，`json`是唯一受支援的檔案型別。 |
| `{PREVIEW}` | 布林值，定義連線的內容是否支援預覽。 |
| `{SOURCE_PARAMS}` | 為您要帶入Experience Platform的來源檔案定義引數。 若要擷取`{SOURCE_PARAMS}`接受的格式型別，您必須以base64編碼整個字串。<br> [!DNL Oracle NetSuite Entities]同時支援客戶和連絡人資料擷取。 根據您使用的物件型別，傳遞下列其中一項： <ul><li>`customer` ：擷取特定客戶資料，包括客戶名稱、地址和金鑰識別碼等詳細資訊。</li><li>`contact` ：擷取聯絡人姓名、電子郵件、電話號碼，以及與客戶相關聯的任何自訂聯絡人相關欄位。</li></ul> |

>[!BEGINTABS]

>[!TAB 客戶]

針對[!DNL Oracle NetSuite Entities]，若要擷取連絡人資料，`{SOURCE_PARAMS}`的值會傳遞為`{"object_type":"customer"}`。 以base64編碼時，其等於`eyAib2JqZWN0X3R5cGUiOiAiY3VzdG9tZXIifQ%3D%3D`，如下所示。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/db7a6f4b-3f5d-487c-9a87-83e84df5074c/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyAib2JqZWN0X3R5cGUiOiAiY3VzdG9tZXIifQ%3D%3D' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!TAB 連絡人]

針對[!DNL Oracle NetSuite Entities]，若要擷取連絡人資料，`{SOURCE_PARAMS}`的值會傳遞為`{"object_type":"contact"}`。 以base64編碼時，其等於`eyAib2JqZWN0X3R5cGUiOiAiY29udGFjdCJ9`，如下所示。


```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/db7a6f4b-3f5d-487c-9a87-83e84df5074c/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyAib2JqZWN0X3R5cGUiOiAiY29udGFjdCJ9' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

>[!ENDTABS]

**回應**

同樣地，視您要利用收到的回應之物件型別而定，如下所示：

>[!NOTE]
>
>部分記錄已截斷，以提供更好的簡報。

>[!BEGINTABS]

>[!TAB 客戶]

成功的回應會傳回結構，如下所示。

+++選取以檢視JSON裝載

```json
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "totalResults": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "offset": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "hasMore": {
                "type": "boolean"
            },
            "links": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "rel": {
                            "type": "string"
                        },
                        "href": {
                            "type": "string"
                        }
                    }
                }
            },
            "items": {
                "type": "object",
                "properties": {
                    "isinactive": {
                        "type": "string"
                    },
                    "weblead": {
                        "type": "string"
                    },
                    "emailtransactions": {
                        "type": "string"
                    },
                    "entityid": {
                        "type": "string"
                    },
                    "dateclosed": {
                        "type": "string"
                    },
                    "entitynumber": {
                        "type": "string"
                    },
                    "emailpreference": {
                        "type": "string"
                    },
                    "creditholdoverride": {
                        "type": "string"
                    },
                    "entitystatus": {
                        "type": "string"
                    },
                    "giveaccess": {
                        "type": "string"
                    },
                    "isbudgetapproved": {
                        "type": "string"
                    },
                    "receivablesaccount": {
                        "type": "string"
                    },
                    "shippingcarrier": {
                        "type": "string"
                    },
                    "isperson": {
                        "type": "string"
                    },
                    "balancesearch": {
                        "type": "string"
                    },
                    "links": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {}
                        }
                    },
                    "currency": {
                        "type": "string"
                    },
                    "overduebalancesearch": {
                        "type": "string"
                    },
                    "id": {
                        "type": "string"
                    },
                    "entitytitle": {
                        "type": "string"
                    },
                    "email": {
                        "type": "string"
                    },
                    "displaysymbol": {
                        "type": "string"
                    },
                    "searchstage": {
                        "type": "string"
                    },
                    "lastmodifieddate": {
                        "type": "string"
                    },
                    "oncredithold": {
                        "type": "string"
                    },
                    "probability": {
                        "type": "string"
                    },
                    "faxtransactions": {
                        "type": "string"
                    },
                    "altname": {
                        "type": "string"
                    },
                    "datecreated": {
                        "type": "string"
                    },
                    "printtransactions": {
                        "type": "string"
                    },
                    "alcoholrecipienttype": {
                        "type": "string"
                    },
                    "overridecurrencyformat": {
                        "type": "string"
                    },
                    "companyname": {
                        "type": "string"
                    },
                    "unbilledorderssearch": {
                        "type": "string"
                    },
                    "shipcomplete": {
                        "type": "string"
                    },
                    "symbolplacement": {
                        "type": "string"
                    }
                }
            }
        }
    },
    "data": [
        {
            "totalResults": 10,
            "offset": 0,
            "count": 10,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "alcoholrecipienttype": "CONSUMER",
                "altname": "Company 1615554322",
                "balancesearch": "0",
                "companyname": "Company 1615554322",
                "creditholdoverride": "AUTO",
                "currency": "1",
                "dateclosed": "2022-12-15",
                "datecreated": "2022-12-15",
                "displaysymbol": "£",
                "email": "customer3@example.com",
                "emailpreference": "DEFAULT",
                "emailtransactions": "F",
                "entityid": "4",
                "entitynumber": "4",
                "entitystatus": "13",
                "entitytitle": "4 Company 1615554322",
                "faxtransactions": "F",
                "giveaccess": "F",
                "id": "404",
                "isbudgetapproved": "F",
                "isinactive": "F",
                "isperson": "F",
                "lastmodifieddate": "2022-12-15",
                "oncredithold": "F",
                "overduebalancesearch": "0",
                "overridecurrencyformat": "F",
                "printtransactions": "F",
                "probability": "1",
                "receivablesaccount": "-10",
                "searchstage": "Customer",
                "shipcomplete": "F",
                "shippingcarrier": "nonups",
                "symbolplacement": "1",
                "unbilledorderssearch": "0",
                "weblead": "F"
            }
        },
        {
            "totalResults": 10,
            "offset": 0,
            "count": 10,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "alcoholrecipienttype": "CONSUMER",
                "altname": "Company 1615554322",
                "balancesearch": "0",
                "companyname": "Company 1615554322",
                "creditholdoverride": "AUTO",
                "currency": "1",
                "dateclosed": "2023-01-19",
                "datecreated": "2023-01-19",
                "displaysymbol": "£",
                "email": "customer3@example.com",
                "emailpreference": "DEFAULT",
                "emailtransactions": "F",
                "entityid": "6",
                "entitynumber": "6",
                "entitystatus": "13",
                "entitytitle": "6 Company 1615554322",
                "faxtransactions": "F",
                "giveaccess": "F",
                "id": "605",
                "isbudgetapproved": "F",
                "isinactive": "F",
                "isperson": "F",
                "lastmodifieddate": "2023-01-19",
                "oncredithold": "F",
                "overduebalancesearch": "0",
                "overridecurrencyformat": "F",
                "printtransactions": "F",
                "probability": "1",
                "receivablesaccount": "-10",
                "searchstage": "Customer",
                "shipcomplete": "F",
                "shippingcarrier": "nonups",
                "symbolplacement": "1",
                "unbilledorderssearch": "0",
                "weblead": "F"
            }
        },
        {
            "totalResults": 10,
            "offset": 0,
            "count": 10,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "alcoholrecipienttype": "CONSUMER",
                "altname": "Company 1615554322",
                "balancesearch": "0",
                "companyname": "Company 1615554322",
                "creditholdoverride": "AUTO",
                "currency": "1",
                "dateclosed": "2023-02-01",
                "datecreated": "2023-02-01",
                "displaysymbol": "£",
                "email": "customer3@example.com",
                "emailpreference": "DEFAULT",
                "emailtransactions": "F",
                "entityid": "9",
                "entitynumber": "9",
                "entitystatus": "13",
                "entitytitle": "9 Company 1615554322",
                "faxtransactions": "F",
                "giveaccess": "F",
                "id": "710",
                "isbudgetapproved": "F",
                "isinactive": "F",
                "isperson": "F",
                "lastmodifieddate": "2023-02-01",
                "oncredithold": "F",
                "overduebalancesearch": "0",
                "overridecurrencyformat": "F",
                "printtransactions": "F",
                "probability": "1",
                "receivablesaccount": "-10",
                "searchstage": "Customer",
                "shipcomplete": "F",
                "shippingcarrier": "nonups",
                "symbolplacement": "1",
                "unbilledorderssearch": "0",
                "weblead": "F"
            }
        },
    ]
},
```

+++

>[!TAB 連絡人]

成功的回應會傳回結構，如下所示。

+++選取以檢視JSON裝載

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "totalResults": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "offset": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "hasMore": {
                "type": "boolean"
            },
            "links": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "rel": {
                            "type": "string"
                        },
                        "href": {
                            "type": "string"
                        }
                    }
                }
            },
            "items": {
                "type": "object",
                "properties": {
                    "isinactive": {
                        "type": "string"
                    },
                    "isprivate": {
                        "type": "string"
                    },
                    "phone": {
                        "type": "string"
                    },
                    "lastmodifieddate": {
                        "type": "string"
                    },
                    "links": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {}
                        }
                    },
                    "company": {
                        "type": "string"
                    },
                    "entityid": {
                        "type": "string"
                    },
                    "datecreated": {
                        "type": "string"
                    },
                    "id": {
                        "type": "string"
                    },
                    "entitytitle": {
                        "type": "string"
                    }
                }
            }
        }
    },
    "data": [
        {
            "totalResults": 10,
            "offset": 0,
            "count": 10,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "company": "504",
                "datecreated": "2023-09-06",
                "entityid": "John Doe2",
                "entitytitle": "John Doe2",
                "id": "1210",
                "isinactive": "F",
                "isprivate": "F",
                "lastmodifieddate": "2023-09-06",
                "phone": "+9199999999998"
            }
        },
        {
            "totalResults": 10,
            "offset": 0,
            "count": 10,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "company": "504",
                "datecreated": "2023-09-06",
                "entityid": "John Doe4",
                "entitytitle": "John Doe4",
                "id": "1212",
                "isinactive": "F",
                "isprivate": "F",
                "lastmodifieddate": "2023-09-06",
                "phone": "+9199999999996"
            }
        },
        {
            "totalResults": 10,
            "offset": 0,
            "count": 10,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "company": "504",
                "datecreated": "2023-09-06",
                "entityid": "John Doe6",
                "entitytitle": "John Doe6",
                "id": "1214",
                "isinactive": "F",
                "isprivate": "F",
                "lastmodifieddate": "2023-09-06",
                "phone": "+9199999999994"
            }
        },
    ]
}
```

+++

>[!ENDTABS]

### 建立來源連線 {#source-connection}

您可以對[!DNL Flow Service] API的`/sourceConnections`端點發出POST要求，以建立來源連線。 來源連線由連線ID、來源資料檔案的路徑以及連線規格ID組成。

**API格式**

```https
POST /sourceConnections
```

**要求**

下列要求會建立[!DNL Oracle NetSuite Entities]的來源連線：

>[!BEGINTABS]

>[!TAB 客戶]

擷取客戶資料時，`object_type`屬性值應該是`customer`。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NetSuite Entities Source Connection",
      "description": "Oracle NetSuite Entities Source Connection",
      "baseConnectionId": "60c81023-99b4-4aae-9c31-472397576dd2",
      "connectionSpec": {
          "id": "fdf850b4-5a8d-4a5a-9ce8-4caef9abb2a8",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
            "object_type": "customer"        
      }
  }'
```

>[!TAB 連絡人]

擷取連絡人資料時，`object_type`屬性值應該是`contact`。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NetSuite Entities Source Connection",
      "description": "Oracle NetSuite Entities Source Connection",
      "baseConnectionId": "60c81023-99b4-4aae-9c31-472397576dd2",
      "connectionSpec": {
          "id": "fdf850b4-5a8d-4a5a-9ce8-4caef9abb2a8",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
            "object_type": "contact"        
      }
  }'
```

>[!ENDTABS]

| 屬性 | 說明 |
| --- | --- |
| `name` | 來源連線的名稱。 確保來源連線的名稱是描述性的，因為您可以使用此名稱來查詢來源連線的資訊。 |
| `description` | 您可以納入的選用值，可提供來源連線的詳細資訊。 |
| `baseConnectionId` | [!DNL Oracle NetSuite Entities]的基本連線識別碼。 此ID是在先前步驟中產生的。 |
| `connectionSpec.id` | 與您的來源對應的連線規格ID。 |
| `data.format` | 您要擷取的[!DNL Oracle NetSuite Entities]資料格式。 目前唯一支援的資料格式為`json`。 |
| `object_type` | [!DNL Oracle NetSuite Entities]同時支援客戶和連絡人擷取。 根據您想要的實體，傳遞下列其中一項： <ul><li>`customer` ：擷取特定客戶資料，包括客戶名稱、地址和金鑰識別碼等詳細資訊。</li><li>`contact` ：擷取聯絡人姓名、電子郵件、電話號碼，以及與客戶相關聯的任何自訂聯絡人相關欄位。</li></ul> |

**回應**

成功的回應會傳回新建立的來源連線的唯一識別碼(`id`)。 在後續步驟中需要此ID才能建立資料流。

```json
{
    "id": "574c049f-29fc-411f-be0d-f80002025f51",
    "etag": "\"0704acb3-0000-0200-0000-6555c5470000\""
}
```

### 建立目標XDM結構描述 {#target-schema}

為了在Experience Platform中使用來源資料，必須建立目標結構描述，以根據您的需求建構來源資料。 然後使用目標結構描述來建立包含來源資料的Experience Platform資料集。

可透過對[結構描述登入API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)執行POST要求來建立目標XDM結構描述。

如需有關如何建立目標XDM結構描述的詳細步驟，請參閱有關使用API [建立結構描述的教學課程](../../../../../xdm/api/schemas.md#create-a-schema)。

### 建立目標資料集 {#target-dataset}

可透過對[目錄服務API](https://developer.adobe.com/experience-platform-apis/references/catalog/)執行POST要求，在承載中提供目標結構描述的ID，來建立目標資料集。

如需有關如何建立目標資料集的詳細步驟，請參閱有關[使用API建立資料集](../../../../../catalog/api/create-dataset.md)的教學課程。

### 建立目標連線 {#target-connection}

目標連線代表與要儲存所擷取資料的目的地之間的連線。 若要建立目標連線，您必須提供對應至資料湖的固定連線規格ID。 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

您現在具有目標結構描述、目標資料集和到資料湖的連線規格ID的唯一識別碼。 使用這些識別碼，您可以使用[!DNL Flow Service] API建立目標連線，以指定將包含傳入來源資料的資料集。

**API格式**

```https
POST /targetConnections
```

**要求**

下列要求會建立[!DNL Oracle NetSuite Entities]的目標連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NetSuite Entities Target Connection Generic Rest",
      "description": " Oracle NetSuite Entities Connection Generic Rest",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/325fd5394ba421246b05c0a3c2cd5efeec2131058a63d473",
              "version": "1.2"
          }
      },
      "params": {
          "dataSetId": "65004470082ac828d2c3d6a0"
      }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 目標連線的名稱。 請確定目標連線的名稱是描述性的，因為您可以使用此名稱來查詢目標連線的資訊。 |
| `description` | 您可以納入的選用值，可提供目標連線的詳細資訊。 |
| `connectionSpec.id` | 對應至資料湖的連線規格ID。 此固定ID為： `6b137bf6-d2a0-48c8-914b-d50f4942eb85`。 |
| `data.format` | 您要擷取的[!DNL Oracle NetSuite Entities]資料格式。 |
| `params.dataSetId` | 在上一步中擷取的目標資料集ID。 |

**回應**

成功的回應會傳回新目標連線的唯一識別碼(`id`)。 此ID在後續步驟中是必要的。

```json
{
    "id": "382fc614-3c5b-46b9-a971-786fb0ae6c5d",
    "etag": "\"e0016100-0000-0200-0000-655707a40000\""
}
```

### 建立對應 {#mapping}

為了將來源資料擷取到目標資料集中，必須首先將其對應到目標資料集所堅持的目標結構描述。 這是透過使用在要求裝載中定義的資料對應對[[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/)執行POST要求來達成。

**API格式**

```http
POST /conversion/mappingSets
```

**要求**

下列要求會建立[!DNL DNL NetSuite Entities]的對應

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
            "source": "items.id",
            "destination": "_extconndev.NS_ID"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.entitytitle",
            "destination": "_extconndev.NS_entity_title"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.datecreated",
            "destination": "_extconndev.NS_datecreated"
        },
        {
            "sourceType": "ATTRIBUTE",
            "destination": "_extconndev.NS_email",
            "source": "items.email"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.lastmodifieddate",
            "destination": "_extconndev.NS_lastmodified"
        }
    ]
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
    "id": "ddf0592bcc9d4ac391803f15f2429f87",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### 建立流程 {#flow}

將資料從[!DNL Oracle NetSuite Entities]引進Experience Platform的最後一步是建立資料流。 到現在為止，您已準備下列必要值：

* [Source連線ID](#source-connection)
* [目標連線ID](#target-connection)
* [對應 ID](#mapping)

資料流負責從來源排程及收集資料。 您可以執行POST要求，同時在裝載中提供先前提及的值來建立資料流。

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
    "name": "Oracle NetSuite Entities connector Flow Generic Rest",
    "description": "Oracle NetSuite Entities connector Description Flow Generic Rest",
    "flowSpec": {
        "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "d8827440-339f-428d-bf38-5e2ab1f0f7bb"
    ],
    "targetConnectionIds": [
        "e349a15e-c639-4047-8b2a-154aa7a857d7"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "10787532e0994eb686e76bdab69a9e88",
                "mappingVersion": 0
            }
        }
    ],
      "scheduleParams": {
          "startTime": 1700202649,
          "frequency": "once"
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
| `scheduleParams.frequency` | 資料流收集資料的頻率。 |
| `scheduleParams.interval` | 間隔會指定兩個連續資料流執行之間的期間。 間隔的值應為非零整數。 |

**回應**

成功的回應會傳回新建立的資料流識別碼(`id`)。 您可以使用此ID來監視、更新或刪除資料流。

```json
{
     "id": "84c64142-1741-4b0b-95a9-65644eba0cf6",
     "etag": "\"3901770b-0000-0200-0000-655708970000\""
}
```

## 附錄

下節提供監視、更新和刪除資料流的步驟相關資訊。

### 監視資料流

建立資料流後，您可以監視透過該資料流擷取的資料，以檢視有關資料流執行、完成狀態和錯誤的資訊。 如需完整的API範例，請閱讀[使用API監視您的來源資料流](../../monitor.md)的指南。

### 更新您的資料流

提供資料流的ID時，透過向[!DNL Flow Service] API的`/flows`端點發出PATCH要求，更新資料流的詳細資訊，例如其名稱和說明，以及其執行排程和相關聯的對應集。 發出PATCH請求時，您必須在`If-Match`標頭中提供資料流的唯一`etag`。 如需完整的API範例，請閱讀[使用API更新來源資料流的指南](../../update-dataflows.md)。

### 更新您的帳戶

在提供您的基本連線ID作為查詢引數的同時，透過對[!DNL Flow Service] API執行PATCH請求來更新來源帳戶的名稱、說明和認證。 發出PATCH請求時，您必須在`If-Match`標頭中提供來源帳戶的唯一`etag`。 如需完整的API範例，請閱讀[使用API更新來源帳戶的指南](../../update.md)。

### 刪除您的資料流

提供您要刪除之資料流的ID做為查詢引數的一部分，同時對[!DNL Flow Service] API執行DELETE要求，以刪除您的資料流。 如需完整的API範例，請閱讀[使用API刪除資料流](../../delete-dataflows.md)的指南。

### 刪除您的帳戶

在提供您要刪除之帳戶的基本連線ID時，對[!DNL Flow Service] API執行DELETE要求，以刪除您的帳戶。 如需完整的API範例，請閱讀[使用API](../../delete.md)刪除來源帳戶的指南。
