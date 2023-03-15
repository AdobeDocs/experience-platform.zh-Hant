---
title: 個人化概覽
description: 了解如何使用Adobe Experience Platform Edge Network Server API，從Adobe個人化解決方案擷取個人化內容。
exl-id: 11be9178-54fe-49d0-b578-69e6a8e6ab90
source-git-commit: f36892103b0b202550c07a70538c97b1cc673840
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 9%

---

# 個人化概覽

使用 [!DNL Server API]，您可以從Adobe個人化解決方案中擷取個人化內容，包括 [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) 和 [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=en).

此外， [!DNL Server API] 透過Adobe Experience Platform個人化目的地(例如 [Adobe Target](../destinations/catalog/personalization/adobe-target-connection.md) 和 [自訂個人化連線](../destinations/catalog/personalization/custom-personalization.md). 若要了解如何為同一頁和下一頁個人化設定Experience Platform，請參閱 [專屬指南](../destinations/ui/configure-personalization-destinations.md).

使用伺服器API時，您必須整合個人化引擎提供的回應與用於呈現網站內容的邏輯。 不同於 [Web SDK](../edge/home.md), [!DNL Server API] 沒有自動套用傳回之內容的機制 [!DNL Adobe Target] 和 [!DNL Offer Decisioning].

## 術語 {#terminology}

使用Adobe個人化解決方案之前，請務必了解下列概念：

* **優惠方案**：優惠方案是行銷訊息，其中可能包含與其關聯的規則，以指定誰有資格檢視選件。
* **決策**:決策（先前稱為優惠方案活動）會通知您選擇優惠方案。
* **結構**:決策結構會通知傳回的選件類型。
* **範圍**:決定的範圍。
   * 在Adobe Target，這是 [!DNL mbox]. 此 [!DNL global mbox] 是 `__view__` 範圍
   * 針對 [!DNL Offer Decisioning]，這些是以Base64編碼的JSON字串，其中包含您要讓offer decisioning服務用來建議選件的活動和位置ID。

## 此 `query` 物件 {#query-object}

擷取個人化內容需要要求範例的明確要求查詢物件。 查詢對象的格式如下：

```json
{
   "query":{
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "alloyStore",
            "siteWide",
            "__view__",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ"
         ]
      }
   }
}
```

| 屬性 | 類型 | 必填/選填 | 說明 |
| --- | --- | --- | ---|
| `schemas` | `String[]` | Target個人化必要項目。 選填Offer decisioning。 | 決策中使用的結構清單，以選取傳回的選件類型。 |
| `scopes` | `String[]` | 選填 | 決策範圍清單。 每個請求最多30個。 |

## 句柄對象 {#handle}

從個人化解決方案擷取的個人化內容會顯示在 `personalization:decisions` handle，其有效負載的格式如下：

```json
{
   "type":"personalization:decisions",
   "payload":[
      {
         "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
         "scope":"__view__",
         "scopeDetails":{
            "decisionProvider":"TGT",
            "activity":{
               "id":"131010"
            },
            "experience":{
               "id":"0"
            },
            "strategies":[
               {
                  "algorithmID":"0",
                  "trafficType":"0"
               }
            ]
         },
         "items":[
            {
               "id":"0",
               "schema":"https://ns.adobe.com/personalization/dom-action",
               "meta":{
                  "offer.name":"Default Content",
                  "experience.id":"0",
                  "activity.name":"Luma target reporting",
                  "activity.id":"131010",
                  "experience.name":"Experience A",
                  "option.id":"2",
                  "offer.id":"0"
               },
               "data":{
                  "type":"setHtml",
                  "format":"application/vnd.adobe.target.dom-action",
                  "content":"Customer Service not chrome",
                  "selector":"HTML > BODY > DIV.page-wrapper:eq(0) > FOOTER.page-footer:eq(0) > DIV.footer:eq(0) > DIV.links:eq(0) > DIV.widget:eq(0) > UL.footer:eq(0) > LI.nav:eq(1) > A:nth-of-type(1)",
                  "prehidingSelector":"HTML > BODY > DIV:nth-of-type(1) > FOOTER:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > UL:nth-of-type(1) > LI:nth-of-type(2) > A:nth-of-type(1)"
               }
            }
         ]
      }
   ]
}
```

| 屬性 | 類型 | 說明 |
| --- | --- | --- |
| `payload.id` | 字串 | 決策ID。 |
| `payload.scope` | 字串 | 產生提議的決定範圍。 |
| `payload.scopeDetails.decisionProvider` | 字串 | 設為 `TGT` 使用Adobe Target時。 |
| `payload.scopeDetails.activity.id` | 字串 | 優惠方案活動的唯一ID。 |
| `payload.scopeDetails.experience.id` | 字串 | 優惠方案版位的唯一ID。 |
| `items[].id` | 字串 | 優惠方案版位的唯一ID。 |
| `items[].data.id` | 字串 | 建議選件的ID。 |
| `items[].data.schema` | 字串 | 與建議選件相關聯的內容綱要。 |
| `items[].data.format` | 字串 | 與建議選件相關聯的內容格式。 |
| `items[].data.language` | 字串 | 與建議選件之內容相關聯的語言陣列。 |
| `items[].data.content` | 字串 | 以字串格式與建議的選件相關聯的內容。 |
| `items[].data.selector` | 字串 | HTML選取器，用來識別DOM動作選件的目標DOM元素。 |
| `items[].data.prehidingSelector` | 字串 | HTML選取器，用於在處理DOM動作選件時識別要隱藏的DOM元素。 |
| `items[].data.deliveryUrl` | 字串 | 以URL格式與建議的選件相關聯的影像內容。 |
| `items[].data.characteristics` | 字串 | 與建議的選件相關聯的特性，為JSON物件格式。 |

## 範例API呼叫 {#sample-call}

**API格式**

```http
POST /ee/v2/interact
```

### 請求 {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}"
-H "Authorization: Bearer {TOKEN}"
-H "x-gw-ims-org-id: {ORG_ID}"
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "event":{
      "xdm":{
         "identityMap":{
            "Email_LC_SHA256":[
               {
                  "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                  "primary":true
               }
            ]
         },
         "eventType":"web.webpagedetails.pageViews",
         "web":{
            "webPageDetails":{
               "URL":"https://alloystore.dev/",
               "name":"home-demo-Home Page"
            }
         },
         "timestamp":"2021-08-09T14:09:20.859Z"
      }
   },
   "query":{
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "__view__",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ"
         ]
      }
   }
}'
```

| 參數 | 類型 | 必填 | 說明 |
| --- | --- | --- | --- |
| `configId` | 字串 | 是 | 資料流ID。 |
| `requestId` | 字串 | 無 | 提供外部請求追蹤ID。 若未提供，邊緣網路將為您產生一個，並傳回回回應內文/標題。 |

### 回應 {#response}

傳回 `200 OK` 狀態和一個或多個 `Handle` 物件，視資料流設定中啟用的邊緣服務而定。

```json
{
   "requestId":"da20d11d-adac-458c-91ac-15bf4e420a15",
   "handle":[
      {
         "payload":[
            {
               "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
               "scope":"__view__",
               "scopeDetails":{
                  "decisionProvider":"TGT",
                  "activity":{
                     "id":"131010"
                  },
                  "experience":{
                     "id":"0"
                  },
                  "strategies":[
                     {
                        "algorithmID":"0",
                        "trafficType":"0"
                     }
                  ]
               },
               "items":[
                  {
                     "id":"0",
                     "schema":"https://ns.adobe.com/personalization/dom-action",
                     "meta":{
                        "offer.name":"Default Content",
                        "experience.id":"0",
                        "activity.name":"Luma target reporting",
                        "activity.id":"131010",
                        "experience.name":"Experience A",
                        "option.id":"2",
                        "offer.id":"0"
                     },
                     "data":{
                        "type":"setHtml",
                        "format":"application/vnd.adobe.target.dom-action",
                        "content":"Customer Service not chrome",
                        "selector":"HTML > BODY > DIV.page-wrapper:eq(0) > FOOTER.page-footer:eq(0) > DIV.footer:eq(0) > DIV.links:eq(0) > DIV.widget:eq(0) > UL.footer:eq(0) > LI.nav:eq(1) > A:nth-of-type(1)",
                        "prehidingSelector":"HTML > BODY > DIV:nth-of-type(1) > FOOTER:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > UL:nth-of-type(1) > LI:nth-of-type(2) > A:nth-of-type(1)"
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions"
      }
   ]
}
```

## 通知 {#notifications}

預先擷取的內容或檢視經造訪或呈現給一般使用者時，應觸發通知。 為了在正確的範圍內觸發通知，請務必追蹤對應的 `id` 每個範圍。

右側通知 `id` ，則必須觸發對應的範圍，才能正確反映報表。

**API格式**

```http
POST /ee/v2/collect
```

### 請求 {#notifications-request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "events":[
      {
         "xdm":{
            "identityMap":{
               "Email_LC_SHA256":[
                  {
                     "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                     "primary":true
                  }
               ]
            },
            "eventType":"web.webpagedetails.pageViews",
            "web":{
               "webPageDetails":{
                  "URL":"https://alloystore.dev/",
                  "name":"home-demo-Home Page"
               }
            },
            "timestamp":"2021-08-09T14:09:20.859Z",
            "_experience":{
               "decisioning":{
                  "propositions":[
                     {
                        "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                        "scope":"__view__",
                        "items":[
                           {
                              "id":"0"
                           }
                        ]
                     }
                  ]
               }
            }
         }
      }
   ]
}'
```

| 參數 | 類型 | 必填 | 說明 |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | 是 | 資料收集端點所使用資料流的ID。 |
| `requestId` | `String` | 無 | 外部請求跟蹤ID。 若未提供，邊緣網路將為您產生一個，並傳回回回應內文/標題。 |
| `silent` | `Boolean` | 無 | 可選布林參數，指示邊緣網路是否應返回 `204 No Content` 含有空裝載的回應。 使用對應的HTTP狀態代碼和裝載來報告嚴重錯誤。 |

### 回應 {#notifications-response}

成功的回應會傳回下列其中一種狀態，並傳回 `requestID` 如果要求中未提供任何項目。

* `202 Accepted` 請求成功處理時；
* `204 No Content` 成功處理請求時，以及 `silent` 參數設為 `true`;
* `400 Bad Request` 當請求未正確形成時（例如，找不到強制主要身分）。

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
