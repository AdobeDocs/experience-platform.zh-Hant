---
keywords: Analytics擴充功能；Analytics擴充功能；目的地分析
title: Adobe Analytics 擴充功能
description: Adobe Analytics擴充功能是Adobe Experience Platform中的分析目的地。 如需擴充功能的詳細資訊，請參閱Exchange上的擴充功能頁面。
exl-id: 95b6e079-09a6-4262-bd01-11f155286aa9
source-git-commit: 468b9309c5184684c0b25c2656a9eef37715af53
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 9%

---

# Adobe Analytics 擴充功能

## 總覽 {#overview}

Adobe Analytics 是領先業界的解決方案，能夠讓您從使用者觀點瞭解客戶，並掌握客戶情報來為您的企業指引方向。

Adobe Analytics是Adobe Experience Platform中的analytics擴充功能。 如需擴充功能的詳細資訊，請參閱 [Adobe Analytics擴充功能概觀](/help/tags/extensions/web/analytics/overview.md) 在「標籤」檔案中。

此目的地是標籤擴充功能。 如需標籤擴充功能在Platform中如何運作的詳細資訊，請參閱 [標籤擴充功能概觀](../launch-extensions/overview.md).

![Adobe Analytics 擴充功能](../../assets/catalog/analytics/adobe-analytics/catalog.png)

## 先決條件 {#prerequisites}

所有已購買Platform的客戶，皆可在「目標」目錄中取得此擴充功能。

若要使用此擴充功能，您需要存取Platform中的標籤。 標籤以隨附的加值功能形式提供給Adobe Experience Cloud客戶。 請連絡您的組織管理員以存取資料收集UI，並要求他們授予您 **[!UICONTROL manage_properties]** 權限，讓您可以安裝擴充功能。

## 安裝擴充功能 {#install-extension}

若要安裝Adobe Analytics擴充功能：

在 [平台介面](https://platform.adobe.com/)，前往 **[!UICONTROL 目的地]** > **[!UICONTROL 目錄]**.

從目錄中選取擴充功能，或使用搜尋列。

按一下目的地以反白標示，然後選取 **[!UICONTROL 設定]** 在右側邊欄。 若 **[!UICONTROL 設定]** 控制項呈灰色，則您缺少 **[!UICONTROL manage_properties]** 權限。 請參閱 [必要條件](#prerequisites).

選取您要安裝擴充功能的標籤屬性。 您也可以選擇建立新屬性。 屬性是規則、資料元素、設定的擴充功能、環境和程式庫的集合。了解中的屬性 [標籤檔案](../../../tags/ui/administration/companies-and-properties.md).

工作流程會帶您前往資料收集UI以完成安裝。

如需擴充功能組態選項的相關資訊，請參閱 [Adobe Analytics擴充功能頁面](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/implement-solutions/analytics.html) 標籤檔案。

您也可以直接在 [資料收集UI](https://experience.adobe.com/#/data-collection/). 請參閱 [新增擴充功能](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 以取得更多資訊。

## 如何使用擴充功能 {#how-to-use}

安裝擴充功能後，您就可以開始設定規則。 在資料收集UI中，您可以為已安裝的擴充功能設定規則，只有在特定情況下才會將事件資料傳送至擴充功能目的地。 如需為擴充功能設定規則的詳細資訊，請參閱 [規則](../../../tags/ui/managing-resources/rules.md) 在標籤檔案中。

## 設定、升級和刪除擴充功能 {#configure-upgrade-delete}

您可以在資料收集UI中設定、升級和刪除擴充功能。

>[!TIP]
>
>如果擴充功能已安裝在您的其中一個屬性上，UI仍會顯示 **[!UICONTROL 安裝]** ，以取得擴充功能。 啟動安裝工作流程，如 [安裝擴充功能](#install-extension) 設定或刪除擴充功能。

若要升級您的擴充功能，請參閱 [擴充功能升級程式](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 在標籤檔案中。
