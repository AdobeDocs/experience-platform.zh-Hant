---
title: 互動式資料收集
description: 瞭解Adobe Experience Platform邊緣網路伺服器API如何執行互動式資料收集。
exl-id: 1b06e755-b6a9-42dd-96c1-98ad67e7d222
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 6%

---

# 互動式資料收集

## 總覽 {#overview}

互動式資料收集端點接收單個事件，並在客戶端希望Adobe Experience Platform邊緣網路伺服器返迴響應時使用。 這些端點還可以從其他體驗邊緣服務返回內容，同時執行資料收集。

伺服器響應包括一個或多個 `Handle` 對象，如下所示。

## API調用示例

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
| `requestId` | `String` | 無 | 提供用於關聯內部伺服器請求的客戶端隨機ID。 如果未提供，則邊緣網路將生成一個並在響應中返回。 |

### 回應 {#response}

成功響應返回HTTP狀態 `200 OK`，帶一個或多個 `Handle` 對象，具體取決於在資料流配置中啟用的即時邊緣服務。

```json
{
   "requestId": "c85402f5-83a1-4fb3-abdd-f4c17bf6dd49",
   "handle": []
}
```
