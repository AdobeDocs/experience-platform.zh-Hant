---
title: 使用Flow Service API為SAP Commerce建立來源連線和資料流
description: 瞭解如何建立來源連線和資料流，以使用Flow Service API將SAP Commerce資料帶入Experience Platform。
badge: Beta
exl-id: 580731b9-0c04-4f83-a475-c1890ac5b7cd
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '2358'
ht-degree: 2%

---

# 為以下專案建立來源連線和資料流： [!DNL SAP Commerce] 使用流量服務API

>[!NOTE]
>
>此 [!DNL SAP Commerce] 來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

下列教學課程將逐步引導您完成建立 [!DNL SAP Commerce] 來源連線和要帶來的資料流 [[!DNL SAP] 訂閱帳單](https://www.sap.com/products/financial-management/subscription-billing.html) 使用將聯絡人和客戶資料傳送至Adobe Experience Platform [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要您深入了解下列 Experience Platform 元件：

* [來源](../../../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

以下小節提供成功連線所需的其他資訊 [!DNL SAP Commerce] 使用 [!DNL Flow Service] API。

### 收集必要的認證

為了連線 [!DNL SAP Commerce] 若要Experience Platform，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| --- | --- |
| `clientId` | 的值 `clientId` 服務金鑰中。 |
| `clientSecret` | 的值 `clientSecret` 服務金鑰中。 |
| `tokenEndpoint` | 的值 `url` 從服務金鑰中，它將類似於 `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| `region` | 您的資料中心位置。 區域存在於中 `url` 且其值類似於 `eu10` 或 `us10`. 例如，如果 `url` 是 `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`，則您需要 `eu10`. |

如需這些認證的詳細資訊，請參閱 [[!DNL SAP Commerce] 檔案](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/c5fcaf96daff4c7a8520188e4d8a1843.html).

## 連線 [!DNL SAP Commerce] 至平台，使用 [!DNL Flow Service] API

以下概述驗證您的憑證所需的步驟 [!DNL SAP Commerce] 來源、建立來源連線，並建立資料流以將您的帳戶和聯絡人資料匯入Experience Platform。

### 建立基礎連線 {#base-connection}

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基本連線ID，請向以下連線ID發出POST請求： `/connections` 端點，同時提供 [!DNL SAP Commerce] 要求內文中的驗證認證。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立 [!DNL SAP Commerce]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SAP Commerce base connection",
      "description": "Authenticated base connection for SAP Commerce",
      "connectionSpec": {
          "id": "d8ee38de-7ae9-4058-9610-c79ce75f8e92",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params": {
              "region": "{REGION}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
              "tokenEndpoint": "{TOKEN_ENDPOINT}"
          }
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 基礎連線的名稱。 確定基本連線的名稱是描述性的，因為您可以使用此名稱來查詢基本連線的資訊。 |
| `description` | 您可以納入的選用值，可提供基礎連線的詳細資訊。 |
| `connectionSpec.id` | 來源的連線規格ID。 在您的來源註冊並透過核准後，即可擷取此ID [!DNL Flow Service] API。 |
| `auth.specName` | 您用來向Platform驗證來源的驗證型別。 |
| `auth.params.region` | 您的資料中心位置。 區域存在於中 `url` 且其值類似於 `eu10` 或 `us10`. 例如，如果 `url` 是 `https://subscriptionbilling.authentication.eu10.hana.ondemand.com` 您將需要 `eu10`. |
| `auth.params.clientId` | 的值 `clientId` 服務金鑰中。 |
| `auth.params.clientSecret` | 的值 `clientSecret` 服務金鑰中。 |
| `auth.params.tokenEndpoint` | 的值 `url` 從服務金鑰中，它將類似於 `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |

**回應**

成功的回應會傳回新建立的基本連線，包括其唯一的連線識別碼(`id`)。 在下一步中探索來源的檔案結構和內容時，需要此ID。

```json
{
     "id": "5f6d6022-3f64-400c-ba01-d4010de2d8ff",
     "etag": "\"f8018de1-0000-0200-0000-6482d7210000\""
}
```

### 探索您的來源 {#explore}

GET取得基本連線ID後，您現在可以透過對 `/connections` 端點，並提供您的基本連線ID作為查詢引數。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

執行GET請求以探索來源的檔案結構和內容時，您必須包括下表列出的查詢引數：

| 參數 | 說明 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 在上一步中產生的基本連線ID。 |
| `objectType=rest` | 您要探索的物件型別。 目前，此值一律設為 `rest`. |
| `{OBJECT}` | 只有在檢視特定目錄時才需要此引數。 其值代表您要探索的目錄路徑。 對於此來源，值將為 `json`. |
| `fileType=json` | 您要帶到Platform的檔案型別。 目前， `json` 是唯一支援的檔案型別。 |
| `{PREVIEW}` | 布林值，定義連線的內容是否支援預覽。 |
| `{SOURCE_PARAMS}` | 定義您要帶到Platform之來源檔案的引數。 擷取接受的格式型別 `{SOURCE_PARAMS}`，您必須以base64編碼整個字串。 <br> [!DNL SAP Commerce] 支援多個API。 根據您使用的物件型別，傳遞下列其中一項： <ul><li>`customers`</li><li>`contacts`</li></ul> |

此 [!DNL SAP Commerce] 來源支援多個API。 根據您運用要傳送的請求的物件型別，如下所示：

>[!NOTE]
>
>部分回應記錄已截斷，以提供更好的簡報。

>[!BEGINTABS]

>[!TAB 客戶]

+++請求

的 [!DNL SAP Commerce] 客戶API值 `{SOURCE_PARAMS}` 傳遞為 `{"object_type":"customers"}`. 以base64編碼時，這等同於 `eyJvYmplY3RfdHlwZSI6ImN1c3RvbWVycyJ9` 如下所示。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJvYmplY3RfdHlwZSI6ImN1c3RvbWVycyJ9' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++回應

成功的回應會傳回JSON結構，如下所示：

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "personalInfo": {
                "type": "object",
                "properties": {
                    "firstName": {
                        "type": "string"
                    },
                    "lastName": {
                        "type": "string"
                    }
                }
            },
            "addresses": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "country": {
                            "type": "string"
                        },
                        "isDefault": {
                            "type": "boolean"
                        },
                        "phone": {
                            "type": "string"
                        },
                        "city": {
                            "type": "string"
                        },
                        "street": {
                            "type": "string"
                        },
                        "postalCode": {
                            "type": "string"
                        },
                        "addressUUID": {
                            "type": "string"
                        },
                        "houseNumber": {
                            "type": "string"
                        },
                        "additionalAddressInfo": {
                            "type": "string"
                        },
                        "state": {
                            "type": "string"
                        },
                        "email": {
                            "type": "string"
                        }
                    }
                }
            },
            "customerNumber": {
                "type": "string"
            },
            "corporateInfo": {
                "type": "object",
                "properties": {}
            },
            "customReferences": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {}
                }
            },
            "externalObjectReferences": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "externalSystemId": {
                            "type": "string"
                        },
                        "externalId": {
                            "type": "string"
                        },
                        "externalIdTypeCode": {
                            "type": "string"
                        }
                    }
                }
            },
            "createdAt": {
                "type": "string"
            },
            "customerType": {
                "type": "string"
            },
            "markets": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "country": {
                            "type": "string"
                        },
                        "salesArea": {
                            "type": "object",
                            "properties": {
                                "division": {
                                    "type": "string"
                                },
                                "distributionChannel": {
                                    "type": "string"
                                },
                                "salesOrganization": {
                                    "type": "string"
                                }
                            }
                        },
                        "priceType": {
                            "type": "string"
                        },
                        "active": {
                            "type": "boolean"
                        },
                        "currency": {
                            "type": "string"
                        },
                        "marketId": {
                            "type": "string"
                        }
                    }
                }
            },
            "createdBy": {
                "type": "string"
            },
            "changedBy": {
                "type": "string"
            },
            "changedAt": {
                "type": "string"
            },
            "defaultAddress": {
                "type": "object",
                "properties": {
                    "country": {
                        "type": "string"
                    },
                    "isDefault": {
                        "type": "boolean"
                    },
                    "phone": {
                        "type": "string"
                    },
                    "city": {
                        "type": "string"
                    },
                    "street": {
                        "type": "string"
                    },
                    "postalCode": {
                        "type": "string"
                    },
                    "addressUUID": {
                        "type": "string"
                    },
                    "houseNumber": {
                        "type": "string"
                    },
                    "additionalAddressInfo": {
                        "type": "string"
                    },
                    "state": {
                        "type": "string"
                    },
                    "email": {
                        "type": "string"
                    }
                }
            }
        }
    },
    "data": [
        {
            "personalInfo": {
                "firstName": "Test 1",
                "lastName": "User 1"
            },
            "addresses": [
                {
                    "email": "user1@test.com",
                    "phone": "123456890",
                    "houseNumber": "123",
                    "city": "New Orleans",
                    "state": "LA",
                    "postalCode": "700089",
                    "country": "US",
                    "addressUUID": "ff871221-ab48-435c-b1f5-903db1c3cea2",
                    "isDefault": true
                }
            ],
            "customerNumber": "2863620303",
            "externalObjectReferences": [
                {
                    "externalSystemId": "t090000",
                    "externalId": "1324566",
                    "externalIdTypeCode": "201"
                }
            ],
            "createdAt": "2023-05-31T06:39:28.499Z",
            "customerType": "INDIVIDUAL",
            "markets": [
                {
                    "marketId": "US",
                    "active": true,
                    "currency": "USD",
                    "country": "US",
                    "salesArea": {
                        "salesOrganization": "SE10",
                        "distributionChannel": "00",
                        "division": "00"
                    },
                    "priceType": "Net"
                }
            ],
            "createdBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "changedBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "changedAt": "2023-05-31T06:39:28.499Z",
            "defaultAddress": {
                "email": "user1@test.com",
                "phone": "123456890",
                "houseNumber": "123",
                "city": "New Orleans",
                "state": "LA",
                "postalCode": "700089",
                "country": "US",
                "addressUUID": "ff871221-ab48-435c-b1f5-903db1c3cea2",
                "isDefault": true
            }
        },
        {
            "personalInfo": {
                "firstName": "Test 2",
                "lastName": "User 2"
            },
            "addresses": [
                {
                    "email": "user2@test.com",
                    "phone": "1234567899",
                    "houseNumber": "876",
                    "city": "New Orleans",
                    "state": "LA",
                    "postalCode": "700089",
                    "country": "US",
                    "addressUUID": "1cd039aa-5b86-4e46-8e37-9ef263332c6b",
                    "isDefault": true
                }
            ],
            "customerNumber": "6776445404",
            "externalObjectReferences": [
                {
                    "externalSystemId": "t089999",
                    "externalId": "1324565",
                    "externalIdTypeCode": "201"
                }
            ],
            "createdAt": "2023-05-31T06:39:28.142Z",
            "customerType": "INDIVIDUAL",
            "markets": [
                {
                    "marketId": "US",
                    "active": true,
                    "currency": "USD",
                    "country": "US",
                    "salesArea": {
                        "salesOrganization": "SE10",
                        "distributionChannel": "00",
                        "division": "00"
                    },
                    "priceType": "Net"
                }
            ],
            "createdBy": "sb-subscription-billing!b123456|revenue-cloud!b12345",
            "changedBy": "sb-subscription-billing!b123456|revenue-cloud!b12345",
            "changedAt": "2023-05-31T06:39:28.142Z",
            "defaultAddress": {
                "email": "user2@test.com",
                "phone": "1234567899",
                "houseNumber": "876",
                "city": "New Orleans",
                "state": "LA",
                "postalCode": "700089",
                "country": "US",
                "addressUUID": "1cd039aa-5b86-4e46-8e37-9ef263332c6b",
                "isDefault": true
            }
        }
    ]
}
```

+++

>[!TAB 連絡人]

+++請求

的 [!DNL SAP Commerce] 連絡人API的值 `{SOURCE_PARAMS}` 傳遞為 `{"object_type":"contacts"}`. 以base64編碼時，這等同於 `eyJvYmplY3RfdHlwZSI6ImNvbnRhY3RzIn0=` 如下所示。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJvYmplY3RfdHlwZSI6ImNvbnRhY3RzIn0=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++回應

成功的回應會傳回JSON結構，如下所示：

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "externalObjectReferences": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {}
                }
            },
            "personalInfo": {
                "type": "object",
                "properties": {
                    "firstName": {
                        "type": "string"
                    },
                    "lastName": {
                        "type": "string"
                    }
                }
            },
            "createdAt": {
                "type": "string"
            },
            "createdBy": {
                "type": "string"
            },
            "changedBy": {
                "type": "string"
            },
            "contactNumber": {
                "type": "string"
            },
            "changedAt": {
                "type": "string"
            }
        }
    },
    "data": [
        {
            "personalInfo": {
                "firstName": "Test 1",
                "lastName": "User 1"
            },
            "createdAt": "2023-05-31T13:33:52.689Z",
            "createdBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "changedBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "contactNumber": "4365374130",
            "changedAt": "2023-05-31T13:33:52.689Z"
        },
        {
            "personalInfo": {
                "firstName": "Test 2",
                "lastName": "User 2"
            },
            "createdAt": "2023-05-31T13:33:52.37Z",
            "createdBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "changedBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "contactNumber": "4075431868",
            "changedAt": "2023-05-31T13:33:52.37Z"
        }
    ]
}
```

+++

>[!ENDTABS]

### 建立來源連線 {#source-connection}

您可以透過向以下發出POST請求來建立來源連線： `/sourceConnections` 的端點 [!DNL Flow Service] API。 來源連線由連線ID、來源資料檔案的路徑以及連線規格ID組成。

**API格式**

```https
POST /sourceConnections
```

根據您使用的物件型別，從下列標籤中選取：

>[!BEGINTABS]

>[!TAB 客戶]

+++請求

以下請求會為建立來源連線 [!DNL SAP Commerce] 客戶資料：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SAP Commerce Source Connection",
      "description": "SAP Commerce Source Connection",
      "baseConnectionId": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "object_type": "customers"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 來源連線的名稱。 確保來源連線的名稱是描述性的，因為您可以使用此名稱來查詢來源連線的資訊。 |
| `description` | 您可以納入的選用值，可提供來源連線的詳細資訊。 |
| `baseConnectionId` | 的基礎連線ID： [!DNL SAP Commerce]. 此ID是在先前步驟中產生的。 |
| `connectionSpec.id` | 與您的來源對應的連線規格ID。 |
| `data.format` | 的格式 [!DNL SAP Commerce] 您要擷取的資料。 目前唯一支援的資料格式為 `json`. |
| `object_type` | [!DNL SAP Commerce] 支援多個API。 若為客戶API，則 `object_type` 引數應設為 `customers`. |
| `path` | 這會與您選取的值相同 `object_type`. |

+++

+++回應

成功的回應會傳回唯一識別碼(`id`)。 在後續步驟中需要此ID才能建立資料流。

```json
{
    "id": "8f1fc72a-f562-4a1d-8597-85b5ca1b1cd3",
    "etag": "\"ed05f1e1-0000-0200-0000-6368b8710000\""
}
```

+++

>[!TAB 連絡人]

+++請求

以下請求會為建立來源連線 [!DNL SAP Commerce] 連絡人資料：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SAP Commerce Source Connection",
      "description": "SAP Commerce Source Connection",
      "baseConnectionId": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "object_type": "contacts"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 來源連線的名稱。 確保來源連線的名稱是描述性的，因為您可以使用此名稱來查詢來源連線的資訊。 |
| `description` | 您可以納入的選用值，可提供來源連線的詳細資訊。 |
| `baseConnectionId` | 的基礎連線ID： [!DNL SAP Commerce]. 此ID是在先前步驟中產生的。 |
| `connectionSpec.id` | 與您的來源對應的連線規格ID。 |
| `data.format` | 的格式 [!DNL SAP Commerce] 您要擷取的資料。 目前唯一支援的資料格式為 `json`. |
| `object_type` | [!DNL SAP Commerce] 支援多個API。 若為連絡人API，請使用 `object_type` 引數應設為 `contacts`. |
| `path` | 這會與您選取的值相同 *`object_type`*. |

+++

+++回應

成功的回應會傳回唯一識別碼(`id`)。 在後續步驟中需要此ID才能建立資料流。

```json
{
    "id": "8f1fc72a-f562-4a1d-8597-85b5ca1b1cd3",
    "etag": "\"ed05f1e1-0000-0200-0000-6368b8710000\""
}
```

+++

>[!ENDTABS]

### 建立目標XDM結構描述 {#target-schema}

為了在Platform中使用來源資料，必須建立目標結構描述，以根據您的需求來建構來源資料。 然後目標結構描述會用來建立包含來源資料的Platform資料集。

您可以透過對以下對象執行POST請求來建立目標XDM結構描述： [結構描述登入API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

如需如何建立目標XDM結構的詳細步驟，請參閱以下教學課程： [使用API建立結構描述](../../../../../xdm/api/schemas.md#create-a-schema).

### 建立目標資料集 {#target-dataset}

您可以透過對執行POST請求來建立目標資料集 [目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，在裝載中提供目標結構描述的ID。

如需如何建立目標資料集的詳細步驟，請參閱教學課程，位於 [使用API建立資料集](../../../../../catalog/api/create-dataset.md).

### 建立目標連線 {#target-connection}

目標連線代表與要儲存所擷取資料的目的地之間的連線。 若要建立目標連線，您必須提供對應至資料湖的固定連線規格ID。 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

您現在具有目標結構描述、目標資料集和到資料湖的連線規格ID的唯一識別碼。 使用這些識別碼，您可以使用以下專案建立目標連線： [!DNL Flow Service] API可指定將包含傳入來源資料的資料集。

**API格式**

```https
POST /targetConnections
```

**要求**

以下請求會為建立目標連線 [!DNL SAP Commerce]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SAP Commerce Target Connection Generic Rest",
      "description": "SAP Commerce Target Connection Generic Rest",
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
          "dataSetId": "645923cd7aeeea1c06c5e92e"
      }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 目標連線的名稱。 請確定目標連線的名稱是描述性的，因為您可以使用此名稱來查詢目標連線的資訊。 |
| `description` | 您可以納入的選用值，可提供目標連線的詳細資訊。 |
| `connectionSpec.id` | 對應至資料湖的連線規格ID。 此固定ID為： `6b137bf6-d2a0-48c8-914b-d50f4942eb85`. |
| `data.format` | 的格式 [!DNL SAP Commerce] 您要擷取的資料。 |
| `params.dataSetId` | 在上一步中擷取的目標資料集ID。 |

**回應**

成功回應會傳回新目標連線的唯一識別碼(`id`)。 此ID在後續步驟中是必要的。

```json
{
    "id": "5b72a4b6-2fb8-4ca7-8ad8-4114a3063c5c",
    "etag": "\"db00c6dc-0000-0200-0000-6482d8280000\""
}
```

### 建立對應 {#mapping}

為了將來源資料擷取到目標資料集中，必須首先將其對應到目標資料集所堅持的目標結構描述。 這是透過向執行POST請求來達成 [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) 要求裝載中定義資料對應。

**API格式**

```http
POST /conversion/mappingSets
```

>[!BEGINTABS]

>[!TAB 客戶]

+++請求

以下請求會為建立對應 [!DNL SAP Commerce] 客戶API資料

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
            "source": "customerNumber",
            "destination": "_extconndev.customerNumber"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "customerType",
            "destination": "_extconndev.customerType"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "changedAt",
            "destination": "_extconndev.changedAt"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "addresses[*].email",
            "destination": "_extconndev.addresses[*].email"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "addresses[*].city",
            "destination": "_extconndev.addresses[*].city"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "addresses[*].addressUUID",
            "destination": "_extconndev.addresses[*].addressUUID"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalSystemId",
            "destination": "_extconndev.externalObjectReferences[*].externalSystemId"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalId",
            "destination": "_extconndev.externalObjectReferences[*].externalId"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalIdTypeCode",
            "destination": "_extconndev.externalObjectReferences[*].externalIdTypeCode"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "customReferences[*].id",
            "destination": "_extconndev.customReferences[*].id"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "customReferences[*].typeCode",
            "destination": "_extconndev.customReferences[*].typeCode"
        }
    ],
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/325fd5394ba421246b05c0a3c2cd5efeec2131058a63d473",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `outputSchema.schemaRef.id` | 的ID [目標XDM結構描述](#target-schema) 已在先前步驟中產生。 |
| `mappings.sourceType` | 正在對應的來源屬性型別。 |
| `mappings.source` | 需要對映至目的地XDM路徑的來源屬性。 |
| `mappings.destination` | 來源屬性對應到的目的地XDM路徑。 |

+++

+++回應

成功的回應會傳回新建立的對應詳細資訊，包括其唯一識別碼(`id`)。 在後續步驟中需要此值，才能建立資料流。

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

+++

>[!TAB 連絡人]

+++請求

以下請求會為建立對應 [!DNL SAP Commerce] 連絡人API資料

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
            "source": "contactNumber",
            "destination": "_extconndev.contactNumber"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "createdAt",
            "destination": "_extconndev.createdAt"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "changedAt",
            "destination": "_extconndev.changedAt"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "personalInfo.lastName",
            "destination": "_extconndev.personalInfo.lastName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "personalInfo.firstName",
            "destination": "_extconndev.personalInfo.firstName"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectRefereneces[*].externalSystemId",
            "destination": "_extconndev.externalObjectReferences[*].externalSystemId"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalId",
            "destination": "_extconndev.externalObjectReferences[*].externalId"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalIdTypeCode",
            "destination": "_extconndev.externalObjectReferences[*].externalIdTypeCode"
        }
    ],
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/extconndev/schemas/325fd5394ba421246b05c0a3c2cd5efeec2131058a63d473",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
      }
    }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `outputSchema.schemaRef.id` | 的ID [目標XDM結構描述](#target-schema) 已在先前步驟中產生。 |
| `mappings.sourceType` | 正在對應的來源屬性型別。 |
| `mappings.source` | 需要對映至目的地XDM路徑的來源屬性。 |
| `mappings.destination` | 來源屬性對應到的目的地XDM路徑。 |

+++

+++回應

成功的回應會傳回新建立的對應詳細資訊，包括其唯一識別碼(`id`)。 在後續步驟中需要此值，才能建立資料流。

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

+++

>[!ENDTABS]

### 建立流程 {#flow}

從匯入資料的最後一步 [!DNL SAP Commerce] 到Platform就是建立資料流。 到現在為止，您已準備下列必要值：

* [來源連線ID](#source-connection)
* [目標連線ID](#target-connection)
* [對應 ID](#mapping)

資料流負責從來源排程及收集資料。 您可以執行POST要求，同時在裝載中提供先前提到的值，藉此建立資料流。

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
      "name": "SAP Commerce Connector Description Flow Generic Rest",
      "description": "SAP Commerce Connector Description Flow Generic Rest",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "2ef2e831-f4f1-4363-a0f7-08b4ea347164"
      ],
      "targetConnectionIds": [
          "5b72a4b6-2fb8-4ca7-8ad8-4114a3063c5c"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "ddf0592bcc9d4ac391803f15f2429f87",
                  "mappingVersion": "0"
              }
          }
      ],
      "scheduleParams": {
          "startTime": "1625040887",
          "frequency": "once",
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 資料流的名稱。 確保資料流的名稱是描述性的，因為您可以使用此名稱來查閱資料流上的資訊。 |
| `description` | 您可以納入的選用值，可提供資料流的詳細資訊。 |
| `flowSpec.id` | 建立資料流所需的流量規格ID。 此固定ID為： `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | 流程規格ID的對應版本。 此值預設為 `1.0`. |
| `sourceConnectionIds` | 此 [來源連線ID](#source-connection) 已在先前步驟中產生。 |
| `targetConnectionIds` | 此 [目標連線ID](#target-connection) 已在先前步驟中產生。 |
| `transformations` | 此屬性包含套用至資料所需的各種轉換。 將非XDM相容的資料引進Platform時，需要此屬性。 |
| `transformations.name` | 指定給轉換的名稱。 |
| `transformations.params.mappingId` | 此 [對應ID](#mapping) 已在先前步驟中產生。 |
| `transformations.params.mappingVersion` | 對應ID的對應版本。 此值預設為 `0`. |
| `scheduleParams.startTime` | 此屬性包含資料流擷取排程的相關資訊。 |
| `scheduleParams.frequency` | 資料流收集資料的頻率。 |
| `scheduleParams.interval` | 間隔會指定兩個連續資料流執行之間的期間。 間隔的值應為非零整數。 |

**回應**

成功的回應會傳回ID (`id`)。 您可以使用此ID來監視、更新或刪除資料流。

```json
{
     "id": "fcd16140-81b4-422a-8f9a-eaa92796c4f4",
     "etag": "\"9200a171-0000-0200-0000-6368c1da0000\""
}
```

## 附錄

下節提供監視、更新和刪除資料流的步驟相關資訊。

### 監視資料流

建立資料流後，您可以監視透過該資料流擷取的資料，以檢視有關資料流執行、完成狀態和錯誤的資訊。 如需完整的API範例，請閱讀以下指南： [使用API監控您的來源資料流](../../monitor.md).

### 更新您的資料流

透過向以下專案發出PATCH請求，更新資料流的詳細資訊，例如其名稱和說明，以及其執行排程和相關聯的對應集 `/flows` 端點 [!DNL Flow Service] API，同時提供資料流的ID。 提出PATCH請求時，您必須提供資料流的 `etag` 在 `If-Match` 標頭。 如需完整的API範例，請閱讀以下指南： [使用API更新來源資料流](../../update-dataflows.md).

### 更新您的帳戶

透過對執行PATCH請求，更新來源帳戶的名稱、說明和認證 [!DNL Flow Service] API，同時提供您的基本連線ID作為查詢引數。 提出PATCH請求時，您必須提供來源帳戶的唯一值 `etag` 在 `If-Match` 標頭。 如需完整的API範例，請閱讀以下指南： [使用API更新您的來源帳戶](../../update.md).

### 刪除您的資料流

透過對執行DELETE請求來刪除您的資料流 [!DNL Flow Service] API，同時提供您要刪除之資料流的ID做為查詢引數的一部分。 如需完整的API範例，請閱讀以下指南： [使用API刪除您的資料流](../../delete-dataflows.md).

### 刪除您的帳戶

向以下網站執行DELETE請求，刪除您的帳戶： [!DNL Flow Service] API，同時提供您要刪除之帳戶的基本連線ID。 如需完整的API範例，請閱讀以下指南： [使用API刪除您的來源帳戶](../../delete.md).
