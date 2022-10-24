---
title: 透過Adobe Target個人化
description: 了解如何使用伺服器API來提供及呈現在Adobe Target中建立的個人化體驗。
exl-id: c9e2f7ef-5022-4dc4-82b4-ecc210f27270
source-git-commit: d6573f8f4d779fb7ed11b44561a0ad9667748b27
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 2%

---

# 透過Adobe Target個人化

## 總覽 {#overview}

Edge Network Server API可在以下協助下提供及呈現在Adobe Target中建立的個人化體驗： [表單式體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en).

>[!IMPORTANT]
>
>透過 [Target可視化體驗撰寫器(VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=en) 伺服器API並未完全支援。 伺服器API可 **擷取** 由VEC建立的活動，但伺服器API無法 **轉譯** 由VEC建立的活動。 如果您想呈現VEC建立的活動，請使用 [Web SDK](../edge/home.md).

## 設定您的資料流 {#configure-your-datastream}

您必須先在資料流設定上啟用Adobe Target個人化，才能將伺服器API與Adobe Target搭配使用。

請參閱 [將服務新增至資料流的指南](../edge/datastreams/overview.md#adobe-target-settings)，以取得如何啟用Adobe Target的詳細資訊。

設定資料流時，您可以（選擇性）提供 [!DNL Property Token], [!DNL Target Environment ID]，和 [!DNL Target Third Party ID Namespace].

![顯示資料流服務設定畫面的UI影像，並選取Adobe Target](assets/target-datastream.png)

您可以選擇下列項目 [!DNL Analytics Logging] 選項：

* **[!DNL Server Side]**:這是 [[!DNL A4T]](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html). 選取此選項時，每次Target傳回個人化內容時，會 [!DNL A4T] 資料會根據來自Target個人化引擎的回應自動傳送至Analytics。
* **[!DNL Client Side]**:選取此選項時，每次Target傳回個人化內容時，會 [!DNL A4T] 資料會傳回至呼叫應用程式。 如果您打算將此資料記錄在Analytics中，您必須確保在後續呼叫 [!DNL Analytics].

   >[!IMPORTANT]
   >
   >除了選取 **[!UICONTROL 用戶端]** 在「目標設定」中，您也必須停用Analytics，邊緣網路才能傳回 [!DNL A4T] 回應的資訊。


## 自訂參數 {#custom-parameters}

中的大部分欄位 [!DNL XDM] 每個請求的一部分會序列化為點記號，然後以自訂或 [!DNL mbox] 參數。


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

在Target中建立對象時，下列值將可作為自訂參數使用：

* `xdm.marketing.campaignGroup`
* `xdm.marketing.campaignName`
* `xdm.marketing.trackingCode`

## Target設定檔更新 {#profile-update}

此 [!DNL Server API] 允許更新Target設定檔。 若要更新Target設定檔，請確定設定檔資料已傳入 `data` 請求的一部分，格式如下：

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

請求的查詢部分決定Target傳回的內容。 在 `personalization` 物件， `schemas` 決定Target要傳回的內容類型。

如果您不確定要擷取的選件類型，您應將這四個結構納入您對邊緣網路的個人化查詢中：

* **HTML型選件：**
https://ns.adobe.com/personalization/html-content-item
* **JSON型選件：**
https://ns.adobe.com/personalization/json-content-item
* **目標重新導向選件**
https://ns.adobe.com/personalization/redirect-item
* **目標DOM操作選件**
https://ns.adobe.com/personalization/dom-action

### 決策範圍 {#decision-scopes}

Adobe Target [!DNL mbox] 名稱應包含在 `decisionScopes` 陣列，以傳回適當的內容。

#### 範例 {#decision-scopes-example}

在以下範例中，會要求所有四種選件類型以及名為的Target活動 `serverapimbox`.

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

以下概述完整請求，其中包括完整的XDM物件、設定檔參數，以及適當的Target查詢。

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

邊緣網路會傳回類似下列的回應。

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

如果訪客根據傳送至Adobe Target的資料符合個人化活動的資格，相關活動內容將會在 `handle` 物件，其中類型為 `personalization:decisions`.

其他內容有時會在 `handle` 還有。 其他內容類型與Target個人化無關。 如果訪客符合多個活動的資格，每個活動將是個別的 `personalization` 陣列中的物件。

下表說明了該部分回應的關鍵元素。

| 屬性 | 說明 | 範例 |
|---|---|---|
| `scope` | 產生建議選件的Target mbox名稱。 | `"scope": "serverapimbox"` |
| `items[].schema` | 與建議選件相關聯的內容綱要。 這將與您在建立個人化活動時選取的活動類型相關。 | `"schema": "https://ns.adobe.com/personalization/json-content-item",` |
| `items[].meta.activity.id` | 優惠方案活動的唯一ID。 通常為6位數。 | `"activity.id": "140281"` |
| `items[].meta.activity.name` | 使用者指定的優惠方案活動名稱。 這會在活動建立步驟期間提供。 | `"activity.name": "Server API Form"` |
| `items[].meta.experience.id` | 個人化體驗的唯一ID。 | `"experience.id": "0"` |
| `items[].meta.experience.name` | 個人化體驗的唯一名稱。 | `"experience.name": "Experience A"` |
| `items[].data.id` | 建議選件的ID。 | `"id": "282484"` |
| `items[].data.format` | 與建議選件相關聯的內容格式。 | `"format: "application/json` |
| `items[].data.content` | 與建議的選件相關聯的內容。 這將用於個人化呼叫應用程式的內容。 | `"content": "<CONTENT CONFIGURED IN TARGET>"` |
