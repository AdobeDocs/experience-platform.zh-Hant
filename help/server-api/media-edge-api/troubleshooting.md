---
keywords: Experience Platform；media edge；熱門主題；日期範圍
solution: Experience Platform
title: Media Edge API快速入門
description: Media Edge API疑難排解指南
source-git-commit: f723114eebc9eb6bfa2512b927c5055daf97188b
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Media Edge API疑難排解指南

本指南提供處理錯誤及取得成功回應的疑難排解指示。

## 使用錯誤回應輔助

為協助疑難排解失敗的回應，錯誤會隨附包含錯誤物件的回應內文。 在此情況下，回應內文會包含問題詳細資訊，如所定義 [HTTP API的RFC 7807問題詳細資料](https://datatracker.ietf.org/doc/html/rfc7807). 為了改善API使用者體驗，問題詳細資訊是描述性的（陣列金鑰的詳細資訊是使用JsonPath顯示到缺少或無效的欄位）。 它們也是累積的（所有無效欄位都將在同一請求中報告）。


## 驗證工作階段開始

建立工作階段開始請求的大部分問題都會導致207多狀態回應。
裝載類似於Experience Edge Network Server API的非嚴重錯誤。 所有Media Analytics錯誤都具有下列型別：  `https://ns.adobe.com/aep/errors/va-edge-0XXX-XXX`. 回應中顯示的數字與錯誤狀態對應。

下列範例顯示「工作階段開始」要求的回應內文，其中缺少必要欄位，且欄位無效。

```
{
    "requestId": "d4be4f91-a535-41e7-80c6-bdd031d3a365",
    "handle": [
        ...
    ],
    "errors": [
        {
            "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
            "status": 400,
            "title": "Invalid request",
            "report": {
                "eventIndex": 0,
                "details": [
                    {
                        "name": "$.xdm.mediaCollection.sessionDetails.name",
                        "reason": "Missing required field"
                    },
                    {
                        "name": "$.xdm.timestamp",
                        "reason": "Field should respect ISO 8601 standard for presenting date and time with offset to UTC (e.g. 2022-05-19T19:31:02Z, 2022-05-19T21:31:02+02:00, 2022-05-19T21:31:02.234+02:00)"
                    }
                ]
            }
        }
    ]
}
```

在上述範例中，兩個問題都由下列專案註明 `name` 和 `reason` 在 `details`：顯示第一個原因 `missing required field` 第二個則說明不符合ISO 8601標準。


>[!NOTE]
>
> 對於從Media Analytics上游引起的錯誤，Adobe建議您繼續處理產生的媒體工作階段。

## 驗證事件

大多數無效事件要求會導致400錯誤要求回應。 在這些情況下，裝載類似於Experience Edge Network Server API嚴重錯誤。

對於事件請求，Media Edge API服務包括未在XDM模型本身中擷取的其他檢查。 這包括檢查路徑 `eventType` 符合要求裝載 `eventType`.


下列範例顯示 `eventType` 與「 」不相符 `adBreakStart` 裝載已傳送至 `ee/va/v1/chapterStart`：

```
{
    "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
    "status": 400,
    "title": "Bad Request",
    "detail": "Invalid request. Please check your input and try again.",
    "report": {
        "details": "The payload eventType adBreakStart was different from the path eventType chapterStart"
    }
}
```

下列範例顯示其他Media Edge API檢查發現 `chapterStart` 呼叫遺失 `chapterDetails` 資訊：

```
{
    "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
    "status": 400,
    "title": "Bad Request",
    "detail": "Invalid request. Please check your input and try again.",
    "report": {
        "details": [
            {
                "name": "$.events[0].xdm.mediaCollection.chapterDetails",
                "reason": "Missing required field"
            }
        ]
    }
}
```

## 處理400層級和500層級錯誤

下表提供處理狀態回應錯誤的指示：


| 錯誤代碼 | 說明 |
| ---------- | --------- |
| 4xx錯誤請求 | 最多4xx個錯誤(例如 `400`， `403`， `404`)不應由使用者重試。 重試請求將不會導致成功回應。 使用者應解決錯誤，然後再重試請求。 系統不會追蹤產生4xx狀態代碼的事件，這可能會影響接收4xx回應的工作階段中資料的正確性。 |
| 410已過期 | 表示伺服器端不再計算用於追蹤的工作階段。 最常見的原因是工作階段超過24小時。 在收到 `410`，請嘗試啟動新工作階段並追蹤它。 |
| 429請求太多 | 此回應代碼表示伺服器正在限制要求的速率。 請遵循 **重試晚於** 回應標題中的指示請務必小心。 任何回流的回應都必須攜帶具有網域特定錯誤代碼的HTTP回應代碼。 |
| 500內部伺服器錯誤 | `500` 錯誤是一般性錯誤，涵蓋所有錯誤。 `500` 錯誤不應重試，以下情況除外 `502`， `503` 和 `504`. |
| 502錯誤的閘道 | 此錯誤碼表示伺服器作為閘道時，從上游伺服器接收到無效的回應。 這可能是因為伺服器之間的網路問題。 暫時的網路問題可以自行解決，因此重試請求可以解決問題。 |
| 503服務無法使用 | 此錯誤碼表示服務暫時無法使用。 這可能發生在維護期間。 的收件者 `503` 錯誤可重試請求，但也應遵循 **重試晚於** 標頭指示。 |


## 在工作階段回應緩慢時將事件加入佇列

開始媒體追蹤工作階段後，媒體播放器可能會在工作階段開始回應從後端返回之前（連同工作階段ID引數）引發。 如果發生這種情形，應用程式必須將所有在工作階段開始要求與其回應之間抵達的追蹤事件加入佇列。 當「工作階段」回應抵達時，您應該先處理所有已排入佇列的事件，接著才能開始處理即時事件。

為獲得最佳結果，請檢查分佈中的「參考播放器」，瞭解在接收工作階段ID之前如何處理事件的指示。

以下範例說明在接收工作階段ID之前處理事件的方法：


```
// For event payload format, see "Request body" sections of "Session Start Request", "Event Requests" respectively.  *
 
VideoPlayer.prototype._collectEvent = function(event) {
    var sessionID = event.events[0].xdm.mediaCollection.sessionID
    var eventType = event.events[0].xdm.eventType.substring("media.".length);
    // If we don't have a Session ID yet,
    // queue the event and return...
    if (sessionId === undefined) {
        console.log("[Player] Queueing event")
        _pendingEvents.push(event)
        return;
    }
 
    // If we DO have a Session ID, process the
    // tracking event...
    apiClient.request({
        "baseUrl": `${endpoint}`,
        "path": `ee/va/v1/${eventType}`,
        "method": `POST`,
        "data": `${event}`
    }).then((response) => {
        if (eventType === "sessionStart") {
            var newSessionID = response.json().handle.filter((h) => h.type === "media-analytics:new-session")[0].payload[0].sessionId;
            _processPendingEvents(newSessionID);
        }
        […]
    }
}
 
VideoPlayer.prototype._processPendingEvents function(sessionID) {
    _pendingEvents.forEach((event) => {
        event.events[0].xdm.mediaCollection.sessionID = sessionID;
        _collectEvent(event);
    });
    _pendingEvents = [];
}
```


