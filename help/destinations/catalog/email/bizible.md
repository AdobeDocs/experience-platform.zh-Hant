---
keywords: bizible；bizible擴充功能；bizible目的地
title: Bizible擴充功能
description: Bizible擴充功能是Adobe Experience Platform中的電子郵件目的地。 如需擴充功能的相關詳細資訊，請參閱Adobe交換上的擴充功能頁面。
exl-id: 9e45416d-b951-411c-a59f-34f84529f721
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 4%

---

# [!DNL Bizible] 擴充功能 {#bizible-extension}

## 概觀 {#overview}

[!DNL Bizible] 是領先業界的B2B歸因解決方案，可讓您擁有無與倫比的資料可見度，因此明智的決策可助您實現增長。

[!DNL Bizible] 是Adobe Experience Platform中的電子郵件擴充功能。 如需有關Bizible的詳細資訊，請閱讀 [行銷歸因](https://experienceleague.adobe.com/docs/bizible/using/introduction-to-bizible/overview-resources/marketing-attribution.html) （在Bizible概述資源中）。

此目的地是標籤延伸模組。 如需有關標籤擴充功能在Platform中如何運作的詳細資訊，請參閱 [標籤擴充功能概觀](../launch-extensions/overview.md).

![Bizible擴充功能](../../assets/catalog/email/bizible/catalog.png)

## 先決條件 {#prerequisites}

此擴充功能適用於 [!DNL Destinations] 已購買Platform之所有客戶的目錄。

若要使用此擴充功能，您需要存取Adobe Experience Platform中的標籤。 標籤以隨附加值功能的形式提供給Adobe Experience Cloud客戶。 請聯絡您的組織管理員以取得標籤的存取權，並要求他們授予您 **[!UICONTROL manage_properties]** 許可權，讓您能夠安裝擴充功能。

## 安裝擴充功能 {#install-extension}

若要安裝 [!DNL Bizible] 副檔名：

在 [平台介面](https://platform.adobe.com/)，前往 **[!UICONTROL 目的地]** > **[!UICONTROL 目錄]**.

從目錄中選取擴充功能或使用搜尋列。

按一下目的地以反白顯示，然後選取 **[!UICONTROL 設定]** 在右側邊欄中。 如果 **[!UICONTROL 設定]** 控制項呈現灰色，您缺少 **[!UICONTROL manage_properties]** 許可權。 另請參閱 [必要條件](#prerequisites).

選取您要安裝擴充功能的標籤屬性。 您也可以選擇建立新屬性。 屬性是規則、資料元素、設定的擴充功能、環境和程式庫的集合。瞭解中的屬性 [標籤檔案](../../../tags/ui/administration/companies-and-properties.md).

工作流程會帶您前往資料收集UI以完成安裝。

您也可以直接在中安裝擴充功能 [資料收集UI](https://experience.adobe.com/#/data-collection/). 請參閱以下指南： [新增擴充功能](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 以取得詳細資訊。

## 如何使用擴充功能 {#how-to-use}

安裝擴充功能後，您就可以開始設定規則。 在資料收集UI中，您可以為已安裝的擴充功能設定規則，以只在某些情況下將事件資料傳送至擴充功能目的地。 如需為擴充功能設定規則的詳細資訊，請參閱以下主題的總覽： [規則](../../../tags/ui/managing-resources/rules.md) 標籤檔案中。

## 設定、升級和刪除擴充功能 {#configure-upgrade-delete}

您可以在資料收集UI中設定、升級和刪除擴充功能。

>[!TIP]
>
>如果擴充功能已安裝在您的其中一個屬性上，UI仍會顯示 **[!UICONTROL 安裝]** 用於擴充功能。 依照中的說明開始安裝工作流程 [安裝擴充功能](#install-extension) 以設定或刪除您的擴充功能。

若要升級您的擴充功能，請參閱 [擴充功能升級程式](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 標籤檔案中。
