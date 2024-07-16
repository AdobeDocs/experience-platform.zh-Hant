---
keywords: 標籤擴充功能；標籤擴充功能；launch目的地；platform標籤擴充功能；platform標籤擴充功能；platform launch目的地
title: Adobe Experience Platform中的標籤擴充功能
description: Adobe Experience Platform提供Adobe新一代的標籤管理功能。 Platform可讓您透過簡單的方式部署及管理所有必要的分析、行銷及廣告整合功能，以便支援相關客戶體驗。
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 2%

---

# Adobe Experience Platform中的標籤擴充功能

Adobe Experience Platform提供Adobe新一代的標籤管理功能。 Platform可讓您透過簡單的方式部署及管理所有必要的分析、行銷及廣告整合功能，以便支援相關客戶體驗。 標籤以隨附加值功能的形式提供給Adobe Experience Cloud客戶。

如需標籤的簡介，請參閱下列資源：

- [標籤總覽](../../../tags/home.md)
- [快速入門手冊](../../../tags/quick-start/quick-start.md)

## 如何在Platform介面中尋找標籤擴充功能 {#how-to-find-extensions-in-interface}

若要在Platform介面中尋找擴充功能，請瀏覽至&#x200B;**[!UICONTROL 目的地]** > **[!UICONTROL 目錄]**，並在&#x200B;**[!UICONTROL 型別]**&#x200B;篩選器中選取&#x200B;**[!UICONTROL 擴充功能]**。

介面中的![擴充功能篩選器](../../assets/catalog/launch-extensions/filter.png)

## 標籤擴充功能的運作方式 {#how-extensions-work}

[標籤擴充功能](../../../tags/home.md#extensions)是增強網站或行動應用程式功能的程式碼套件。 這可能包括傳送原始事件資料到類似[Google Analytics](/help/destinations/catalog/analytics/google-universal-analytics.md)的目的地，但它們也可以提供其他功能。

區分標籤和事件轉送擴充功能很重要。 Platform目的地使用者介面中出現的擴充功能是&#x200B;*標籤擴充功能*。 請參閱事件轉送概觀，以取得關於標籤和事件轉送](/help/tags/ui/event-forwarding/overview.md#differences-between-event-forwarding-and-tags)之間[差異的詳細資訊。



<!--

Extensions forward raw event data to several types of destinations. Think of extensions as an **Event Forwarding** type of destination. This is a simpler type of integration with destination platforms, which only forwards raw event data. Examples of those are the [Gainsight personalization extension](../personalization/gainsight.md) or the [Confirmit Voice of the Customer extension](../voice/confirmit-digital-feedback.md).

**Profile/Segment Export** destinations in Adobe Experience Platform capture event data, combine it with other data sources, apply segmentation, and export audiences and qualified profiles to destinations. Examples of those are the [Amazon S3 cloud storage destination](../cloud-storage/amazon-s3.md) or the [Google Display & Video 360 advertising destination](../advertising/google-dv360.md).

![Tag extensions compared to other destinations](../../assets/common/launch-and-other-destinations.png)

-->

## 使用標籤擴充功能的好處 {#extensions-benefits}

現有的Experience Cloud客戶可免費使用Platform的標籤功能。 系統透過易於使用的擴充功能（您可安裝、設定、更新和刪除）簡化網站上的標籤部署作業。 標籤在您的網站上留下很小的空間，讓您能夠保持頁面快速載入。

雖然您無法啟用對象來標籤擴充功能，但您可以設定規則，只在某些情況下轉送事件資料。 這項強大的功能可讓您只在特定情況下轉送事件資料，而不是在每次互動時傳送事件資料。 如需詳細資訊，請參閱[標籤檔案](../../../tags/ui/managing-resources/rules.md)中的規則。

## 擴充功能的範例使用案例 {#extensions-use-cases}

擴充功能可讓您滿足各種客戶使用案例。 使用擴充功能的一些範例使用案例包括：

- 您可以透過Facebook畫素擴充功能，將網站或原生應用程式資料傳送至Facebook。 facebook Pixel會指出訪客瀏覽到網站或應用程式的哪些部分，將該資訊轉送至Facebook，然後您可以透過Facebook重新鎖定訪客。
- 您可以將網站和應用程式的事件資料轉送到Google Analytics中，以便根據該資料進行分析並做出決策。
- 您可以根據使用者與頁面互動的方式，根據您設定的規則，在適當的時間開啟使用者端聊天箱應用程式。

## 擴充功能類別 {#extension-categories}

擴充功能在Platform中可能屬於下列類別：

- [Advertising](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [資料管理平台](../data-management/overview.md)
- [電子郵件行銷目的地](../email-marketing/overview.md)
- [個人化](../personalization/overview.md)
- [調查](../survey/overview.md)
- [客戶的心聲](../voice/overview.md)
