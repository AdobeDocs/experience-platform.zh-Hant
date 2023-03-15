---
keywords: JW播放器；JW播放器；JW播放器；JW擴充功能；JW擴充功能
title: JW Player Analytics（測試版）擴充功能
description: JW Player Analytics(Beta)擴充功能是Adobe Experience Platform中的分析目的地。 如需擴充功能的詳細資訊，請參閱Exchange上的擴充功能頁面。
exl-id: 32bdb2db-5c1b-4184-b6d3-b07dc4d0b324
source-git-commit: b4e869f9bc29122db4fc66ccda752a50c7db729f
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 3%

---

# [!DNL JW Player Analytics] （測試版）擴充功能 {#jw-player-analytics-extension}

## 總覽 {#overview}

此擴充功能會安裝 [!DNL JW Player] 連接適配器 [!DNL JW Player] AdobeVideo Analytics的事件。 運用AdobeVideo Analytics的強大功能，取得詳細的深入分析，以了解客戶的視訊觀看習慣。

[!DNL JW Player Analytics] （測試版）是Adobe Experience Platform中的分析擴充功能。 如需擴充功能的詳細資訊，請參閱 [AdobeExchange](https://exchange.adobe.com/experiencecloud.details.101523.jw-player-analytics-launch-extension.html).

此目的地是標籤擴充功能。 如需標籤擴充功能在Platform中如何運作的詳細資訊，請參閱 [標籤擴充功能概觀](../launch-extensions/overview.md).

![JW Analytics擴充功能](../../assets/catalog/analytics/jw-analytics/catalog.png)

## 先決條件 {#prerequisites}

此擴充功能適用於 [!DNL Destinations] 目錄供已購買Platform的所有客戶使用。

若要使用此擴充功能，您需要存取Adobe Experience Platform中的標籤。 標籤以隨附的加值功能形式提供給Adobe Experience Cloud客戶。 請連絡您的組織管理員以取得標籤的存取權，並要求他們授予您 **[!UICONTROL manage_properties]** 權限，讓您可以安裝擴充功能。

## 安裝擴充功能 {#install-extension}

若要安裝 [!DNL JW Player Analytics] （測試版）擴充功能：

在 [平台介面](https://platform.adobe.com/)，前往 **[!UICONTROL 目的地]** > **[!UICONTROL 目錄]**.

從目錄中選取擴充功能，或使用搜尋列。

按一下目的地以反白標示，然後選取 **[!UICONTROL 設定]** 在右側邊欄。 若 **[!UICONTROL 設定]** 控制項呈灰色，則您缺少 **[!UICONTROL manage_properties]** 權限。 請參閱 [必要條件](#prerequisites).

選取您要安裝擴充功能的屬性。 您也可以選擇建立新屬性。 屬性是規則、資料元素、設定的擴充功能、環境和程式庫的集合。了解中的屬性 [「屬性」頁部分](../../../tags/ui/administration/companies-and-properties.md#properties-page) 的。

工作流程會逐步引導您完成安裝。

如需擴充功能組態選項的相關資訊，請參閱 [JW Player Analytics（測試版）擴充功能頁面](https://exchange.adobe.com/experiencecloud.details.101523.jw-player-analytics-launch-extension.html) 在AdobeExchange中。

您也可以直接在 [資料收集UI](https://experience.adobe.com/#/data-collection/). 如需詳細資訊，請參閱 [新增擴充功能](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 在標籤檔案中。

## 如何使用擴充功能 {#how-to-use}

安裝擴充功能後，您就可以開始設定規則。

您可以為已安裝的擴充功能設定規則，以僅在特定情況下將事件資料傳送至擴充功能目的地。 如需為擴充功能設定規則的詳細資訊，請參閱 [標籤檔案](../../../tags/ui/managing-resources/rules.md).

## 設定、升級和刪除擴充功能 {#configure-upgrade-delete}

您可以在資料收集UI中設定、升級和刪除擴充功能。

>[!TIP]
>
>如果擴充功能已安裝在您的其中一個屬性上，平台UI仍會顯示 **[!UICONTROL 安裝]** ，以取得擴充功能。 啟動安裝工作流程，如 [安裝擴充功能](#install-extension) 設定或刪除擴充功能。

若要升級您的擴充功能，請參閱 [擴充功能升級程式](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 在標籤檔案中。
