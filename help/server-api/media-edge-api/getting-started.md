---
keywords: Experience Platform；media edge；熱門主題；日期範圍
solution: Experience Platform
title: Media Edge API快速入門
description: Media Edge API快速入門
source-git-commit: 4f60b00026a226aa6465b2c21b3c2198962a1e3b
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Media Edge API快速入門

本指南提供成功與Media Edge API服務進行初始互動的說明。 這包括開始媒體工作階段，然後追蹤傳送至Adobe Experience Platform (AEP)解決方案(例如Customer Journey Analytics (CJA))的事件。 Media Edge API服務是以工作階段開始端點啟動。 工作階段開始後，即可追蹤下列一或多個事件：

* play
* ping
* bitrateChange
* bufferStart
* pauseStart
* adBreakStart
* adStart
* adComplete
* adSkip
* adBreakComplete
* chapterStart
* chapterComplete
* chapterSkip
* error
* sessionEnd
* sessionComplete
* statesUpdate

每個事件都有自己的端點。 所有Media Edge API端點都是POST方法，事件資料都有JSON要求內文。 如需Media Edge API端點、引數和範例的詳細資訊，請參閱 [Media Edge Swagger檔案](swagger.md).

本指南說明如何在啟動工作階段後追蹤下列事件：

* 緩衝開始
* 播放
* 工作階段完成

## 實作 API

除了在模型和路徑上呼叫的細微差異之外，Media Edge API的實施與Media Collection API相同。 Media Collection的實作詳細資訊對Media Edge API仍然有效，如下列檔案所述：

* [在播放器中設定 HTTP 要求類型](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=en)
* [傳送 Ping 事件](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=en)
* [逾時條件](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-timeout.html?lang=en)
* [控制事件順序](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-ctrl-order.html?lang=en)

## Authorization

目前，Media Edge API的請求不需要授權標頭。


## 啟動工作階段

若要啟動伺服器上的媒體工作階段，請使用「工作階段開始」端點。 成功的回應包括 `sessionId`，此為後續事件要求的必要引數。

提出工作階段開始要求之前，您需要具備下列條件：

* 此 `datastreamId`—POST工作階段開始要求的必要引數。 擷取 `datastreamId`，請參閱 [設定資料串流](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=zh-Hant).

* 請求承載的JSON物件，包含最低要求資料（如以下請求範例所示）。

取得此資訊後，請提供 `datastreamId` 在以下呼叫中：

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionStart?configId={datastream ID} \`

### 範例請求

下列範例顯示工作階段開始cURL要求：

```
curl -i --request POST '{uri}/ee/va/v1/sessionStart?configId={dataStreamId}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Media Analytics API Sample",
            "playerName": "sample-html5-api-player",
            "contentType": "VOD",
            "length": 60,
            "channel": "sample-channel",
            "appVersion": "va-api-1.0.0"
          },
          "playhead": 0
        }
      }
    }
  ]
}'
```

在上述範例要求中， `eventType` 值包含前置詞 `media.` 根據 [體驗資料模型(XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hant) 用於指定網域。

此外，資料型別對應 `eventType` 在上述範例中，如下所示：

| 事件型別 | 資料型別 |
| -------- | ------ |
| mediaSessionStart | [sessionDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/sessiondetails.schema.md) |
| media.chapterStart | [chapterDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/chapterdetails.schema.md) |
| media.adBreakStart | [advertisingPodDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/advertisingpoddetails.schema.md) |
| media.adStart | [advertisingDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/advertisingdetails.schema.md) |
| media.error | [errorDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/errordetails.schema.md) |
| media.statesUpdate | [statesStart](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmstatesstart)：陣列[playerStateData]， [statesEnd](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmstatesend)：陣列[playerStateData] |
| media.sessionStart， media.chapterStart， media.adStart | [customMetadata](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmcustommetadata) |
| 全部 | [qoeDataDetails](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/qoedatadetails.schema.md) |

### 範例回應

下列範例顯示工作階段開始請求的成功回應：

```
HTTP/2 200
x-request-id: 99603f5c-95cf-49ad-9afb-0ba6c5867fd7
x-rate-limit-remaining: 599
vary: Origin
date: Tue, 07 Mar 2023 14:37:58 GMT
x-konductor: 23.3.2:367bc7dc
x-adobe-edge: IRL1;6
server: jag
content-type: application/json;charset=utf-8
strict-transport-security: max-age=31536000; includeSubDomains
cache-control: no-cache, no-store, max-age=0, no-transform
x-xss-protection: 1; mode=block
x-content-type-options: nosniff

