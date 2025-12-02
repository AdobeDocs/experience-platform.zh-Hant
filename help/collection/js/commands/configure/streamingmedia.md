---
title: streamingMedia
description: 設定Web SDK以收集與您Web屬性上媒體使用相關的資料。
exl-id: f7733619-d35e-43eb-ac90-052717310c39
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 8%

---

# `streamingMedia`

`streamingMedia`元件可協助您收集與網站上的媒體工作階段相關的資料。

收集的資料可包括關於媒體播放、暫停、完成和其他相關事件的資訊。 收集後，您可以將此資料傳送至Adobe Experience Platform或Adobe Analytics以產生報表。 此功能提供全方位的解決方案，可追蹤及瞭解您網站上的媒體使用行為。

## 先決條件

若要使用Web SDK的`streamingMedia`元件，您必須符合下列必要條件：

* 確保您有權存取Adobe Experience Platform或Adobe Analytics。
* 您必須使用Web SDK 2.20.0版或更新版本。 請參閱[網頁SDK安裝概觀](../../install/overview.md)，瞭解如何安裝最新版本。
* 為您使用的資料流啟用&#x200B;**[[!UICONTROL Media Analytics]](/help/datastreams/configure.md#advanced-options)**&#x200B;選項。
* 確定您的資料流使用的結構描述包含媒體收集結構描述欄位。
* 在Web SDK中設定串流媒體功能，如本頁所示。

呼叫`configure`命令時，新增`streamingMedia`物件。

```js
alloy("configure", {
    streamingMedia: {
        channel: "Video channel",
        playerName: "Example player",
        appVersion: "Media Analytics with Web SDK 2.20.0",
        mainPingInterval: 10,
        adPingInterval: 10
    }
});
```

| 屬性 | 類型 | 必要 | 說明 |
| --- | --- | --- | --- |
| **`channel`** | 字串 | 是 | 串流媒體收集發生的頻道名稱。 範例：`Video channel`。 |
| **`playerName`** | 字串 | 是 | 媒體播放器的名稱。 |
| **`appVersion`** | 字串 | 無 | 媒體播放器應用程式的版本。 |
| **`mainPingInterval`** | 整數 | 無 | 主要內容的Ping頻率（秒）。 預設值為 `10`。值範圍從`10`到`50`秒。  如果未指定值，則使用[自動追蹤的工作階段](../createmediasession.md#automatic)時使用預設值。 |
| **`adPingInterval`** | 整數 | 無 | 廣告內容的Ping頻率（秒）。 預設值為 `10`。值範圍從`1`到`10`秒。 如果未指定值，則使用[自動追蹤的工作階段](../createmediasession.md#automatic)時使用預設值。 |

## 使用Web SDK標籤擴充功能設定串流媒體

可以使用[串流媒體組態設定](/help/tags/extensions/client/web-sdk/configure/streaming-media.md)，在Web SDK標籤擴充功能中設定這些設定。
