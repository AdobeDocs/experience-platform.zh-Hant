---
title: Adobe Experience Platform Web SDK概述
description: 了解如何使用Adobe Experience Platform Web SDK將Platform功能整合至您的網站。
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;Edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;Web SDK;SDK;Web SDK;Launch；啟動
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 92344ca9c2daf603d866c8a3cc4e92b72a382fb1
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 1%

---

# Adobe Experience Platform Web SDK概述

Adobe Experience Platform Web SDK是用戶端JavaScript程式庫，可讓Adobe Experience Cloud的客戶與 [!DNL Experience Cloud] 透過Adobe Experience Platform Edge Network。 除了JavaScript程式庫，還有 [標籤擴充功能](./extension/web-sdk-extension-configuration.md) 協助您進行Web SDK設定。

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] 是組成Experience Edge的集合的一部分。 Experience Edge包含三種技術：

* **[!DNL Adobe Experience Platform Web SDK]:** JavaScript SDK和標籤擴充功能可大幅簡化部署 [!DNL Adobe] 技術
* **Adobe Experience Platform Mobile SDK:** v5行動SDK的擴充功能，可讓客戶使用新的部署方法
* **[!DNL Adobe Experience Platform Edge Network]:** 全球分佈式伺服器網路，支援新的部署方法 [!DNL Adobe] 產品

此 [!DNL Adobe Experience Edge] 是低延遲資料收集、可插拔計算以及跨所有可定址通道快速啟動資料的新框架。

[!DNL Adobe Experience Edge] 為每個管道（JavaScript、Mobile、伺服器端）提供單一整合SDK，可將資料傳送至通用Adobe網域(`adobedc.net`)，並接收回資料和體驗傳送的單一裝載。

在伺服器端，統一的邊緣網關和通用平台服務框架使插件和部署新功能變得容易，並可以輕鬆部署到此即時計算環境中。  此架構特色：

* 縮短客戶實現價值的時間
* 結束「點」整合的需求
* 與舊程式庫相比，提高效能
* 降低成本
* 提高創新速度
* 為Adobe客戶創造持續的競爭優勢

單一整合的邊緣系統可讓客戶以整合的體驗形式管理其所有通路的廣告、行銷或個人化行銷活動。  它允許 [!DNL Adobe] 以更低的總體擁有成本為客戶提供服務。  它還通過使即時邊緣可插拔和允許 [!DNL Adobe] 以及其客戶，以更快地向即時系統添加新功能和客戶定義的邏輯。

## 影片概述

以下影片提供Adobe Experience Platform的概觀 [!DNL Web SDK] 和Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK取代為Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK取代了下列SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

這不只是現有程式庫的包裝函式。 徹底重寫。 其目的是結束標籤必須以正確順序引發的挑戰、與程式庫版本設定挑戰的不一致，以及更好的相依性管理。 這是實作 [!DNL Experience Cloud] 它 [開放來源](https://github.com/adobe/alloy).

除了新程式庫外，還有新端點可簡化Adobe解決方案的HTTP要求。 之前，Visitor.js傳送封鎖呼叫給訪客ID服務，然後AT.js傳送呼叫給Adobe Target,DIL.js傳送呼叫給Adobe Audience Manager，最後AppMeasurement.js傳送呼叫給Adobe Analytics。 這個新程式庫和端點可以擷取ID，擷取 [!DNL Target] 體驗，將資料傳送至 [!DNL Audience Manager]，並在單一呼叫中將資料傳遞至Adobe Experience Platform。

下列影片示範Adobe Experience Platform [!DNL Web SDK] 和Adobe Experience Platform [!DNL Edge Network] 執行中。 視訊範例使用單一呼叫來Adobe，其會將資料傳送至 [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager]，和 [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

此產品不斷發展，以支援越來越多的使用案例。 若要跟上最新的進度，請參閱 [支援使用案例頁面](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/supported-use-cases.html). 本頁面列出我們目前支援的使用案例，並提供可用的詳細資訊連結。

* **尚未支援的使用案例：** 這些是我們未來將支援的藍圖中的使用案例。
* **正在使用的案例：** 這些是團隊目前正在著手完成的發行使用案例。
* **支援的使用案例：** 這些是目前支援和運作的使用案例。
* **我們不支援的使用案例：** 這些是我們決定不支援的使用案例。
