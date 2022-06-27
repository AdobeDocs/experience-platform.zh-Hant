---
title: 與Adobe Analytics互動
description: 瞭解如何使用邊緣網路伺服器API與Adobe Analytics交互。
exl-id: b5e7a4d0-9aea-4e70-a7d6-b9aad09aaddf
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 1%

---

# 與Adobe Analytics互動

## 總覽 {#overview}

Adobe Analytics的資料收集工作是將XDM資料轉換為Adobe Analytics能夠理解的格式。 幾個XDM欄位 [自動映射](../edge/data-collection/adobe-analytics/automatically-mapped-vars.md) 到分析變數。

您也可以 [手動映射XDM值](../edge/data-collection/adobe-analytics/manually-mapping-variables.md) 舊分析變數。

要使Adobe Analytics能夠從伺服器API接收資料，您需要 [配置資料流](../edge/datastreams/overview.md#adobe-analytics-settings) 要將事件轉發到Adobe Analytics，請在資料流配置頁中輸入報告套件ID。

![Adobe Analytics資料流配置](assets/analytics-datastream.png)

## 與Adobe Analytics互動 {#interacting-analytics}

### API格式 {#format}

```http
POST /ee/v2/interact?dataStreamId={DATASTREAM_ID}
```

### 請求 {#request}

下面的示例包括幾個自動映射的值 `_experience.analytics` 欄位組。 它還包括基於JSON的資料層。 雖然這些資料層無法自動映射，但可以使用 [資料收集的資料準備](../edge/datastreams/data-prep.md) 將這些值映射到包含上述欄位組的架構。

用戶映射到這些欄位的所有值將自動映射到相應的分析值，就像它們包含在API請求中一樣。

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

### 雷龐塞 {#response}

```json
{
   "requestId": "d2ad6364-5675-4a86-ba41-50e7a4c4a299",
   "handle": []
}
```