{
    "requestId": "df14bca1-ba0f-4574-ae80-a4e24a960c00",
    "handle": [
        {
            "payload": [
                {
                    "sessionId": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333"
                }
            ],
            "type": "media-analytics:new-session",
            "eventIndex": 0
        },
        {
            "payload": [
                {
                    "key": "kndctr_6D9FE18C5536A5E90A4C98A6_AdobeOrg_cluster",
                    "value": "irl1",
                    "maxAge": 1800
                },
                {
                    "key": "kndctr_6D9FE18C5536A5E90A4C98A6_AdobeOrg_identity",
                    "value": "CiY1MTkxMDM4OTc1MzkwMTY4NTQ1NjAxNDg4OTgzODU5MTAzMDcyMVIPCKKt8KnsMBgBKgRJUkwx8AGirfCp7DA=",
                    "maxAge": 34128000
                }
            ],
            "type": "state:store"
        }
    ]
}
```

在上述範例回應中， `sessionId` 顯示為 `af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333`. 您將在後續事件請求中使用此ID作為必要引數。

如需工作階段開始端點引數和範例的詳細資訊，請參閱 [Media Edge Swagger](swagger.md) 檔案。

如需XDM媒體資料引數的詳細資訊，請參閱 [媒體詳細資訊結構描述](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmplayhead).


## 緩衝開始事件要求

緩衝在媒體播放器上開始時，緩衝開始事件會發出訊號。 「緩衝繼續」不是API服務中的事件；而是在緩衝開始後傳送播放事件時推斷。 若要提出「緩衝開始」事件要求，請使用 `sessionId` 在呼叫的裝載中至下列端點：

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/bufferStart \`

### 範例請求

下列範例顯示緩衝開始cURL要求：

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/bufferStart' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.bufferStart",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

在上述範例要求中，相同的 `sessionId` 先前呼叫中傳回的引數，會作為緩衝開始請求中的必要引數使用。

成功回應表示200狀態，不包含任何內容。

如需「緩衝開始」端點引數和範例的詳細資訊，請參閱 [Media Edge Swagger](swagger.md) 檔案。


## 播放事件要求

當媒體播放器將其狀態從其他狀態（例如「正在緩衝」、「已暫停」或「錯誤」）變更為「正在播放」時，就會傳送「播放」事件。 若要提出「播放」事件請求，請使用 `sessionId` 在呼叫的裝載中至下列端點：

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/play \`

### 範例請求

以下範例顯示Play cURL要求：

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/play' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.play",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

成功回應表示200狀態，不包含任何內容。

如需「播放」端點引數和範例的詳細資訊，請參閱 [Media Edge Swagger](swagger.md) 檔案。

## 工作階段完成事件要求

到達主要內容的結尾時，會傳送「工作階段完成」事件。 若要提出「工作階段完成」事件請求，請使用 `sessionId` 在呼叫的裝載中至下列端點：

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionComplete \`

### 範例請求

下列範例顯示工作階段完成cURL要求：

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/sessionComplete' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionComplete",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

成功回應表示200狀態，不包含任何內容。

如需「工作階段完成」端點引數和範例的詳細資訊，請參閱 [Media Edge Swagger](swagger.md) 檔案。

## 回應代碼

下表顯示Media Edge API請求可能產生的回應代碼：

| 狀態 | 說明 |
| ---------- | --------- |
| 200 | 工作階段已成功建立 |
| 207 | 連線至Experience Edge Network的其中一個服務發生問題(請參閱 [疑難排解指南](troubleshooting.md)) |
| 400級 | 錯誤請求 |
| 500層級 | Server error |

如需有關處理錯誤和不成功回應代碼的詳細資訊，請參閱 [Media Edge疑難排解指南](troubleshooting.md).


