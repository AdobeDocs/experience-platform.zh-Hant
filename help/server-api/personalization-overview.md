---
title: 個人化概覽
description: 瞭解如何使用Adobe Experience Platform Edge Network Server API從Adobe個人化解決方案擷取個人化內容。
exl-id: 11be9178-54fe-49d0-b578-69e6a8e6ab90
source-git-commit: 378f222b5c673632ce5792c52fc32410106def37
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 9%

---

# 個人化概覽

使用 [!DNL Server API]，您可以從Adobe個人化解決方案擷取個人化內容，包括 [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) 和 [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=en).

此外， [!DNL Server API] 透過Adobe Experience Platform個人化目的地，提供相同頁面和下一頁個人化功能，例如 [Adobe Target](../destinations/catalog/personalization/adobe-target-connection.md) 和 [自訂個人化連線](../destinations/catalog/personalization/custom-personalization.md). 若要瞭解如何為同頁和下一頁個人化設定Experience Platform，請參閱 [專用指南](../destinations/ui/activate-edge-personalization-destinations.md).

使用伺服器API時，您必須整合個人化引擎提供的回應，與用來呈現網站上內容的邏輯。 不喜歡 [Web SDK](../edge/home.md)，則 [!DNL Server API] 沒有自動套用傳回內容的機制 [!DNL Adobe Target] 和 [!DNL Offer Decisioning].

## 術語 {#terminology}

在使用Adobe個人化解決方案之前，請務必瞭解以下概念：

* **優惠方案**：優惠方案是行銷訊息，其中可能包含與其關聯的規則，以指定誰有資格檢視選件。
* **決定**：決定（先前稱為優惠活動）會通知優惠選擇。
* **結構描述**：決定的結構描述會通知傳回的優惠型別。
* **範圍**：決定的範圍。
   * 在Adobe Target中，這是 [!DNL mbox]. 此 [!DNL global mbox] 是 `__view__` 範圍
   * 對象 [!DNL Offer Decisioning]，這些是JSON的Base64編碼字串，包含您希望offer decisioning服務用來建議選件的活動和位置ID。

## 此 `query` 物件 {#query-object}

擷取個人化內容需要請求範例的明確請求查詢物件。 查詢物件具有下列格式：

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
| `schemas` | `String[]` | Target個人化的必要專案。 選填Offer decisioning。 | 用於決定中的結構描述清單，以選取傳回的優惠型別。 |
| `scopes` | `String[]` | 選填 | 決定範圍清單。 每個請求最多30個。 |

## 控制代碼物件 {#handle}

從個人化解決方案中擷取的個人化內容會顯示在 `personalization:decisions` 控點，其裝載格式如下：

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
| `payload.id` | 字串 | 決定ID。 |
| `payload.scope` | 字串 | 導致建議優惠方案的決定範圍。 |
| `payload.scopeDetails.decisionProvider` | 字串 | 設定為 `TGT` 使用Adobe Target時。 |
| `payload.scopeDetails.activity.id` | 字串 | 優惠活動的唯一ID。 |
| `payload.scopeDetails.experience.id` | 字串 | 優惠方案位置的唯一ID。 |
| `items[].id` | 字串 | 優惠方案位置的唯一ID。 |
| `items[].data.id` | 字串 | 建議優惠方案的ID。 |
| `items[].data.schema` | 字串 | 與建議選件相關聯的內容結構描述。 |
| `items[].data.format` | 字串 | 與建議選件相關聯的內容格式。 |
| `items[].data.language` | 字串 | 與建議選件內容相關的一系列語言。 |
| `items[].data.content` | 字串 | 以字串格式與建議選件相關聯的內容。 |
| `items[].data.selector` | 字串 | HTML選取器用來識別DOM動作選件的目標DOM元素。 |
| `items[].data.prehidingSelector` | 字串 | HTML選擇器，用於識別在處理DOM動作選件時要隱藏的DOM元素。 |
| `items[].data.deliveryUrl` | 字串 | 以URL格式呈現與建議選件相關聯的影像內容。 |
| `items[].data.characteristics` | 字串 | 與JSON物件格式的建議選件相關聯的特性。 |

## API呼叫範例 {#sample-call}

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
| `configId` | 字串 | 是 | 資料串流ID。 |
| `requestId` | 字串 | 無 | 提供外部要求追蹤ID。 如果未提供，Edge Network會為您產生回應，並將其傳回至回應內文/標頭。 |

### 回應 {#response}

傳回 `200 OK` 狀態與一或多個 `Handle` 物件，視在資料流設定中啟用的邊緣服務而定。

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

當使用者造訪或呈現預先擷取的內容或檢視時，應觸發通知。 為了在正確的範圍內引發通知，請務必追蹤對應的 `id` 用於每個範圍。

具有右側的通知 `id` 必須引發對應範圍的「 」，才能正確反映報表。

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
| `dataStreamId` | `String` | 是 | 資料收集端點使用的資料串流的ID。 |
| `requestId` | `String` | 無 | 外部外部請求追蹤ID。 如果未提供，Edge Network會為您產生回應，並將其傳回至回應內文/標頭。 |
| `silent` | `Boolean` | 無 | 選用的布林值引數，指出Edge Network是否應該傳回 `204 No Content` 以空白承載回應。 系統會使用對應的HTTP狀態代碼和裝載來報告嚴重錯誤。 |

### 回應 {#notifications-response}

成功回應會傳回下列其中一種狀態，以及 `requestID` 請求中未提供任何請求時。

* `202 Accepted` 成功處理要求時；
* `204 No Content` 成功處理要求時，且 `silent` 引數已設為 `true`；
* `400 Bad Request` 要求格式不正確時（例如，找不到必要的主要身分）。

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
