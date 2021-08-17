---
keywords: 標籤延伸模組；標籤延伸模組；launch目的地；平台標籤擴充功能；平台標籤擴充功能；platform launch目的地
title: 在Adobe Experience Platform中標籤擴充功能
description: Adobe Experience Platform提供新一代的標籤管理功能，來自Adobe。 Platform可讓您透過簡單的方式部署及管理所有必要的分析、行銷及廣告標籤功能，以便支援相關客戶體驗。
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: 272cf2906b44ccfeca041d9620ac0780e24ad1ae
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# 在Adobe Experience Platform中標籤擴充功能

Adobe Experience Platform提供新一代的標籤管理功能，來自Adobe。 Platform可讓您透過簡單的方式部署及管理所有必要的分析、行銷及廣告標籤功能，以便支援相關客戶體驗。 標籤以隨附的加值功能形式提供給Adobe Experience Cloud客戶。

如需標籤的簡介，請參閱下列資源：

- [標籤概述](../../../tags/home.md)
- [快速入門手冊](../../../tags/quick-start/quick-start.md)

## 如何在Platform介面中尋找標籤擴充功能 {#how-to-find-extensions-in-interface}

若要在Platform介面中尋找擴充功能，請瀏覽至&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**，然後在&#x200B;**[!UICONTROL Types]**&#x200B;篩選器中選取&#x200B;**[!UICONTROL Extensions]**。

![介面中的擴充功能篩選器](../../assets/catalog/launch-extensions/filter.png)

## 標籤擴充功能如何運作 {#how-extensions-work}

擴充功能會將原始事件資料轉送至數種目的地。 請將擴充功能視為目標的&#x200B;**事件轉送**&#x200B;類型。 這是與目的地平台整合的更簡單類型，目的地平台只會轉送原始事件資料。 這些範例包括[Gainsight個人化擴充功能](../personalization/gainsight.md)或[確認客戶擴充功能之聲音](../voice/confirmit-digital-feedback.md)。

**Adobe Experience Platform中的設** 定檔/區段匯出目的地會擷取事件資料、將其與其他資料來源結合、套用區段，以及將區段和合格設定檔匯出至目的地。這些範例包括[Amazon S3雲端儲存空間目的地](../cloud-storage/amazon-s3.md)或[Google Display &amp; Video 360廣告目的地](../advertising/google-dv360.md)。

![與其他目的地比較的標籤擴充功能](../../assets/common/launch-and-other-destinations.png)

## 使用標籤擴充功能的優點 {#extensions-benefits}

現有Experience Cloud客戶可免費使用Platform的標籤功能。 此系統透過易於使用的擴充功能，簡化網站上的標籤部署，供您安裝、設定、更新及刪除。 標籤會在您的網站上留下很小的空間，並可讓您讓頁面快速載入。

雖然您無法啟動區段以標籤擴充功能，但您可以設定規則，僅在某些情況下轉送事件資料。 此功能強大，可讓您只在特定情況下轉送事件資料，而非在每次互動時傳送事件資料。 如需詳細資訊，請參閱[標籤檔案](../../../tags/ui/managing-resources/rules.md)中的規則。

## 擴充功能的使用案例範例 {#extensions-use-cases}

擴充功能可讓您滿足各種客戶使用案例。 使用擴充功能的一些範例使用案例為：

- 您可以透過Facebook像素擴充功能，將網站或原生應用程式資料傳送至Facebook。 Facebook Pixel會指出訪客瀏覽至您的網站或應用程式的哪些部分，並將該資訊轉送至Facebook，而您可以透過Facebook重新鎖定訪客。
- 您可以將網站和應用程式的事件資料轉送至Google Analytics，以便根據該資料進行分析並做出決策。
- 您可以根據您設定的規則，根據使用者與頁面互動的方式，在正確的時間開啟用戶端的Chatbox應用程式。

## 擴充功能類別 {#extension-categories}

Platform中的擴充功能可屬於下列類別：

- [Advertising](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [資料管理平台](../data-management/overview.md)
- [電子郵件行銷目的地](../email-marketing/overview.md)
- [個人化](../personalization/overview.md)
- [調查](../survey/overview.md)
- [客戶之聲](../voice/overview.md)
