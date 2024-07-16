---
title: streamingMedia
description: 設定Web SDK以收集與您Web屬性上媒體使用相關的資料。
exl-id: f7733619-d35e-43eb-ac90-052717310c39
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 6%

---

# `streamingMedia`

`streamingMedia`元件可協助您收集與網站上的媒體工作階段相關的資料。

收集的資料可包括關於媒體播放、暫停、完成和其他相關事件的資訊。 收集後，您可以將此資料傳送至Adobe Experience Platform和/或Adobe Analytics以產生報表。 此功能提供全方位的解決方案，可追蹤及瞭解您網站上的媒體使用行為。

## 先決條件 {#prerequisites}

若要使用Web SDK的`streamingMedia`元件，您必須符合下列必要條件：

* 確保您有權存取Adobe Experience Platform和/或Adobe Analytics。
* 您必須使用Web SDK 2.20.0版或更新版本。 請參閱[Web SDK安裝概述](../../install/overview.md)，瞭解如何安裝最新版本。
* 為您使用的資料流啟用&#x200B;**[[!UICONTROL Media Analytics]](../../../datastreams/configure.md#advanced-options)**&#x200B;選項。
* 確定您的資料流使用的結構描述包含媒體收集結構描述欄位。
* 透過[標籤擴充功能](#tag-extension)或透過[JavaScript資料庫](#library)設定Web SDK組態的串流媒體功能（如本頁所示）。

## 使用Web SDK標籤擴充功能設定串流媒體 {#tag-extension}

若要在Web SDK標籤擴充功能中設定串流媒體，請遵循下列步驟。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 擴充功能]**，然後按一下[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 設定]**。
1. 依照[Web SDK標籤延伸設定頁面](../../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#media-collection)中的說明設定&#x200B;**[!UICONTROL 串流媒體]**&#x200B;設定。

## 使用Web SDK JavaScript程式庫設定串流媒體 {#library}

若要在Web SDK中設定串流媒體，請使用下列屬性。

呼叫`configure`命令時，新增`streamingMedia`物件。

```js
alloy("configure", {
    streamingMedia: {
        channel: "video channel",
        playerName: "test player",
        appVersion: "Media Analytics with Web SDK 2.20.0",
        mainPingInterval: 10,
        adPingInterval: 10
    }
});
```

| 屬性 | 類型 | 必要 | 說明 |
|---------|----------|---------|---------|
| `channel` | 字串 | 是 | 串流媒體收集發生的頻道名稱。 範例：`Video channel`。 |
| `playerName` | 字串 | 是 | 媒體播放器的名稱。 |
| `appVersion` | 字串 | 無 | 媒體播放器應用程式的版本。 |
| `mainPingInterval` | 整數 | 無 | 主要內容的Ping頻率（秒）。 預設值為 `10`。值範圍從`10`到`50`秒。  如果未指定值，則使用[自動追蹤的工作階段](../createmediasession.md#automatic)時使用預設值。 |
| `adPingInterval` | 整數 | 無 | 廣告內容的Ping頻率（秒）。 預設值為 `10`。值範圍從`1`到`10`秒。 如果未指定值，則使用[自動追蹤的工作階段](../createmediasession.md#automatic)時使用預設值。 |
