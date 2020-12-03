---
keywords: media analytics extension;media analytics;audio and video extension
title: Adobe Media Analytics for Audio and Video 擴充功能
seo-title: Adobe Media Analytics for Audio and Video 擴充功能
description: Adobe Media Analytics for Audio and Video Extension是即時客戶資料平台中的分析目的地。 如需擴充功能的詳細資訊，請參閱Adobe Exchange的擴充功能頁面。
seo-description: Adobe Media Analytics for Video Extension是即時客戶資料平台中的分析目標。 如需擴充功能的詳細資訊，請參閱Adobe Exchange的擴充功能頁面。
translation-type: tm+mt
source-git-commit: 80db19822551883da272787affb6f7dc9dc3a745
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 9%

---


# Adobe Media Analytics for Audio and Video 擴充功能 版{#adobe-analytics-for-video-extension}

## 概述 {#overview}

Adobe Media Analytics for Audio and Video是基本Analytics產品的附加元件，可為客戶提供強穩的視訊、音訊和廣告度量。

Adobe Media Analytics for Audio and Video是即時客戶資料平台中的分析擴充功能。 如需擴充功能的詳細資訊，請參閱 [Adobe Exchange的擴充功能頁面](https://exchange.adobe.com/experiencecloud.details.100157.html)。

此目的地是分 [!DNL Adobe Experience Platform Launch] 機。 如需擴充功能在即 [!DNL Platform Launch] 時CDP中如何運作的詳細資訊，請參 [閱Experience Platform Launch擴充功能總覽](../launch-extensions/overview.md)。

![Adobe Media Analytics for Audio and Video 擴充功能](../../assets/catalog/analytics/adobe-video-analytics/catalog.png)

## 先決條件 {#prerequisites}

此擴展功能可在目錄 [!DNL Destinations] 中為已購買即時CDP的所有客戶提供。

若要使用此擴充功能，您需要存取 [!DNL Adobe Experience Platform Launch]。 [!DNL Platform Launch] Adobe Experience Cloud客戶可享有附加的附加價值功能。 請連絡您的組織管理員以取得 [!DNL Platform Launch] 存取權，並要求他們授予您 **[!UICONTROL manage_properties]** 權限，以便安裝擴充功能。

## 安裝擴充功能 {#install-extension}

若要安裝Adobe Analytics for Video Extension:

在即時 [CDP介面中](http://platform.adobe.com/)，轉至「目 **[!UICONTROL 標]** 」 **[!UICONTROL >「目]**&#x200B;錄」。

從目錄中選擇副檔名或使用搜索欄。

按一下目標以反白顯示，然後選 **[!UICONTROL 取右邊欄]** 中的設定。 如果「 **[!UICONTROL 設定]** 」控制項呈灰色，表示您遺失 **[!UICONTROL manage_properties]** 權限。 請參 [閱必要條件](#prerequisites)。

在「選 **[!UICONTROL 擇可用的平台啟動屬性]** 」窗口中，選擇 [!DNL Platform Launch] 要安裝擴展的屬性。 您也可以在中選擇建立新屬性 [!DNL Platform Launch]。 屬性是規則、資料元素、設定的擴充功能、環境和程式庫的集合。瞭解檔案「屬性」 [頁面區段中](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) 的 [!DNL Launch] 屬性。

工作流程會帶您 [!DNL Platform Launch] 完成安裝。

如需擴充功能設定選項的詳細資訊，請參 [閱檔案中的「Adobe Media Analytics for Audio and Video extension](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html) 」 [!DNL Experience Launch] 頁面。

您也可以直接在 [Adobe Experience Platform Launch介面中安裝擴充功能](https://launch.adobe.com/)。 請參 [閱說明檔案中的](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) 「新增擴充 [!DNL Platform Launch] 功能」。

## 如何使用擴充功能 {#how-to-use}

在安裝擴充功能後，您可以直接在中開始設定擴充功能的規則 [!DNL Platform Launch]。

在中， [!DNL Platform Launch]您可以為已安裝的擴充功能設定規則，只有在特定情況下，才能將事件資料傳送至擴充功能目的地。 如需為擴充功能設定規則的詳細資訊，請參閱規 [則檔案](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html)。

## 設定、升級和刪除擴充功能 {#configure-upgrade-delete}

您可以在介面中設定、升級和刪除擴充 [!DNL Platform Launch] 功能。

>[!TIP]
>
>如果某個屬性上已安裝擴展，則即時CDP UI仍顯示該擴展的 **[!UICONTROL 安裝]** 。 如「安裝擴充功能」中所述，開始安 [裝工作流程](#install-extension) ，以取 [!DNL Platform Launch] 得並設定或刪除擴充功能。

若要升級您的擴充功能，請參 [閱說明檔案](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) 中的擴充 [!DNL Platform Launch] 功能升級。



