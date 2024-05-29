---
title: createMediaSession
description: 瞭解如何設定Web SDK以自動管理媒體工作階段
source-git-commit: 83d3de67e7680369dc890f58b16d9668058e221c
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 7%

---


# `createMediaSession`

此 `createMediaSession` 命令是Web SDK的一部分 `streamingMedia` 元件。 您可以使用此元件來收集與網站上媒體工作階段相關的資料。 請參閱 `streamingMedia` [檔案](configure/streamingmedia.md) 以瞭解如何設定此元件。

收集的資料可包括關於媒體播放、暫停、完成和其他相關事件的資訊。 收集後，您可以將此資料傳送至 [適用於串流媒體的Adobe Analytics](https://experienceleague.adobe.com/zh-hant/docs/media-analytics/using/media-overview)，以彙總量度。 此功能提供全方位的解決方案，可追蹤及瞭解您網站上的媒體使用行為。

您可以在Web SDK中以兩種方式建立媒體工作階段：

* [自動追蹤的媒體工作階段](#automatic) 允許Web SDK管理媒體Ping事件傳送至 [適用於串流媒體的Adobe Analytics](https://experienceleague.adobe.com/zh-hant/docs/media-analytics/using/media-overview). 這些Ping的頻率是由的組態設定所決定 [streamingMedia](configure/streamingmedia.md) 元件。
* [手動追蹤的媒體工作階段](#manual) 讓您更能掌控工作階段Ping事件的傳送作業 [適用於串流媒體的Adobe Analytics](https://experienceleague.adobe.com/zh-hant/docs/media-analytics/using/media-overview). 此外，您也可以儲存 `sessionID` 適用於媒體工作階段。

## 建立自動追蹤的媒體工作階段 {#automatic}

若要自動開始追蹤媒體工作階段，請呼叫 `createMediaSession` 方法，其選項如下：

```javascript
    alloy("createMediaSession", {
        playerId: "movie-test",
        getPlayerDetails: () => {
            return {
                playhead: document.getElementById("movie-test").currentTime,
                qoeDataDetails: {
                    bitrate: 1000,
                    startupTime: 1000,
                    fps: 30,
                    droppedFrames: 10
                }
            };
        },
        xdm: {
            eventType: "media.sessionStart",
            mediaCollection: {
                sessionDetails: {
                    ...
                }
            }
        }
    });
```

| 屬性 | 類型 | 必要 | 說明 |
|---------|----------|---------|---------|
| `playerId` | 字串 | 是 | 播放器ID，代表媒體工作階段的唯一識別碼。 |
| `getPlayerDetails` | 函數 | 是 | 傳回播放器詳細資料的函式。 此回呼函式將會由Web SDK在的每個媒體事件之前呼叫 `playerId` 已提供。 |
| `xdm.eventType ` | 物件 | 無 | 媒體事件型別。 若未提供，此專案會自動設為 `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | 物件 | 是 | 工作階段詳細資料物件。 此 `sessionDetails` 物件應包含工作階段詳細資料屬性。 請參閱 [媒體收集結構描述](../../xdm/data-types/media-collection-details.md) 檔案以取得詳細資訊。 |


## 建立手動追蹤的媒體工作階段 {#manual}

若要開始手動追蹤媒體工作階段，請呼叫 `createMediaSession` 方法，其選項如下：

```javascript
const sessionPromise = alloy("createMediaSession", {
    xdm: {
        eventType: "media.sessionStart",
        mediaCollection: {
            playhead: 0,
            sessionDetails: {
                ...
            },
            qoeDataDetails: {
                bitrate: 1000,
                startupTime: 1000,
                fps: 30,
                droppedFrames: 10
            }
        }
    }
});
```

| 屬性 | 類型 | 已要求 | 說明 |
|---------|----------|---------|---------|
| `xdm.eventType` | 物件 | 無 | 媒體事件型別。 若未提供，則會自動設為 `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | 物件 | 是 | 工作階段詳細資料物件。 此 `sessionDetails` 物件應包含工作階段詳細資料屬性。 請參閱 [媒體收集結構描述](../../xdm/data-types/media-collection-details.md) 檔案以取得詳細資訊。 |
| `xdm.mediaCollection.playhead` | 整數 | 是 | 目前的播放點。 |
| `xdm.mediaCollection.qoeDataDetails` | 物件 | 無 | 體驗資料細節的品質。 請參閱 [媒體收集結構描述](../../xdm/data-types/media-collection-details.md) 檔案以取得詳細資訊。 |
