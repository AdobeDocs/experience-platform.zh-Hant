---
title: Experience Platform Launch Extensions
seo-title: Experience Platform Launch Extensions
description: ' Launch 是新一代 Adobe 標籤管理功能。Launch 可讓客戶透過簡單的方式部署及管理所有必要的分析、行銷及廣告標籤功能，以便支援相關客戶體驗。'
seo-description: ' Launch 是新一代 Adobe 標籤管理功能。Launch 可讓客戶透過簡單的方式部署及管理所有必要的分析、行銷及廣告標籤功能，以便支援相關客戶體驗。'
translation-type: tm+mt
source-git-commit: 2a082dc46b50eba1a38eb9d6946e17f851b2fd3f

---


# Experience Platform Launch extensions {#experience-platform-launch-extensions}

Experience Platform Launch 是新一代 Adobe 標籤管理功能。Launch 可讓客戶透過簡單的方式部署及管理所有必要的分析、行銷及廣告標籤功能，以便支援相關客戶體驗。Launch是以隨附的增值功能提供給Adobe Experience Cloud客戶。

如需Experience Platform Launch功能的簡介，請參閱下列資源：
* Experience Platform Launch [documentation](https://docs.adobe.com/content/help/zh-Hant/launch/using/overview.html)
* Experience Platform Launch快 [速入門影片](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/videos.html)。 從Experience Platform Launch [和](https://www.youtube.com/embed/rwqqkG1SERU)[Publishing流程簡介開始](https://helpx.adobe.com/tw/analytics/how-to/adobe-launch-publishing-process.html)，接著再談到下一個概念。

## 如何在Adobe即時CDP介面中尋找Launch擴充功能

若要在Adobe即時CDP介面中尋找Launch擴充功能，請瀏覽至篩 **[!UICONTROL Destinations > Catalog]** 選器並 **[!UICONTROL Extensions]** 選取 **[!UICONTROL Types]** 選項。

![介面中的擴充功能篩選](/help/rtcdp/destinations/assets/extensions-filter.png)

## Launch擴充功能的運作方式

啟動擴充功能會將原始事件資料轉送至數種目的地。 將擴充功能設想為 **「事件轉發** 」類型的目標。 這是與目標平台整合的更簡單類型，目標平台只會轉送原始事件資料。 例如Gainsight個人化 [擴充功能](/help/rtcdp/destinations/gainsight-extension.md) , [或客戶擴充功能的確認聲音](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md)。

**Adobe即時客戶資料平台** (Real-time Customer Data Platform)中的描述檔／區段匯出目標可擷取事件資料、將其與其他資料來源結合、套用區段，以及將區段和合格的描述檔匯出至目標。 例如， [Amazon S3雲端儲存空間或](/help/rtcdp/destinations/amazon-s3-destination.md) Google Display &amp; Video 360廣告目標 [](/help/rtcdp/destinations/google-dv360-destination.md)。

![Experience Platform Launch擴充功能與其他目的地的比較](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

## 使用Launch擴充功能的優點

Experience Platform Launch是現有Experience Cloud客戶免費的。 Launch透過易於使用的擴充功能簡化網站上的標籤部署，您可以安裝、設定、更新和刪除這些擴充功能。 Launch在您的網站上佔用的空間很小，可讓您快速保持頁面載入。

>[!IMPORTANT]
>
>雖然您無法將區段啟用為啟動擴充功能，但您可以設定規則，在特定情況下只轉送事件資料。 閱讀以下更多資訊。

您可以建立 *規則* ，以決定何時將事件資料轉送至擴充功能。 此強大功能可讓您僅在特定情況下轉送事件資料，而不需在每次互動時傳送事件資料。 如需詳細資訊，請閱讀 [Launch檔案中的規則](https://docs.adobe.com/help/zh-Hant/launch/using/reference/manage-resources/rules.html)。

## Launch擴充功能的範例使用案例

啟動擴充功能可讓您滿足各種客戶使用案例。 使用Launch擴充功能的一些範例使用案例包括：

* 您可以透過Facebook像素延伸模組，將網站或原生應用程式資料傳送至Facebook。 Facebook Pixel會指出訪客瀏覽至您的網站或應用程式的哪些部分，將該資訊轉送至Facebook，而您可以透過Facebook重新定位訪客。
* 您可以將事件資料從您的網站和應用程式轉送至Google Analytics，以便根據該資料進行分析並做出決策。
* 您可以根據您在Launch中設定的規則，根據使用者與頁面的互動方式，在適當的時間開啟用戶端聊天方塊應用程式。


## 擴充功能類別

Launch extensions可歸入Adobe即時CDP的下列類別：

* [廣告](/help/rtcdp/destinations/advertising-destinations.md)
* [Analytics](/help/rtcdp/destinations/analytics-destinations.md)
* [資料管理平台](/help/rtcdp/destinations/dmp-destinations.md)
* [電子郵件行銷目標](/help/rtcdp/destinations/email-marketing-destinations.md)
* [個性化](/help/rtcdp/destinations/personalization-destinations.md)
* [調查](/help/rtcdp/destinations/survey-destinations.md)
* [客戶之聲](/help/rtcdp/destinations/voice-of-customer-destinations.md)
