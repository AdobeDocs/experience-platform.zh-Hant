---
keywords: bizible;bizible extension;bizible destination
title: Bizible extension
description: Bizible擴充功能是Adobe Experience Platform的電子郵件目的地。 如需擴充功能的詳細資訊，請參閱Adobe交換的擴充功能頁面。
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 4%

---


# [!DNL Bizible] 擴充功能 {#bizible-extension}

## 概述 {#overview}

[!DNL Bizible] 是領先業界的B2B歸因解決方案，可讓您無法並行地洞察資料，以便您做出明智的決策，以推動經濟增長。

[!DNL Bizible] 是Adobe Experience Platform的電子郵件分機。有關擴展功能的詳細資訊，請參閱[AdobeExchange](https://exchange.adobe.com/experiencecloud.details.101055.bizible-analytics.html)上的擴展頁。

此目標是[!DNL Adobe Experience Platform Launch]擴展。 如需[!DNL Platform Launch]擴充功能在Platform中運作的詳細資訊，請參閱[Experience Platform Launch擴充功能概述](../launch-extensions/overview.md)。

![Bizible extension](../../assets/catalog/email/bizible/catalog.png)

## 先決條件 {#prerequisites}

此擴充功能可在[!DNL Destinations]目錄中，針對所有已購買平台的客戶提供。

若要使用此擴充功能，您需要存取[!DNL Adobe Experience Platform Launch]。 [!DNL Platform Launch] 作為附帶的增值功能提供給Adobe Experience Cloud客戶。請連絡您的組織管理員以取得[!DNL Platform Launch]的存取權，並要求他們授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;權限，以便您安裝擴充功能。

## 安裝擴展{#install-extension}

要安裝[!DNL Bizible]擴展：

在[平台介面](http://platform.adobe.com/)中，轉至&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**。

從目錄中選擇副檔名或使用搜索欄。

按一下目的地以反白標示，然後在右側導軌中選取&#x200B;**[!UICONTROL Configure]**。 如果&#x200B;**[!UICONTROL Configure]**&#x200B;控制項呈灰色，表示您遺失&#x200B;**[!UICONTROL manage_properties]**&#x200B;權限。 請參閱[先決條件](#prerequisites)。

在&#x200B;**[!UICONTROL Select available Platform Launch property]**&#x200B;窗口中，選擇要安裝副檔名的[!DNL Platform Launch]屬性。 您也可以在[!DNL Platform Launch]中選擇建立新屬性。 屬性是規則、資料元素、設定的擴充功能、環境和程式庫的集合。瞭解[!DNL Launch]檔案的[「屬性」頁面部分](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page)中的屬性。

工作流將帶您到[!DNL Platform Launch]完成安裝。

有關擴展配置選項和安裝支援的資訊，請參見AdobeExchange](https://exchange.adobe.com/experiencecloud.details.101055.bizible-analytics.html)上的[「Bizible」頁。

您也可以直接在[Adobe Experience Platform Launch介面](https://launch.adobe.com/tw/)中安裝擴展。 請參閱[!DNL Platform Launch]檔案中的[新增副檔名](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension)。

## 如何使用副檔名{#how-to-use}

安裝擴充功能後，您就可以直接在[!DNL Platform Launch]中開始設定擴充功能的規則。

在[!DNL Platform Launch]中，您可以為已安裝的擴充功能設定規則，只有在特定情況下才會將事件資料傳送至擴充功能目的地。 如需為擴充功能設定規則的詳細資訊，請參閱[規則檔案](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html)。

## 配置、升級和刪除擴展{#configure-upgrade-delete}

您可以在[!DNL Platform Launch]介面中設定、升級和刪除擴充功能。

>[!TIP]
>
>如果擴充功能已安裝在您的其中一個屬性上，平台UI仍會針對擴充功能顯示&#x200B;**[!UICONTROL Install]**。 啟動安裝工作流程，如[Install extension](#install-extension)所述，以前往[!DNL Platform Launch]並設定或刪除您的擴充功能。

若要升級您的擴充功能，請參閱[!DNL Platform Launch]檔案中的[擴充升級](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html)。