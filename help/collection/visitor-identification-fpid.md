---
title: 透過FPID的訪客身分識別
description: 瞭解如何使用FPID，透過Edge Network API一致地識別訪客
seo-description: Learn how to consistently identify visitors via the Edge Network API, by using the FPID
keywords: 邊緣網路；閘道；API；訪客；識別；fpid
exl-id: c61d2e7c-7b5e-4b14-bd52-13dde34e32e3
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# 透過FPID的訪客身分識別

[!DNL First-party IDs] (`FPIDs`)是由客戶產生、管理和儲存的裝置ID。 這可讓客戶控制識別使用者裝置。 傳送`FPIDs`後，Edge Network不會針對不包含的全新`ECID`請求產生全新。

`FPID`可以作為`identityMap`的一部分包含在API要求內文中，也可以作為Cookie傳送。

`FPID`可由Edge Network決定性地轉譯為`ECID`，因此`FPID`識別與Experience Cloud解決方案完全相容。 從特定`FPID`取得`ECID`一律會產生相同的結果，因此使用者將擁有一致的體驗。

以這種方式取得的`ECID`可透過`identity.fetch`查詢擷取：

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

對於同時包含`FPID`和`ECID`的請求，已存在於請求中的`ECID`將優先於可從`FPID`產生的請求。 換言之，Edge Network使用已提供的`ECID`，而`FPID`則被忽略。 只有在自行提供`FPID`時，才會產生新的`ECID`。

就裝置ID而言，`server`資料串流應使用`FPID`作為裝置ID。 其他身分（亦即`EMAIL`）也可於要求內文中提供，但Edge Network需要明確提供主要身分。 主要身分是將設定檔資料儲存到的基本身分。

>[!NOTE]
>
>沒有身分的請求（分別在請求內文中沒有明確設定的主要身分）將失敗。

`server`資料流要求的下列`identityMap`欄位群組格式正確：

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

在`server`資料流要求上設定下列`identityMap`欄位群組時，會產生錯誤回應：

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

在此案例中，Edge Network傳回的錯誤回應類似於以下內容：

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

## 使用`FPID`的訪客身分識別

若要透過`FPID`識別使用者，在向Edge Network提出任何請求之前，請確定已傳送`FPID` Cookie。 `FPID`可以在Cookie中或作為要求內文中`identityMap`的一部分傳遞。

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

## 以`identityMap`欄位傳遞含`FPID`的要求

下列範例將[!DNL FPID]當做`identityMap`引數傳遞。

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
