---
title: 互動式資料收集
description: 瞭解Adobe Experience PlatformEdge Network伺服器API如何執行互動式資料收集。
exl-id: 1b06e755-b6a9-42dd-96c1-98ad67e7d222
source-git-commit: f8434746c4a023ec895d23a59e04fca4baecfc36
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 5%

---

# 互動式資料收集

## 概觀 {#overview}

互動式資料收集端點會接收單一事件，並在使用者端預期Adobe Experience PlatformEdge Network伺服器傳回回應時使用。 這些端點在執行資料收集時也可以從其他Edge Network服務傳回內容。

>[!IMPORTANT]
>
>`/interact`端點主要是設計給Experience PlatformSDK使用。 此端點可能會有額外的變更，其行為可能會演化，恕不另行通知。 例如，未來可能會將新專案新增至回應裝載。

伺服器回應包含一個或多個`Handle`物件，如下所示。

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

| 參數 | 類型 | 必要 | 說明 |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | 可以。 | 資料串流ID。 |
| `requestId` | `String` | 無 | 提供用於關聯內部伺服器請求的使用者端隨機ID。 如果未提供任何專案，Edge Network將會產生一個專案，並在回應中傳回。 |

### 回應 {#response}

成功的回應會傳回HTTP狀態`200 OK`，包含一或多個`Handle`物件，視資料流設定中啟用的即時邊緣服務而定。

```json
{
   "requestId": "c85402f5-83a1-4fb3-abdd-f4c17bf6dd49",
   "handle": []
}
```
