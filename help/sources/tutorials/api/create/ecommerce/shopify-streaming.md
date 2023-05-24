---
title: 使用流服務API建立流源連接和資料流以便對資料進行篩選
description: 瞭解如何使用流服務API為Shopify資料建立流源連接和資料流。
badge: β
exl-id: d44414a1-48fb-41e2-8cec-23cad867ba7d
source-git-commit: feb05d5bddc4135c5fe14d3ec5d8fad62c5e2236
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 1%

---

# 建立流源連接和資料流 [!DNL Shopify] 使用流服務API的資料

>[!NOTE]
>
>的 [!DNL Shopify] 流源位於beta中。 請閱讀 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

以下教程介紹了如何建立流源連接和資料流以從中流式傳輸資料的步驟 [[!DNL Shopify]](https://www.shopify.com/) Adobe Experience Platform用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門 {#getting-started}

本指南要求對以下Experience Platform元件進行工作理解：

* [源](../../../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 流 [!DNL Shopify] 使用流服務API向平台發送資料

下面概述了建立源連接和資料流以流式傳輸所需的步驟 [!DNL Shopify] 資料到平台。

### 建立源連接 {#source-connection}

通過向Oracle提供POST請求建立源連接 [!DNL Flow Service] API，在提供源的連接規範ID時，提供名稱和說明等詳細資訊以及資料格式。

**API格式**

```https
POST /sourceConnections
```

**要求**

以下請求為 *源*:

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
| `name` | 源連接的名稱。 確保源連接的名稱是描述性的，因為您可以使用它查找有關源連接的資訊。 |
| `description` | 可以包括的可選值，用於提供有關源連接的詳細資訊。 |
| `connectionSpec.id` | 與源對應的連接規範ID。 |
| `data.format` | 格式 [!DNL Shopify] 要攝取的資料。 目前，唯一支援的資料格式是 `json`。 |

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

通過執行對目標XDM的POST請求，可以建立目標XDM模式 [架構註冊表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)。

有關如何建立目標XDM架構的詳細步驟，請參見上的教程 [使用API建立架構](../../../../../xdm/api/schemas.md)。

### 建立目標資料集 {#target-dataset}

通過對目標資料集執行POST請求，可以建立目標資料集 [目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，提供負載內目標架構的ID。

有關如何建立目標資料集的詳細步驟，請參見上的教程 [使用API建立資料集](../../../../../catalog/api/create-dataset.md)。

### 建立目標連接 {#target-connection}

目標連接表示到要儲存所攝取資料的目的地的連接。 要建立目標連接，必須提供與資料湖相對應的固定連接規範ID。 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

您現在具有唯一標識符、目標模式、目標資料集以及到資料湖的連接規範ID。 使用這些標識符，可以使用 [!DNL Flow Service] API，用於指定將包含入站源資料的資料集。

**API格式**

```https
POST /targetConnections
```

**要求**

以下請求為 [!DNL Shopify]:


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
| `name` | 目標連接的名稱。 確保目標連接的名稱是描述性的，因為您可以使用它查找有關目標連接的資訊。 |
| `description` | 可以包括的可選值，用於提供有關目標連接的詳細資訊。 |
| `connectionSpec.id` | 與資料湖對應的連接規範ID。 此固定ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |
| `data.format` | 格式 [!DNL Shopify] 要帶到平台的資料。 |
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
| `xdmSchema` | 的ID [目標XDM架構](#target-schema) 生成。 |
| `mappings.destinationXdmPath` | 要映射源屬性的目標XDM路徑。 |
| `mappings.sourceAttribute` | 需要映射到目標XDM路徑的源屬性。 |
| `mappings.identity` | 一個布爾值，它指定是否將映射集標籤為 [!DNL Identity Service]。 |

**回應**

成功的響應返回新建立的映射的詳細資訊，包括其唯一標識符(`id`)。 在後續步驟中建立資料流時需要此值。

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

### 建立流 {#flow}

向從 [!DNL Shopify] 平台是建立資料流。 現在，您準備了以下必需值：

* [源連接ID](#source-connection)
* [目標連接ID](#target-connection)
* [對應 ID](#mapping)

資料流負責從源調度和收集資料。 通過在負載中提供先前提到的值的同時執行POST請求，可以建立資料流。

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
| `name` | 資料流的名稱。 確保資料流的名稱是描述性的，因為您可以使用它查找有關資料流的資訊。 |
| `description` | 可以包括的可選值，用於提供有關資料流的詳細資訊。 |
| `flowSpec.id` | 建立資料流所需的流規範ID。 此固定ID為： `e77fde5a-22a8-11ed-861d-0242ac120002`。 |
| `flowSpec.version` | 流規範ID的相應版本。 此值預設為 `1.0`。 |
| `sourceConnectionIds` | 的 [源連接ID](#source-connection) 生成。 |
| `targetConnectionIds` | 的 [目標連接ID](#target-connection) 生成。 |
| `transformations` | 此屬性包含需要應用於資料的各種轉換。 將不符合XDM的資料帶入平台時需要此屬性。 |
| `transformations.name` | 分配給轉換的名稱。 |
| `transformations.params.mappingId` | 的 [映射ID](#mapping) 生成。 |
| `transformations.params.mappingVersion` | 映射ID的相應版本。 此值預設為 `0`。 |

**回應**

成功的響應返回ID(`id`)。 您可以使用此ID監視、更新或刪除資料流。

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

### 獲取流終結點URL

建立資料流後，現在可以檢索流終結點URL。 您將使用此終結點URL將源訂閱到webhook，從而允許源與Experience Platform通信。

要檢索流終結點URL，請向 `/flows` 並提供資料流的ID。

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

成功的響應將返回有關資料流的資訊，包括標籤為的終結點URL `inletUrl`。

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

以下部分提供了有關可以執行哪些步驟來監視、更新和刪除資料流的資訊。

### 監視資料流

建立資料流後，您可以監視正在通過其接收的資料，以查看有關流運行、完成狀態和錯誤的資訊。 有關完整的API示例，請閱讀上的指南 [使用API監視源資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html)。

### 更新資料流

通過向發出PATCH請求，更新資料流的詳細資訊，如其名稱和說明，以及其運行計畫和關聯映射集 `/flows` 端點 [!DNL Flow Service] API，同時提供資料流的ID。 發出PATCH請求時，必須提供資料流的唯一性 `etag` 的 `If-Match` 標題。 有關完整的API示例，請閱讀上的指南 [使用API更新源資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### 更新帳戶

通過執行對的PATCH請求，更新源帳戶的名稱、說明和憑據 [!DNL Flow Service] API，同時將基本連接ID作為查詢參數提供。 發出PATCH請求時，必須提供源帳戶的唯一 `etag` 的 `If-Match` 標題。 有關完整的API示例，請閱讀上的指南 [使用API更新源帳戶](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html)。

### 刪除資料流

通過執行DELETE請求刪除資料流 [!DNL Flow Service] API，同時提供要作為查詢參數一部分刪除的資料流的ID。 有關完整的API示例，請閱讀上的指南 [使用API刪除資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html)。

### 刪除帳戶

通過執行DELETE請求刪除帳戶 [!DNL Flow Service] API，同時提供要刪除的帳戶的基本連接ID。 有關完整的API示例，請閱讀上的指南 [使用API刪除源帳戶](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html)。
