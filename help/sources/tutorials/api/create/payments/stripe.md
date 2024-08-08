---
title: 使用API從您的 [!DNL Stripe] 帳戶擷取付款資料以Experience Platform
description: 瞭解如何使用Flow Service API從您的Stripe帳戶擷取付款資料以Experience Platform
badge: Beta
exl-id: a9cb3ef6-aab0-4a5b-894e-ce90b82f35a8
source-git-commit: 48aef63cffbdc52a6a96ef69e5db4f54274144b6
workflow-type: tm+mt
source-wordcount: '2020'
ht-degree: 1%

---

# 從您的[!DNL Stripe]帳戶擷取付款資料，以使用APIExperience Platform

>[!NOTE]
>
>[!DNL Stripe]來源是測試版。 閱讀來源概觀中的[條款與條件](../../../../home.md#terms-and-conditions)，以取得有關使用測試版標籤之來源的詳細資訊。

閱讀下列教學課程，瞭解如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)將付款資料從[!DNL Stripe]擷取到Adobe Experience Platform。

## 快速入門

本指南需要您實際瞭解下列Experience Platform元件：

* [來源](../../../../home.md)：Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 驗證

請閱讀[[!DNL Stripe] 總覽](../../../../connectors/payments/stripe.md)，瞭解如何擷取您的驗證認證的相關資訊。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../../../landing/api-guide.md)的指南。

## 連線[!DNL Stripe]至Experience Platform

請遵循以下指南以瞭解如何驗證您的[!DNL Stripe]來源、建立來源連線，以及建立資料流以將您的付款資料帶入Experience Platform。

### 建立基礎連線 {#base-connection}

基礎連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基礎連線ID。 您可以使用基本連線ID從來源內部探索及導覽檔案。 此外，您可以識別要擷取的特定專案，包括有關這些專案的資料型別和格式的詳細資訊。

