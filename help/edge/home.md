---
title: Adobe Experience Platform Web SDK說明
seo-title: Adobe Experience Platform Web SDK說明
description: 瞭解Adobe Experience Platform Web SDK是什麼，以及如何使用它。
seo-description: 瞭解如何讓Adobe Experience Cloud客戶與Experience Cloud中的各種服務互動。
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js；網頁sdk;SDK;Web SDK;Launch；啟動
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 1%

---


# 什麼是Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK是用戶端JavaScript程式庫，可讓Adobe Experience Cloud客戶透過Adobe Experience Platform Edge Network與[!DNL Experience Cloud]中的各種服務互動。 除了JavaScript程式庫外，還有[Experience Platform Launch擴充功能](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html)，可協助您進行Web SDK設定。

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] 是組成Experience Edge的系列的一部分。Experience Edge包含三種技術：

* **[!DNL Adobe Experience Platform Web SDK]：可** 大幅簡化部署技術 [!DNL Experience Platform Launch] 的JavaScript SDK和擴充功 [!DNL Adobe] 能
* **Adobe Experience Platform Mobile SDK:v5** 行動SDK的擴充功能，可讓客戶使用新的部署方法
* **[!DNL Adobe Experience Platform Edge Network]：全** 球分散式伺服器網路，可提供新的產品部署方 [!DNL Adobe] 法

[!DNL Adobe Experience Edge]是適用於所有可定址通道的低延遲資料收集、可插拔計算和快速資料激活的新框架。

[!DNL Adobe Experience Edge] 為每個通道（JavaScript、Mobile、伺服器端）提供單一整合SDK，可將資料傳送至共同的Adobe網域(`adobedc.net`)，並接收單一裝載回傳資料和體驗。

在伺服器端，統一的邊緣閘道和通用的平台服務架構，讓您輕鬆將外掛程式和部署新功能至此即時運算環境。  此架構特色：

* 縮短客戶實現價值的時間
* 結束「點」整合的需求
* 與舊程式庫相比，提高效能
* 降低成本
* 提高創新速度
* 為Adobe客戶創造持續的競爭優勢

單一整合的邊緣系統可讓客戶將其所有通道的廣告、行銷或個人化宣傳活動管理為整合體驗。  它允許[!DNL Adobe]為客戶提供總擁有成本更低的服務。  它還通過使即時邊緣可插拔，使[!DNL Adobe]及其客戶能夠更快地在該即時系統中添加新功能和客戶定義的邏輯，從而幫助提高產品創新的速度。

## 影片概述

以下影片概述Adobe Experience Platform [!DNL Web SDK]和Adobe Experience Platform [!DNL Edge Network]。

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK已由Adobe Experience Platform Web SDK取代

Adobe Experience Platform Web SDK取代下列SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

這不只是現有程式庫的包裝函式。 這完全是重寫。 其目的在於結束標籤必須以正確順序觸發的挑戰、與程式庫版本修訂挑戰不一致，以及更佳的相依性管理。 它是實現[!DNL Experience Cloud]的新方法，它是[開放原始碼](https://github.com/adobe/alloy)。

除了新的程式庫外，還有新的端點，可簡化對Adobe解決方案的HTTP要求。 之前，Visitor.js會將封鎖呼叫傳送至訪客ID服務，然後AT.js會傳送呼叫至Adobe Target,DIL.js會傳送呼叫至Adobe Audience Manager，最後AppMeasurement.js會傳送呼叫至Adobe Analytics。 此新程式庫和端點可以擷取ID、擷取[!DNL Target]體驗、傳送資料至[!DNL Audience Manager]，並透過單一呼叫將資料傳送至Adobe Experience Platform。

以下視訊示範Adobe Experience Platform [!DNL Web SDK]和Adobe Experience Platform [!DNL Edge Network]的實際運作。 視訊範例使用單一Adobe呼叫，將資料傳送至[!DNL Experience Platform]、[!DNL Analytics]、[!DNL Audience Manager]和[!DNL Target]。

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

本產品不斷發展，不斷成長，以支援越來越多的使用案例。 為跟上最新的腳步，請查看我們的[支援的使用案例展示板](https://github.com/adobe/alloy/projects/5)。 我們會隨時更新目前支援的使用案例，以及我們正在進行的使用案例，讓您做出最佳決策。

* **尚未支援的使用案例：** 我們未來將支援這些使用案例。
* **進行中的使用案例：** 這些是團隊目前正在完成發行的使用案例。
* **支援的使用案** 例：這些是目前支援和適用的使用案例。
* **我們不支援的使用案例：** 這些是我們決定不支援的使用案例。
