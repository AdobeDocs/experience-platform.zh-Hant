---
keywords: Awin Advertiser mastertag擴充功能；mastertag標籤；Awin;awin;AWIN
title: Awin Advertiser Mastertag擴充功能
description: Awin Advertiser Mastertag擴充功能是Adobe Experience Platform中的廣告目的地。 如需擴充功能的詳細資訊，請參閱Exchange上的擴充功能頁面。
exl-id: 99a9ea40-b89f-4503-91a7-60cc8e1cd6d3
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 3%

---

# [!DNL Awin Advertiser Mastertag] 擴充功能 {#awin-mastertag-extension}

## 概覽 {#overview}

[!DNL MasterTag]是JavaScript程式庫，其中包含Awin追蹤解決方案所需的所有函式，應無條件附加至網站上的每個頁面，包括確認頁面，但排除顯示或處理付款資訊的任何頁面。

[!DNL Awin Advertiser Mastertag] 是Adobe Experience Platform中的廣告擴充功能。如需擴充功能的詳細資訊，請參閱[AdobeExchange](https://exchange.adobe.com/experiencecloud.details.103176.awin-advertiser-mastertag.html)上的擴充功能頁面。

此目的地是標籤擴充功能。 如需擴充功能在Platform中如何運作的詳細資訊，請參閱[標籤擴充功能概述](../launch-extensions/overview.md)。

![UI中的Awin Advertiser Mastertag擴充功能](../../assets/catalog/advertising/awin-mastertag/catalog.png)

## 先決條件 {#prerequisites}

[!DNL Destinations]目錄中提供此擴充功能，供已購買Platform的所有客戶使用。

若要使用此擴充功能，您需要存取Adobe Experience Platform中的標籤。 標籤以隨附的加值功能形式提供給Adobe Experience Cloud客戶。 請連絡您的組織管理員以取得標籤的存取權，並要求他們授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;權限，以便您安裝擴充功能。

## 安裝擴充功能 {#install-extension}

要安裝[!DNL Awin Advertiser Mastertag]擴展，請執行以下操作：

在[Platform interface](http://platform.adobe.com/)中，前往&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**。

從目錄中選取擴充功能，或使用搜尋列。

按一下目的地以反白標示，然後選取右側邊欄中的&#x200B;**[!UICONTROL 設定]**。 如果&#x200B;**[!UICONTROL Configure]**&#x200B;控制項呈灰色，表示您缺少&#x200B;**[!UICONTROL manage_properties]**&#x200B;權限。 請參閱[必要條件](#prerequisites)。

選取您要安裝擴充功能的標籤屬性。 您也可以選擇建立新屬性。 屬性是規則、資料元素、設定的擴充功能、環境和程式庫的集合。了解[標籤檔案](../../../tags/ui/administration/companies-and-properties.md)中的屬性。

工作流程會帶您前往資料收集UI以完成安裝。

如需擴充功能設定選項和安裝支援的相關資訊，請參閱AdobeExchange](https://exchange.adobe.com/experiencecloud.details.103176.awin-advertiser-mastertag.html)上的[Awin廣告商Mastertag頁面。

您也可以直接在[資料收集UI](https://experience.adobe.com/#/data-collection/)中安裝擴充功能。 如需詳細資訊，請參閱[新增新擴充功能](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension)的指南。


## 如何使用擴充功能 {#how-to-use}

安裝擴充功能後，您就可以開始設定規則。 在資料收集UI中，您可以為已安裝的擴充功能設定規則，只有在特定情況下才會將事件資料傳送至擴充功能目的地。 如需為擴充功能設定規則的詳細資訊，請參閱標籤檔案中[rules](../../../tags/ui/managing-resources/rules.md)的概觀。

## 設定、升級和刪除擴充功能 {#configure-upgrade-delete}

您可以在資料收集UI中設定、升級和刪除擴充功能。

>[!TIP]
>
>如果擴充功能已安裝在您的其中一個屬性上，則UI仍會為擴充功能顯示&#x200B;**[!UICONTROL Install]**。 按照[Install extension](#install-extension)中的說明啟動安裝工作流，以配置或刪除您的擴展。

若要升級您的擴充功能，請參閱標籤檔案中[擴充功能升級程式](../../../tags/ui/managing-resources/extensions/extension-upgrade.md)的指南。
