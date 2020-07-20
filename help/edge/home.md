---
title: Adobe Experience Platform Web SDK說明
seo-title: Adobe Experience Platform Web SDK說明
description: 瞭解Adobe Experience Platform Web SDK是什麼，以及如何使用它。
seo-description: 可讓Adobe Experience Cloud的客戶與Experience Cloud中的各種服務互動。
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---


# 什麼是Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK是用戶端JavaScript程式庫，可讓Adobe Experience Cloud的客戶透過Adobe與各種服務 [!DNL Experience Cloud] 互動 [!DNL Experience Platform Edge Network]。

以下視訊提供Adobe Experience Platform和的概 [!DNL Web SDK] 觀 [!DNL Edge Network]。

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK已由Adobe Experience Platform Web SDK取代

Adobe Experience Platform Web SDK取代下列SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

這不只是現有程式庫的包裝函式。 這完全是重寫。 其目的在於結束標籤必須以正確順序觸發的挑戰、與程式庫版本修訂挑戰不一致，以及更佳的相依性管理。 它是一種新的實現方式， [!DNL Experience Cloud] 是開源 [的](https://github.com/adobe/alloy)。

除了新的程式庫外，還有新的端點，可簡化對Adobe解決方案的HTTP要求。 之前，Visitor.js會將封鎖呼叫傳送至訪客ID服務，然後AT.js會傳送呼叫至Adobe Target,DIL.js會傳送呼叫至Adobe Audience Manager，最後AppMeasurement.js會傳送呼叫至Adobe Analytics。 這個新的程式庫和端點可以在單 [!DNL Target] 次呼叫中擷取ID、擷取體驗、傳送資 [!DNL Audience Manager]料至Adobe Experience Platform，並將資料傳遞至Adobe Experience Platform。

以下視訊示範Adobe Experience Platform及其 [!DNL Web SDK] 實際 [!DNL Edge Network] 運作。 視訊範例使用單一Adobe呼叫，將資料傳 [!DNL Experience Platform]送 [!DNL Analytics]至 [!DNL Audience Manager]、和 [!DNL Target]。

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)


## 快速入門

我們強烈建議您 [參閱我們的快速入門手冊](getting-started/quick-start-with-launch.md) ，以取得如何開始使用Adobe Launch的快速教學課程。

本產品不斷發展，不斷成長，以支援越來越多的使用案例。 為跟上最新的腳步，請查看我們支援 [的使用案例展示板](https://github.com/adobe/alloy/projects/5)。 我們會隨時更新目前支援的使用案例，以及我們正在進行的使用案例，讓您做出最佳決策。

* __尚未支援的使用案例__ -這些是我們規劃中未來將支援的使用案例。
* __使用案例進行中__ -這些是團隊目前正在完成的發行使用案例。
* __支援的使用案例__ -這些是目前支援和適用的使用案例。
* __我們不支援的使用案例__ -這些是我們決定不支援的使用案例。
