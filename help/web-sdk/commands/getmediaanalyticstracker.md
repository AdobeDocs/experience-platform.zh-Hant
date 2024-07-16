---
title: getMediaAnalyticsTracker
description: 瞭解如何建立Media Analytics追蹤器物件，並使用它來追蹤媒體事件。
exl-id: ae968da8-7763-4b2a-a716-3014ba0d270d
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 3%

---

# `getMediaAnalyticsTracker`

此Web SDK命令會擷取Media Analytics追蹤器。 您可以使用此命令來建立物件執行個體，然後使用與[Media JS程式庫](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)提供的相同API來追蹤媒體事件。

`getMediaAnalyticsTracker`命令會傳回舊版Media Analytics API。


| 方法名稱 | 說明 | 語法 |
|-----------------|---|----------------|
| `getInstance` | 建立媒體例項以追蹤播放工作階段。 | `Media.getInstance()` |
| `createMediaObject` | 建立包含媒體資訊的物件。 如果傳遞無效的引數，則傳回空白物件。 | `Media.createMediaObject(name, id, length, streamType, mediaType)` |
| `createAdBreakObject` | 建立包含廣告插播資訊的物件。 如果傳遞無效的引數，則傳回空白物件。 | `Media.createAdBreakObject(name, position, startTime)` |
| `createAdObject` | 建立包含廣告資訊的物件。 如果傳遞無效的引數，則傳回空白物件。 | `Media.createAdObject(name, id, position, length)` |
| `createChapterObject` | 建立包含章節資訊的物件。 如果傳遞無效的引數，則傳回空白物件。 | `Media.createChapterObject(name, position, length, startTime)` |
| `createStateObject` | 建立包含狀態資訊的物件。 如果傳遞無效的引數，則傳回空白物件。 | `Media.createStateObject(name)` |
| `createQoEObject` | 建立包含QoE資訊的物件。 如果傳遞無效的引數，則傳回空白物件。 | `Media.createQoEObject(bitrate, startupTime, fps, droppedFrames)` |

## 執行個體方法

| 方法名稱 | 說明 | 語法 |
|---|---|----|
| `trackSessionStart` | 追蹤開始播放的意圖。 這會在媒體追蹤器例項上啟動追蹤工作階段。 | `trackerInstance.trackSessionStart(mediaInfo, contextData)` |
| `trackPlay` | 追蹤媒體播放或在上次暫停後繼續。 | `trackerInstance.trackPlay()` |
| `trackPause` | 追蹤媒體暫停。 | `trackerInstance.trackPause()` |
| `trackComplete` | 追蹤媒體完成。 只有在媒體已完整檢視後，才呼叫此方法。 | `trackerInstance.trackComplete()` |
| `trackSessionEnd` | 追蹤檢視工作階段的結尾。 即使使用者未檢視媒體至完成，仍呼叫此方法。 | `trackerInstance.trackSessionEnd()` |
| `trackError` | 追蹤媒體播放期間發生的錯誤。 | `trackerInstance.trackError("errorId")` |
| `trackEvent` | 追蹤自訂事件。 | `trackerInstance.trackEvent(event, info, contextData)` |
| `updatePlayhead` | 更新播放點位置。 | `trackerInstance.updatePlayhead(playhead)` |
| `updateQoEObject` | 更新體驗品質。 | `trackerInstance.updateQoEObject(qoe)` |

## 常數

| 常數名稱 | 說明 | 值 |
|-----------------|--|-----------------|
| `MediaType` | 媒體型別 | `Video`、`Audio` |
| `StreamType` | 直播類型 | `VOD`，`Live`，`Linear`，`Podcast`，`Audiobook`，`AOD` |
| `VideoMetadataKeys` | 這會定義視訊資料流的標準中繼資料索引鍵 | `Show`、`Season`、`Episode`、`AssetId`、`Genre`、`FirstAirDate`、`FirstDigitalDate`、`Rating`、`Originator`、`Network`、`ShowType`、`AdLoad`、`MVPD`、`Authorized`、`DayPart`、`Feed`、`StreamFormat` |
| `AudioMetadataKeys` | 這會定義音訊資料流的標準中繼資料索引鍵。 | `Artist`，`Album`，`Label`，`Author`，`Station`，`Publisher` |
| `AdMetadataKeys` | 這會定義廣告的標準中繼資料索引鍵。 | `Advertiser`，`CampaignId`，`CreativeId`，`PlacementId`，`SiteId`，`CreativeUrl` |
| `Event` | 這會定義追蹤事件的型別。 | `AdBreakStart`、`AdBreakComplete`、`AdStart`、`AdComplete`、`AdSkip`、`ChapterStart`、`ChapterComplete`、`ChapterSkip`、`SeekStart`、`SeekComplete`、`BufferStart`、`BufferComplete`、`BitrateChange`、`StateStart`、`StateEnd` |
| `PlayerState` | 這會定義追蹤播放器狀態的標準值。 | `FullScreen`，`ClosedCaption`，`Mute`，`PictureInPicture`，`InFocus` |
