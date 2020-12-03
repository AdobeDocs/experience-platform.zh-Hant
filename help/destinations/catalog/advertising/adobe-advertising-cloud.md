---
keywords: Advertising Cloud;advertising cloud extension; advertising cloud destination
title: Adobe Advertising Cloud擴充功能
seo-title: Adobe Advertising Cloud擴充功能
description: Adobe Advertising Cloud擴充功能是即時客戶資料平台中的廣告目的地。 如需擴充功能的詳細資訊，請參閱Adobe Exchange的擴充功能頁面。
seo-description: Adobe Advertising Cloud擴充功能是即時客戶資料平台中的廣告目的地。 如需擴充功能的詳細資訊，請參閱Adobe Exchange的擴充功能頁面。
translation-type: tm+mt
source-git-commit: c24676970629f5a39297001357f8af40895533d9
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 3%

---


# Adobe Advertising Cloud Extension {#adobe-advertising-cloud-extension}

## 概述 {#overview}

這是DSP和 [!DNL Advertising Cloud] 搜尋( [!DNL Advertising Cloud] 目前不支援DCO)的轉換和區段標籤實作擴充功能。

Adobe Advertising Cloud是即時客戶資料平台中的廣告延伸。

此目的地是分 [!DNL Adobe Experience Platform Launch] 機。 如需擴充功能在即 [!DNL Platform Launch] 時CDP中如何運作的詳細資訊，請參 [閱Experience Platform Launch擴充功能總覽](../launch-extensions/overview.md)。

![Adobe Advertising Cloud擴充功能](../../assets/catalog/advertising/adobe-advertising-cloud/catalog.png)

## 先決條件 {#prerequisites}

此擴展功能可在「目標」目錄中為所有已購買即時CDP的客戶提供。

若要使用此擴充功能，您需要存取 [!DNL Experience Platform Launch]。 [!DNL Experience Platform Launch] Adobe Experience Cloud客戶可享有附加的附加價值功能。 請連絡您的組織管理員以取得 [!DNL Launch] 存取權，並要求他們授予您 **[!UICONTROL manage_properties]** 權限，以便安裝擴充功能。

## 安裝擴充功能 {#install-extension}

若要安裝Adobe Advertising Cloud擴充功能：

在即時 [CDP介面中](http://platform.adobe.com/)，轉至「目 **[!UICONTROL 標]** 」 **[!UICONTROL >「目]**&#x200B;錄」。

從目錄中選擇副檔名或使用搜索欄。

按一下目標以反白顯示，然後選 **[!UICONTROL 取右邊欄]** 中的設定。 如果「 **[!UICONTROL 設定]** 」控制項呈灰色，表示您遺失 **[!UICONTROL manage_properties]** 權限。 請參 [閱必要條件](#prerequisites)。

在「選 **[!UICONTROL 擇可用的平台啟動屬性]** 」窗口中，選擇 [!DNL Platform Launch] 要安裝擴展的屬性。 您也可以在中選擇建立新屬性 [!DNL Platform Launch]。 屬性是規則、資料元素、設定的擴充功能、環境和程式庫的集合。瞭解檔案「屬性」 [頁面區段中](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) 的 [!DNL Launch] 屬性。

工作流程會帶您 [!DNL Platform Launch] 完成安裝。

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
