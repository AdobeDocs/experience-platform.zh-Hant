---
keywords: bing;bing廣告事件跟蹤；事件跟蹤bing;UET;UET擴展
title: 必應廣告通用事件跟蹤(UET)擴展
description: 必應廣告環球事件跟蹤(UET)擴展是Adobe Experience Platform的一個廣告目的地。 有關擴展功能的詳細資訊，請參閱AdobeExchange上的擴展頁。
exl-id: f2fc4d1f-01b0-4813-902c-9a3c30a8fa78
source-git-commit: c8d6c156b3351324fe1be11144afeae91f7a2a59
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 4%

---

# [!DNL Bing Ads Universal Event Tracking] (UET)擴展 {#bing-ads-extension}

## 總覽 {#overview}

的 [!DNL Bing Ads Universal Event Tracking] (UET)標籤擴展是跟蹤某人按一下您的搜索廣告後發生的情況的有用方法。 通過使用單個UET標籤記錄客戶在您的網站上所做的工作，您可以利用該資料，從而允許您使用重新營銷清單跟蹤轉換或目標受眾。

[!DNL Bing Ads Universal Event Tracking] UET)是Adobe Experience Platform的廣告分銷。 有關擴展功能的詳細資訊，請參閱上的擴展頁 [AdobeExchange](https://exchange.adobe.com/experiencecloud.details.100154.html)。

此目標是標籤擴展。 有關標籤擴展在平台中如何工作的詳細資訊，請參見 [標籤擴展概述](../launch-extensions/overview.md)。

![必應廣告擴展](../../assets/catalog/advertising/bing-ads/catalog.png)

## 先決條件 {#prerequisites}

此擴展在 [!DNL Destinations] 為購買平台的所有客戶編錄。

要使用此副檔名，您需要訪問Adobe Experience Platform中的標籤。 標籤作為附帶的增值功能提供給Adobe Experience Cloud客戶。 請與組織管理員聯繫以獲得對標籤的訪問權限，並請他們授予您 **[!UICONTROL 管理屬性]** 以便您可以安裝擴展。

## 安裝擴展 {#install-extension}

安裝 [!DNL Bing Ads Universal Event Tracking] (UET)分機：

在 [平台介面](https://platform.adobe.com/)，轉到 **[!UICONTROL 目標]** > **[!UICONTROL 目錄]**。

從目錄中選擇副檔名或使用搜索欄。

按一下目標以突出顯示它，然後選擇 **[!UICONTROL 配置]** 右欄。 如果 **[!UICONTROL 配置]** 控制項呈灰色顯示，您缺少 **[!UICONTROL 管理屬性]** 權限。 請參閱 [先決條件](#prerequisites)。

選擇要在其中安裝擴展的標籤屬性。 您還可以選擇建立新屬性。 屬性是規則、資料元素、設定的擴充功能、環境和程式庫的集合。瞭解中的屬性 [標籤文檔](../../../tags/ui/administration/companies-and-properties.md)。

工作流將帶您到資料收集UI以完成安裝。

有關擴展配置選項和安裝支援的資訊，請參見 [Bing廣告AdobeExchange上的通用事件跟蹤(UET)頁](https://exchange.adobe.com/experiencecloud.details.100154.html)。

您還可以直接在 [資料收集UI](https://experience.adobe.com/#/data-collection/)。 請參閱上的指南 [添加新擴展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 的子菜單。


## 如何使用擴展 {#how-to-use}

安裝擴展後，可以開始設定規則。 在「資料收集UI」中，您可以為已安裝的擴展設定規則，以便僅在某些情況下將事件資料發送到擴展目標。 有關設定擴展規則的詳細資訊，請參閱 [規則](../../../tags/ui/managing-resources/rules.md) 的下界。

## 配置、升級和刪除擴展 {#configure-upgrade-delete}

可以在資料收集UI中配置、升級和刪除擴展。

>[!TIP]
>
>如果某個屬性上已安裝擴展，則仍會顯示UI **[!UICONTROL 安裝]** 的。 啟動安裝工作流，如中所述 [安裝擴展](#install-extension) 配置或刪除擴展。

要升級擴展，請參閱 [擴展升級過程](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 的下界。
