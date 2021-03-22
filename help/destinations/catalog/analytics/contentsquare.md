---
keywords: contentsquare extension;contentsquare目標；contentsquare
title: Contentsquare擴充功能
description: Contentsquare擴充功能是Adobe Experience Platform的分析目的地。 如需擴充功能的詳細資訊，請參閱Adobe交換的擴充功能頁面。
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 5%

---


# [!DNL Contentsquare] 擴充功能 {#contentsquare-extension}

## 概述 {#overview}

視覺化頁面內行為，瞭解客戶放棄的原因，以及您如何改善。 為每個Analytics區段和Target測試的UX和內容元素歸因收入。 安裝[!DNL Contentsquare]標籤，設定自訂變數和事件。 只要按幾下滑鼠，即可開始收集UX分析資料。

[!DNL Contentsquare] 是Adobe Experience Platform的分析擴充功能。有關擴展功能的詳細資訊，請參閱[AdobeExchange](https://exchange.adobe.com/experiencecloud.details.100364.html)上的擴展頁。

這裡是Adobe Experience Platform Launch分機。 如需有關Platform launch擴充功能在Platform中運作的詳細資訊，請參閱[Adobe Experience Platform Launch擴充功能概觀](../launch-extensions/overview.md)。

![Contentsquare擴充功能](../../assets/catalog/analytics/contentsquare/catalog.png)


## 先決條件 {#prerequisites}

此擴充功能可在[!DNL Destinations]目錄中，針對所有已購買平台的客戶提供。

若要使用此擴充功能，您必須存取Adobe Experience Platform Launch。 platform launch是以附帶的增值功能提供給Adobe Experience Cloud客戶的。 請連絡您的組織管理員以取得Platform launch的存取權，並要求他們授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;權限，以便您安裝擴充功能。

## 安裝擴展{#install-extension}

要安裝[!DNL Contentsquare]擴展：

在[平台介面](http://platform.adobe.com/)中，轉至&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**。

從目錄中選擇副檔名或使用搜索欄。

按一下目的地以反白標示，然後在右側導軌中選取&#x200B;**[!UICONTROL Configure]**。 如果&#x200B;**[!UICONTROL Configure]**&#x200B;控制項呈灰色，表示您遺失&#x200B;**[!UICONTROL manage_properties]**&#x200B;權限。 請參閱[先決條件](#prerequisites)。

在&#x200B;**[!UICONTROL Select available Platform Launch property]**&#x200B;窗口中，選擇要安裝副檔名的Platform launch屬性。 您也可以選擇在Platform launch中建立新屬性。 屬性是規則、資料元素、設定的擴充功能、環境和程式庫的集合。瞭解Platform launch文檔的[「屬性」頁面部分](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page)中的屬性。

工作流程會帶您Platform launch完成安裝。

有關擴展配置選項的資訊，請參閱Adobe交換上的[Contentsquare擴展頁](https://exchange.adobe.com/experiencecloud.details.100364.html)。

您也可以直接在[Adobe Experience Platform Launch介面](https://launch.adobe.com/tw/)中安裝擴展。 請參閱Platform launch文檔中的[添加新副檔名](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension)。

## 如何使用副檔名{#how-to-use}

安裝擴充功能後，您就可以直接在Platform launch中開始設定擴充功能的規則。

在Platform launch中，您可以為已安裝的擴充功能設定規則，只有在特定情況下，才會將事件資料傳送至擴充功能目的地。 如需為擴充功能設定規則的詳細資訊，請參閱[規則檔案](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html)。

## 配置、升級和刪除擴展{#configure-upgrade-delete}

您可以在Platform launch介面中設定、升級和刪除擴充功能。

>[!TIP]
>
>如果擴充功能已安裝在您的其中一個屬性上，平台UI仍會針對擴充功能顯示&#x200B;**[!UICONTROL Install]**。 啟動安裝工作流程（如[Install extension](#install-extension)所述），以開始Platform launch並設定或刪除您的擴充功能。

若要升級您的擴充功能，請參閱Platform launch檔案中的[擴充升級](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html)。



