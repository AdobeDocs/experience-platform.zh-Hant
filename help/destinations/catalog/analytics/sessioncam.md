---
keywords: SessionCam;session cam;sessioncam
title: SessionCam擴充功能
seo-title: SessionCam擴充功能
description: SessionCam擴充功能是即時客戶資料平台中的分析目標。 如需擴充功能的詳細資訊，請參閱Adobe Exchange的擴充功能頁面。
seo-description: SessionCam擴充功能是即時客戶資料平台中的分析目標。 如需擴充功能的詳細資訊，請參閱Adobe Exchange的擴充功能頁面。
translation-type: tm+mt
source-git-commit: 80db19822551883da272787affb6f7dc9dc3a745
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 4%

---


# [!DNL SessionCam] 擴充功能 {#sessioncam-extension}

## 概述 {#overview}

[!DNL SessionCam] 提供一套重要的工具，可顯示使用者行為，並顯示要修正的最重要問題。

[!DNL SessionCam] 是即時客戶資料平台的分析擴充功能。 如需擴充功能的詳細資訊，請參閱 [Adobe Exchange的擴充功能頁面](https://exchange.adobe.com/experiencecloud.details.100517.html)。

此目的地是Adobe Experience Platform Launch擴充功能。 如需Platform Launch擴充功能如何在即時CDP中運作的詳細資訊，請參閱 [Adobe Experience Platform Launch擴充功能總覽](../launch-extensions/overview.md)。

![SessionCam擴充功能](../../assets/catalog/analytics/sessioncam/catalog.png)

## 先決條件 {#prerequisites}

此擴展功能可在目錄 [!DNL Destinations] 中為已購買即時CDP的所有客戶提供。

若要使用此擴充功能，您需要存取Adobe Experience Platform Launch。 Platform Launch是以附加的增值功能提供給Adobe Experience Cloud客戶。 請連絡您的組織管理員以取得Platform Launch的存取權，並要求他們授予您 **[!UICONTROL manage_properties]** 權限，以便您安裝擴充功能。

## 安裝擴充功能 {#install-extension}

要安裝擴展 [!DNL SessionCam] 名：

在即時 [CDP介面中](http://platform.adobe.com/)，轉至「目 **[!UICONTROL 標]** 」 **[!UICONTROL >「目]**&#x200B;錄」。

從目錄中選擇副檔名或使用搜索欄。

按一下目標以反白顯示，然後選 **[!UICONTROL 取右邊欄]** 中的設定。 如果「 **[!UICONTROL 設定]** 」控制項呈灰色，表示您遺失 **[!UICONTROL manage_properties]** 權限。 請參 [閱必要條件](#prerequisites)。

在「選 **[!UICONTROL 擇可用的平台啟動屬性]** 」窗口中，選擇要安裝擴展的平台啟動屬性。 您也可以選擇在Platform Launch中建立新屬性。 屬性是規則、資料元素、設定的擴充功能、環境和程式庫的集合。瞭解Platform Launch檔案的「 [屬性」頁面](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) ，以瞭解屬性。

工作流程會帶您前往Platform Launch以完成安裝。

如需擴充功能設定選項和安裝支援的詳細資訊，請參 [閱Adobe Exchange的SessionCam頁面](https://exchange.adobe.com/experiencecloud.details.100517.html)。

您也可以直接在 [Adobe Experience Platform Launch介面中安裝擴充功能](https://launch.adobe.com/)。 請參 [閱Platform Launch檔案中](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) 「新增擴充功能」。

## 如何使用擴充功能 {#how-to-use}

在安裝擴充功能後，您就可以直接在Platform Launch中開始設定擴充功能的規則。

在Platform Launch中，您可以為已安裝的擴充功能設定規則，只有在特定情況下，才會將事件資料傳送至擴充功能目的地。 如需為擴充功能設定規則的詳細資訊，請參閱規 [則檔案](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html)。

## 設定、升級和刪除擴充功能 {#configure-upgrade-delete}

您可以在Platform Launch介面中設定、升級和刪除擴充功能。

>[!TIP]
>
>如果某個屬性上已安裝擴展，則即時CDP UI仍顯示該擴展的 **[!UICONTROL 安裝]** 。 開始安裝工作流程，如 [Install extension所述](#install-extension) ，以前往Platform Launch並設定或刪除您的擴充功能。

若要升級您的擴充功能，請參 [閱Platform Launch檔案中的](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) 「擴充功能升級」。