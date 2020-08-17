---
keywords: web sdk;SDK;web SDK;Launch;launch
title: Adobe Experience Platform Web SDK說明
seo-title: Adobe Experience Platform Web SDK說明
description: 瞭解Adobe Experience Platform Web SDK是什麼，以及如何使用它。
seo-description: 可讓Adobe Experience Cloud的客戶與Experience Cloud中的各種服務互動。
translation-type: tm+mt
source-git-commit: 8f7ce97cdefd4fe79cb806e71e12e936caca3774
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 2%

---


# 什麼是Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK是用戶端JavaScript程式庫，可讓Adobe Experience Cloud的客戶透過Adobe與各種服務 [!DNL Experience Cloud] 互動 [!DNL Experience Platform Edge Network]。 除了JavaScript程式庫外，還有 [Launch擴充功能](https://docs.adobe.com/content/help/zh-Hant/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html) ，可協助您進行Web SDK設定。

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] 是組成Experience Edge的系列的一部分。 Experience Edge包含三種技術：

* **[!DNL Adobe Experience Platform Web SDK]:** JavaScript SDK和擴充功能可 [!DNL Launch] 大幅簡化部署技術的作 [!DNL Adobe] 業
* **Adobe Experience Platform Mobile SDK:** v5行動SDK的擴充功能，可讓客戶使用新的部署方法
* **[!DNL Adobe Experience Platform Edge Network]:** 全球分散式伺服器網路，提供新的產品部署方 [!DNL Adobe] 法

此 [!DNL Adobe Experience Edge] 新架構適用於所有可定址通道的低延遲資料收集、可插拔運算和快速啟動資料。

[!DNL Adobe Experience Edge] 為每個通道（JavaScript、Mobile、伺服器端）提供單一整合SDK，可將資料傳送至共同的Adobe網域(`adobedc.net`)，並接收單一裝載回傳資料和體驗。

在伺服器端，統一的邊緣閘道和通用的平台服務架構，讓您輕鬆將外掛程式和部署新功能至此即時運算環境。  此架構特色：

* 縮短客戶實現價值的時間
* 結束「點」整合的需求
* 與舊程式庫相比，提高效能
* 降低成本
* 提高創新速度
* 為Adobe客戶創造持續的競爭優勢

單一整合的邊緣系統可讓客戶將其所有通道的廣告、行銷或個人化宣傳活動管理為整合體驗。  它可讓 [!DNL Adobe] 客戶以較低的總擁有成本提供服務。  它還可讓即時邊緣可插拔，並讓其客戶更快速地在該即時系統中新增功能和客戶定義邏輯，以協助提高產品創新的速度。 [!DNL Adobe]

## 影片概述

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

* **尚未支援的使用案例：** 這些是我們規劃中未來將支援的使用案例。
* **進行中的使用案例：** 這些是團隊目前正在完成的發行使用案例。
* **支援的使用案例：** 這些是目前支援的使用案例。
* **我們不支援的使用案例：** 這些是我們決定不支援的使用案例。
