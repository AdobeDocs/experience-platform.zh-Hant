---
title: 進階設定
description: 設定Web SDK標籤擴充功能的進階設定。
exl-id: d830a210-77ab-4823-b5fa-c1194a01bea3
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 20%

---

# 進階設定 {#advanced}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_advanced"
>title="進階設定"
>abstract="進階設定。Adobe 建議大部分實施都維持這些選項的原狀。"

此組態區段可讓您變更進階設定。 Adobe 建議大部分實施都維持這些選項的原狀。

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
