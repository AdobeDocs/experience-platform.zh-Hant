---
title: sendMediaEvent
description: 瞭解如何使用sendMediaEvent命令來追蹤Web SDK中的媒體工作階段。
exl-id: a38626fd-4810-40a0-8893-e98136634fac
source-git-commit: 877e12f1d53bb4a8d7c2564490d4e8f3e9e34e34
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---

# `sendMediaEvent`

`sendMediaEvent`命令是Web SDK `streamingMedia`元件的一部分。 您可以使用此元件來收集與網站上媒體工作階段相關的資料。 請參閱`streamingMedia` [檔案](configure/streamingmedia.md)以瞭解如何設定此元件。

使用`sendMediaEvent`命令來追蹤媒體播放次數、暫停、完成、播放器狀態更新及其他相關事件。

Web SDK可根據媒體工作階段追蹤的型別處理媒體事件：

* **自動追蹤工作階段的事件處理**。 在此模式中，您不需要將`sessionID`傳遞至媒體事件或播放點值。 Web SDK會根據您提供的播放器ID和啟動媒體工作階段時提供的`getPlayerDetails`回呼函式，為您處理此工作。
* **手動追蹤工作階段的事件處理**。 在此模式中，您必須將`sessionID`與播放點值（整數值）一起傳遞至媒體事件。 如有需要，您也可以傳遞體驗品質資料詳細資訊。

## 依型別處理媒體事件 {#handle-by-type}

選取下方的標籤，以檢視每個事件型別和工作階段追蹤方法（自動或手動）的事件型別處理範例。


### 播放 {#play}

`media.play`事件型別用於追蹤媒體播放開始的時間。 當播放器從其他狀態變更為「正在播放」狀態時，應傳送此事件。 在播放器改變為「正在播放」之前，其他可能的狀態包括「正在緩衝」、使用者從「已暫停」狀態恢復、播放器從錯誤中復原或自動播放。

>[!BEGINTABS]

>[!TAB 自動工作階段追蹤]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.play"
    }
});
```

>[!TAB 手動工作階段追蹤]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.play",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### 暫停 {#pause}

`media.pauseStart`事件型別用於追蹤媒體播放何時暫停。 此事件應在使用者按下&#x200B;**[!UICONTROL 暫停]**&#x200B;時傳送。 沒有繼續事件型別。 當您在`media.pauseStart`之後傳送`media.play`事件時會推斷為繼續。

>[!BEGINTABS]

>[!TAB 自動工作階段追蹤]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.pauseStart"
    }
});
```

>[!TAB 手動工作階段追蹤]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.pauseStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### 錯誤 {#error}

`media.error`事件型別用於追蹤媒體播放期間發生錯誤的時間。 發生錯誤時，應傳送此事件。

>[!BEGINTABS]

>[!TAB 自動工作階段追蹤]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.error",
        mediaCollection: {
            errorDetails: {
                name: "network-error",
                source: "player"
            }
        }
    }
});
```

>[!TAB 手動工作階段追蹤]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.error",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                errorDetails: {
                    name: "network-error",
                    source: "player"
                }
            }
        }
    });
});
```

>[!ENDTABS]


### 廣告插播開始 {#ad-break-start}

`media.adBreakStart`事件型別用於追蹤廣告插播何時開始。 此事件應在廣告插播開始時傳送。

>[!BEGINTABS]

>[!TAB 自動工作階段追蹤]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adBreakStart",
        mediaCollection: {
            advertisingPodDetails: {
                friendlyName: "Mid-roll",
                offset: 0,
                index: 1
            }
        }
    }
});
```

>[!TAB 手動工作階段追蹤]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adBreakStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                advertisingPodDetails: {
                    friendlyName: "Mid-roll",
                    offset: 0,
                    index: 1
                }
            }
        }
    });
});
```

>[!ENDTABS]


### 廣告插播完成 {#ad-break-complete}

`media.adBreakComplete`事件型別用於追蹤廣告插播完成的時間。 此事件應在廣告插播完成時傳送。

>[!BEGINTABS]

>[!TAB 自動工作階段追蹤]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adBreakComplete"
    }
});
```

>[!TAB 手動工作階段追蹤]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adBreakComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### 廣告開始 {#ad-start}

`media.adStart`事件型別是用來追蹤廣告何時開始。 此事件應在廣告開始時傳送。

>[!BEGINTABS]

>[!TAB 自動工作階段追蹤]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adStart",
        mediaCollection: {
            advertisingDetails: {
                friendlyName: "Ad 1",
                name: "/uri-reference/001",
                length: 10,
                advertiser: "Adobe Marketing",
                campaignID: "Adobe Analytics",
                creativeID: "creativeID",
                creativeURL: "https://creativeurl.com",
                placementID: "placementID",
                siteID: "siteID",
                podPosition: 11,
                playerName: "HTML5 player"
            },
            customMetadata: [{
                    name: "myCustomValue3",
                    value: "c3"
                },
                {
                    name: "myCustomValue2",
                    value: "c2"
                },
                {
                    name: "myCustomValue1",
                    value: "c1"
                }
            ]
        }
    }
});
```

>[!TAB 手動工作階段追蹤]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
        eventType: "media.adStart",
        mediaCollection: {
            playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
            sessionID,
            advertisingDetails: {
              friendlyName: "Ad 1",
              name: "/uri-reference/001",
              length: 10,
              advertiser: "Adobe Marketing",
              campaignID: "Adobe Analytics",
              creativeID: "creativeID",
              creativeURL: "https://creativeurl.com",
              placementID: "placementID",
              siteID: "siteID",
              podPosition: 11,
              playerName: "HTML5 player"
            },
            customMetadata: [
              {
                name: "myCustomValue3",
                value: "c3"
              },
              {
                name: "myCustomValue2",
                value: "c2"
              },
              {
                name: "myCustomValue1",
                value: "c1"
              }]
        }
        }
    });
});
```

>[!ENDTABS]


### 廣告完成 {#ad-complete}

`media.adComplete`事件型別用於追蹤廣告完成的時間。 此事件應在廣告完成時傳送。

>[!BEGINTABS]

>[!TAB 自動工作階段追蹤]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adComplete"
    }
});
```

