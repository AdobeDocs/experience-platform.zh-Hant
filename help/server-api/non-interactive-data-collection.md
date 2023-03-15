---
title: 非互動式資料收集
description: 了解Adobe Experience Platform Edge Network Server API如何執行非互動式資料收集。
exl-id: 1a704e8f-8900-4f56-a843-9550007088fe
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 4%

---

# 非互動式資料收集

## 總覽 {#overview}

非互動式事件資料收集端點可用來傳送多個事件以Experience Platform資料集或其他插座。

若一般使用者事件在本機排入短時間佇列（例如沒有網路連線），則建議以批次傳送事件。

批次事件不一定屬於相同的一般使用者，這表示事件在其中可包含不同的身分 `identityMap` 物件。

## 非互動式API呼叫範例 {#example}

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
| `dataStreamId` | `String` | 是 | 資料收集端點所使用資料流的ID。 |
| `requestId` | `String` | 無 | 提供外部請求追蹤ID。 若未提供，邊緣網路將為您產生一個，並傳回回回應內文/標題。 |
| `silent` | `Boolean` | 無 | 可選布林參數，指示邊緣網路是否應返回 `204 No Content` 回應是否含有空裝載。 使用對應的HTTP狀態代碼和裝載來報告嚴重錯誤。 |


### 回應 {#response}

成功的回應會傳回下列其中一種狀態，並傳回 `requestID` 如果要求中未提供任何項目。

* `202 Accepted` 請求成功處理時；
* `204 No Content` 成功處理請求時，以及 `silent` 參數設為 `true`;
* `400 Bad Request` 當請求未正確形成時（例如，找不到強制主要身分）。

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
