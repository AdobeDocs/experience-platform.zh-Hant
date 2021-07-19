---
keywords: target擴充功能；target;target v2;target v2擴充功能
title: Adobe Target v2 擴充功能
description: Adobe Target v2擴充功能是Adobe Experience Platform中的個人化目的地。 如需擴充功能的詳細資訊，請參閱Exchange上的擴充功能頁面。
exl-id: d1d5ebbc-9093-42b0-8d88-58779df3ec89
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 13%

---

# Adobe Target v2 擴充功能 {#adobe-target-v2-extension}

## 概覽 {#overview}

Adobe Target 是 Adobe Experience Cloud 解決方案，提供您量身訂做和個人化客戶體驗所需的一切，以將您的網站和行動網站、應用程式、社交媒體和其他數位通道的營收最大化。

Adobe Target v2是Adobe Experience Platform中的個人化擴充功能。 如需擴充功能的詳細資訊，請參閱[AdobeExchange](https://exchange.adobe.com/experiencecloud.details.102722.adobe-target-v2-launch-extension.html)上的擴充功能頁面。

此目的地為Adobe Experience Platform Launch擴充功能。 如需Platform launch擴充功能在Platform中如何運作的詳細資訊，請參閱[Adobe Experience Platform Launch擴充功能概述](../launch-extensions/overview.md)。

![Adobe Target v2 擴充功能](../../assets/catalog/personalization/adobe-target-v2/catalog.png)

## 先決條件 {#prerequisites}

[!DNL Destinations]目錄中提供此擴充功能，供已購買Platform的所有客戶使用。

若要使用此擴充功能，您需要[!DNL Adobe Experience Platform Launch]的存取權。 [!DNL Platform Launch] 以隨附增值功能的形式提供給Adobe Experience Cloud客戶。請連絡您的組織管理員以取得[!DNL Platform Launch]的存取權，並要求他們授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;權限，以便您安裝擴充功能。

## 安裝擴充功能 {#install-extension}

若要安裝Adobe Target v2擴充功能：

在[Platform interface](http://platform.adobe.com/)中，前往&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**。

從目錄中選取擴充功能，或使用搜尋列。

按一下目的地以反白標示，然後選取右側邊欄中的&#x200B;**[!UICONTROL 設定]**。 如果&#x200B;**[!UICONTROL Configure]**&#x200B;控制項呈灰色，表示您缺少&#x200B;**[!UICONTROL manage_properties]**&#x200B;權限。 請參閱[必要條件](#prerequisites)。

在&#x200B;**[!UICONTROL 選擇可用的Launch屬性]**&#x200B;窗口中，選擇要安裝該擴展的[!DNL Launch]屬性。 您也可以選擇在[!DNL Launch]中建立新屬性。 屬性是規則、資料元素、設定的擴充功能、環境和程式庫的集合。了解[!DNL Launch]檔案的[屬性頁面區段](../../../tags/ui/administration/companies-and-properties.md#properties-page)中的屬性。

工作流程會帶您前往[!DNL Launch]以完成安裝。

如需擴充功能設定選項的相關資訊，請參閱[!DNL Experience Launch]檔案中的[Adobe Target v2擴充功能頁面](../../../tags/extensions/web/target-v2/overview.md)。

您也可以直接在[Adobe Experience Platform Launch介面](https://launch.adobe.com/tw/)中安裝擴充功能。 請參閱[!DNL Platform Launch]檔案中的[新增擴充功能](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 。


## 如何使用擴充功能 {#how-to-use}

安裝擴充功能後，即可直接在[!DNL Platform Launch]中開始設定擴充功能的規則。

在[!DNL Platform Launch]中，您可以為已安裝的擴充功能設定規則，以僅在特定情況下將事件資料傳送至擴充功能目的地。 如需為擴充功能設定規則的詳細資訊，請參閱[規則檔案](../../../tags/ui/managing-resources/rules.md)。

## 設定、升級和刪除擴充功能 {#configure-upgrade-delete}

您可以在[!DNL Platform Launch]介面中配置、升級和刪除擴展。

>[!TIP]
>
>如果擴充功能已安裝在您的其中一個屬性上，Platform UI仍會顯示擴充功能的&#x200B;**[!UICONTROL Install]**。 按照[安裝擴充功能](#install-extension)中的說明，開始安裝工作流程以前往[!DNL Platform Launch]並設定或刪除您的擴充功能。

若要升級您的擴充功能，請參閱[!DNL Platform Launch]檔案中的[擴充功能升級](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 。
