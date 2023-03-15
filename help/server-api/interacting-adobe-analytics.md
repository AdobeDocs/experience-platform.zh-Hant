---
title: 與Adobe Analytics互動
description: 了解如何使用Edge Network Server API與Adobe Analytics互動。
exl-id: b5e7a4d0-9aea-4e70-a7d6-b9aad09aaddf
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 1%

---

# 與Adobe Analytics互動

## 總覽 {#overview}

Adobe Analytics資料收集的運作方式是將XDM資料轉譯為Adobe Analytics可理解的格式。 數個XDM欄位包括 [自動對應](../edge/data-collection/adobe-analytics/automatically-mapped-vars.md) 至Analytics變數。

您也可以 [手動對應XDM值](../edge/data-collection/adobe-analytics/manually-mapping-variables.md) 舊版Analytics變數。

若要讓Adobe Analytics能夠從伺服器API接收資料，您必須 [設定資料流](../edge/datastreams/overview.md#adobe-analytics-settings) 若要將事件轉送至Adobe Analytics，請在datastream設定頁面中輸入報表套裝ID。

![Adobe Analytics Datastream設定](assets/analytics-datastream.png)

## 與Adobe Analytics互動 {#interacting-analytics}

### API格式 {#format}

```http
POST /ee/v2/interact?dataStreamId={DATASTREAM_ID}
```

### 請求 {#request}

以下範例包含 `_experience.analytics` 欄位群組。 也包含JSON型資料層。 雖然這些資料層無法自動對應，但您仍可使用 [資料收集的資料準備](../edge/datastreams/data-prep.md) 將這些值映射到包含上述欄位組的架構。

使用者對應至這些欄位的所有值，都會自動對應至適當的Analytics值，就像這些值包含在API請求中一樣。

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
