---
keywords: 目標擴充功能；目標；目標v2；目標v2擴充功能
title: Adobe Target v2 擴充功能
description: Adobe Target v2擴充功能是Adobe Experience Platform中的個人化目的地。 如需擴充功能的相關詳細資訊，請參閱Adobe交換上的擴充功能頁面。
exl-id: d1d5ebbc-9093-42b0-8d88-58779df3ec89
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 13%

---

# Adobe Target v2 擴充功能 {#adobe-target-v2-extension}

## 總覽 {#overview}

Adobe Target 是 Adobe Experience Cloud 解決方案，提供您量身訂做和個人化客戶體驗所需的一切，以將您的網站和行動網站、應用程式、社交媒體和其他數位通道的營收最大化。

Adobe Target v2是Adobe Experience Platform中的個人化擴充功能。 如需擴充功能的相關詳細資訊，請參閱擴充功能頁面，網址為 [Adobe交換](https://exchange.adobe.com/experiencecloud.details.102722.adobe-target-v2-launch-extension.html).

此目的地是標籤延伸模組。 如需標籤擴充功能在Platform中如何運作的詳細資訊，請參閱 [標籤擴充功能概觀](../launch-extensions/overview.md).

![Adobe Target v2 擴充功能](../../assets/catalog/personalization/adobe-target-v2/catalog.png)

## 先決條件 {#prerequisites}

此擴充功能適用於 [!DNL Destinations] 已購買Platform之所有客戶的目錄。

若要使用此擴充功能，您需要存取Adobe Experience Platform中的標籤。 標籤是以隨附的加值功能形式提供給Adobe Experience Cloud客戶。 請聯絡您的組織管理員以取得標籤的存取權，並要求他們授予您 **[!UICONTROL manage_properties]** 許可權，方便您安裝擴充功能。

## 安裝擴充功能 {#install-extension}

若要安裝Adobe Target v2擴充功能：

在 [平台介面](https://platform.adobe.com/)，前往 **[!UICONTROL 目的地]** > **[!UICONTROL 目錄]**.

從目錄選取擴充功能或使用搜尋列。

按一下目的地以反白顯示，然後選取 **[!UICONTROL 設定]** 在右側邊欄中。 如果 **[!UICONTROL 設定]** 控制項呈現灰色，表示您遺漏 **[!UICONTROL manage_properties]** 許可權。 另請參閱 [必要條件](#prerequisites).

選取您要安裝擴充功能的屬性。 您也可以選擇建立新屬性。 屬性是規則、資料元素、設定的擴充功能、環境和程式庫的集合。檢視檔案： [屬性](../../../tags/ui/administration/companies-and-properties.md#properties-page) 標籤檔案中以進一步瞭解。

工作流程會逐步引導您完成安裝步驟。

如需擴充功能組態選項的相關資訊，請參閱 [Adobe Target v2擴充功能頁面](../../../tags/extensions/client/target-v2/overview.md) 標籤檔案中。

您也可以直接在中安裝擴充功能 [資料彙集UI](https://experience.adobe.com/#/data-collection/). 請參閱指南： [新增擴充功能](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 以取得詳細資訊。


## 如何使用擴充功能 {#how-to-use}

安裝擴充功能後，您就可以開始設定規則。 在資料收集UI中，您可以為已安裝的擴充功能設定規則，以只在某些情況下將事件資料傳送至擴充功能目的地。 如需為擴充功能設定規則的詳細資訊，請參閱以下主題的概觀： [規則](../../../tags/ui/managing-resources/rules.md) 標籤檔案中。

## 設定、升級和刪除擴充功能 {#configure-upgrade-delete}

您可以在資料收集UI中設定、升級和刪除擴充功能。

>[!TIP]
>
>如果擴充功能已安裝在您的其中一個屬性上，UI仍會顯示 **[!UICONTROL 安裝]** 用於擴充功能。 依照中的說明開始安裝工作流程 [安裝擴充功能](#install-extension) 以設定或刪除您的擴充功能。

若要升級您的擴充功能，請參閱 [擴充功能升級程式](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 標籤檔案中。
