---
keywords: Marketo Munchkin;marketo munchkin;Marketo Munchkin extension;marketo munchkin extension;marketo;Marketo
title: Marketo Munchkin 擴充功能
seo-title: Marketo Munchkin 擴充功能
description: Marketo Munchkin擴充功能是Adobe即時客戶資料平台中的個人化目標。 如需擴充功能的詳細資訊，請參閱Adobe Exchange的擴充功能頁面。
seo-description: Marketo Munchkin擴充功能是Adobe即時客戶資料平台中的個人化目標。 如需擴充功能的詳細資訊，請參閱Adobe Exchange的擴充功能頁面。
translation-type: tm+mt
source-git-commit: 511d64d1555151a70bdb9f71e4b50ec461c8a2e7
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 9%

---


# [!DNL Marketo Munchkin] 擴充功能 {#marketo-munchkin-extension}

## 概述 {#overview}

從銷售機會管理到以客戶為基礎的行銷， [!DNL Marketo Engagement Platform] 都能簡化您在客戶和潛在客戶體驗的每個階段規劃、策劃和衡量互動的方式。

[!DNL Marketo’s Munchkin][!DNL Marketo] JavaScript 可追蹤一般使用者頁面瀏覽次數，以及您的 登陸頁面和外部網頁的點擊次數。

[!DNL Marketo Munchkin] 是Adobe即時客戶資料平台中的電子郵件擴充功能。 如需擴充功能的詳細資訊，請參閱 [Adobe Exchange的擴充功能頁面](https://exchange.adobe.com/experiencecloud.details.101054.marketo-munchkin.html)。

此目的地是Adobe Experience Platform Launch擴充功能。 如需Platform Launch擴充功能如何在Adobe即時CDP中運作的詳細資訊，請參閱 [Adobe Experience Platform Launch擴充功能總覽](/help/rtcdp/destinations/experience-platform-launch-extensions.md)。

![Marketo Munchkin 擴充功能](assets/marketo-munchkin-extension.png)

## 先決條件 {#prerequisites}

此擴充功能可在目錄 [!DNL Destinations] 中提供給所有已購買Adobe即時CDP的客戶。

若要使用此擴充功能，您需要存取Adobe Experience Platform Launch。 Platform Launch是以附加的增值功能提供給Adobe Experience Cloud客戶。 請連絡您的組織管理員以取得Platform Launch的存取權，並要求他們授予您 **[!UICONTROL manage_properties]** 權限，以便您安裝擴充功能。

## 安裝擴充功能 {#install-extension}

要安裝擴展 [!DNL Marketo Munchkin] 名：

1. 在 [Adobe Real-time CDP介面中](http://platform.adobe.com/)，前往「目的地 **[!UICONTROL >目]** 錄 ****」。
2. 從目錄中選擇副檔名或使用搜索欄。
3. 按一下目標以反白顯示，然後選 **[!UICONTROL 取右邊欄]** 中的設定。 如果「 **[!UICONTROL 設定]** 」控制項呈灰色，表示您遺失 **[!UICONTROL manage_properties]** 權限。 請參 [閱必要條件](#prerequisites)。
4. 在「選 **[!UICONTROL 擇可用的平台啟動屬性]** 」窗口中，選擇要安裝擴展的平台啟動屬性。 您也可以選擇在Platform Launch中建立新屬性。 屬性是規則、資料元素、設定的擴充功能、環境和程式庫的集合。瞭解Platform Launch檔案的「 [屬性」頁面](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) ，以瞭解屬性。
5. 工作流程會帶您前往Platform Launch以完成安裝。

如需擴充功能設定選項和安裝支援的詳細資訊，請參 [閱Adobe Exchange的Marketo Munchkin頁面](https://exchange.adobe.com/experiencecloud.details.101054.marketo-munchkin.html)。

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