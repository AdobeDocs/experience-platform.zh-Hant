---
keywords: Nielsen VideoJS Player Handler;nielsen video js player;nielsen videojs player;Nielsen;nielsen;Nielsen videojs player;Nielsen Digital SDK;nielsen digital sdk
title: Nielsen VideoJS播放器處理常式擴充功能
seo-title: Nielsen VideoJS播放器處理常式擴充功能
description: Nielsen VideoJS播放器處理常式擴充功能是即時客戶資料平台中的分析目的地。 如需擴充功能的詳細資訊，請參閱Adobe Exchange的擴充功能頁面。
seo-description: Nielsen VideoJS播放器處理常式擴充功能是即時客戶資料平台中的分析目的地。 如需擴充功能的詳細資訊，請參閱Adobe Exchange的擴充功能頁面。
translation-type: tm+mt
source-git-commit: 6eabcd70b133051205b669253f280cb92c24412f
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 4%

---


# [!DNL Nielsen VideoJS Player Handler] 擴充功能 {#nielsen-vjs-extension}

## 概述 {#overview}

[!DNL Nielsen Digital SDK] 啟動擴充功能透過下列數位測量產品提供觀眾測量：

DCR:提供非線性數位內容（包括含廣告的內容）的日常測量解決方案，可讓您全面檢視桌上型電腦、行動裝置、平板電腦和連線裝置上的數位內容受眾消費。

DTVR:這說明參與節目來源的桌上型電腦和行動裝置上發生的線性電視檢視。 這是MRC針對在電腦和行動裝置上檢視的節目，對電視觀眾評估所做貢獻的第一個認證解決方案。

[!DNL Nielsen VideoJS Player Handler] 是即時客戶資料平台的分析擴充功能。 如需擴充功能的詳細資訊，請參閱 [Adobe Exchange的擴充功能頁面](https://exchange.adobe.com/experiencecloud.details.101361.nielsen-digital-sdk-extension.html)。

此目的地是Adobe Experience Platform Launch擴充功能。 如需Platform Launch擴充功能如何在Adobe即時CDP中運作的詳細資訊，請參閱 [Adobe Experience Platform Launch擴充功能總覽](/help/rtcdp/destinations/experience-platform-launch-extensions.md)。

![Nielsen VideoJS播放器處理常式擴充功能](assets/nielsen-videojs-extension.png)

## 先決條件 {#prerequisites}

此擴充功能可在目錄 [!DNL Destinations] 中提供給所有已購買Adobe即時CDP的客戶。

若要使用此擴充功能，您需要存取Adobe Experience Platform Launch。 Platform Launch是以附加的增值功能提供給Adobe Experience Cloud客戶。 請連絡您的組織管理員以取得Platform Launch的存取權，並要求他們授予您 **[!UICONTROL manage_properties]** 權限，以便您安裝擴充功能。

## 安裝擴充功能 {#install-extension}

要安裝擴展 [!DNL Nielsen VideoJS Player Handler] 名：

1. 在 [Adobe Real-time CDP介面中](http://platform.adobe.com/)，前往「目的地 **[!UICONTROL >目]** 錄 ****」。
2. 從目錄中選擇副檔名或使用搜索欄。
3. 按一下目標以反白顯示，然後選 **[!UICONTROL 取右邊欄]** 中的設定。 如果「 **[!UICONTROL 設定]** 」控制項呈灰色，表示您遺失 **[!UICONTROL manage_properties]** 權限。 請參 [閱必要條件](#prerequisites)。
4. 在「選 **[!UICONTROL 擇可用的平台啟動屬性]** 」窗口中，選擇要安裝擴展的平台啟動屬性。 您也可以選擇在Platform Launch中建立新屬性。 屬性是規則、資料元素、設定的擴充功能、環境和程式庫的集合。瞭解Platform Launch檔案的「 [屬性」頁面](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) ，以瞭解屬性。
5. 工作流程會帶您前往Platform Launch以完成安裝。

如需擴充功能設定選項和安裝支援的詳細資訊，請參閱Adobe Exchange上的 [Nielsen數位SDK頁面](https://exchange.adobe.com/experiencecloud.details.101361.nielsen-digital-sdk-extension.html)。

您也可以直接在 [Adobe Experience Platform Launch介面中安裝擴充功能](https://launch.adobe.com/)。 請參 [閱Platform Launch檔案中](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) 「新增擴充功能」。

## 如何使用擴充功能 {#how-to-use}

在安裝擴充功能後，您就可以直接在Platform Launch中開始設定擴充功能的規則。

在Platform Launch中，您可以為已安裝的擴充功能設定規則，只有在特定情況下，才會將事件資料傳送至擴充功能目的地。 如需為擴充功能設定規則的詳細資訊，請參閱規 [則檔案](https://docs.adobe.com/help/zh-Hant/launch/using/reference/manage-resources/rules.html)。

## 設定、升級和刪除擴充功能 {#configure-upgrade-delete}

您可以在Platform Launch介面中設定、升級和刪除擴充功能。

>[!TIP]
>
>如果擴充功能已安裝在您的其中一個屬性上，Adobe即時CDP使用者介面仍會顯示擴充 **[!UICONTROL 功能的]** 「安裝」。 開始安裝工作流程，如 [Install extension所述](#install-extension) ，以前往Platform Launch並設定或刪除您的擴充功能。

若要升級您的擴充功能，請參 [閱Platform Launch檔案中的](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) 「擴充功能升級」。