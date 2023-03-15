---
title: 互動式資料收集
description: 了解Adobe Experience Platform Edge Network Server API如何執行互動式資料收集。
exl-id: 1b06e755-b6a9-42dd-96c1-98ad67e7d222
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 6%

---

# 互動式資料收集

## 總覽 {#overview}

互動式資料收集端點會接收單一事件，並在用戶端預期Adobe Experience Platform邊緣網路伺服器會傳回回應時使用。 執行資料收集時，這些端點也可以從其他Experience Edge服務傳回內容。

伺服器響應包括一個或多個 `Handle` 物件，如下所示。

## API呼叫範例

### API格式 {#format}

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
   "event": {
      "xdm": {
         "identityMap": {
            "Email_LC_SHA256": [
               {
                  "id": "0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                  "primary": true
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
   }
}'
```

| 參數 | 類型 | 必填 | 說明 |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | 可以。 | 資料流ID。 |
| `requestId` | `String` | 無 | 提供用於關聯內部伺服器請求的用戶端隨機ID。 若未提供，邊緣網路將產生一個，並在回應中傳回。 |

### 回應 {#response}

成功的回應會傳回HTTP狀態 `200 OK`，包含一或多個 `Handle` 物件，視資料流設定中啟用的即時邊緣服務而定。

```json
{
   "requestId": "c85402f5-83a1-4fb3-abdd-f4c17bf6dd49",
   "handle": []
}
```
