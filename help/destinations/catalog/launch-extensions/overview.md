---
keywords: 標籤擴展；標籤擴展；啟動目標平台標籤擴展；平台標籤擴展；platform launch目標
title: 標籤擴展在Adobe Experience Platform
description: Adobe Experience Platform提供了Adobe的下一代標籤管理功能。 平台為您提供了部署和管理所有分析、營銷和廣告標籤的簡單方法，這些標籤是為相關客戶體驗提供動力所必需的。
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: fe71294cb73a25c2c4708b0a6ebe04fc2b97afdf
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---

# 標籤擴展在Adobe Experience Platform

Adobe Experience Platform提供了Adobe的下一代標籤管理功能。 平台為您提供了部署和管理所有分析、營銷和廣告標籤的簡單方法，這些標籤是為相關客戶體驗提供動力所必需的。 標籤作為附帶的增值功能提供給Adobe Experience Cloud客戶。

有關標籤的簡介，請參閱以下資源：

- [標記總覽](../../../tags/home.md)
- [快速入門指南](../../../tags/quick-start/quick-start.md)

## 如何在平台介面中查找標籤擴展 {#how-to-find-extensions-in-interface}

要在平台介面中查找擴展，請瀏覽至 **[!UICONTROL 目標]** > **[!UICONTROL 目錄]** 選擇 **[!UICONTROL 擴展]** 的 **[!UICONTROL 類型]** 的子菜單。

![介面中的擴展篩選器](../../assets/catalog/launch-extensions/filter.png)

## 標籤擴展的工作原理 {#how-extensions-work}

A [標籤擴展](../../../tags/home.md#extensions) 是一個代碼包，可增強網站或移動應用的功能。 這可能包括將原始事件資料發送到目標，例如 [Google Analytics](/help/destinations/catalog/analytics/google-universal-analytics.md) 但也可以發揮其他功能。

區分標籤和事件轉發擴展非常重要。 平台目標用戶介面中顯示的擴展 *標籤擴展*。 有關Windows Server的詳細資訊，請參閱事件轉發概述 [標籤和事件轉發之間的差異](/help/tags/ui/event-forwarding/overview.md#differences-between-event-forwarding-and-tags)。



<!--

Extensions forward raw event data to several types of destinations. Think of extensions as an **Event Forwarding** type of destination. This is a simpler type of integration with destination platforms, which only forwards raw event data. Examples of those are the [Gainsight personalization extension](../personalization/gainsight.md) or the [Confirmit Voice of the Customer extension](../voice/confirmit-digital-feedback.md).

**Profile/Segment Export** destinations in Adobe Experience Platform capture event data, combine it with other data sources, apply segmentation, and export segments and qualified profiles to destinations. Examples of those are the [Amazon S3 cloud storage destination](../cloud-storage/amazon-s3.md) or the [Google Display & Video 360 advertising destination](../advertising/google-dv360.md).

![Tag extensions compared to other destinations](../../assets/common/launch-and-other-destinations.png)

-->

## 使用標籤擴展的好處 {#extensions-benefits}

平台的標籤功能對現有Experience Cloud客戶是免費的。 該系統通過易於使用的擴展功能簡化了網站上的標籤部署，這些擴展功能可以安裝、配置、更新和刪除。 標籤在您的網站上留下很小的空間，使您能夠保持頁面快速載入。

雖然無法激活段以標籤擴展，但可以設定規則以僅轉發某些情況下的事件資料。 此功能強大，使您只能在某些情況下轉發事件資料，而不是在每次交互中發送事件資料。 有關詳細資訊，請閱讀 [標籤文檔](../../../tags/ui/managing-resources/rules.md)。

## 擴展的示例使用案例 {#extensions-use-cases}

擴展使您能夠滿足各種客戶使用情形。 使用擴展的一些示例使用案例包括：

- 您可以通過Facebook像素擴展將網站或本地應用資料發送到Facebook。 Facebook像素指示訪問者瀏覽的站點或應用程式的哪些部分，將該資訊轉發到Facebook，您可以通過Facebook將訪問者重新定向。
- 您可以將事件資料從您的網站和應用轉發到Google Analytics中，以便根據這些資料進行分析和做出決策。
- 您可以根據您設定的規則，根據用戶與頁面的交互方式，在適當的時間開啟客戶端聊天框應用。

## 擴展類別 {#extension-categories}

擴展可以屬於平台中的以下類別：

- [Advertising](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [資料管理平台](../data-management/overview.md)
- [電子郵件營銷目標](../email-marketing/overview.md)
- [個人化](../personalization/overview.md)
- [調查](../survey/overview.md)
- [客戶之聲](../voice/overview.md)
