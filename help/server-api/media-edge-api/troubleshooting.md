---
solution: Experience Platform
title: Media Edge API快速入門
description: Media Edge API疑難排解指南
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---


# Media Edge API疑難排解指南

本指南提供處理錯誤及取得成功回應的疑難排解指示。

## 使用錯誤回應輔助

為協助疑難排解失敗的回應，錯誤會隨附包含錯誤物件的回應內文。 在此情況下，回應內文會包含由所定義的問題詳細資訊 [HTTP API的RFC 7807問題詳細資訊](https://datatracker.ietf.org/doc/html/rfc7807). 為了改善API使用者體驗，問題詳細資訊是描述性的（陣列索引鍵的詳細資訊是使用JsonPath顯示到缺少或無效的欄位）。 它們也是累積的（所有無效欄位都將在同一請求中報告）。


## 驗證工作階段開始

工作階段開始要求的大部分問題都會導致207多狀態回應。
裝載類似於 [伺服器API](../error-handling.md)的非嚴重錯誤。 所有Media Analytics錯誤都具有以下型別：  `https://ns.adobe.com/aep/errors/va-edge-0XXX-XXX`. 回應中顯示的數字與錯誤狀態對應。

下列範例顯示工作階段開始要求的回應內文，其中缺少必要欄位，且欄位無效。

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

在上述範例中，兩個問題都由下列專案註明 `name` 和 `reason` 在 `details`：顯示第一個原因 `missing required field` 第二個則描述不符合ISO 8601標準的情況。


>[!NOTE]
>
> 若為從Media Analytics上游引起的錯誤，Adobe建議您繼續處理產生的媒體工作階段。

## 驗證事件

大多數無效事件請求會導致400錯誤請求回應。 在這些情況下，裝載類似於伺服器API嚴重錯誤。

對於事件請求，Media Edge API服務包含未在XDM模型本身中擷取的其他檢查。 這包括檢查路徑 `eventType` 符合請求承載 `eventType`.


下列範例顯示 `eventType` 與不相符 `adBreakStart` 裝載已傳送至 `ee/va/v1/chapterStart`：

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

下列範例顯示其他Media Edge API檢查結果 `chapterStart` 呼叫遺失 `chapterDetails` 資訊：

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


| 錯誤碼 | 說明 |
| ---------- | --------- |
| 4xx錯誤請求 | 大多數4xx錯誤(例如 `400`， `403`， `404`)不應由使用者重試。 重試請求將不會導致成功的回應。 使用者應解決錯誤，然後再重試要求。 不會追蹤產生4xx狀態代碼的事件，這可能會影響收到4xx回應的工作階段中的資料準確度。 |
| 410已過期 | 表示伺服器端將不再計算用於追蹤的工作階段。 最常見的原因是工作階段超過24小時。 在收到 `410`，嘗試開始新的工作階段並追蹤它。 |
| 429太多請求 | 此回應代碼表示伺服器正在限制要求的速率。 請遵循 **於以下時間後重試** 回應標題中的指示請務必小心。 任何回流的回應都必須攜帶HTTP回應代碼以及網域特定的錯誤代碼。 |
| 500內部伺服器錯誤 | `500` 錯誤是一般性錯誤，涵蓋所有錯誤。 `500` 錯誤不應重試，除了 `502`， `503` 和 `504`. |
| 502錯誤的閘道 | 此錯誤碼表示伺服器作為閘道時，從上游伺服器收到無效的回應。 這可能是因為伺服器之間的網路問題所造成。 暫時的網路問題可以自行解決，因此重試請求或許可以解決問題。 |
| 503服務無法使用 | 此錯誤碼表示服務暫時無法使用。 這可能發生在維護期間。 的收件者 `503` 錯誤可重試請求，但同時也應遵循 **於以下時間後重試** 標題指示。 |


## 在工作階段回應緩慢時將事件加入佇列

開始媒體追蹤工作階段後，媒體播放器可能會在工作階段開始回應從後端返回之前（連同工作階段ID引數）引發。 如果發生這種情形，應用程式必須將所有在工作階段開始要求與其回應之間抵達的追蹤事件加入佇列。 當「工作階段」回應抵達時，您應該先處理所有已加入佇列的事件，接著才能開始處理即時事件。

為了獲得最佳結果，請檢查分佈中的「參考播放器」，以取得如何在接收工作階段ID之前處理事件的指示。

下列範例說明在接收工作階段ID之前處理事件的方法：


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