若要建立基底連線ID，請在提供您的[!DNL Stripe]驗證認證作為要求內文的一部分時，向`/connections`端點提出POST要求。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL Stripe]的基礎連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Stripe base connection",
      "description": "Authenticated base connection for Stripe",
      "connectionSpec": {
          "id": "cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Refresh Code",
          "params": {
            "accessToken": "{ACCESS_TOKEN}",
          }
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 基礎連線的名稱。 確定基本連線的名稱是描述性的，因為您可以使用此名稱來查詢基本連線的資訊。 |
| `description` | 您可以納入的選用值，可提供基礎連線的詳細資訊。 |
| `connectionSpec.id` | 來源的連線規格ID。 [!DNL Stripe]的連線規格ID為`cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3`，此ID已修正。 |
| `auth.specName` | 您用來驗證來源以進行Experience Platform的驗證型別。 |
| `auth.params.accessToken` | 您[!DNL Stripe]帳戶的存取權杖。 閱讀[[!DNL Stripe] 驗證指南](../../../../connectors/payments/stripe.md#prerequisites)以瞭解如何擷取存取權杖的步驟。 |

**回應**

成功的回應會傳回新建立的基礎連線，包括其唯一的連線識別碼(`id`)。 在下一步中探索來源的檔案結構和內容時，需要此ID。

```json
{
  "id": "a9950001-a386-4642-a0cd-5eaac6db5556",
  "etag": "\"dc01244d-0000-0200-0000-65ea4e500000\""
}
```

### 探索您的來源 {#explore}

取得基礎連線ID後，您現在可以透過對`/connections`端點執行GET要求，同時提供基礎連線ID作為查詢引數，來探索來源資料的內容和結構。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

**要求**

執行GET請求以探索來源的檔案結構和內容時，您必須包括下表列出的查詢引數：

| 參數 | 說明 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 在上一步中產生的基本連線ID。 |
| `objectType=rest` | 您要探索的物件型別。 此值一律設為`rest`。 |
| `{OBJECT}` | 只有在檢視特定目錄時才需要此引數。 其值代表您要探索的目錄路徑。 對於此來源，值為`json`。 |
| `fileType=json` | 您要帶到Platform的檔案型別。 目前，`json`是唯一受支援的檔案型別。 |
| `{PREVIEW}` | 布林值，定義連線的內容是否支援預覽。 |
| `{SOURCE_PARAMS}` | [!DNL Base64-]編碼字串，指向您要探索的資源路徑。 您的資源路徑必須以[!DNL Base64]編碼，才能取得`{SOURCE_PARAMS}`的核准格式。 例如，`{"resourcePath":"charges"}`編碼為`eyJyZXNvdXJjZVBhdGgiOiJjaGFyZ2VzIn0%3D`。 可用資源路徑的清單包括： <ul><li>`charges`</li><li>`subscriptions`</li><li>`refunds`</li><li>`balance_transactions`</li><li>`customers`</li><li>`prices`</li></ul> |

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/a9950001-a386-4642-a0cd-5eaac6db5556/explore?objectType=rest&object=json&fileType=json&preview=false&sourceParams=eyJyZXNvdXJjZVBhdGgiOiJjaGFyZ2VzIn0%3D' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回JSON結構，如下所示：

+++選取以檢視JSON裝載

```json
{
  "format": "hierarchical",
  "schema": {
    "type": "object",
    "properties": {
      "data": {
        "type": "object",
        "properties": {
          "balance_transaction": {},
          "billing_details": {
            "type": "object",
            "properties": {
              "address": {
                "type": "object",
                "properties": {
                  "country": {},
                  "city": {},
                  "state": {},
                  "postal_code": {},
                  "line2": {},
                  "line1": {}
                }
              },
              "phone": {},
              "name": {},
              "email": {}
            }
          },
          "metadata": {
            "type": "object",
            "properties": {}
          },
          "livemode": {
            "type": "boolean"
          },
          "radar_options": {
            "type": "object",
            "properties": {}
          },
          "destination": {},
          "description": {
            "type": "string"
          },
          "failure_message": {},
          "fraud_details": {
            "type": "object",
            "properties": {}
          },
          "source": {},
          "amount_refunded": {
            "type": "integer",
            "minimum": -9007199254740992,
            "maximum": 9007199254740991
          },
          "statement_descriptor": {
            "type": "string"
          },
          "transfer_data": {},
          "receipt_url": {
            "type": "string"
          },
          "shipping": {},
          "review": {},
          "captured": {
            "type": "boolean"
          },
          "calculated_statement_descriptor": {
            "type": "string"
          },
          "currency": {
            "type": "string"
          },
          "refunded": {
            "type": "boolean"
          },
          "id": {
            "type": "string"
          },
          "outcome": {
            "type": "object",
            "properties": {
              "reason": {},
              "risk_level": {
                "type": "string"
              },
              "risk_score": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
              },
              "seller_message": {
                "type": "string"
              },
              "network_status": {
                "type": "string"
              },
              "type": {
                "type": "string"
              }
            }
          },
          "payment_method": {
            "type": "string"
          },
          "order": {},
          "dispute": {},
          "amount": {
            "type": "integer",
            "minimum": -9007199254740992,
            "maximum": 9007199254740991
          },
          "disputed": {
            "type": "boolean"
          },
          "failure_code": {},
          "transfer_group": {},
          "on_behalf_of": {},
          "created": {
            "type": "integer",
            "minimum": -9007199254740992,
            "maximum": 9007199254740991
          },
          "payment_method_details": {
            "type": "object",
            "properties": {
              "type": {
                "type": "string"
              },
              "card": {
                "type": "object",
                "properties": {
                  "country": {
                    "type": "string"
                  },
                  "last4": {
                    "type": "string"
                  },
                  "funding": {
                    "type": "string"
                  },
                  "mandate": {},
                  "wallet": {},
                  "exp_month": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                  },
                  "exp_year": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                  },
                  "overcapture": {
                    "type": "object",
                    "properties": {
                      "maximum_amount_capturable": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                      },
                      "status": {
                        "type": "string"
                      }
                    }
                  },
                  "amount_authorized": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                  },
                  "network": {
                    "type": "string"
                  },
                  "network_token": {
                    "type": "object",
                    "properties": {
                      "used": {
                        "type": "boolean"
                      }
                    }
                  },
                  "incremental_authorization": {
                    "type": "object",
                    "properties": {
                      "status": {
                        "type": "string"
                      }
                    }
                  },
                  "checks": {
                    "type": "object",
                    "properties": {
                      "cvc_check": {
                        "type": "string"
                      },
                      "address_line1_check": {},
                      "address_postal_code_check": {}
                    }
                  },
                  "extended_authorization": {
                    "type": "object",
                    "properties": {
                      "status": {
                        "type": "string"
                      }
                    }
                  },
                  "installments": {},
                  "capture_before": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                  },
                  "fingerprint": {
                    "type": "string"
                  },
                  "three_d_secure": {},
                  "brand": {
                    "type": "string"
                  },
                  "multicapture": {
                    "type": "object",
                    "properties": {
                      "status": {
                        "type": "string"
                      }
                    }
                  }
                }
              }
            }
          },
          "amount_captured": {
            "type": "integer",
            "minimum": -9007199254740992,
            "maximum": 9007199254740991
          },
          "source_transfer": {},
          "failure_balance_transaction": {},
          "receipt_number": {},
          "application": {},
          "receipt_email": {},
          "paid": {
            "type": "boolean"
          },
          "application_fee": {},
          "payment_intent": {
            "type": "string"
          },
          "invoice": {},
          "statement_descriptor_suffix": {},
          "application_fee_amount": {},
          "object": {
            "type": "string"
          },
          "customer": {
            "type": "string"
          },
          "status": {
            "type": "string"
          }
        }
      }
    }
  }
}
```

+++

### 建立來源連線 {#source-connection}

您可以向[!DNL Flow Service] API的`/sourceConnections`端點發出POST要求，以建立來源連線。 來源連線由連線ID、來源資料檔案的路徑以及連線規格ID組成。

**API格式**

```https
POST /sourceConnections
```

**要求**

下列要求會建立[!DNL Stripe]的來源連線。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Stripe Source Connection For Charges Data",
      "description": "Stripe source connection for charges data",
      "baseConnectionId": "a9950001-a386-4642-a0cd-5eaac6db5556",
      "connectionSpec": {
        "id": "cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3",
        "version": "1.0"
      },
      "data": {
        "format": "json"
      },
      "params": {
        "resourcePath": "charges"
      },
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 來源連線的名稱。 確定來源連線的名稱是描述性的，因為您可以使用此名稱來查詢來源連線的資訊。 |
| `description` | 您可以納入的選用值，可提供來源連線的詳細資訊。 |
| `baseConnectionId` | [!DNL Stripe]的基本連線識別碼。 此ID是在先前步驟中產生的。 |
| `connectionSpec.id` | 與您的來源對應的連線規格ID。 |
| `data.format` | 您要擷取的[!DNL Stripe]資料格式。 目前唯一支援的資料格式為`json`。 |

成功的回應會傳回新建立的來源連線的唯一識別碼(`id`)。 在後續步驟中需要此ID才能建立資料流。

```json
{
  "id": "abbfac4e-202c-4e04-902d-6f73e9041068",
  "etag": "\"0a033818-0000-0200-0000-65ea5a770000\""
}
```

### 建立目標XDM結構描述 {#target-schema}

為了在Experience Platform中使用來源資料，必須建立目標結構描述，以根據您的需求來建構來源資料。 然後目標結構描述會用來建立包含來源資料的Platform資料集。

可透過對[結構描述登入API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)執行POST要求來建立目標XDM結構描述。

如需有關如何建立目標XDM結構描述的詳細步驟，請參閱有關使用API [建立結構描述的教學課程](../../../../../xdm/api/schemas.md#create-a-schema)。

### 建立目標資料集 {#target-dataset}

可以透過對[目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)執行POST要求，在承載中提供目標結構描述的ID來建立目標資料集。

如需有關如何建立目標資料集的詳細步驟，請參閱有關[使用API建立資料集](../../../../../catalog/api/create-dataset.md)的教學課程。

### 建立目標連線 {#target-connection}

目標連線代表與要儲存所擷取資料的目的地之間的連線。 若要建立目標連線，您必須提供對應至資料湖的固定連線規格ID。 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

您現在具有目標結構描述、目標資料集和到資料湖的連線規格ID的唯一識別碼。 使用這些識別碼，您可以使用[!DNL Flow Service] API建立目標連線，以指定將包含傳入來源資料的資料集。

**API格式**

```https
POST /targetConnections
```

**要求**

下列要求會建立[!DNL Stripe]的目標連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Stripe Target Connection For Charges Data",
      "description": "Stripe target connection for charges data",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{ORG_ID}/schemas/5f76be8c4e4b847fdac13ca42aa6b596a89a5b91dea48b16",
              "version": "application/vnd.adobe.xed-full+json;version=1.3"
          }
      },
      "params": {
          "dataSetId": "65e622315f78042c9e8166e8"
      }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 目標連線的名稱。 請確定目標連線的名稱是描述性的，因為您可以使用此名稱來查詢目標連線的資訊。 |
| `description` | 您可以納入的選用值，可提供目標連線的詳細資訊。 |
| `connectionSpec.id` | 對應至資料湖的連線規格ID。 此固定ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |
| `data.format` | 您要擷取的[!DNL Stripe]資料格式。 |
| `params.dataSetId` | 目標資料集的ID。 此ID是由[建立目標資料集](#target-dataset)產生的。 |

**回應**

成功的回應會傳回新目標連線的唯一識別碼(`id`)。 此ID在後續步驟中是必要的。

```json
{
  "id": "69879751-ba43-48df-8cd0-39d2bb76a5b8",
  "etag": "\"4b02ef5b-0000-0200-0000-65ea5f730000\""
}
```

### 建立對應 {#mapping}

為了將來源資料擷取到目標資料集中，必須首先將其對應到目標資料集所堅持的目標結構描述。 這是透過使用在要求裝載中定義的資料對應對[[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/)執行POST要求來達成。

**API格式**

```http
POST /conversion/mappingSets
```

下列要求會建立[!DNL Stripe]的對應。

+++選取以檢視請求範例

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
      "xdmSchema": "https://ns.adobe.com/exchangesandboxcharlie/schemas/5f76be8c4e4b847fdac13ca42aa6b596a89a5b91dea48b16",
      "xdmVersion": "1.0",
      },
      "mappings":[
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.id",
            "sourceAttribute":"data.id",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.refunded",
            "sourceAttribute":"data.refunded",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.disputed",
            "sourceAttribute":"data.disputed",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.last4",
            "sourceAttribute":"data.payment_method_details.card.last4",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.livemode",
            "sourceAttribute":"data.livemode",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.status",
            "sourceAttribute":"data.status",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.overcapture.maximum_amount_capturable",
            "sourceAttribute":"data.payment_method_details.card.overcapture.maximum_amount_capturable",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.receipt_url",
            "sourceAttribute":"data.receipt_url",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.fingerprint",
            "sourceAttribute":"data.payment_method_details.card.fingerprint",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_intent",
            "sourceAttribute":"data.payment_intent",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.overcapture.status",
            "sourceAttribute":"data.payment_method_details.card.overcapture.status",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.network_token.used",
            "sourceAttribute":"data.payment_method_details.card.network_token.used",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.funding",
            "sourceAttribute":"data.payment_method_details.card.funding",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.amount",
            "sourceAttribute":"data.amount",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.customer",
            "sourceAttribute":"data.customer",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.incremental_authorization.status",
            "sourceAttribute":"data.payment_method_details.card.incremental_authorization.status",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.multicapture.status",
            "sourceAttribute":"data.payment_method_details.card.multicapture.status",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.amount_captured",
            "sourceAttribute":"data.amount_captured",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method",
            "sourceAttribute":"data.payment_method",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.object",
            "sourceAttribute":"data.object",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.captured",
            "sourceAttribute":"data.captured",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.created",
            "sourceAttribute":"data.created",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.paid",
            "sourceAttribute":"data.paid",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.amount_refunded",
            "sourceAttribute":"data.amount_refunded",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.currency",
            "sourceAttribute":"data.currency",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.country",
            "sourceAttribute":"data.payment_method_details.card.country",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.exp_year",
            "sourceAttribute":"data.payment_method_details.card.exp_year",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.amount_authorized",
            "sourceAttribute":"data.payment_method_details.card.amount_authorized",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.network",
            "sourceAttribute":"data.payment_method_details.card.network",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details",
            "sourceAttribute":"data.payment_method_details",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.exp_month",
            "sourceAttribute":"data.payment_method_details.card.exp_month",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.calculated_statement_descriptor",
            "sourceAttribute":"data.calculated_statement_descriptor",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.brand",
            "sourceAttribute":"data.payment_method_details.card.brand",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.balance_transaction",
            "sourceAttribute":"data.balance_transaction",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.extended_authorization.status",
            "sourceAttribute":"data.payment_method_details.card.extended_authorization.status",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.outcome",
            "sourceAttribute":"data.outcome",
            "identity":false,
            "version":0
        }
      ]
}
```


| 屬性 | 說明 |
| --- | --- |
| `xdmSchema` | 目標XDM結構描述的ID。 此ID是透過建立[目標XDM結構描述](#target-schema)所產生。 |
| `destinationXdmPath` | 來源屬性對應到的XDM欄位。 |
| `sourceAttribute` | 正在對應的來源資料欄位。 |
| `identity` | 一個布林值，定義欄位是否會保留在[身分識別服務](../../../../../identity-service/home.md)中。 |
| `version` | 您正在使用的對應版本。 |

+++

**回應**

成功的回應會傳回新建立的對應詳細資料，包括其唯一識別碼(`id`)。 在後續步驟中需要此值，才能建立資料流。

```json
{
  "id": "f4aad280fdec4770b7e33066945919d8",
  "version": 0,
  "createdDate": 1709860257007,
  "modifiedDate": 1709860257007,
  "createdBy": "{CREATED_BY}",
  "modifiedBy": "{MODIFIED_BY}"
}
```

### 建立流程 {#flow}

將資料從[!DNL Stripe]引進Platform的最後一步是建立資料流。 到現在為止，您已準備下列必要值：

* [Source連線ID](#source-connection)
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
    "name": "Stripe Connector Flow Generic Rest",
    "description": "Stripe Connector Description Flow Generic Rest",
    "flowSpec": {
        "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "abbfac4e-202c-4e04-902d-6f73e9041068"
    ],
    "targetConnectionIds": [
        "69879751-ba43-48df-8cd0-39d2bb76a5b8"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "f4aad280fdec4770b7e33066945919d8",
                "mappingVersion": 0
            }
        }
    ],
    "scheduleParams": {
        "startTime": "1710267858",
        "frequency": "minute",
        "interval": {{interval}}
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
| `scheduleParams.startTime` | 您的資料流將開始的時間。 您必須以Unix時間戳記的格式提供開始時間值。 |
| `scheduleParams.frequency` | 資料流收集資料的頻率。 您可以將擷取頻率設定為：  <ul><li>**一次**：將您的頻率設定為`once`以建立一次性內嵌。 建立一次性擷取資料流時，無法使用間隔和回填的設定。 依預設，排程頻率會設定為一次。</li><li>**分鐘**：將頻率設為`minute`，排程您的資料流以每分鐘擷取資料。</li><li>**小時**：將頻率設為`hour`，排程您的資料流以每小時為基礎擷取資料。</li><li>**天**：將您的頻率設為`day`，排程您的資料流每天擷取資料。</li><li>**周**：將頻率設為`week`，排程您的資料流每週擷取資料。</li></ul> |
| `scheduleParams.interval` | 間隔會指定兩個連續資料流執行之間的期間。 例如，如果您將頻率設為「天」，並將間隔設為15，則您的資料流將每隔15天執行一次。 間隔值應為非零整數。 每個頻率的最小接受間隔值如下：<ul><li>**一次**：不適用</li><li>**分鐘**： 15</li><li>**小時**： 1</li><li>**天**： 1</li><li>**周**： 1</li></ul> |

**回應**

成功的回應會傳回新建立的資料流識別碼(`id`)。 您可以使用此ID來監視、更新或刪除資料流。

```json
{
     "id": "84c64142-1741-4b0b-95a9-65644eba0cf6",
     "etag": "\"3901770b-0000-0200-0000-655708970000\""
}
```

## 附錄

下節提供監視、更新和刪除資料流時可採取之步驟的相關資訊。

### 監視資料流

建立資料流後，您可以監視透過該資料流擷取的資料，以檢視有關資料流執行、完成狀態和錯誤的資訊。 如需完整的API範例，請閱讀[使用API監視您的來源資料流](../../monitor.md)的指南。

### 更新您的資料流

在提供資料流ID的同時，向[!DNL Flow Service] API的/flows端點發出PATCH要求，以更新資料流的詳細資訊，例如其名稱和說明，以及其執行排程和相關聯的對應集。 提出PATCH要求時，您必須在`If-Match`標頭中提供資料流的唯一`etag`。 如需完整的API範例，請閱讀[使用API更新來源資料流的指南](../../update-dataflows.md)。

### 更新您的帳戶

在提供您的基本連線ID作為查詢引數的同時，透過對[!DNL Flow Service] API執行PATCH請求來更新來源帳戶的名稱、說明和認證。 發出PATCH要求時，您必須在`If-Match`標頭中提供來源帳戶的唯一`etag`。 如需完整的API範例，請閱讀[使用API更新來源帳戶的指南](../../update.md)。

### 刪除您的資料流

提供您要刪除之資料流的ID做為查詢引數的一部分，同時對[!DNL Flow Service] API執行DELETE要求，以刪除您的資料流。 如需完整的API範例，請閱讀[使用API刪除資料流](../../delete-dataflows.md)的指南。

### 刪除您的帳戶

在提供您要刪除之帳戶的基本連線ID時，透過對[!DNL Flow Service] API執行DELETE要求來刪除帳戶。 如需完整的API範例，請閱讀[使用API](../../delete.md)刪除來源帳戶的指南。
