---
title: 與Adobe Analytics互動
description: 瞭解如何使用Edge Network伺服器API與Adobe Analytics互動。
exl-id: b5e7a4d0-9aea-4e70-a7d6-b9aad09aaddf
source-git-commit: 5de1ec17b78c97be21c0d2afd6f0b119a6074b6f
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 1%

---

# 與Adobe Analytics互動

## 概觀 {#overview}

Adobe Analytics資料收集的運作方式是將XDM資料轉譯成Adobe Analytics可以理解的格式。 多個XDM欄位是[自動對應到Analytics變數的](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html)。 您也可以手動將XDM值對應至舊版Analytics變數。

若要讓Adobe Analytics能夠接收來自伺服器API的資料，您需要[設定資料流](../datastreams/overview.md#adobe-analytics-settings)，以在資料流設定頁面中輸入報表套裝ID，將事件轉送至Adobe Analytics。

![Adobe Analytics資料流組態](assets/analytics-datastream.png)

## 與Adobe Analytics互動 {#interacting-analytics}

### API格式 {#format}

```http
POST /ee/v2/interact?dataStreamId={DATASTREAM_ID}
```

### 請求 {#request}

下列範例包含來自`_experience.analytics`欄位群組的數個自動對應值。 它也包括以JSON為基礎的資料層。 雖然這些資料層無法自動對應，但可以使用[資料收集的資料準備](../datastreams/data-prep.md)將這些值對應到包含上述欄位群組的結構描述。

使用者對應到這些欄位的所有值都會自動對應到適當的Analytics值，就像這些值包含在API請求中一樣。

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" \
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" \
-d '{
   "event": {
      "xdm": {
         "eventType": "web.webpagedetails.pageViews",
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
            "version": "2.8.0+2.9.0",
            "environment": "browser"
         },
         "_experience": {
            "analytics": {
               "customDimensions": {
                  "eVars": {
                     "eVar14": "eVar14"
                  }
               },
               "event1to100": {
                  "event13": {
                     "value": 1
                  },
                  "event14": {
                     "value": 2
                  }
               }
            }
         }
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
      }
   }
}'
```

### 回應 {#response}

```json
{
   "requestId": "d2ad6364-5675-4a86-ba41-50e7a4c4a299",
   "handle": []
}
```