>[!TAB 手動工作階段追蹤]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### 廣告略過 {#ad-skip}

`media.adSkip`事件型別是用來追蹤何時略過廣告。 此事件應在略過廣告時傳送。

>[!BEGINTABS]

>[!TAB 自動工作階段追蹤]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adSkip"
    }
});
```

>[!TAB 手動工作階段追蹤]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adSkip",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### 章節開始 {#chapter-start}

`media.chapterStart`事件型別用於追蹤章節何時開始。 此事件應在章節開始時傳送。

>[!BEGINTABS]

>[!TAB 自動工作階段追蹤]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterStart",
        mediaCollection: {
            chapterDetails: {
                friendlyName: "Chapter 1",
                position: 1,
                length: 10,
                index: 1,
                offset: 0
            },
            customMetadata: [{
                    name: "myCustomValue3",
                    value: "c3"
                },
                {
                    name: "myCustomValue2",
                    value: "c2"
                },
                {
                    name: "myCustomValue1",
                    value: "c1"
                }
            ]
        }
    }
});
```

>[!TAB 手動工作階段追蹤]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                chapterDetails: {
                    friendlyName: "Chapter 1",
                    position: 1,
                    length: 10,
                    index: 1,
                    offset: 0
                },
                customMetadata: [{
                        name: "myCustomValue3",
                        value: "c3"
                    },
                    {
                        name: "myCustomValue2",
                        value: "c2"
                    },
                    {
                        name: "myCustomValue1",
                        value: "c1"
                    }
                ]
            }
        }
    });
});
```

>[!ENDTABS]


### 章節完成 {#chapter-complete}

`media.chapterComplete`事件型別用於追蹤章節何時完成。 此事件應在章節完成時傳送。

>[!BEGINTABS]

>[!TAB 自動工作階段追蹤]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterComplete"
    }
});
```

>[!TAB 手動工作階段追蹤]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### 章節略過 {#chapter-skip}

`media.chapterSkip`事件型別用於追蹤何時略過章節。 此事件應在略過章節時傳送。

>[!BEGINTABS]

>[!TAB 自動工作階段追蹤]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterSkip"
    }
});
```

>[!TAB 手動工作階段追蹤]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterSkip",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### 緩衝開始 {#buffer-start}

`media.bufferStart`事件型別是用來追蹤緩衝何時開始。 此事件應在緩衝開始時傳送。 沒有`bufferResume`事件型別。 當您在`bufferStart`之後傳送播放事件時推斷出`bufferResume`。

>[!BEGINTABS]

>[!TAB 自動工作階段追蹤]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.bufferStart"
    }
});
```

>[!TAB 手動工作階段追蹤]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.bufferStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### 位元速率變更 {#bitrate-change}

`media.bitrateChange`事件型別用於追蹤位元速率變更的時間。 此事件應在位元速率變更時傳送。

>[!BEGINTABS]

>[!TAB 自動工作階段追蹤]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.bitrateChange",
        mediaCollection: {
            qoeDataDetails: {
                framesPerSecond: 1,
                bitrate: 35000,
                droppedFrames: 30,
                timeToStart: 1364
            }
        }
    }
});
```

>[!TAB 手動工作階段追蹤]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.bitrateChange",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                qoeDataDetails: {
                    bitrate: 35000,
                    droppedFrames: 30,
                    timeToStart: 1364
                }
            }
        }
    });
});
```

>[!ENDTABS]


### 狀態更新 {#state-updates}

`media.statesUpdate`事件型別用於追蹤播放器狀態何時變更。 此事件應在播放器狀態變更時傳送。

>[!BEGINTABS]

>[!TAB 自動工作階段追蹤]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.statesUpdate",
        mediaCollection: {
            statesStart: [{
                    name: "mute"
                },
                {
                    name: "pictureInPicture"
                }
            ],
            statesEnd: [{
                name: "fullScreen"
            }]
        }
    }
});
```

>[!TAB 手動工作階段追蹤]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.stateUpdate",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                statesStart: [{
                        name: "mute"
                    },
                    {
                        name: "pictureInPicture"
                    }
                ],
                statesEnd: [{
                    name: "fullScreen"
                }]
            }
        }
    });
});
```

>[!ENDTABS]


### 工作階段結束 {#session-end}

`media.sessionEnd`事件型別用於通知Media Analytics後端在使用者放棄檢視內容且不太可能返回時立即關閉工作階段。

如果您未傳送`sessionEnd`事件，則放棄的工作階段會在未收到任何事件達10分鐘後逾時，或是播放點在30分鐘內未移動。 工作階段會自動刪除。

>[!BEGINTABS]

>[!TAB 自動工作階段追蹤]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionEnd"
    }
});
```

>[!TAB 手動工作階段追蹤]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.sessionEnd",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### 工作階段完成 {#session-complete}

`media.sessionComplete`事件型別用於追蹤媒體工作階段完成的時間。 當主要內容的結尾到達時，應傳送此事件。

>[!BEGINTABS]

>[!TAB 自動工作階段追蹤]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionComplete"
    }
});
```

>[!TAB 手動工作階段追蹤]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.sessionComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]
