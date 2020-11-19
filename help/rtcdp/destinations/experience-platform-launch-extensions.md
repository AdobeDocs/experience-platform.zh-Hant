---
keywords: launch extensions;launch extension;launch destinations; platform launch extensions;platform launch extension;platform launch destinations
title: Experience Platform Launch 延伸功能
seo-title: Experience Platform Launch 延伸功能
description: Launch 是新一代 Adobe 標籤管理功能。Launch 可讓客戶透過簡單的方式部署及管理所有必要的分析、行銷及廣告整合功能，以便支援相關客戶體驗。
seo-description: Launch 是新一代 Adobe 標籤管理功能。Launch 可讓客戶透過簡單的方式部署及管理所有必要的分析、行銷及廣告整合功能，以便支援相關客戶體驗。
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 21%

---


# Adobe Experience Platform Launch 擴充功能 {#experience-platform-launch-extensions}

Adobe Experience Platform Launch是Adobe的新一代標籤管理功能。  Platform Launch 可讓客戶透過簡單的方式部署及管理所有必要的分析、行銷及廣告整合功能，以便支援相關客戶體驗。Platform Launch是以附加的增值功能提供給Adobe Experience Cloud客戶。

如需Experience Platform Launch功能的簡介，請參閱下列資源：
* Adobe Experience Platform Launch [documentation](https://docs.adobe.com/content/help/zh-Hant/launch/using/overview.html)
* Adobe Experience Platform Launch [quick start videos](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/videos.html). 從Adobe [Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU) and [Publishing流程簡介開始](https://helpx.adobe.com/tw/analytics/how-to/adobe-launch-publishing-process.html)，接著再談到下一個概念。

## 如何在Adobe即時CDP介面中尋找Platform Launch擴充功能 {#how-to-find-extensions-in-interface}

若要在Adobe即時CDP介面中尋找Platform Launch擴充功能，請瀏覽至 **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** ，然後在TypesFilter中選取 **[!UICONTROL Extensions]** **** Intessions。

![介面中的擴充功能篩選](/help/rtcdp/destinations/assets/extensions-filter.png)

## Platform Launch擴充功能的運作方式 {#how-extensions-work}

Platform Launch擴充功能可將原始事件資料轉送至數種目的地。 將擴充功能設想為 **「事件轉發** 」類型的目標。 這是與目標平台整合的更簡單類型，目標平台只會轉送原始事件資料。 例如Gainsight個人化 [擴充功能](/help/rtcdp/destinations/gainsight-extension.md) , [或客戶擴充功能的確認聲音](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md)。

**即時客戶資料平台中的描述檔** /區段匯出目標會擷取事件資料，並與其他資料來源結合，套用區段，以及將區段和合格的描述檔匯出至目標。 例如， [Amazon S3雲端儲存空間或](/help/rtcdp/destinations/amazon-s3-destination.md) Google Display &amp; Video 360廣告目標 [](/help/rtcdp/destinations/google-dv360-destination.md)。

![Experience Platform Launch擴充功能與其他目的地的比較](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

## 使用Platform Launch擴充功能的優點 {#extensions-benefits}

Adobe Experience Platform Launch是現有Experience Cloud客戶免費的。 Platform Launch透過易於使用的擴充功能簡化網站上的標籤部署，您可以安裝、設定、更新和刪除這些擴充功能。 Platform Launch在您的網站上佔用的空間很小，可讓您快速保持頁面載入。

>[!IMPORTANT]
>
>雖然您無法將區段啟用至Platform Launch擴充功能，但您可以設定規則，在特定情況下只轉送事件資料。 閱讀以下更多資訊。

您可以建立 *規則* ，以決定何時將事件資料轉送至擴充功能。 此強大功能可讓您僅在特定情況下轉送事件資料，而不需在每次互動時傳送事件資料。 如需詳細資訊，請閱讀 [Adobe Experience Platform Launch檔案中的規則](https://docs.adobe.com/help/zh-Hant/launch/using/reference/manage-resources/rules.html)。

## Platform Launch擴充功能的範例使用案例 {#extensions-use-cases}

Platform Launch擴充功能可讓您滿足各種客戶使用案例。 使用Platform Launch擴充功能的一些範例使用案例包括：

* 您可以透過Facebook像素延伸模組，將網站或原生應用程式資料傳送至Facebook。 Facebook Pixel會指出訪客瀏覽至您的網站或應用程式的哪些部分，將該資訊轉送至Facebook，而您可以透過Facebook重新定位訪客。
* 您可以將事件資料從您的網站和應用程式轉送至Google Analytics，以便根據該資料進行分析並做出決策。
* 您可以根據您在Platform Launch中設定的規則，在適當的時間根據使用者與頁面的互動方式開啟用戶端聊天方塊應用程式。


## 擴充功能類別 {#extension-categories}

Platform Launch擴充功能可歸入Adobe Real-time CDP的下列類別：

* [廣告](/help/rtcdp/destinations/advertising-destinations.md)
* [Analytics](/help/rtcdp/destinations/analytics-destinations.md)
* [資料管理平台](/help/rtcdp/destinations/dmp-destinations.md)
* [電子郵件行銷目標](/help/rtcdp/destinations/email-marketing-destinations.md)
* [個性化](/help/rtcdp/destinations/personalization-destinations.md)
* [調查](/help/rtcdp/destinations/survey-destinations.md)
* [客戶之聲](/help/rtcdp/destinations/voice-of-customer-destinations.md)
