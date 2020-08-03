---
title: Adform擴充功能
seo-title: Adform擴充功能
description: Adform擴充功能是Adobe即時客戶資料平台中的分析目標。 如需擴充功能的詳細資訊，請參閱Adobe Exchange的擴充功能頁面。
seo-description: Adform擴充功能是Adobe即時客戶資料平台中的分析目標。 如需擴充功能的詳細資訊，請參閱Adobe Exchange的擴充功能頁面。
translation-type: tm+mt
source-git-commit: be4cf64c89a189a09a4a7774c8fadc76c6ee8458
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 5%

---


# Adform擴充功能 {#adform-extension}

## 概述 {#overview}

Adform網站追蹤擴充功能可讓廣告商使用平台，在其網站上輕鬆實作Adform追蹤 [!DNL Experience Platform Launch] 點。

[!DNL Adform] 是Adobe即時客戶資料平台中的分析擴充功能。 如需擴充功能的詳細資訊，請參閱 [Adobe Exchange的擴充功能頁面](https://exchange.adobe.com/experiencecloud.details.103195.adform-website-tracking.html)

此目的地是分 [!DNL Experience Platform Launch] 機。 如需Adobe Real- [!DNL Launch] time CDP擴充功能如何運作的詳細資訊，請參閱 [Experience Platform Launch擴充功能總覽](/help/rtcdp/destinations/experience-platform-launch-extensions.md)。

![Adform擴充功能](/help/rtcdp/destinations/assets/adform-extension.png)

## 先決條件 {#prerequisites}

此擴充功能可在目錄 [!DNL Destinations] 中提供給所有已購買Adobe即時CDP的客戶。

若要使用此擴充功能，您需要存取 [!DNL Experience Platform Launch]。 [!DNL Experience Platform Launch] Adobe Experience Cloud客戶可享有附加的附加價值功能。 請連絡您的組織管理員以取得 [!DNL Launch] 存取權，並要求他們授予您 **[!UICONTROL manage_properties]** 權限，以便安裝擴充功能。

## 安裝擴充功能 {#install-extension}

若要安裝Adform擴充功能：

1. 在 [Adobe Real-time CDP介面中](http://platform.adobe.com/)，前往「目 **[!UICONTROL 的地]** >目 **[!UICONTROL 錄]**」。
2. 從目錄中選擇副檔名或使用搜索欄。
3. 按一下目的地以反白標示，然後選取右 **[!UICONTROL 側導軌中的「安裝擴充功能]** 」。 如果 **[!UICONTROL Install Extension]** （安裝擴充功能）控制項呈灰色顯示 **[!UICONTROL ，表示您遺失]** manage_properties權限。 請參 [閱必要條件](#prerequisites)。
4. 在「選 **[!UICONTROL 擇可用的啟動屬性]** 」窗口中，選擇 [!DNL Launch] 要安裝副檔名的屬性。 您也可以在Launch中選擇建立新屬性。 屬性是規則、資料元素、設定的擴充功能、環境和程式庫的集合。瞭解檔案「屬性」 [頁面區段中](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) 的 [!DNL Launch] 屬性。
5. 工作流程會帶您 [!DNL Launch] 完成安裝。

如需擴充功能設定選項和安裝支援的詳細資訊，請參 [閱Adobe Exchange的「Adform」頁面](https://exchange.adobe.com/experiencecloud.details.103195.adform-website-tracking.html)。

您也可以直接在 [Experience Platform Launch介面中安裝擴充功能](https://launch.adobe.com/)。 請參 [閱說明檔案中的](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) 「新增擴充 [!DNL Launch] 功能」。


## 如何使用擴充功能 {#how-to-use}

在安裝擴充功能後，您可以直接在中開始設定擴充功能的規則 [!DNL Launch]。

在中， [!DNL Launch]您可以為已安裝的擴充功能設定規則，只有在特定情況下，才能將事件資料傳送至擴充功能目的地。 如需為擴充功能設定規則的詳細資訊，請參閱規 [則檔案](https://docs.adobe.com/help/zh-Hant/launch/using/reference/manage-resources/rules.html)。

## 設定、升級和刪除擴充功能 {#configure-upgrade-delete}

您可以在介面中設定、升級和刪除擴充 [!DNL Launch] 功能。

>[!TIP]
>
>如果擴充功能已安裝在您的其中一個屬性上，Adobe即時CDP使用者介面仍會顯示擴充 **[!UICONTROL 功能的]** 「安裝」。 如「安裝擴充功能」中所述，開始安 [裝工作流程](#install-extension) ，以取 [!DNL Launch] 得並設定或刪除擴充功能。

若要升級您的擴充功能，請參 [閱說明檔案](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) 中的擴充 [!DNL Launch] 功能升級。



