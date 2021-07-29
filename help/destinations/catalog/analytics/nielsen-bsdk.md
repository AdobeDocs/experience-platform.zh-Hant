---
keywords: Nielsen BSDK;nielsen bsdk;nielsen BSDK
title: Nielsen BSDK擴充功能
description: Nielsen BSDK擴充功能是Adobe Experience Platform中的分析目的地。 如需擴充功能的詳細資訊，請參閱Exchange上的擴充功能頁面。
exl-id: e1c10673-e3f4-474d-98d7-960124b2bfc7
source-git-commit: 6bbccf6751240637c861c2962b64e5247d8abb43
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 4%

---

# [!DNL Nielsen BSDK] 擴充功能 {#nielsen-bsdk-extension}

## 概覽 {#overview}

[!DNL Nielsen Digital SDK] 標籤擴充功能透過下列數位測量產品提供對象測量：

DCR:提供每日測量非線性數位內容（包括含廣告的內容）的測量解決方案，可讓您全面檢視案頭、行動裝置、平板電腦和連線裝置上的數位內容受眾消耗情況。

DTVR:這說明參與節目來源的案頭和行動裝置上發生的線性電視檢視。 這是MRC為在電腦和移動設備上觀看節目而對電視觀眾測量做出貢獻的第一個認證解決方案。

[!DNL Nielsen BSDK] 是Adobe Experience Platform中的analytics擴充功能。如需擴充功能的詳細資訊，請參閱[AdobeExchange](https://exchange.adobe.com/experiencecloud.details.101361.html)上的擴充功能頁面。

此目的地是標籤擴充功能。 如需有關標籤擴充功能在Platform中如何運作的詳細資訊，請參閱[標籤擴充功能概述](../launch-extensions/overview.md)。

![Nielsen BSDK擴充功能](../../assets/catalog/analytics/nielsen-bsdk/catalog.png)

## 先決條件 {#prerequisites}

[!DNL Destinations]目錄中提供此擴充功能，供已購買Platform的所有客戶使用。

若要使用此擴充功能，您需要存取Adobe Experience Platform中的標籤。 標籤以隨附的加值功能形式提供給Adobe Experience Cloud客戶。 請連絡您的組織管理員以取得標籤的存取權，並要求他們授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;權限，以便您安裝擴充功能。 並要求他們授予您&#x200B;**[!UICONTROL manage_properties]**&#x200B;權限，以便您安裝擴充功能。

## 安裝擴充功能 {#install-extension}

要安裝[!DNL Nielsen BSDK]擴展，請執行以下操作：

在[Platform interface](http://platform.adobe.com/)中，前往&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**。

從目錄中選取擴充功能，或使用搜尋列。

按一下目的地以反白標示，然後選取右側邊欄中的&#x200B;**[!UICONTROL 設定]**。 如果&#x200B;**[!UICONTROL Configure]**&#x200B;控制項呈灰色，表示您缺少&#x200B;**[!UICONTROL manage_properties]**&#x200B;權限。 請參閱[必要條件](#prerequisites)。

選取您要安裝擴充功能的屬性。 您也可以選擇建立新屬性。 屬性是規則、資料元素、設定的擴充功能、環境和程式庫的集合。了解標籤檔案中[的「屬性」頁面區段](../../../tags/ui/administration/companies-and-properties.md#properties-page)中的屬性。

工作流程會逐步帶您完成安裝的步驟。

如需擴充功能組態選項和安裝支援的相關資訊，請參閱AdobeExchange](https://exchange.adobe.com/experiencecloud.details.101361.html)上的[ Nielsen BSDK頁面。

您也可以直接在[資料收集UI](https://experience.adobe.com/#/data-collection/)中安裝擴充功能。 如需詳細資訊，請參閱標籤檔案中的[新增新擴充功能](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension)一節。

## 如何使用擴充功能 {#how-to-use}

安裝擴充功能後，您就可以開始設定規則。

您可以為已安裝的擴充功能設定規則，以僅在特定情況下將事件資料傳送至擴充功能目的地。 如需為擴充功能設定規則的詳細資訊，請參閱[標籤檔案](../../../tags/ui/managing-resources/rules.md)。

## 設定、升級和刪除擴充功能 {#configure-upgrade-delete}

您可以在資料收集UI中設定、升級和刪除擴充功能。

>[!TIP]
>
>如果擴充功能已安裝在您的其中一個屬性上，Platform UI仍會顯示擴充功能的&#x200B;**[!UICONTROL Install]**。 按照[Install extension](#install-extension)中的說明啟動安裝工作流，以配置或刪除您的擴展。

若要升級您的擴充功能，請參閱標籤檔案中[擴充功能升級程式](../../../tags/ui/managing-resources/extensions/extension-upgrade.md)的指南。
