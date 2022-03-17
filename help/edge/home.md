---
title: Adobe Experience PlatformWeb SDK概述
description: 瞭解如何使用Adobe Experience PlatformWeb SDK將平台功能整合到您的網站中。
keywords: Adobe Experience PlatformWeb SDK；平台Web SDK;Web SDK；邊緣；Visitor.js;AppMeasurement.js;AT.js;DIL.js;web sdk;SDK;Web SDK；啟動；啟動
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 71857ffc5e671f4d9a0502fb95d89d30fdec1f15
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 1%

---

# Adobe Experience PlatformWeb SDK概述

Adobe Experience PlatformWeb SDK是客戶端JavaScript庫，它允許Adobe Experience Cloud客戶與中的各種服務進行交互 [!DNL Experience Cloud] 通過Adobe Experience Platform邊緣網路。 除JavaScript庫外，還 [標籤擴展](./extension/web-sdk-extension-configuration.md) 以幫助您配置Web SDK。

**有關設定帶標籤的Web SDK並將資料發送到解決方案的逐步指南，請參閱 [使用Web SDK教程實施Adobe Experience Cloud](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=en)**

## 體驗邊緣

[!DNL Adobe Experience Platform Web SDK] 是組成體驗邊緣的集合的一部分。 Experience Edge包括三種技術：

* **[!DNL Adobe Experience Platform Web SDK]:** JavaScript SDK和標籤擴展，可大大簡化部署 [!DNL Adobe] 技術
* **Adobe Experience Platform移動SDK:** v5移動SDK的擴展，允許客戶使用新的部署方法
* **[!DNL Adobe Experience Platform Edge Network]:** 一種全球分佈式伺服器網路，支援一種新的部署方法 [!DNL Adobe] 產品

的 [!DNL Adobe Experience Edge] 是一個新的框架，用於跨所有可定址通道進行低延遲資料收集、可插拔計算和快速資料激活。

[!DNL Adobe Experience Edge] 為每個通道（JavaScript、Mobile和伺服器端）提供單個統一的SDK，該通道將資料發送到公共Adobe域(`adobedc.net`)，並接收單個負載，以便提供資料和體驗。

在伺服器端，統一邊緣網關和通用平台服務框架使插件和部署新功能變得容易到此即時計算環境中。  此架構特色：

* 減少客戶的價值
* 結束對「點」整合的需求
* 與舊庫相比，提高了效能
* 降低成本
* 提高創新速度
* 為Adobe客戶創造持續的競爭優勢

單一的整合邊緣系統使客戶能夠管理其所有渠道的廣告，營銷或個性化活動，作為一種綜合體驗。  它允許 [!DNL Adobe] 為客戶提供總擁有成本更低的服務。  它還通過使即時邊緣可插拔和允許 [!DNL Adobe] 並讓客戶更快地向該即時系統添加新功能和客戶定義邏輯。

## 影片概述

以下視頻概述了Adobe Experience Platform [!DNL Web SDK] 和Adobe Experience Platform [!DNL Edge Network]。

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK被Adobe Experience PlatformWeb SDK取代

Adobe Experience PlatformWeb SDK取代了以下SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

這不僅僅是現有庫的包裝。 這是徹底的重寫。 其目的是結束以下挑戰：標籤必須按正確的順序啟動、與庫版本控制挑戰不一致以及更好的依賴關係管理。 這是實施 [!DNL Experience Cloud] 而且 [開源](https://github.com/adobe/alloy)。

除了新庫外，還有一個新的端點，可優化對Adobe解決方案的HTTP請求。 之前，Visitor.js向訪問者身份服務發送阻斷呼叫，然後AT.js向Adobe Target發送呼叫，DIL·js向Adobe Audience Manager發送呼叫，最後AppMeasurement.js向Adobe Analytics發送呼叫。 此新庫和終結點可以檢索ID，獲取 [!DNL Target] 體驗，將資料發送到 [!DNL Audience Manager]，並在一次呼叫中將資料傳遞給Adobe Experience Platform。

以下視頻演示了Adobe Experience Platform [!DNL Web SDK] 和Adobe Experience Platform [!DNL Edge Network] 的下界。 視頻示例使用單個呼叫來Adobe，該呼叫將資料發送到 [!DNL Experience Platform]。 [!DNL Analytics]。 [!DNL Audience Manager], [!DNL Target]。

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

此產品不斷發展和增長，以支援越來越多的使用案例。 要跟上最新資訊並瞭解我們當前支援的內容，請參閱 [支援的使用案例頁](https://github.com/orgs/adobe/projects/18/views/1)。
