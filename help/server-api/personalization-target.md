---
title: 通過Adobe Target個性化
description: 瞭解如何使用伺服器API來提供和呈現在Adobe Target建立的個性化體驗。
exl-id: c9e2f7ef-5022-4dc4-82b4-ecc210f27270
source-git-commit: 091d5440d7346861b7c882fa0a17bd03d528e438
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 1%

---

# 通過Adobe Target個性化

## 總覽 {#overview}

邊緣網路伺服器API可以在Adobe Target的幫助下提供和呈現個性化體驗 [基於表單的體驗作曲家](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en)。

>[!IMPORTANT]
>
>通過 [目標視覺體驗合成器(VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) 伺服器API不完全支援。 伺服器API可以 **檢索** 由VEC建立的活動，但Server API不能 **呈現** 由VEC建立的活動。 如果要呈現由VEC建立的活動，請實施 [混合個性化](../edge/personalization/hybrid-personalization.md) 使用Web SDK和邊緣網路伺服器API。

## 配置資料流 {#configure-your-datastream}

在與Adobe Target一起使用伺服器API之前，必須在資料流配置上啟用Adobe Target個性化。

查看 [將服務添加到資料流的指南](../edge/datastreams/overview.md#adobe-target-settings)，以獲取有關如何啟用Adobe Target的詳細資訊。

配置資料流時，您可以（可選）提供 [!DNL Property Token]。 [!DNL Target Environment ID], [!DNL Target Third Party ID Namespace]。

![顯示資料流服務配置螢幕的UI影像，已選擇Adobe Target](assets/target-datastream.png)


## 自訂參數 {#custom-parameters}

中的大多數欄位 [!DNL XDM] 將每個請求的一部分序列化為點標籤，然後以自定義或 [!DNL mbox] 參數。


### 範例 {#custom-parameters-example}

給出以下XDM示例：

```json
"xdm":{
   "marketing":{
      "campaignGroup":"winter22",
      "campaignName":"homeOwnerPromo22",
      "trackingCode":"hop22"
   }
}
```

在「目標」中建立訪問群體時，以下值將作為自定義參數可用：

* `xdm.marketing.campaignGroup`
* `xdm.marketing.campaignName`
* `xdm.marketing.trackingCode`

## 目標配置檔案更新 {#profile-update}

的 [!DNL Server API] 允許更新目標配置檔案。 要更新目標配置檔案，請確保將配置檔案資料傳遞到 `data` 格式的部分：

```json
"data":  {
    "__adobe.target": {
        "profile.eyeColor": "brown",
        "profile.hairColor": "brown"
    }
}
```

## 查詢目標活動 {#querying-target-activities}

### 綱要 {#schemas}

請求的查詢部分確定目標返回的內容。 在 `personalization` 對象， `schemas` 確定目標要返回的內容類型。

在您不確定要檢索的服務類型的情況下，您應將四個架構包括在對邊緣網路的個性化查詢中：

* **基於HTML的產品：**
https://ns.adobe.com/personalization/html-content-item
* **基於JSON的優惠：**
https://ns.adobe.com/personalization/json-content-item
* **目標重定向服務**
https://ns.adobe.com/personalization/redirect-item
* **目標DOM操作提供**
https://ns.adobe.com/personalization/dom-action

### 決策範圍 {#decision-scopes}

Adobe Target [!DNL mbox] 名稱應包括在 `decisionScopes` 陣列以返回相應的內容。

#### 範例 {#decision-scopes-example}

在下例中，請求所有四種服務類型，同時請求一個名為 `serverapimbox`。

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

## API調用示例 {#api-example}

**API格式**

```http
POST /ee/v2/interact
```

### 請求 {#request}

下面概述了包含完整XDM對象、配置檔案參數以及相應目標查詢的完整請求。

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

邊緣網路將返回與下面類似的響應。

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

如果訪問者根據發送到Adobe Target的資料有資格進行個性化活動，相關活動內容將在 `handle` 對象，其中類型為 `personalization:decisions`。

其他內容有時會在 `handle` 也是。 其他內容類型與目標個性化不相關。 如果訪問者有資格進行多項活動，則每項活動都將是單獨的 `personalization` 的子目錄。

下表說明了該部分答復的關鍵要素。

| 屬性 | 說明 | 範例 |
|---|---|---|
| `scope` | 導致建議的報價的目標框名稱。 | `"scope": "serverapimbox"` |
| `items[].schema` | 與建議的優惠關聯的內容的模式。 這將與建立個性化設定活動時選擇的活動類型相關。 | `"schema": "https://ns.adobe.com/personalization/json-content-item",` |
| `items[].meta.activity.id` | 優惠活動的唯一ID。 通常為6位數。 | `"activity.id": "140281"` |
| `items[].meta.activity.name` | 用戶指定的聘用活動的名稱。 在活動建立步驟中提供。 | `"activity.name": "Server API Form"` |
| `items[].meta.experience.id` | 個性化體驗的唯一ID。 | `"experience.id": "0"` |
| `items[].meta.experience.name` | 個性化體驗的唯一名稱。 | `"experience.name": "Experience A"` |
| `items[].data.id` | 建議的報價的ID。 | `"id": "282484"` |
| `items[].data.format` | 與建議的優惠關聯的內容的格式。 | `"format: "application/json` |
| `items[].data.content` | 與建議的優惠關聯的內容。 這將用於個性化調用應用程式的內容。 | `"content": "<CONTENT CONFIGURED IN TARGET>"` |
