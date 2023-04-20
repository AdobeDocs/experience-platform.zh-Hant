---
title: 使用流服務API建立流源連接和資料流，以便對資料進行修改
description: 了解如何使用流量服務API為Shopify資料建立串流來源連線和資料流。
badge: "Beta"
hidefromtoc: y
hide: y
source-git-commit: 279d8e307c8ca5a799a47c6f903b9a082d9cf034
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 1%

---

# 為建立流源連接和資料流 [!DNL Shopify] 使用流量服務API的資料

>[!NOTE]
>
>此 [!DNL Shopify] 串流來源為測試版。 請閱讀 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用測試版標籤來源的詳細資訊。

以下教程介紹了如何建立流源連接和資料流以從中流資料的步驟 [[!DNL Shopify]](https://www.shopify.com/) 至Adobe Experience Platform使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門 {#getting-started}

本指南需要妥善了解下列Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

## 資料流 [!DNL Shopify] 使用流量服務API將資料傳送至平台

以下概述了建立源連接和資料流以流式傳輸您的 [!DNL Shopify] 資料至Platform。

### 建立源連接 {#source-connection}

向發出POST請求以建立來源連線 [!DNL Flow Service] API，在提供來源的連線規格ID時，會提供名稱和說明等詳細資訊，以及資料的格式。

**API格式**

```https
POST /sourceConnections
```

**要求**

以下請求將建立源連接 *您的來源*:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Shopify Streaming Source Connection",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "description": "Shopify Streaming Source Connection",
      "connectionSpec": {
          "id": "e77fd9d2-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      }
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 源連接的名稱。 請確保源連接的名稱是描述性的，因為您可以使用此名稱查找有關源連接的資訊。 |
| `description` | 可包含的選用值，用於提供來源連線的詳細資訊。 |
| `connectionSpec.id` | 與源對應的連接規範ID。 |
| `data.format` | 格式 [!DNL Shopify] 您要擷取的資料。 目前，唯一支援的資料格式是 `json`. |

**回應**

成功的回應會傳回唯一識別碼(`id`)。 在後續步驟中需要此ID才能建立資料流。

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

### 建立目標XDM結構 {#target-schema}

為了在Platform中使用來源資料，必須建立目標架構，以根據您的需求來建構來源資料。 然後，目標架構會用來建立包含來源資料的Platform資料集。

您可以透過執行POST要求來建立目標XDM結構 [結構註冊表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

如需建立Target XDM結構的詳細步驟，請參閱 [使用API建立結構](../../../../../xdm/api/schemas.md).

### 建立目標資料集 {#target-dataset}

目標資料集的建立方式，是透過對 [目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，提供裝載中目標架構的ID。

如需如何建立目標資料集的詳細步驟，請參閱 [使用API建立資料集](../../../../../catalog/api/create-dataset.md).

### 建立目標連線 {#target-connection}

目標連線代表要儲存所擷取資料的目的地連線。 要建立目標連接，必須提供與資料庫對應的固定連接規範ID。 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

您現在擁有唯一識別碼、目標結構、目標資料集，以及資料湖的連線規格ID。 使用這些識別碼，您可以使用 [!DNL Flow Service] API，指定包含傳入來源資料的資料集。

**API格式**

```https
POST /targetConnections
```

**要求**

下列請求會為 [!DNL Shopify]:


```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Shopify Streaming Target Connection",
      "description": "Shopify Streaming Target Connection",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json",
          "schema": {
              "id": "{TARGET_XDM_SCHEMA}",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "{TARGET_DATASET}"
      }
  }'
```


| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 目標連接的名稱。 請確定目標連線的名稱是描述性的，因為您可以使用此名稱來查詢目標連線的資訊。 |
| `description` | 可包含的選用值，用於提供目標連線的詳細資訊。 |
| `connectionSpec.id` | 與資料湖對應的連接規範ID。 此固定ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | 格式 [!DNL Shopify] 要帶入Platform的資料。 |
| `params.dataSetId` | 上一步驟中擷取的目標資料集ID。 |


**回應**

成功的回應會傳回新目標連線的唯一識別碼(`id`)。 後續步驟需要此ID。

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

### 建立對應 {#mapping}

若要將來源資料內嵌至目標資料集，必須先將其對應至目標資料集所遵守的目標架構。 這是透過執行POST要求來達成 [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) 在要求裝載中定義的資料對應。

**API格式**

```http
POST /conversion/mappingSets
```

**要求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "{TARGET_XDM_SCHEMA}",
      "xdmVersion": "1.0",
      "mappings": [
          {
              "destinationXdmPath": "person.name.firstName",
              "sourceAttribute": "firstName",
              "identity": false,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.lastName",
              "sourceAttribute": "lastName",
              "identity": false,
              "version": 0
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

### 建立流程 {#flow}

將資料從 [!DNL Shopify] 到平台是建立資料流。 您現在已準備下列必要值：

* [源連接ID](#source-connection)
* [Target連線ID](#target-connection)
* [對應 ID](#mapping)

資料流負責從源中調度和收集資料。 您可以在裝載中提供先前提及的值時，執行POST要求來建立資料流。

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
      "name": "Shopify Streaming Dataflow",
      "description": "Shopify Streaming Dataflow",
      "flowSpec": {
          "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
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
          "mappingVersion": 0
        }
      }
    ]
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 資料流的名稱。 確保資料流的名稱是描述性的，因為您可以使用此名稱查找資料流的資訊。 |
| `description` | 一個可選值，可以包括該值以提供有關資料流的詳細資訊。 |
| `flowSpec.id` | 建立資料流所需的流規範ID。 此固定ID為： `e77fde5a-22a8-11ed-861d-0242ac120002`. |
| `flowSpec.version` | 流規範ID的相應版本。 此值預設為 `1.0`. |
| `sourceConnectionIds` | 此 [源連接ID](#source-connection) 在先前的步驟中產生。 |
| `targetConnectionIds` | 此 [目標連線ID](#target-connection) 在先前的步驟中產生。 |
| `transformations` | 此屬性包含需要套用至資料的各種轉換。 將不符合XDM的資料帶入Platform時，此屬性為必要屬性。 |
| `transformations.name` | 指派給轉換的名稱。 |
| `transformations.params.mappingId` | 此 [對應ID](#mapping) 在先前的步驟中產生。 |
| `transformations.params.mappingVersion` | 對應ID的對應版本。 此值預設為 `0`. |

**回應**

成功的回應會傳回ID(`id`)。 您可以使用此ID監視、更新或刪除資料流。

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

### 取得您的串流端點URL

建立資料流後，您現在可以檢索流終結點URL。 您將使用此端點URL將源訂閱到Webhook，從而允許源與Experience Platform通信。

若要擷取串流端點URL，請向 `/flows` 端點，並提供資料流的ID。

**API格式**

```http
GET /flows/{FLOW_ID}
```

**要求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回有關資料流的資訊，包括終結點URL，標籤為 `inletUrl`.

```json
{
   "header":{
      "xactionId":"1658464615769:0062:161",
      "source":{
         "name":"shopify"
      },
      "sandboxId":"d537df80-c5d7-11e9-aafb-87c71c35cac8",
      "sandboxName":"prod",
      "originalTimestamp":1658464615770,
      "msgId":"1658464615769:0062:161",
      "msgVersion":"1.0",
      "traceContext":{
         "traceId":"ff3e7544618471eee6b934a4c5929d4e",
         "spanId":"74a759c5cc5f5a06",
         "isSampled":1.0
      },
      "_dcsMeta":{
         "inletId":"9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
         "authenticatedRequest":false,
         "debug":true
      }
   },
   "body":{
      "id":4135234371722,
      "admin_graphql_api_id":"gid://shopify/Order/4135234371722",
      "app_id":1354745,
      "browser_ip":null,
      "buyer_accepts_marketing":false,
      "cancel_reason":null,
      "cancelled_at":null,
      "cart_token":null,
      "checkout_id":21706716217482,
      "checkout_token":"b143503216124d50141fe0832fa3f4b0",
      "client_details":{
         "accept_language":null,
         "browser_height":null,
         "browser_ip":null,
         "browser_width":null,
         "session_hash":null,
         "user_agent":null
      },
      "closed_at":null,
      "confirmed":true,
      "contact_email":null,
      "created_at":"2022-07-22T00:36:48-04:00",
      "currency":"INR",
      "current_subtotal_price":"40000.00",
      "current_subtotal_price_set":{
         "shop_money":{
            "amount":"40000.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"40000.00",
            "currency_code":"INR"
         }
      },
      "current_total_discounts":"0.00",
      "current_total_discounts_set":{
         "shop_money":{
            "amount":"0.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"0.00",
            "currency_code":"INR"
         }
      },
      "current_total_duties_set":null,
      "current_total_price":"47200.00",
      "current_total_price_set":{
         "shop_money":{
            "amount":"47200.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"47200.00",
            "currency_code":"INR"
         }
      },
      "current_total_tax":"7200.00",
      "current_total_tax_set":{
         "shop_money":{
            "amount":"7200.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"7200.00",
            "currency_code":"INR"
         }
      },
      "customer_locale":null,
      "device_id":null,
      "discount_codes":[
          
      ],
      "email":"",
      "estimated_taxes":false,
      "financial_status":"paid",
      "fulfillment_status":null,
      "gateway":"manual",
      "landing_site":null,
      "landing_site_ref":null,
      "location_id":39129743498,
      "name":"#1005",
      "note":null,
      "note_attributes":[
          
      ],
      "number":5,
      "order_number":1005,
      "order_status_url":"https://connnectors-test.myshopify.com/31913214090/orders/ffd48198c78ef460177e44e22b19e6ab/authenticate?key=79a40d7da4b23d6a0beb2ba774f6ac83",
      "original_total_duties_set":null,
      "payment_gateway_names":[
         "manual"
      ],
      "phone":null,
      "presentment_currency":"INR",
      "processed_at":"2022-07-22T00:36:48-04:00",
      "processing_method":"manual",
      "reference":null,
      "referring_site":null,
      "source_identifier":null,
      "source_name":"shopify_draft_order",
      "source_url":null,
      "subtotal_price":"40000.00",
      "subtotal_price_set":{
         "shop_money":{
            "amount":"40000.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"40000.00",
            "currency_code":"INR"
         }
      },
      "tags":"",
      "tax_lines":[
         {
            "price":"7200.00",
            "rate":0.18,
            "title":"IGST",
            "price_set":{
               "shop_money":{
                  "amount":"7200.00",
                  "currency_code":"INR"
               },
               "presentment_money":{
                  "amount":"7200.00",
                  "currency_code":"INR"
               }
            },
            "channel_liable":false
         }
      ],
      "taxes_included":false,
      "test":false,
      "token":"ffd48198c78ef460177e44e22b19e6ab",
      "total_discounts":"0.00",
      "total_discounts_set":{
         "shop_money":{
            "amount":"0.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"0.00",
            "currency_code":"INR"
         }
      },
      "total_line_items_price":"40000.00",
      "total_line_items_price_set":{
         "shop_money":{
            "amount":"40000.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"40000.00",
            "currency_code":"INR"
         }
      },
      "total_outstanding":"0.00",
      "total_price":"47200.00",
      "total_price_set":{
         "shop_money":{
            "amount":"47200.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"47200.00",
            "currency_code":"INR"
         }
      },
      "total_price_usd":"589.95",
      "total_shipping_price_set":{
         "shop_money":{
            "amount":"0.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"0.00",
            "currency_code":"INR"
         }
      },
      "total_tax":"7200.00",
      "total_tax_set":{
         "shop_money":{
            "amount":"7200.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"7200.00",
            "currency_code":"INR"
         }
      },
      "total_tip_received":"0.00",
      "total_weight":800,
      "updated_at":"2022-07-22T00:36:49-04:00",
      "user_id":44968935562,
      "discount_applications":[
          
      ],
      "fulfillments":[
          
      ],
      "line_items":[
         {
            "id":10630730743946,
            "admin_graphql_api_id":"gid://shopify/LineItem/10630730743946",
            "fulfillable_quantity":1,
            "fulfillment_service":"manual",
            "fulfillment_status":null,
            "gift_card":false,
            "grams":800,
            "name":"Mobile Phones",
            "origin_location":{
               "id":3141069111434,
               "country_code":"IN",
               "province_code":"UP",
               "name":"Noida",
               "address1":"Noida",
               "address2":"",
               "city":"Noida",
               "zip":"201301"
            },
            "price":"40000.00",
            "price_set":{
               "shop_money":{
                  "amount":"40000.00",
                  "currency_code":"INR"
               },
               "presentment_money":{
                  "amount":"40000.00",
                  "currency_code":"INR"
               }
            },
            "product_exists":true,
            "product_id":4525859963018,
            "properties":[
                
            ],
            "quantity":1,
            "requires_shipping":true,
            "sku":"",
            "taxable":true,
            "title":"Mobile Phones",
            "total_discount":"0.00",
            "total_discount_set":{
               "shop_money":{
                  "amount":"0.00",
                  "currency_code":"INR"
               },
               "presentment_money":{
                  "amount":"0.00",
                  "currency_code":"INR"
               }
            },
            "variant_id":32045196640394,
            "variant_inventory_management":"shopify",
            "variant_title":"",
            "vendor":"Connnectors Test",
            "tax_lines":[
               {
                  "channel_liable":false,
                  "price":"7200.00",
                  "price_set":{
                     "shop_money":{
                        "amount":"7200.00",
                        "currency_code":"INR"
                     },
                     "presentment_money":{
                        "amount":"7200.00",
                        "currency_code":"INR"
                     }
                  },
                  "rate":0.18,
                  "title":"IGST"
               }
            ],
            "duties":[
                
            ],
            "discount_allocations":[
                
            ]
         }
      ],
      "payment_terms":null,
      "refunds":[
          
      ],
      "shipping_lines":[
          
      ]
   }
}
```

## 附錄

以下部分提供了可以採取哪些步驟監視、更新和刪除資料流的資訊。

### 監視資料流

建立資料流後，您可以監視正在通過資料流進行內嵌的資料，以查看有關流運行、完成狀態和錯誤的資訊。 如需完整的API範例，請參閱 [使用API監控來源資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### 更新資料流

通過向發出PATCH請求，更新資料流的詳細資訊，如其名稱和說明，以及運行計畫和關聯的映射集 `/flows` 端點 [!DNL Flow Service] API，同時提供資料流的ID。 發出PATCH請求時，必須提供資料流的唯一 `etag` 在 `If-Match` 頁首。 如需完整的API範例，請參閱 [使用API更新源資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### 更新您的帳戶

通過向執行PATCH請求，更新源帳戶的名稱、說明和憑據 [!DNL Flow Service] API，同時將基本連線ID設為查詢參數。 提出PATCH請求時，您必須提供來源帳戶的唯一 `etag` 在 `If-Match` 頁首。 如需完整的API範例，請參閱 [使用API更新您的來源帳戶](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### 刪除資料流

通過執行DELETE請求以刪除資料流 [!DNL Flow Service] API，同時提供您要在查詢參數中刪除之資料流的ID。 如需完整的API範例，請參閱 [使用API刪除資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### 刪除您的帳戶

對執行DELETE請求以刪除帳戶 [!DNL Flow Service] API，同時提供您要刪除之帳戶的基本連線ID。 如需完整的API範例，請參閱 [使用API刪除您的來源帳戶](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).