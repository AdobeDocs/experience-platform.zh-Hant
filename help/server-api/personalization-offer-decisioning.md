---
title: 通過Offer decisioning個性化
description: 瞭解如何使用伺服器API通過Offer decisioning提供和呈現個性化體驗。
exl-id: 5348cd3e-08db-4778-b413-3339cb56b35a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 2%

---

# 通過Offer decisioning個性化

## 總覽 {#overview}

邊緣網路伺服器API可提供在 [offer decisioning](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=en) 到Web頻道。

[!DNL Offer Decisioning] 支援一個非可視介面，以建立、激活和提供您的活動和個性化體驗。

## 配置資料流 {#configure-your-datastream}

在將伺服器API與Offer decisioning結合使用之前，必須在資料流配置上啟用Adobe Experience Platform個性化，並啟用 **[!UICONTROL offer decisioning]** 的雙曲餘切值。

查看 [將服務添加到資料流的指南](../edge/datastreams/overview.md#adobe-experience-platform-settings)，以獲取有關如何啟用Offer decisioning的詳細資訊。

![顯示資料流服務配置螢幕的UI影像，已選擇Offer decisioning](assets/aep-od-datastream.png)

## 建立對象 {#audience-creation}

[!DNL Offer Decisioning] 依靠Adobe Experience Platform分類服務來創造觀眾。 您可以找到 [!DNL Segmentation Service] [這裡](../segmentation/home.md)。

## 定義決策範圍 {#creating-decision-scopes}

的 [!DNL Offer Decision Engine] 使用Adobe Experience Platform資料 [即時客戶配置檔案](../profile/home.md)，以及 [!DNL Offer Library]，在適當的時間向適當的客戶和渠道提供優惠。

瞭解有關 [!DNL Offer Decisioning Engine]，請參閱 [文檔](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=zh-Hant)。

之後 [配置資料流](#configure-your-datastream)，您必須定義要在個性化市場活動中使用的決策範圍。

[決策範圍](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/create-manage-activities/create-offer-activities.html?lang=en#add-decision-scopes) 是Base64編碼的JSON字串，包含您希望的活動和位置ID [!DNL Offer Decisioning Service] 在提出要約時使用。

**決策範圍JSON**

```json
{
   "activityId":"xcore:offer-activity:11cfb1fa93381aca",
   "placementId":"xcore:offer-placement:1175009612b0100c"
}
```

**決策範圍Base64編碼字串**

```shell
"eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
```

在建立優惠和收集後，您需要定義 [決策範圍](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/create-manage-activities/create-offer-activities.html?lang=en#add-decision-scopes)。

複製Base64編碼的決策範圍。 您將在 `query` 伺服器API請求的對象。

![顯示Offer decisioningUI的UI影像，突出顯示決策範圍。](assets/decision-scope.png)

```json
"query":{
   "personalization":{
      "decisionScopes":[
         "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9"
      ]
   }
}
```

## API調用示例 {#api-example}

**API格式**

```http
POST /ee/v2/interact
```

### 請求 {#request}

下面概述了包含完整XDM對象、資料對象和Offer decisioning查詢的完整請求。

>[!NOTE]
>
>的 `xdm` 和 `data` 對象是可選的，並且僅當您建立的段具有在其中任何一個對象中使用欄位的條件時，才需要Offer decisioning。

```shell
curl -X POST 'https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org: {ORG_ID}' \
--header 'Authorization: Bearer {TOKEN}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "event": {
        "xdm": {
            "eventType": "web.webpagedetails.pageViews",
            "identityMap": {
                "ECID": [
                    {
                        "id": "05907638112924484241029082405297151763",
                        "authenticatedState": "ambiguous",
                        "primary": true
                    }
                ]
            },
            "web": {
                "webPageDetails": {
                    "URL": "https://alloystore.dev",
                    "name": "Home Page"
                },
                "webReferrer": {
                    "URL": ""
                }
            },
            "device": {
                "screenHeight": 1440,
                "screenWidth": 3440,
                "screenOrientation": "landscape"
            },
            "environment": {
                "type": "browser",
                "browserDetails": {
                    "viewportWidth": 3440,
                    "viewportHeight": 1440
                }
            },
            "placeContext": {
                "localTime": "2022-03-22T22:45:21.193-06:00",
                "localTimezoneOffset": 360
            },
            "timestamp": "2022-03-23T04:45:21.193Z",
            "implementationDetails": {
                "name": "https://ns.adobe.com/experience/alloy/reactor",
                "version": "1.0",
                "environment": "serverapi"
            }
        },
        "data": {
            "page": {
                "pageInfo": {
                    "pageName": "Promotions",
                    "siteSection": "Home"
                },
                "promos": {
                    "heroPromos": "purse,shoes,sunglasses"
                },
                "customVariables": {
                    "testGroup": "orange/black theme"
                },
                "events": {
                    "homePage": true
                },
                "products": [
                    {
                        "productSKU": "abc123",
                        "productName": "shirt"
                    }
                ]
            },
            "__adobe.target": {
                "profile.eyeColor": "brown",
                "profile.hairColor": "brown"
            }
        }
    },
    "query": {
        "personalization": {
            "decisionScopes": [
                "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9"
            ]
        }
    }
}'
```

### 回應 {#response}

邊緣網路將返回與下面類似的響應。

```json
{
   "requestId":"b375077d-7e1d-4c18-b7d3-e4da0fb4fbc5",
   "handle":[
      {
         "payload":[
            
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      },
      {
         "payload":[
            {
               "id":"120d5db7-181c-42c5-8653-88b3cd3e1e69",
               "scope":"eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9",
               "activity":{
                  "id":"xcore:offer-activity:14efca8941895181",
                  "etag":"1"
               },
               "placement":{
                  "id":"xcore:offer-placement:12d544ae54e7e7db",
                  "etag":"1"
               },
               "items":[
                  {
                     "id":"xcore:personalized-offer:14efc848a3577d92",
                     "etag":"2",
                     "schema":"https://ns.adobe.com/experience/offer-management/content-component-json",
                     "data":{
                        "id":"xcore:personalized-offer:14efc848a3577d92",
                        "format":"application/json",
                        "language":[
                           "en-us"
                        ],
                        "content":"{\n\t\"ODEFirstTest\" : \"Personalizaton Content\"\n}",
                        "characteristics":{
                           "reporting":"testRequest"
                        }
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      },
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiYwNTkwNzYzODExMjkyNDQ4NDI0MTAyOTA4MjQwNTI5NzE1MTc2M1IOCLr6xb39LxgBKgNPUjLwAbr6xb39Lw==",
               "maxAge":34128000
            }
         ],
         "type":"state:store"
      }
   ]
}
```

如果訪問者有資格根據發送到的資料進行個性化設定活動 [!DNL Offer Decisioning]，相關活動內容將在 `handle` 對象，其中類型為 `personalization:decisions`。

其他內容將在 `handle` 對象也一樣。 其他內容類型與 [!DNL Offer Decisioning] 個性化。 如果訪問者有資格進行多項活動，則這些活動將包含在陣列中。

下表說明了該部分答復的關鍵要素。

| 屬性 | 說明 | 範例 |
|---|---|---|
| `scope` | 與已退回的建議要約關聯的決定範圍。 | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | 優惠活動的唯一ID。 | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | 聘用位置的唯一ID。 | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | 建議的服務的唯一ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | 與建議的優惠關聯的內容的模式。 | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | 建議的服務的唯一ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | 與建議的優惠關聯的內容的格式。 | `"format": "text/html"` |
| `language` | 與建議的服務內容關聯的一組語言。 | `"language": [ "en-US" ]` |
| `content` | 以字串格式與建議的優惠關聯的內容。 | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | 以URL格式與建議的優惠相關聯的影像內容。 | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | JSON對象包含與建議的服務關聯的特性。 | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |
