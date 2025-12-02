---
title: 串流媒體組態設定
description: 自訂Web SDK標籤擴充功能收集串流媒體資料的方式。
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 4%

---

# 串流媒體組態設定

媒體收集功能可協助您收集與媒體工作階段相關的資料，例如媒體播放數、暫停數、完成數及其他相關事件。 收集後，您可以將此資料傳送至Adobe Experience Platform或Adobe Analytics以產生報表。 此功能提供全方位的解決方案，可追蹤及瞭解您網站上的媒體使用行為。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL Extensions]**，然後選取&#x200B;**[!UICONTROL Configure]**&#x200B;卡片上的[!UICONTROL Adobe Experience Platform Web SDK]。
1. 向下捲動至&#x200B;**[!UICONTROL Streaming media]**&#x200B;區段。

![此影像顯示標籤UI中Web SDK標籤擴充功能的媒體收集設定](../assets/media-collection.png)

## 先決條件

若要使用Web SDK的串流媒體元件，您必須符合下列先決條件：

* 確保您有權存取Adobe Experience Platform或Adobe Analytics。
* 為您使用的資料流啟用&#x200B;**[[!UICONTROL Media Analytics]](/help/datastreams/configure.md#advanced-options)**&#x200B;選項。
* 確定您的資料流使用的結構描述包含媒體收集結構描述欄位。
* 在Web SDK標籤擴充功能中設定串流媒體功能，如本頁所示。

## [!UICONTROL Channel]

發生媒體收集之管道的名稱。 例如 `Video channel`。任何字串值都有效。

## [!UICONTROL Player Name]

屬性用於媒體播放的媒體播放器名稱。

## [!UICONTROL Application Version]

您的屬性用於媒體播放的媒體播放器應用程式版本。

## [!UICONTROL Main ping interval]

主要內容的Ping頻率（秒）。 預設值為 `10`。值範圍從`10`到`50`秒。 如果未指定值，則使用[自動追蹤的工作階段](/help/collection/js/commands/createmediasession.md#automatic)時使用預設值。

## [!UICONTROL Ad ping interval]

廣告內容的Ping頻率（以秒為單位）。 預設值為 `10`。值範圍從`1`到`10`秒。 如果未指定值，則使用[自動追蹤的工作階段](/help/collection/js/commands/createmediasession.md#automatic)時使用預設值。
