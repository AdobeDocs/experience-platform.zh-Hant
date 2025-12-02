---
title: 自訂建置元件
description: 建立自訂Web SDK建置，此功能可讓您縮小建置大小。
source-git-commit: d6aea91d6989775ff5b6038b216ed2518f4a7d98
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# 自訂建置元件

Web SDK資料庫包含多個模組，用於各種功能，例如個人化、身分、連結追蹤等。 根據您的使用案例，您可能只需要特定功能，而不需要整個程式庫。 停用組建元件可讓您僅使用所需的模組，藉此縮小程式庫大小並提升效能。

停用元件時，無法再編輯該元件的設定。 如果您使用多個Web SDK執行個體，則選取的組建元件會套用至所有執行個體。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL Extensions]**，然後選取&#x200B;**[!UICONTROL Configure]**&#x200B;卡片上的[!UICONTROL Adobe Experience Platform Web SDK]。
1. 展開頂端的&#x200B;**[!UICONTROL Custom build components]**&#x200B;摺疊式功能表。

>[!WARNING]
>
>錯誤地修改這些設定可能會導致意外的結果，包括資料遺失。 先在開發環境中徹底測試您的實作，然後再將這些變更發佈到生產環境。

Adobe提供停用下列Web SDK組建元件的功能：

| 建置元件 | 說明 | 從屬特徵 |
| --- | --- | --- |
| **[!UICONTROL Activity collector]** | 允許自動連結收集和Activity Map追蹤。 | |
| **[!UICONTROL Advertising]** | 啟用Adobe Advertising與Customer Journey Analytics的整合。 | |
| **[!UICONTROL Audiences]** | 支援與Adobe Audience Manager整合，例如ID同步。 | |
| **[!UICONTROL Consent]** | 允許使用同意功能。 | [[!UICONTROL Set consent]](../actions/set-consent.md)動作 |
| **[!UICONTROL Event merge]** | 已棄用。 | [[!UICONTROL Event merge ID]](../data-element-types.md)資料元素（已棄用）<br>[[!UICONTROL Reset event merge ID]](../actions/reset-event-merge-id.md)動作（已棄用） |
| **[!UICONTROL Media Analytics bridge]** | 支援與舊版Media Analytics整合。 | [[!UICONTROL Get media analytics tracker]](../actions/get-media-analytics-tracker.md)動作 |
| **[!UICONTROL Personalization]** | 支援與Adobe Target和Adobe Journey Optimizer的整合。 | [[!UICONTROL Apply propositions]](../actions/apply-propositions.md)動作 |
| **[!UICONTROL Push notifications]** | 啟用Adobe Journey Optimizer的網頁推播通知。 | [[!UICONTROL Send push subscription]](../actions/send-push-subscription.md)動作 |
| **[!UICONTROL Rules engine]** | 使用Adobe Journey Optimizer啟用裝置決策。 | [[!UICONTROL Evaluate rulsets]](../actions/evaluate-rulesets.md)動作<br> [[!UICONTROL Subscribe ruleset items]](../event-types.md#subscribe-ruleset-items)個事件 |
| **[!UICONTROL Streaming media]** | 支援與串流媒體收集整合。 | [[!UICONTROL Send media event]](../actions/send-media-event.md)動作 |
