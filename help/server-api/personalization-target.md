---
title: 透過Adobe Target的Personalization
description: 瞭解如何使用伺服器API來傳遞和轉譯在Adobe Target中建立的個人化體驗。
exl-id: c9e2f7ef-5022-4dc4-82b4-ecc210f27270
source-git-commit: ddffe9bf30741b457f7de1099b50ac1624fca927
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 1%

---

# 透過Adobe Target的Personalization

## 概觀 {#overview}

在[表單式體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)的協助下，Edge Network伺服器API可以傳送及轉譯在Adobe Target中建立的個人化體驗。

>[!IMPORTANT]
>
>伺服器API不完全支援透過[Target視覺化體驗撰寫器(VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)建立的Personalization體驗。 伺服器API可以&#x200B;**擷取VEC建立的**&#x200B;活動，但伺服器API無法&#x200B;**轉譯VEC建立的**&#x200B;活動。 如果您想要轉譯VEC建立的活動，請使用Web SDK和Edge Network伺服器API實作[混合式個人化](../web-sdk/personalization/hybrid-personalization.md)。

## 設定您的資料串流 {#configure-your-datastream}

您必須先在資料流設定上啟用Adobe Target個人化，才能將伺服器API與Adobe Target搭配使用。

如需如何啟用Adobe Target的詳細資訊，請參閱將服務新增至資料流](../datastreams/overview.md#adobe-target-settings)的[指南。

設定資料流時，您可以（選擇性）提供[!DNL Property Token]、[!DNL Target Environment ID]和[!DNL Target Third Party ID Namespace]的值。

![顯示資料流服務設定畫面的UI影像，已選取Adobe Target](assets/target-datastream.png)

## 自訂引數 {#custom-parameters}

每個要求的[!DNL XDM]部分中的大部分欄位都會序列化為點標籤法，然後以自訂或[!DNL mbox]引數的形式傳送至Target。


### 範例 {#custom-parameters-example}

提供下列XDM範例：

```json
"xdm":{
   "marketing":{
      "campaignGroup":"winter22",
      "campaignName":"homeOwnerPromo22",
      "trackingCode":"hop22"
   }
}
```

在Target中建立對象時，下列值可作為自訂引數使用：

* `marketing.campaignGroup`
* `marketing.campaignName`
* `marketing.trackingCode`

## Target設定檔更新 {#profile-update}

[!DNL Server API]允許更新Target設定檔。 若要更新Target設定檔，請確定設定檔資料是以下列格式在請求的`data`部分傳遞：

```json
"data":  {
    "__adobe.target": {
        "profile.eyeColor": "brown",
        "profile.hairColor": "brown"
    }
}
```

## 查詢Target活動 {#querying-target-activities}

### 結構描述 {#schemas}

請求的查詢部分決定了Target會傳回哪些內容。 在`personalization`物件下，`schemas`會決定Target要傳回的內容型別。

若您不確定要擷取哪一種選件，則應在Edge Network的個人化查詢中納入全部四個結構描述：

* **HTML型優惠：**
https://ns.adobe.com/personalization/html-content-item
* **JSON型選件：**
https://ns.adobe.com/personalization/json-content-item
* **目標重新導向選件**
https://ns.adobe.com/personalization/redirect-item
* **目標DOM操作選件**
https://ns.adobe.com/personalization/dom-action

### 決定範圍 {#decision-scopes}

Adobe Target [!DNL mbox]名稱應包含在`decisionScopes`陣列中，以傳回適當的內容。

#### 範例 {#decision-scopes-example}

在下列範例中，所有四種選件型別都與稱為`serverapimbox`的Target活動一起要求。

```json
"query":{
   "personalization":{
      "schemas":[
         "https://ns.adobe.com/personalization/html-content-item",
         "https://ns.adobe.com/personalization/json-content-item",
         "https://ns.adobe.com/personalization/redirect-item",
         "https://ns.adobe.com/personalization/dom-action"
      ],
      "decisionScopes":[
         "serverapimbox"
      ]
   }
}
```

## API呼叫範例 {#api-example}

**API格式**

```http
POST /ee/v2/interact
```

### 請求 {#request}

包含完整XDM物件、設定檔引數以及適當Target查詢的完整請求概述如下。

```shell
curl -X POST 'https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org: {ORG_ID}' \
--header 'Authorization: Bearer {TOKEN}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "event": {
        "xdm": {
            "eventType": "web.webpagedetails.pageViews",
            "identityMap": {
                "ECID": [
                    {
                        "id": "05907638112924484241029082405297151763",
                        "authenticatedState": "ambiguous",
                        "primary": true
                    }
                ]
            },
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
                "version": "1.0",
                "environment": "serverapi"
            },
            "data": {
                "__adobe": {
                    "target": {
                        "profile.eyeColor": "brown",
                        "profile.hairColor": "brown",
                        "profile.shoeColor": "black"
                    }
                }
            }
        }
    },
    "query": {
        "personalization": {
            "schemas": [
                "https://ns.adobe.com/personalization/html-content-item",
                "https://ns.adobe.com/personalization/json-content-item",
                "https://ns.adobe.com/personalization/redirect-item",
                "https://ns.adobe.com/personalization/dom-action"
            ],
            "decisionScopes": [
                "serverapimbox"
            ]
        }
    }
}'
```

### 回應 {#response}

Edge Network會傳回類似以下的回應。

```json
{
   "requestId":"10959bbf-f83d-40e1-9521-d9145f19cdc5",
   "handle":[
      {
         "payload":[
            {
               "id":"AT:eyJhY3Rpdml0eUlkIjoiMTQwMjgxIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
               "scope":"serverapimbox",
               "scopeDetails":{
                  "decisionProvider":"TGT",
                  "activity":{
                     "id":"140281"
                  },
                  "experience":{
                     "id":"0"
                  },
                  "strategies":[
                     {
                        "algorithmID":"0",
                        "trafficType":"0"
                     }
                  ],
                  "characteristics":{
                     "eventToken":"xycjBJlZhwVV5MN0kMkmoGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
                  }
               },
               "items":[
                  {
                     "id":"282484",
                     "schema":"https://ns.adobe.com/personalization/json-content-item",
                     "meta":{
                        "offer.name":"/server_apiform/experiences/0/pages/0/zones/0/1648103551041",
                        "experience.id":"0",
                        "activity.name":"Server API Form",
                        "activity.id":"140281",
                        "experience.name":"Experience A",
                        "option.id":"2",
                        "offer.id":"282484"
                     },
                     "data":{
                        "id":"282484",
                        "format":"application/json",
                        "content":{
                           "value":"a/b json experience a",
                           "platform":"server"
                        }
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      },
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiYwNTkwNzYzODExMjkyNDQ4NDI0MTAyOTA4MjQwNTI5NzE1MTc2M1IOCL-pwpv9LxgBKgNPUjLwAb-pwpv9Lw==",
               "maxAge":34128000
            }
         ],
         "type":"state:store"
      }
   ]
}
```

如果訪客根據傳送至Adobe Target的資料符合個人化活動的資格，則相關活動內容將會在`handle`物件下找到，其中型別為`personalization:decisions`。

有時也會在`handle`下傳回其他內容。 其他內容型別與Target個人化無關。 如果訪客符合多個活動的資格，則每個活動在陣列中將是一個單獨的`personalization`物件。

下表說明該部分回應的主要元素。

| 屬性 | 說明 | 範例 |
|---|---|---|
| `scope` | 產生建議優惠方案的Target mbox名稱。 | `"scope": "serverapimbox"` |
| `items[].schema` | 與建議選件相關之內容的結構描述。 這會與您建立個人化活動時選取的活動型別相關。 | `"schema": "https://ns.adobe.com/personalization/json-content-item",` |
| `items[].meta.activity.id` | 優惠活動的唯一ID。 通常是6位數的數字。 | `"activity.id": "140281"` |
| `items[].meta.activity.name` | 使用者指定的優惠方案活動的名稱。 這會在活動建立步驟期間提供。 | `"activity.name": "Server API Form"` |
| `items[].meta.experience.id` | 個人化體驗的唯一ID。 | `"experience.id": "0"` |
| `items[].meta.experience.name` | 個人化體驗的唯一名稱。 | `"experience.name": "Experience A"` |
| `items[].data.id` | 建議優惠的ID。 | `"id": "282484"` |
| `items[].data.format` | 與建議選件相關聯的內容格式。 | `"format: "application/json` |
| `items[].data.content` | 與建議選件相關聯的內容。 這將用於呼叫應用程式內容的個人化。 | `"content": "<CONTENT CONFIGURED IN TARGET>"` |

## 伺服器端個人化範例應用程式 {#sample}

在[此URL](https://github.com/adobe/alloy-samples/tree/main/target/personalization-server-side)找到的範例應用程式示範了使用Adobe Experience Platform從Adobe Target取得個人化內容。 網頁會根據傳回的個人化內容而變更。

此範例&#x200B;_不_&#x200B;依賴使用者端資料庫（例如[!DNL Web SDK]）來取得個人化內容。 而是使用Adobe Experience Platform API來擷取個人化內容。 然後實作會根據傳回的個人化內容在伺服器端產生HTML。
