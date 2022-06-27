---
title: 非互動式資料收集
description: 瞭解Adobe Experience Platform邊緣網路伺服器API如何執行非互動式資料收集。
exl-id: 1a704e8f-8900-4f56-a843-9550007088fe
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 4%

---

# 非互動式資料收集

## 總覽 {#overview}

非互動式事件資料收集端點用於將多個事件發送到Experience Platform資料集或其它插座。

建議在最終用戶事件在本地排隊一段短時間（例如，沒有網路連接時）時以批處理形式發送事件。

批處理事件不一定屬於同一最終用戶，這意味著事件可以在其中包含不同的身份 `identityMap` 的雙曲餘切值。

## 非互動式API調用示例 {#example}

### API格式 {#api-format}

```http
POST /ee/v2/collect
```

### 請求 {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" 
-d '{
   "events": [
      {
         "xdm": {
            "identityMap": {
               "FPID": [
                  {
                     "id": "79bf8e83-f708-414b-b1ed-5789ff33bf0b",
                     "primary": "true"
                  }
               ]
            },
            "eventType": "web.webpagedetails.pageViews",
            "web": {
               "webPageDetails": {
                  "URL": "https://alloystore.dev/",
                  "name": "home-demo-Home Page"
               }
            },
            "timestamp": "2021-08-09T14:09:20.859Z"
         },
         "data": {
            "prop1": "custom value"
         }
      },
      {
         "xdm": {
            "identityMap": {
               "FPID": [
                  {
                     "id": "871e8460-a329-4e96-a5b6-ff359fb0afb9",
                     "primary": "true"
                  }
               ]
            },
            "eventType": "web.webinteraction.linkClicks",
            "web": {
               "webInteraction": {
                  "linkClicks": {
                     "value": 1
                  }
               },
               "name": "My Custom Link",
               "URL": "https://myurl.com"
            },
            "timestamp": "2021-08-09T14:09:20.859Z"
         }
      }
   ]
}'
```

| 參數 | 類型 | 必填 | 說明 |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | 是 | 資料收集終結點使用的資料流的ID。 |
| `requestId` | `String` | 無 | 提供外部請求跟蹤ID。 如果未提供，則邊緣網路將為您生成一個，並將其返回到響應正文/標頭中。 |
| `silent` | `Boolean` | 無 | 指示邊緣網路是否應返回的可選布爾參數 `204 No Content` 響應是否為空負載。 使用相應的HTTP狀態代碼和負載報告嚴重錯誤。 |


### 回應 {#response}

成功的響應返回以下狀態之一，並返回 `requestID` 的下界。

* `202 Accepted` 請求成功處理時；
* `204 No Content` 成功處理請求時， `silent` 參數設定為 `true`;
* `400 Bad Request` 當請求未正確形成時（例如，找不到強制主標識）。

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
