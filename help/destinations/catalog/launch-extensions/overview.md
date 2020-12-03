---
keywords: launch extensions;launch extension;launch destinations; platform launch extensions;platform launch extension;platform launch destinations
title: Experience Platform Launch 延伸功能
seo-title: Experience Platform Launch 延伸功能
description: Launch 是新一代 Adobe 標籤管理功能。Launch 可讓客戶透過簡單的方式部署及管理所有必要的分析、行銷及廣告整合功能，以便支援相關客戶體驗。
seo-description: Launch 是新一代 Adobe 標籤管理功能。Launch 可讓客戶透過簡單的方式部署及管理所有必要的分析、行銷及廣告整合功能，以便支援相關客戶體驗。
translation-type: tm+mt
source-git-commit: 85e6a65e1407ca60e7b63681c045fadaaa24aef9
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 19%

---


# Adobe Experience Platform Launch 擴充功能 {#overview.md}

Adobe Experience Platform Launch是Adobe的新一代標籤管理功能。  Platform Launch 可讓客戶透過簡單的方式部署及管理所有必要的分析、行銷及廣告整合功能，以便支援相關客戶體驗。Platform Launch是以附加的增值功能提供給Adobe Experience Cloud客戶。

如需Experience Platform Launch功能的簡介，請參閱下列資源：
- Adobe Experience Platform Launch [documentation](https://experienceleague.adobe.com/docs/launch/using/overview.html)
- Adobe Experience Platform Launch [quick start videos](https://experienceleague.adobe.com/docs/launch/using/intro/get-started/videos.html?). 從Adobe [Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU) and [Publishing流程簡介開始](https://helpx.adobe.com/tw/analytics/how-to/adobe-launch-publishing-process.html)，接著再談到下一個概念。

## 如何在即時CDP介面中查找平台啟動擴展 {#how-to-find-extensions-in-interface}

要在即時CDP介面中查找平台啟動擴展，請瀏覽到 **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** ，然後在Types過濾器中選 **[!UICONTROL 擇擴展]****** 擴展。

![介面中的擴充功能篩選](../../assets/catalog/launch-extensions/filter.png)

## Platform Launch擴充功能的運作方式 {#how-extensions-work}

Platform Launch擴充功能可將原始事件資料轉送至數種目的地。 將擴充功能設想為 **「事件轉發** 」類型的目標。 這是與目標平台整合的更簡單類型，目標平台只會轉送原始事件資料。 例如Gainsight個人化 [擴充功能](../personalization/gainsight.md) , [或客戶擴充功能的確認聲音](../voice/confirmit-digital-feedback.md)。

**即時客戶資料平台中的描述檔** /區段匯出目標會擷取事件資料，並與其他資料來源結合，套用區段，以及將區段和合格的描述檔匯出至目標。 例如， [Amazon S3雲端儲存空間或](../cloud-storage/amazon-s3.md) Google Display &amp; Video 360廣告目標 [](../advertising/google-dv360.md)。

![Experience Platform Launch擴充功能與其他目的地的比較](../../assets/common/launch-and-other-destinations.png)

## 使用Platform Launch擴充功能的優點 {#extensions-benefits}

Adobe Experience Platform Launch是現有Experience Cloud客戶免費的。 Platform Launch透過易於使用的擴充功能簡化網站上的標籤部署，您可以安裝、設定、更新和刪除這些擴充功能。 Platform Launch在您的網站上佔用的空間很小，可讓您快速保持頁面載入。

>[!IMPORTANT]
>
>雖然您無法將區段啟用至Platform Launch擴充功能，但您可以設定規則，在特定情況下只轉送事件資料。 閱讀以下更多資訊。

您可以建立 *規則* ，以決定何時將事件資料轉送至擴充功能。 此強大功能可讓您僅在特定情況下轉送事件資料，而不需在每次互動時傳送事件資料。 如需詳細資訊，請閱讀 [Adobe Experience Platform Launch檔案中的規則](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html)。

## Platform Launch擴充功能的範例使用案例 {#extensions-use-cases}

Platform Launch擴充功能可讓您滿足各種客戶使用案例。 使用Platform Launch擴充功能的一些範例使用案例包括：

- 您可以透過Facebook像素延伸模組，將網站或原生應用程式資料傳送至Facebook。 Facebook Pixel會指出訪客瀏覽至您的網站或應用程式的哪些部分，將該資訊轉送至Facebook，而您可以透過Facebook重新定位訪客。
- 您可以將事件資料從您的網站和應用程式轉送至Google Analytics，以便根據該資料進行分析並做出決策。
- 您可以根據您在Platform Launch中設定的規則，在適當的時間根據使用者與頁面的互動方式開啟用戶端聊天方塊應用程式。

## 擴充功能類別 {#extension-categories}

Platform Launch擴展可以在即時CDP中歸類於以下類別：

- [廣告](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [資料管理平台](../data-management/overview.md)
- [電子郵件行銷目標](../email-marketing/overview.md)
- [個性化](../personalization/overview.md)
- [調查](../survey/overview.md)
- [客戶之聲](../voice/overview.md)
