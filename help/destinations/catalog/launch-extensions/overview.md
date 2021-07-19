---
keywords: launch擴充功能；launch擴充功能；launch目的地platform launch擴充功能；platform launch擴充功能；platform launch目的地
title: Adobe Experience Platform Launch擴充功能
description: Adobe Experience Platform Launch是新一代Adobe標籤管理功能。  Platform Launch 可讓客戶透過簡單的方式部署及管理所有必要的分析、行銷及廣告整合功能，以便支援相關客戶體驗。
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 12%

---

# Adobe Experience Platform Launch 擴充功能

Adobe Experience Platform Launch是新一代Adobe標籤管理功能。  Platform Launch 可讓客戶透過簡單的方式部署及管理所有必要的分析、行銷及廣告整合功能，以便支援相關客戶體驗。platform launch是以隨附的增值功能形式提供給Adobe Experience Cloud客戶。

如需Experience Platform Launch功能的簡介，請參閱下列資源：

- Adobe Experience Platform Launch [documentation](https://experienceleague.adobe.com/docs/launch/using/home.html?lang=zh-Hant)
- Adobe Experience Platform Launch [快速入門影片](../../../tags/quick-start/videos.md)。 從[Adobe Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU)和[發佈程式概述](https://helpx.adobe.com/tw/analytics/how-to/adobe-launch-publishing-process.html)開始，然後轉至下一個概念。

## 如何在Platform介面中尋找Platform launch擴充功能 {#how-to-find-extensions-in-interface}

若要在Platform介面中尋找Platform launch擴充功能，請瀏覽至&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**，然後在&#x200B;**[!UICONTROL Types]**&#x200B;篩選器中選取&#x200B;**[!UICONTROL Extensions]**。

![介面中的擴充功能篩選器](../../assets/catalog/launch-extensions/filter.png)

## platform launch擴充功能如何運作 {#how-extensions-work}

platform launch擴充功能會將原始事件資料轉送至數種目的地。 請將擴充功能視為目標的&#x200B;**事件轉送**&#x200B;類型。 這是與目的地平台整合的更簡單類型，目的地平台只會轉送原始事件資料。 這些範例包括[Gainsight個人化擴充功能](../personalization/gainsight.md)或[確認客戶擴充功能之聲音](../voice/confirmit-digital-feedback.md)。

**Adobe Experience Platform中的設** 定檔/區段匯出目的地會擷取事件資料、將其與其他資料來源結合、套用區段，以及將區段和合格設定檔匯出至目的地。這些範例包括[Amazon S3雲端儲存空間目的地](../cloud-storage/amazon-s3.md)或[Google Display &amp; Video 360廣告目的地](../advertising/google-dv360.md)。

![Experience Platform Launch擴充功能與其他目的地比較](../../assets/common/launch-and-other-destinations.png)

## 使用Platform launch擴充功能的優點 {#extensions-benefits}

Adobe Experience Platform Launch現有Experience Cloud客戶可免費使用。 platform launch可透過簡單易用的擴充功能，簡化網站上的標籤部署，供您安裝、設定、更新和刪除。 platform launch在您的網站上佔用的空間很小，可讓您保持頁面快速載入。

>[!IMPORTANT]
>
>雖然您無法啟動區段以Platform launch擴充功能，但您可以設定規則，僅在某些情況下轉送事件資料。 請閱讀更多下文。

您可以建立&#x200B;*規則*，以決定何時將事件資料轉送至擴充功能。 此功能強大，可讓您只在特定情況下轉送事件資料，而非在每次互動時傳送事件資料。 如需詳細資訊，請參閱[Adobe Experience Platform Launch檔案](../../../tags/ui/managing-resources/rules.md)中的規則。

## platform launch擴充功能的範例使用案例 {#extensions-use-cases}

platform launch擴充功能可讓您滿足各種客戶使用案例。 使用Platform launch擴充功能的一些範例使用案例為：

- 您可以透過Facebook像素擴充功能，將網站或原生應用程式資料傳送至Facebook。 Facebook Pixel會指出訪客瀏覽至您的網站或應用程式的哪些部分，並將該資訊轉送至Facebook，而您可以透過Facebook重新鎖定訪客。
- 您可以將網站和應用程式的事件資料轉送至Google Analytics，以便根據該資料進行分析並做出決策。
- 您可以根據您在Platform launch中設定的規則，根據使用者與頁面互動的方式，在正確的時間開啟用戶端的Chatbox應用程式。

## 擴充功能類別 {#extension-categories}

platform launch擴充功能可在Platform中屬於下列類別：

- [Advertising](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [資料管理平台](../data-management/overview.md)
- [電子郵件行銷目的地](../email-marketing/overview.md)
- [個人化](../personalization/overview.md)
- [調查](../survey/overview.md)
- [客戶之聲](../voice/overview.md)
