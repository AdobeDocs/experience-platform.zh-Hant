---
title: 基於FPID的訪客身份識別
description: 瞭解如何使用FPID通過伺服器API一致地識別訪問者
seo-description: Learn how to consistently identify visitors via the Server API, by using the FPID
keywords: 邊緣網路；網關；api;visitor;identification;fpid
exl-id: c61d2e7c-7b5e-4b14-bd52-13dde34e32e3
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# 基於FPID的訪客身份識別

[!DNL First-party IDs] (`FPIDs`)是由客戶生成、管理和儲存的設備ID。 這使客戶能夠控制識別用戶設備。 通過發送 `FPIDs`，邊緣網路不生成全新 `ECID` 一個不包含請求的請求。

的 `FPID` 可以作為API請求主體的一部分 `identityMap` 或者它可以作為cookie發送。

安 `FPID` 可以確定性地翻譯成 `ECID` 邊緣網路，所以 `FPID` 身份與Experience Cloud解決方案完全相容。 獲取 `ECID` 從特定 `FPID` 始終會產生相同的結果，因此用戶將擁有一致的體驗。

的 `ECID` 通過 `identity.fetch` 查詢：

```json
{
   "query":{
      "identity":{
         "fetch":[
            "ECID"
         ]
      }
   }
}
```

對於同時包含 `FPID` 和 `ECID`，也請參見Wiki頁。 `ECID` 請求中已存在的請求將優先於從 `FPID`。 換句話說，邊緣網路使用 `ECID` 已提供和 `FPID` 忽略。 新 `ECID` 僅在 `FPID` 是自己提供的。

就設備ID而言， `server` 資料流應使用 `FPID` 作為設備ID。 其他身份(即 `EMAIL`)，但邊緣網路要求顯式提供主標識。 主標識是配置檔案資料將儲存到的基本標識。

>[!NOTE]
>
>沒有標識的請求將失敗。

以下 `identityMap` 為 `server` 資料流請求：

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"123e4567-e89b-12d3-a456-426614174000",
            "authenticatedState":"ambiguous",
            "primary":true
         }
      ],
      "EMAIL":[
         {
            "id":"email@mail.com",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

以下 `identityMap` 在上設定時，欄位組將導致錯誤響應 `server` 資料流請求：

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"123e4567-e89b-12d3-a456-426614174000",
            "authenticatedState":"ambiguous"
         }
      ],
      "EMAIL":[
         {
            "id":"email@mail.com",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

在此情況下，邊緣網路返回的錯誤響應與以下類似：

```json
{
   "type":"https://ns.adobe.com/aep/errors/EXEG-0306-400",
   "status":400,
   "title":"No primary identity set in request (event)",
   "detail":"No primary identity found in the input event. Update the request accordingly to your schema and try again.",
   "report":{
      "requestId":"{REQUEST_ID}",
      "configId":"{CONFIG_ID}",
      "orgId":"{ORG_ID}"
   }
}
```

## 訪問者識別 `FPID`

通過 `FPID`，確保 `FPID` 在向邊緣網路發出任何請求之前已發送了cookie。 的 `FPID` 可以以cookie或作為 `identityMap` 在請求的正文中。

<!--

## Request with `FPID` passed as cookie header

```shell
curl -X POST 'https://edge.adobedc.net/v2/interact?dataStreamId={Data Stream ID}' \
-H 'cookie: FPID=e98f38e6-6183-442d-8cd2-0e384f4c8aa8' \
-H 'Content-Type: application/json' \
-d '{
    "event": 
        {
            "xdm": {
                "web": {
                    "webPageDetails": {
                        "URL": "https://alloystore.dev"
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
                        "viewportWidth": 1907,
                        "viewportHeight": 545
                    }
                },
                "placeContext": {
                    "localTime": "2022-03-21T21:32:59.991-06:00",
                    "localTimezoneOffset": 360
                },
                "timestamp": "2022-03-22T03:32:59.992Z",
                "implementationDetails": {
                    "name": "https://ns.adobe.com/experience/alloy/reactor",
                    "version": "1.0",
                    "environment": "serverapi"
                }
            }
        },
    "query": {
        "identity": {
            "fetch": [
                "ECID"
            ]
        }
    },
    "meta":
        {
            "state":
            {
                "domain": "alloystore.dev",
                "cookiesEnabled": true
            }
        }
}'
```
-->

## 請求 `FPID` 傳遞 `identityMap` 場

下面的示例通過 [!DNL FPID] 作為 `identityMap` 的下界。

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}"
-H "Authorization: Bearer {TOKEN}"
-H "x-gw-ims-org-id: {ORG_ID}"
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "event": {
      "xdm": {
         "identityMap": {
            "FPID": [
               {
                  "id": "e98f38e6-6183-442d-8cd2-0e384f4c8aa8",
                  "authenticatedState": "ambiguous",
                  "primary": true
               }
            ]
         },
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev"
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
               "viewportWidth": 1907,
               "viewportHeight": 545
            }
         },
         "placeContext": {
            "localTime": "2022-03-21T21:32:59.991-06:00",
            "localTimezoneOffset": 360
         },
         "timestamp": "2022-03-22T03:32:59.992Z",
         "implementationDetails": {
            "name": "https://ns.adobe.com/experience/alloy/reactor",
            "version": "1.0",
            "environment": "serverapi"
         }
      }
   },
   "query": {
      "identity": {
         "fetch": [
            "ECID"
         ]
      }
   }
}'
```
