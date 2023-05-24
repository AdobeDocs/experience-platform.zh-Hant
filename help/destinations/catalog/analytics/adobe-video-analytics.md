---
keywords: 媒體分析擴展；媒體分析；音頻和視頻擴展
title: Adobe Media Analytics for Audio and Video 擴充功能
description: Adobe Medium音頻和視頻擴展分析是Adobe Experience Platform的一個分析目標。 有關擴展功能的詳細資訊，請參閱AdobeExchange上的擴展頁。
exl-id: bf33e3e8-a95b-47e3-a1dc-c8f68f80b080
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 8%

---

# Adobe Media Analytics for Audio and Video 擴充功能 {#adobe-analytics-for-video-extension}

## 總覽 {#overview}

Adobe Medium分析音頻和視頻是基礎分析產品的附加元件，為客戶提供對視頻、音頻和廣告的穩健度量。

Adobe Medium音頻和視頻分析是Adobe Experience Platform的分析分析擴展。 有關擴展功能的詳細資訊，請參閱上的擴展頁 [AdobeExchange](https://exchange.adobe.com/experiencecloud.details.100157.html)。

此目標是標籤擴展。 有關標籤擴展在平台中如何工作的詳細資訊，請參見 [標籤擴展概述](../launch-extensions/overview.md)。

![Adobe Media Analytics for Audio and Video 擴充功能](../../assets/catalog/analytics/adobe-video-analytics/catalog.png)

## 先決條件 {#prerequisites}

此擴展在 [!DNL Destinations] 為購買平台的所有客戶編錄。

要使用此副檔名，您需要訪問Adobe Experience Platform中的標籤。 標籤作為附帶的增值功能提供給Adobe Experience Cloud客戶。 請與組織管理員聯繫以獲得對標籤的訪問權限，並請他們授予您 **[!UICONTROL 管理屬性]** 以便您可以安裝擴展。

## 安裝擴展 {#install-extension}

要安裝用於視頻擴展的Adobe Analytics:

在 [平台介面](https://platform.adobe.com/)，轉到 **[!UICONTROL 目標]** > **[!UICONTROL 目錄]**。

從目錄中選擇副檔名或使用搜索欄。

按一下目標以突出顯示它，然後選擇 **[!UICONTROL 配置]** 右欄。 如果 **[!UICONTROL 配置]** 控制項呈灰色顯示，您缺少 **[!UICONTROL 管理屬性]** 權限。 請參閱 [先決條件](#prerequisites)。

選擇要在其中安裝擴展的標籤屬性。 您還可以選擇建立新屬性。 屬性是規則、資料元素、設定的擴充功能、環境和程式庫的集合。瞭解中的屬性 [標籤文檔](../../../tags/ui/administration/companies-and-properties.md)。

工作流將帶您到資料收集UI以完成安裝。

有關擴展配置選項的資訊，請參見 [Adobe Medium音頻和視頻擴展頁分析](../../../tags/extensions/client/media-analytics/overview.md) 的下界。

您還可以直接在 [資料收集UI](https://experience.adobe.com/#/data-collection/)。 請參閱上的指南 [添加新擴展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 的子菜單。

## 如何使用擴展 {#how-to-use}

安裝擴展後，可以開始設定規則。 在「資料收集UI」中，您可以為已安裝的擴展設定規則，以便僅在某些情況下將事件資料發送到擴展目標。 有關設定擴展規則的詳細資訊，請參閱 [規則](../../../tags/ui/managing-resources/rules.md) 的下界。

## 配置、升級和刪除擴展 {#configure-upgrade-delete}

可以在資料收集UI中配置、升級和刪除擴展。

>[!TIP]
>
>如果某個屬性上已安裝擴展，則仍會顯示UI **[!UICONTROL 安裝]** 的。 啟動安裝工作流，如中所述 [安裝擴展](#install-extension) 配置或刪除擴展。

要升級擴展，請參閱 [擴展升級過程](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 的下界。
