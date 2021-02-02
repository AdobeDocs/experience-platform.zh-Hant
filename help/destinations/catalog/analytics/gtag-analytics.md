---
keywords: Google全域網站標籤；gtag;google gtag;google extension;google gtag extension;GTAG
title: Google全域網站標籤延伸功能
seo-title: Google全域網站標籤延伸功能
description: Google全域網站標籤延伸模組是Adobe Experience Platform中的分析目的地。 如需擴充功能的詳細資訊，請參閱Adobe Exchange的擴充功能頁面。
seo-description: Google全域網站標籤延伸模組是Adobe Experience Platform中的分析目的地。 如需擴充功能的詳細資訊，請參閱Adobe Exchange的擴充功能頁面。
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 3%

---


# [!DNL Google Global Site Tag] 擴充功能 {#gtag-analytics-extension}

## 概述 {#overview}

透過[!DNL Google's Global Site Tag]或gtag.js，將資料傳送至[!DNL Google Analytics]、[!DNL Google Ads]和[!DNL Google Marketing Platform]。 可以設定每個產品的多個帳戶。

[!DNL Google Global Site Tag] 是Adobe Experience Platform中的分析擴充功能。如需擴充功能的詳細資訊，請參閱[Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101437.google-global-site-tag-gtag.html)上的擴充頁。

此目的地是Adobe Experience Platform Launch擴充功能。 如需Platform Launch擴充功能在Platform中運作的詳細資訊，請參閱[Adobe Experience Platform Launch擴充功能概觀](../launch-extensions/overview.md)。

![Google全域網站標籤延伸功能](../../assets/catalog/analytics/gtag-analytics/catalog.png)

## 先決條件 {#prerequisites}

此擴充功能可在[!DNL Destinations]目錄中，針對所有已購買平台的客戶提供。

若要使用此擴充功能，您需要存取Adobe Experience Platform Launch。 Platform Launch是以附加的增值功能提供給Adobe Experience Cloud客戶。 請連絡您的組織管理員以取得Platform Launch的存取權，並要求他們授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;權限，以便您安裝擴充功能。

## 安裝擴展{#install-extension}

要安裝[!DNL Google Global Site Tag]擴展：

在[平台介面](http://platform.adobe.com/)中，轉至&#x200B;**[!UICONTROL 目標]** > **[!UICONTROL 目錄]**。

從目錄中選擇副檔名或使用搜索欄。

按一下目的地以反白標示，然後選取右側導軌中的「設定」。 ****&#x200B;如果&#x200B;**[!UICONTROL Configure]**&#x200B;控制項呈灰色，表示您遺失&#x200B;**[!UICONTROL manage_properties]**&#x200B;權限。 請參閱[先決條件](#prerequisites)。

在&#x200B;**[!UICONTROL 選擇可用的平台啟動屬性]**&#x200B;窗口中，選擇要安裝擴展的平台啟動屬性。 您也可以選擇在Platform Launch中建立新屬性。 屬性是規則、資料元素、設定的擴充功能、環境和程式庫的集合。瞭解Platform Launch檔案的[「屬性」頁面區段](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page)中的屬性。

工作流程會帶您前往Platform Launch以完成安裝。

如需擴充功能設定選項的詳細資訊，請參閱擴充功能的[Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101437.google-global-site-tag-gtag.html)頁面。

您也可以直接在[Adobe Experience Platform Launch介面](https://launch.adobe.com/tw/)中安裝擴充功能。 請參閱Platform Launch檔案中的[新增副檔名](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension)。

## 如何使用副檔名{#how-to-use}

在安裝擴充功能後，您就可以直接在Platform Launch中開始設定擴充功能的規則。

在Platform Launch中，您可以為已安裝的擴充功能設定規則，只有在特定情況下，才會將事件資料傳送至擴充功能目的地。 如需為擴充功能設定規則的詳細資訊，請參閱[規則檔案](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html)。

## 配置、升級和刪除擴展{#configure-upgrade-delete}

您可以在Platform Launch介面中設定、升級和刪除擴充功能。

>[!TIP]
>
>如果擴充功能已安裝在您的其中一個屬性上，平台UI仍會針對擴充功能顯示&#x200B;**[!UICONTROL Install]**。 啟動安裝工作流程（如[Install extension](#install-extension)所述），以前往「平台啟動」並設定或刪除您的擴充功能。

若要升級您的擴充功能，請參閱Platform Launch檔案中的[Extension upgrade](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html)。



