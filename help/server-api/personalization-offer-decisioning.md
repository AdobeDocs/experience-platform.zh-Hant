---
title: Personalization (透過Offer Decisioning)
description: 瞭解如何使用伺服器API，透過Offer decisioning傳遞及呈現個人化體驗。
exl-id: 5348cd3e-08db-4778-b413-3339cb56b35a
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 1%

---

# Personalization (透過Offer Decisioning)

## 概觀 {#overview}

Edge Network伺服器API可將以[Offer decisioning](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=zh-Hant)管理的個人化體驗傳送至網路頻道。

[!DNL Offer Decisioning]支援非視覺化介面，以建立、啟用及傳遞您的活動和個人化體驗。

## 先決條件 {#prerequisites}

設定整合之前，透過[!DNL Offer Decisioning]的Personalization需要您擁有[Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=zh-Hant)的存取權。

## 設定您的資料串流 {#configure-your-datastream}

您必須先在資料流組態上啟用Adobe Experience Platform個人化，並啟用&#x200B;**[!UICONTROL Offer decisioning]**&#x200B;選項，才能搭配使用Server API與Offer decisioning。

如需如何啟用Offer decisioning的詳細資訊，請參閱將服務新增至資料流](../datastreams/overview.md#adobe-experience-platform-settings)的[指南。

![顯示資料流服務設定畫面的UI影像，已選取Offer decisioning](assets/aep-od-datastream.png)

## 對象建立 {#audience-creation}

[!DNL Offer Decisioning]仰賴Adobe Experience Platform Segmentation Service建立對象。 您可以在[這裡](../segmentation/home.md)找到[!DNL Segmentation Service]的檔案。

## 定義決定範圍 {#creating-decision-scopes}

[!DNL Offer Decision Engine]使用Adobe Experience Platform資料、[即時客戶設定檔](../profile/home.md)以及[!DNL Offer Library]，在適當的時間將優惠方案提供給適當的客戶和管道。

若要深入瞭解[!DNL Offer Decisioning Engine]，請參閱專屬的[檔案](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=zh-Hant)。

在[設定您的資料流](#configure-your-datastream)之後，您必須定義要用於個人化行銷活動中的決定範圍。

[決定範圍](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/create-manage-activities/create-offer-activities.html#add-decision-scopes)是Base64編碼的JSON字串，其中包含您希望[!DNL Offer Decisioning Service]在提出優惠方案時使用的活動和位置ID。

**決定範圍JSON**

```json
{
   "activityId":"xcore:offer-activity:11cfb1fa93381aca",
   "placementId":"xcore:offer-placement:1175009612b0100c"
}
```

**決定範圍Base64編碼的字串**

```shell
"eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
```

建立優惠和集合後，您需要定義[決定範圍](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/create-manage-activities/create-offer-activities.html#add-decision-scopes)。

複製Base64編碼的決定範圍。 您會在伺服器API要求的`query`物件中使用它。

![顯示Offer decisioningUI的UI影像，強調決定範圍。](assets/decision-scope.png)

```json
"query":{
   "personalization":{
      "decisionScopes":[
         "eyJ4ZG06YWN0aXZpdHlJZCI6Inhjb3JlOm9mZmVyLWFjdGl2aXR5OjE0ZWZjYTg5NDE4OTUxODEiLCJ4ZG06cGxhY2VtZW50SWQiOiJ4Y29yZTpvZmZlci1wbGFjZW1lbnQ6MTJkNTQ0YWU1NGU3ZTdkYiJ9"
      ]
   }
}
```

## API呼叫範例 {#api-example}

**API格式**

```http
POST /ee/v2/interact
```

### 請求 {#request}

包含完整XDM物件、資料物件和Offer decisioning查詢的完整請求概述如下。

>[!NOTE]
>
>`xdm`和`data`物件是選用專案，只有在您已建立區段，且區段的條件在其中任何一個物件中使用欄位時，才需要Offer decisioning。

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

Edge Network會傳回類似以下的回應。

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

如果訪客根據傳送至[!DNL Offer Decisioning]的資料符合個人化活動的資格，則會在`handle`物件下找到相關活動內容，其中型別為`personalization:decisions`。

其他內容也會傳回`handle`物件下。 其他內容型別與[!DNL Offer Decisioning]個人化無關。 如果訪客符合多個活動的資格，則會將其包含在陣列中。

下表說明該部分回應的主要元素。

| 屬性 | 說明 | 範例 |
|---|---|---|
| `scope` | 與傳回的建議優惠方案相關的決定範圍。 | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | 優惠活動的唯一ID。 | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | 優惠方案位置的唯一ID。 | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | 建議優惠方案的唯一ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | 與建議選件相關之內容的結構描述。 | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | 建議優惠方案的唯一ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | 與建議選件相關聯的內容格式。 | `"format": "text/html"` |
| `language` | 與建議選件內容關聯的一系列語言。 | `"language": [ "en-US" ]` |
| `content` | 以字串格式與建議選件相關聯的內容。 | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | 以URL格式呈現與建議選件相關聯的影像內容。 | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | JSON物件，其中包含與建議選件相關聯的特性。 | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |
