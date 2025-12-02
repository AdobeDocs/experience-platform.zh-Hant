---
title: 進階組態設定
description: 設定Web SDK標籤擴充功能的進階設定。
source-git-commit: d6aea91d6989775ff5b6038b216ed2518f4a7d98
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# 進階組態設定

此組態區段可讓您變更進階設定。 Adobe建議大部分實施都保留這些選項。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL Extensions]**，然後選取&#x200B;**[!UICONTROL Configure]**&#x200B;卡片上的[!UICONTROL Adobe Experience Platform Web SDK]。
1. 向下捲動至&#x200B;**[!UICONTROL Advanced Settings]**&#x200B;區段。

![顯示使用Web SDK標籤延伸模組之進階設定的影像](../assets/advanced-settings.png)

目前有一個可用選項。

## [!UICONTROL Edge base path]

使用此欄位來變更用來與Edge Network互動的基本路徑。 如果您參與某些Alpha或Beta測試，Adobe可能會要求您變更此欄位；否則，Adobe建議將其保留為預設值`ee`。

此欄位在設定JavaScript資料庫時相當於[`edgeBasePath`](/help/collection/js/commands/configure/edgebasepath.md)的標籤。
