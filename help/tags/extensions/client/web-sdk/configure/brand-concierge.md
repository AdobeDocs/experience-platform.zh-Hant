---
title: Brand Concierge組態設定
description: 設定Brand Concierge聊天的工作階段持續性和串流逾時。
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 4%

---

# Brand Concierge組態設定

>[!AVAILABILITY]
>
>適用於Web SDK的Brand Concierge目前處於&#x200B;**測試版**。 功能和檔案可能會有所變更。

**[!UICONTROL Brand Concierge]**&#x200B;區段可讓您控制Brand Concierge聊天工作階段在Web SDK標籤擴充功能中的行為。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL Extensions]**，然後選取&#x200B;**[!UICONTROL Configure]**&#x200B;卡片上的[!UICONTROL Adobe Experience Platform Web SDK]。
1. 向下捲動至&#x200B;**[!UICONTROL Brand Concierge]**&#x200B;區段。

提供下列選項：

## [!UICONTROL Sticky conversation session]

此核取方塊會使用工作階段Cookie跨頁面載入保留Brand Concierge工作階段。 此選項預設為停用。 如需設定此值的指引，請參閱JavaScript資料庫檔案中的[`conversation`](/help/collection/js/commands/configure/conversation.md)。

## [!UICONTROL Stream timeout (seconds)]

觸發逾時錯誤前，等候交談資料流區塊的最長時間（以秒為單位）。 預設值為`10`秒。
