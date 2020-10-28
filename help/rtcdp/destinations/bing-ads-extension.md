---
keywords: bing;bing ads event tracking;event tracking bing;UET;UET extension
title: Bing Ads通用事件追蹤(UET)擴充功能
seo-title: Bing Ads通用事件追蹤(UET)擴充功能
description: Bing Ads通用事件追蹤(UET)擴充功能是Adobe即時客戶資料平台中的廣告目的地。 如需擴充功能的詳細資訊，請參閱Adobe Exchange的擴充功能頁面。
seo-description: Bing Ads通用事件追蹤(UET)擴充功能是Adobe即時客戶資料平台中的廣告目的地。 如需擴充功能的詳細資訊，請參閱Adobe Exchange的擴充功能頁面。
translation-type: tm+mt
source-git-commit: d9bf874dbfcc00c0a6e267f1a2e96f1223054825
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 6%

---


# [!DNL Bing Ads Universal Event Tracking] (UET)擴充功能 {#bing-ads-extension}

## 概述 {#overview}

[!DNL Bing Ads Universal Event Tracking] (UET)for是 [!DNL Experience Platform Launch] 追蹤某人點按您的搜尋廣告後所發生情況的實用方法。 透過使用單一UET標籤來記錄客戶在您網站上的行為，您可以運用該資料，讓您使用再行銷清單來追蹤轉換或鎖定受眾。

[!DNL Bing Ads Universal Event Tracking] (UET)是Adobe即時客戶資料平台中的廣告延伸。 如需擴充功能的詳細資訊，請參閱 [Adobe Exchange的擴充功能頁面](https://exchange.adobe.com/experiencecloud.details.100154.html)。

此目的地是分 [!DNL Adobe Experience Platform Launch] 機。 如需Adobe Real- [!DNL Platform Launch] time CDP擴充功能如何運作的詳細資訊，請參閱 [Experience Platform Launch擴充功能總覽](/help/rtcdp/destinations/experience-platform-launch-extensions.md)。

![Bing Ads擴充功能](assets/bing-ads-extension.png)


## 先決條件 {#prerequisites}

此擴充功能可在目錄 [!DNL Destinations] 中提供給所有已購買Adobe即時CDP的客戶。

若要使用此擴充功能，您需要存取 [!DNL Adobe Experience Platform Launch]。 [!DNL Platform Launch] Adobe Experience Cloud客戶可享有附加的附加價值功能。 請連絡您的組織管理員以取得 [!DNL Platform Launch] 存取權，並要求他們授予您 **[!UICONTROL manage_properties]** 權限，以便安裝擴充功能。

## 安裝擴充功能 {#install-extension}

要安裝( [!DNL Bing Ads Universal Event Tracking] UET)擴展：

1. 在 [Adobe Real-time CDP介面中](http://platform.adobe.com/)，前往「目的地 **[!UICONTROL >目]** 錄 ****」。
2. 從目錄中選擇副檔名或使用搜索欄。
3. 按一下目標以反白顯示，然後選 **[!UICONTROL 取右邊欄]** 中的設定。 如果「 **[!UICONTROL 設定]** 」控制項呈灰色，表示您遺失 **[!UICONTROL manage_properties]** 權限。 請參 [閱必要條件](#prerequisites)。
4. 在「選 **[!UICONTROL 擇可用的平台啟動屬性]** 」窗口中，選擇 [!DNL Platform Launch] 要安裝擴展的屬性。 您也可以在中選擇建立新屬性 [!DNL Platform Launch]。 屬性是規則、資料元素、設定的擴充功能、環境和程式庫的集合。瞭解檔案「屬性」 [頁面區段中](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) 的 [!DNL Launch] 屬性。
5. 工作流程會帶您 [!DNL Platform Launch] 完成安裝。

如需擴充功能設定選項和安裝支援的詳細資訊，請參閱Adobe Exchange上的 [Bing Ads通用事件追蹤(UET)頁面](https://exchange.adobe.com/experiencecloud.details.100154.html)。

您也可以直接在 [Adobe Experience Platform Launch介面中安裝擴充功能](https://launch.adobe.com/)。 請參 [閱說明檔案中的](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) 「新增擴充 [!DNL Platform Launch] 功能」。


## 如何使用擴充功能 {#how-to-use}

在安裝擴充功能後，您可以直接在中開始設定擴充功能的規則 [!DNL Platform Launch]。

在中， [!DNL Platform Launch]您可以為已安裝的擴充功能設定規則，只有在特定情況下，才能將事件資料傳送至擴充功能目的地。 如需為擴充功能設定規則的詳細資訊，請參閱規 [則檔案](https://docs.adobe.com/help/zh-Hant/launch/using/reference/manage-resources/rules.html)。

## 設定、升級和刪除擴充功能 {#configure-upgrade-delete}

您可以在介面中設定、升級和刪除擴充 [!DNL Platform Launch] 功能。

>[!TIP]
>
>如果擴充功能已安裝在您的其中一個屬性上，Adobe即時CDP使用者介面仍會顯示擴充 **[!UICONTROL 功能的]** 「安裝」。 如「安裝擴充功能」中所述，開始安 [裝工作流程](#install-extension) ，以取 [!DNL Platform Launch] 得並設定或刪除擴充功能。

若要升級您的擴充功能，請參 [閱說明檔案](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) 中的擴充 [!DNL Platform Launch] 功能升級。
