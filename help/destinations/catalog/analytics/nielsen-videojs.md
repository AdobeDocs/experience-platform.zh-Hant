---
keywords: 尼爾森視頻JS播放器處理器；尼爾森視頻JS播放器；尼爾森視頻播放器；尼爾森；尼爾森視頻播放器；尼爾森數字軟體開發工具包
title: Nielsen VideoJS播放器處理程式擴展
description: Nielsen VideoJS播放器處理程式擴展是Adobe Experience Platform的一個分析目的地。 有關擴展功能的詳細資訊，請參閱AdobeExchange上的擴展頁。
exl-id: d640bf40-c6af-4aff-8303-933fe71f4a7e
source-git-commit: b4e869f9bc29122db4fc66ccda752a50c7db729f
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 3%

---

# [!DNL Nielsen VideoJS Player Handler] 擴充功能 {#nielsen-vjs-extension}

## 總覽 {#overview}

[!DNL Nielsen Digital SDK] 標籤擴展通過以下數字測量產品提供觀眾測量：

DCR:一種提供非線性數字內容（包括帶有廣告的內容）的日常測量的測量解決方案將使您能夠全面瞭解案頭、移動、平板電腦和連接設備上的數字內容受眾消費情況。

DTVR:這說明在用於參與節目源的案頭和移動設備上發生的線性電視觀看。 這是首個獲得MRC認證的解決方案，因為MRC對在電腦和移動設備上觀看電視節目的電視觀眾量度做出了貢獻。

[!DNL Nielsen VideoJS Player Handler] 是Adobe Experience Platform的分析推廣。 有關擴展功能的詳細資訊，請參閱上的擴展頁 [AdobeExchange](https://exchange.adobe.com/experiencecloud.details.101361.nielsen-digital-sdk-extension.html)。

此目標是標籤擴展。 有關標籤擴展在平台中如何工作的詳細資訊，請參見 [標籤擴展概述](../launch-extensions/overview.md)。

![Nielsen VideoJS播放器處理程式擴展](../../assets/catalog/analytics/nielsen-videojs/catalog.png)

## 先決條件 {#prerequisites}

此擴展在 [!DNL Destinations] 為購買平台的所有客戶編錄。

要使用此副檔名，您需要訪問Adobe Experience Platform中的標籤。 標籤作為附帶的增值功能提供給Adobe Experience Cloud客戶。 請與組織管理員聯繫以獲得對標籤的訪問權限，並請他們授予您 **[!UICONTROL 管理屬性]** 以便您可以安裝擴展。

## 安裝擴展 {#install-extension}

安裝 [!DNL Nielsen VideoJS Player Handler] 擴展：

在 [平台介面](https://platform.adobe.com/)，轉到 **[!UICONTROL 目標]** > **[!UICONTROL 目錄]**。

從目錄中選擇副檔名或使用搜索欄。

按一下目標以突出顯示它，然後選擇 **[!UICONTROL 配置]** 右欄。 如果 **[!UICONTROL 配置]** 控制項呈灰色顯示，您缺少 **[!UICONTROL 管理屬性]** 權限。 請參閱 [先決條件](#prerequisites)。

選擇要在其中安裝副檔名的屬性。 您還可以選擇建立新屬性。 屬性是規則、資料元素、設定的擴充功能、環境和程式庫的集合。瞭解中的屬性 [「屬性」頁部分](../../../tags/ui/administration/companies-and-properties.md#properties-page) 中。

工作流將指導您完成安裝的步驟。

有關擴展配置選項和安裝支援的資訊，請參見 [Nielsen數字軟體開發工具包AdobeExchange頁面](https://exchange.adobe.com/experiencecloud.details.101361.nielsen-digital-sdk-extension.html)。

您還可以直接在 [資料收集UI](https://experience.adobe.com/#/data-collection/)。 有關詳細資訊，請參閱 [添加新擴展](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 的下界。

## 如何使用擴展 {#how-to-use}

安裝擴展後，可以開始設定規則。

您可以為已安裝的擴展設定規則，以便僅在某些情況下將事件資料發送到擴展目標。 有關設定擴展規則的詳細資訊，請參閱 [標籤文檔](../../../tags/ui/managing-resources/rules.md)。

## 配置、升級和刪除擴展 {#configure-upgrade-delete}

可以在資料收集UI中配置、升級和刪除擴展。

>[!TIP]
>
>如果某個屬性上已安裝擴展，則仍會顯示平台UI **[!UICONTROL 安裝]** 的。 啟動安裝工作流，如中所述 [安裝擴展](#install-extension) 配置或刪除擴展。

要升級擴展，請參閱 [擴展升級過程](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 的下界。
