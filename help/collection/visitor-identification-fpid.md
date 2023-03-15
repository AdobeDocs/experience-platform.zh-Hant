---
title: 透過FPID識別訪客
description: 了解如何使用FPID透過伺服器API一致地識別訪客
seo-description: Learn how to consistently identify visitors via the Server API, by using the FPID
keywords: 邊緣網路；閘道；API；訪客；身分識別；fpid
exl-id: c61d2e7c-7b5e-4b14-bd52-13dde34e32e3
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# 透過FPID識別訪客

[!DNL First-party IDs] (`FPIDs`)是客戶產生、管理和儲存的裝置ID。 這可讓客戶控制識別使用者裝置。 透過傳送 `FPIDs`，邊緣網路不會產生全新 `ECID` ，以取得不包含任何項的要求。

此 `FPID` 可包含在API要求內文中，作為 `identityMap` 或可以Cookie形式傳送。

安 `FPID` 可以決定性地翻譯成 `ECID` 邊緣網路，所以 `FPID` 身分與Experience Cloud解決方案完全相容。 取得 `ECID` 從特定 `FPID` 結果一律相同，因此使用者會有一致的體驗。

此 `ECID` 取得的方式可透過 `identity.fetch` 查詢：

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

若請求中同時包含 `FPID` 和 `ECID`, `ECID` 請求中已存在的請求優先於可從 `FPID`. 換言之，邊緣網路會使用 `ECID` 已提供和 `FPID` 會忽略。 新 `ECID` 只有在 `FPID` 是自行提供。

就裝置ID而言， `server` datastreams應使用 `FPID` 做為裝置ID。 其他身分(即 `EMAIL`)也可在要求內文中提供，但邊緣網路要求明確提供主要身分。 主要身分是要儲存設定檔資料的基本身分。

>[!NOTE]
>
>若要求內文中分別未明確設定主要身分的沒有身分，則會失敗。

以下 `identityMap` 為 `server` datastream請求：

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

以下 `identityMap` 欄位群組在 `server` datastream請求：

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

在此情況下，邊緣網路傳回的錯誤回應類似於：

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

## 訪客身分識別(使用 `FPID`

若要透過 `FPID`，請確定 `FPID` 在向邊緣網路提出任何請求前已傳送cookie。 此 `FPID` 可傳遞至Cookie，或做為 `identityMap` 在請求內文中。

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

## 請求 `FPID` 傳遞 `identityMap` 欄位

以下範例將 [!DNL FPID] as a `identityMap` 參數。

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
