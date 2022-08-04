---
title: 個性化概述
description: 瞭解如何使用Adobe Experience Platform邊緣網路伺服器API從Adobe個性化解決方案中檢索個性化內容。
exl-id: 11be9178-54fe-49d0-b578-69e6a8e6ab90
source-git-commit: f36892103b0b202550c07a70538c97b1cc673840
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 個性化概述

使用 [!DNL Server API]，您可以從Adobe個性化解決方案中檢索個性化內容，包括 [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) 和 [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=en)。

此外， [!DNL Server API] 通過Adobe Experience Platform個性化目標(如 [Adobe Target](../destinations/catalog/personalization/adobe-target-connection.md) 和 [自定義個性化連接](../destinations/catalog/personalization/custom-personalization.md)。 要瞭解如何為同頁和下一頁個性化配置Experience Platform，請參閱 [專用指南](../destinations/ui/configure-personalization-destinations.md)。

使用伺服器API時，必須將個性化引擎提供的響應與用於在站點上呈現內容的邏輯整合。 與 [Web SDK](../edge/home.md)，也請參見Wiki頁。 [!DNL Server API] 沒有自動應用返回的內容的機制 [!DNL Adobe Target] 和 [!DNL Offer Decisioning]。

## 術語 {#terminology}

在使用Adobe個性化解決方案之前，請確保瞭解以下概念：

* **優惠方案**：優惠方案是行銷訊息，其中可能包含與其關聯的規則，以指定誰有資格檢視選件。
* **決定**:決定（以前稱為要約活動）通知要約的選擇。
* **架構**:決策的模式通知返回的要約類型。
* **範圍**:決定的範圍。
   * 在Adobe Target，這是 [!DNL mbox]。 的 [!DNL global mbox] 是 `__view__` 範圍
   * 對於 [!DNL Offer Decisioning]，這些是Base64編碼的JSON字串，包含您希望offer decisioning服務用於建議聘用的活動和位置ID。

## 的 `query` 對象 {#query-object}

檢索個性化內容需要請求示例的顯式請求查詢對象。 查詢對象具有以下格式：

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
| `schemas` | `String[]` | 目標個性化要求。 可選Offer decisioning。 | 在決策中使用的方案清單，用於選擇返回的聘用類型。 |
| `scopes` | `String[]` | 選填 | 決策範圍清單。 每個請求最多30個。 |

## 句柄對象 {#handle}

從個性化解決方案中檢索到的個性化內容被呈現在 `personalization:decisions` handle，其負載具有以下格式：

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
| `payload.scope` | 字串 | 導致提議的報價的決定範圍。 |
| `payload.scopeDetails.decisionProvider` | 字串 | 設定為 `TGT` 用Adobe Target。 |
| `payload.scopeDetails.activity.id` | 字串 | 優惠活動的唯一ID。 |
| `payload.scopeDetails.experience.id` | 字串 | 聘用位置的唯一ID。 |
| `items[].id` | 字串 | 聘用位置的唯一ID。 |
| `items[].data.id` | 字串 | 建議的報價的ID。 |
| `items[].data.schema` | 字串 | 與建議的優惠關聯的內容的模式。 |
| `items[].data.format` | 字串 | 與建議的優惠關聯的內容的格式。 |
| `items[].data.language` | 字串 | 與建議的服務內容關聯的一組語言。 |
| `items[].data.content` | 字串 | 以字串格式與建議的優惠關聯的內容。 |
| `items[].data.selector` | 字串 | HTML選擇器，用於標識DOM操作提供的目標DOM元素。 |
| `items[].data.prehidingSelector` | 字串 | HTML選擇器，用於在處理DOM操作提供時標識要隱藏的DOM元素。 |
| `items[].data.deliveryUrl` | 字串 | 以URL格式與建議的優惠相關聯的影像內容。 |
| `items[].data.characteristics` | 字串 | 與JSON對象格式的建議提供關聯的特性。 |

## 示例API調用 {#sample-call}

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
| `requestId` | 字串 | 無 | 提供外部請求跟蹤ID。 如果未提供，則邊緣網路將為您生成一個，並將其返回到響應正文/標頭中。 |

### 回應 {#response}

返回 `200 OK` 狀態和一個或多個 `Handle` 對象，具體取決於在資料流配置中啟用的邊緣服務。

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

當預取的內容或視圖已訪問或呈現給最終用戶時，應觸發通知。 為了在適當範圍內關閉通知，請確保跟蹤相應的 `id` 每個範圍。

右邊的通知 `id` 為了正確反映報告，需要觸發相應的範圍。

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
| `dataStreamId` | `String` | 是 | 資料收集終結點使用的資料流的ID。 |
| `requestId` | `String` | 無 | 外部請求跟蹤ID。 如果未提供，則邊緣網路將為您生成一個，並將其返回到響應正文/標頭中。 |
| `silent` | `Boolean` | 無 | 指示邊緣網路是否應返回的可選布爾參數 `204 No Content` 空負載響應。 使用相應的HTTP狀態代碼和負載報告嚴重錯誤。 |

### 回應 {#notifications-response}

成功的響應返回以下狀態之一，並返回 `requestID` 的下界。

* `202 Accepted` 請求成功處理時；
* `204 No Content` 成功處理請求時， `silent` 參數設定為 `true`;
* `400 Bad Request` 當請求未正確形成時（例如，找不到強制主標識）。

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
