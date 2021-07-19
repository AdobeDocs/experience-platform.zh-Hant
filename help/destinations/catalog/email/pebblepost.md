---
keywords: PebblePost;Pebblepost;PebblePost程式直接郵件；Pebblepost程式直接郵件
title: PebblePost擴展
description: PebblePost擴充功能是Adobe Experience Platform的電子郵件目的地。 如需擴充功能的詳細資訊，請參閱Exchange上的擴充功能頁面。
exl-id: 2d0308db-9d75-4cd1-97de-70ce3837369d
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 3%

---

# [!DNL PebblePost] 擴充功能 {#pebblepost-extension}

## 概覽 {#overview}

[!DNL PebblePost's Programmatic Direct Mail®] 解決方案可協助數位行銷人員將線上興趣和意圖連結至可轉換的離線、有形媒體。行銷人員現在可以運用在Adobe中建立的自訂資料區段，針對具有相關、更長久、內部媒體曝光的消費者。 根據回應路徑活動和站上轉換即時分析效能。

[!DNL PebblePost] 是Adobe Experience Platform中的電子郵件擴充功能。如需擴充功能的詳細資訊，請參閱[AdobeExchange](https://exchange.adobe.com/experiencecloud.details.100315.programmatic-direct-mail.html)上的擴充功能頁面。

此目的地為Adobe Experience Platform Launch擴充功能。 如需Platform launch擴充功能在Platform中如何運作的詳細資訊，請參閱[Adobe Experience Platform Launch擴充功能概述](../launch-extensions/overview.md)。

![PebblePost擴展](../../assets/catalog/email/pebblepost/catalog.png)

## 先決條件 {#prerequisites}

[!DNL Destinations]目錄中提供此擴充功能，供已購買Platform的所有客戶使用。

若要使用此擴充功能，您需要存取Adobe Experience Platform Launch。 platform launch是以隨附的增值功能形式提供給Adobe Experience Cloud客戶。 請連絡您的組織管理員以取得Platform launch的存取權，並要求他們授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;權限，以便您安裝擴充功能。

## 安裝擴充功能 {#install-extension}

要安裝[!DNL PebblePost]擴展，請執行以下操作：

在[Platform interface](http://platform.adobe.com/)中，前往&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**。

從目錄中選取擴充功能，或使用搜尋列。

按一下目的地以反白標示，然後選取右側邊欄中的&#x200B;**[!UICONTROL 設定]**。 如果&#x200B;**[!UICONTROL Configure]**&#x200B;控制項呈灰色，表示您缺少&#x200B;**[!UICONTROL manage_properties]**&#x200B;權限。 請參閱[必要條件](#prerequisites)。

在&#x200B;**[!UICONTROL 選擇可用Platform launch屬性]**&#x200B;窗口中，選擇要安裝擴展的Platform launch屬性。 您也可以選擇在Platform launch中建立新屬性。 屬性是規則、資料元素、設定的擴充功能、環境和程式庫的集合。了解Platform launch檔案的[屬性頁面區段](../../../tags/ui/administration/companies-and-properties.md#properties-page)中的屬性。

工作流程會帶您Platform launch完成安裝。

有關擴展配置選項和安裝支援的資訊，請參閱AdobeExchange](https://exchange.adobe.com/experiencecloud.details.100315.programmatic-direct-mail.html)上的[PebblePost頁。

您也可以直接在[Adobe Experience Platform Launch介面](https://launch.adobe.com/tw/)中安裝擴充功能。 請參閱Platform launch檔案中的[新增擴充功能](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension)。

## 如何使用擴充功能 {#how-to-use}

安裝擴充功能後，您就可以直接在Platform launch中開始為其設定規則。

在Platform launch中，您可以為已安裝的擴充功能設定規則，以僅在特定情況下將事件資料傳送至擴充功能目的地。 如需為擴充功能設定規則的詳細資訊，請參閱[規則檔案](../../../tags/ui/managing-resources/rules.md)。

## 設定、升級和刪除擴充功能 {#configure-upgrade-delete}

您可以在Platform launch介面中設定、升級和刪除擴充功能。

>[!TIP]
>
>如果擴充功能已安裝在您的其中一個屬性上，Platform UI仍會顯示擴充功能的&#x200B;**[!UICONTROL Install]**。 按照[安裝擴充功能](#install-extension)中的說明，開始安裝工作流程以Platform launch並配置或刪除您的擴充功能。

若要升級您的擴充功能，請參閱Platform launch檔案中的[擴充功能升級](../../../tags/ui/managing-resources/extensions/extension-upgrade.md)。
