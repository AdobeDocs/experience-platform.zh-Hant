---
keywords: livefyre；livefyre擴充功能
title: Adobe Livefyre擴充功能
description: Adobe Livefyre擴充功能是Adobe Experience Platform中的社交目的地。 如需擴充功能的相關詳細資訊，請參閱Adobe Exchange上的擴充功能頁面。
exl-id: a134c144-e7b8-4d48-8c90-5999e5ceb8a0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 3%

---

# Adobe Livefyre擴充功能 {#adobe-livefyre-extension}

## 概觀 {#overview}

Adobe Livefyre可讓您發現、整理並發佈使用者產生的內容流到您的網站，以建立真實且高度個人化的體驗。

Adobe Livefyre是Adobe Experience Platform中的社交擴充功能。 如需Adobe Livefyre的詳細資訊，請參閱[Livefyre實作指南](https://experienceleague.adobe.com/docs/livefyre/implementation/home.html)。

此目的地是標籤延伸模組。 如需有關標籤擴充功能在Experience Platform中如何運作的詳細資訊，請參閱[標籤擴充功能概觀](../launch-extensions/overview.md)。

![Adobe Livefyre擴充功能](../../assets/catalog/social/adobe-livefyre/catalog.png)

## 先決條件 {#prerequisites}

此擴充功能會在[!DNL Destinations]目錄中提供給所有已購買Experience Platform的客戶。

若要使用此擴充功能，您需要存取Adobe Experience Platform中的標籤。 標籤以隨附加值功能的形式提供給Adobe Experience Cloud客戶。 請連絡您的組織管理員以取得標籤的存取權，並要求他們授與您許可權&#x200B;**[!UICONTROL manage_properties]**，讓您可以安裝擴充功能。

## 安裝擴充功能 {#install-extension}

若要安裝Adobe Livefyre擴充功能：

在[Experience Platform介面](https://platform.adobe.com/)中，前往&#x200B;**[!UICONTROL 目的地]** > **[!UICONTROL 目錄]**。

從目錄中選取擴充功能或使用搜尋列。

按一下目的地以反白顯示，然後在右側邊欄中選取&#x200B;**[!UICONTROL 設定]**。 如果&#x200B;**[!UICONTROL Configure]**&#x200B;控制項呈現灰色，表示您缺少&#x200B;**[!UICONTROL manage_properties]**&#x200B;許可權。 請參閱[必要條件](#prerequisites)。

選取您要安裝擴充功能的標籤屬性。 您也可以選擇建立新屬性。 屬性是規則、資料元素、設定的擴充功能、環境和程式庫的集合。在[標籤檔案](../../../tags/ui/administration/companies-and-properties.md)中瞭解屬性。

工作流程會帶您前往資料收集UI以完成安裝。

您也可以直接在[資料收集UI](https://experience.adobe.com/#/data-collection/)中安裝擴充功能。 如需詳細資訊，請參閱[新增擴充功能](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension)的指南。

## 如何使用擴充功能 {#how-to-use}

安裝擴充功能後，您就可以開始設定規則。 在資料收集UI中，您可以為已安裝的擴充功能設定規則，以只在某些情況下將事件資料傳送至擴充功能目的地。 如需有關設定擴充功能規則的詳細資訊，請參閱標籤檔案中有關[規則](../../../tags/ui/managing-resources/rules.md)的概觀。

## 設定、升級和刪除擴充功能 {#configure-upgrade-delete}

您可以在資料收集UI中設定、升級和刪除擴充功能。

>[!TIP]
>
>如果擴充功能已安裝在您的其中一個屬性上，UI仍會顯示擴充功能的&#x200B;**[!UICONTROL 安裝]**。 依照[安裝擴充功能](#install-extension)中的說明啟動安裝工作流程，以設定或刪除您的擴充功能。

若要升級您的擴充功能，請參閱標籤檔案中的[擴充功能升級程式](../../../tags/ui/managing-resources/extensions/extension-upgrade.md)指南。
