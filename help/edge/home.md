---
title: Adobe Experience Platform Web SDK概述
description: 了解如何使用Adobe Experience Platform Web SDK將Platform功能整合至您的網站。
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;Edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;Web SDK;SDK;Web SDK;Launch；啟動
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 00801465435133fce29002c8bd0f2256745ba2c2
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 1%

---

# Adobe Experience Platform Web SDK概述 {#overview}

Adobe Experience Platform Web SDK是用戶端JavaScript程式庫，可讓Adobe Experience Cloud的客戶與 [!DNL Experience Cloud] 透過Adobe Experience Platform Edge Network。 除了JavaScript程式庫，還有 [標籤擴充功能](./extension/web-sdk-extension-configuration.md) 協助您進行Web SDK設定。

如需使用標籤來設定Web SDK及將資料傳送至解決方案的逐步指南，請參閱我們的 [使用Web SDK實作Adobe Experience Cloud教學課程](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=en).

>[!IMPORTANT]
>
>此產品不斷發展，以支援越來越多的使用案例。 若要跟上最新的趨勢，並了解我們目前支援的功能，請參閱 [支援使用案例頁面](https://github.com/orgs/adobe/projects/18/views/1).

## Adobe Experience Edge

[!DNL Adobe Experience Platform Web SDK] 是組成 [!DNL Adobe Experience Edge]. [!DNL Experience Edge] 包含下列技術：

* **[[!DNL Adobe Experience Platform Web SDK]](#overview):** JavaScript SDK和標籤擴充功能可大幅簡化部署 [!DNL Adobe] 技術。
* **[[!DNL Adobe Experience Platform Mobile SDK]](https://aep-sdks.gitbook.io/docs/getting-started/overview):** v5行動SDK的擴充功能，可讓客戶使用新的部署方法
* **[[!DNL Adobe Experience Platform Edge Network]](../server-api/overview.md):** 全球分佈式伺服器網路，支援新的部署方法 [!DNL Adobe] 產品

此 [!DNL Adobe Experience Edge] 是低延遲資料收集、可插拔計算以及跨所有可定址通道快速啟動資料的新框架。

[!DNL Adobe Experience Edge] 為每個管道（JavaScript、Mobile、伺服器端）提供單一整合SDK，可將資料傳送至通用Adobe網域(`adobedc.net`)，並接收回資料和體驗傳送的單一裝載。

在伺服器端，統一的邊緣網關和通用平台服務框架使插件和部署新功能變得容易，並可以輕鬆部署到此即時計算環境中。  此架構特色：

* 縮短客戶實現價值的時間
* 結束「點」整合的需求
* 與舊程式庫相比，提高效能
* 降低成本
* 提高創新速度
* 為Adobe客戶創造持續的競爭優勢

單一整合的邊緣系統可讓客戶以整合的體驗形式管理其所有通路的廣告、行銷或個人化行銷活動。 它允許 [!DNL Adobe] 以更低的總體擁有成本為客戶提供服務。  它還通過使即時邊緣可插拔和允許 [!DNL Adobe] 以及其客戶，以更快地向即時系統添加新功能和客戶定義的邏輯。

## 影片概述 {#video}

以下影片提供Adobe Experience Platform的概觀 [!DNL Web SDK] 和Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## 由Web SDK取代的程式庫 {#sdks}

Web SDK不只是現有程式庫的包裝函式。 這是一個全新的圖書館，從頭開始編寫，以結合現有圖書館的功能。 其目的是結束標籤必須以正確順序引發的挑戰、與程式庫版本設定挑戰的不一致，以及更好的相依性管理。 這是實作 [!DNL Experience Cloud] 它 [開放來源](https://github.com/adobe/alloy).

Web SDK會取代下列SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

除了新程式庫外，還有新端點可簡化Adobe解決方案的HTTP要求。 之前，Visitor.js傳送封鎖呼叫給訪客ID服務，然後AT.js傳送呼叫給Adobe Target,DIL.js傳送呼叫給Adobe Audience Manager，最後AppMeasurement.js傳送呼叫給Adobe Analytics。 這個新程式庫和端點可以擷取ID，擷取 [!DNL Target] 體驗，將資料傳送至 [!DNL Audience Manager]，並在單一呼叫中將資料傳遞至Adobe Experience Platform。

下列影片示範Adobe Experience Platform [!DNL Web SDK] 和Adobe Experience Platform [!DNL Edge Network] 執行中。 視訊範例使用單一呼叫來Adobe，其會將資料傳送至 [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager]，和 [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## 從現有程式庫移轉至Web SDK {#migrating-to-web-sdk}

簡化從 [現有程式庫](#sdks) 至Web SDK,Adobe提供簡化的升級路徑，讓您將網站的每個個別頁面移轉至Web SDK，而無須一次移轉整個網站。

這表示您可以在頁面上使用Web SDK，並將現有程式庫保留在其他頁面上，直到您也能移轉它們為止。

### at.js移轉至Web SDK的考量事項 {#considerations}

移轉使用 [!DNL at.js] 至Web SDK，請務必啟用下列Web SDK設定選項。 這可確保在使用 [!DNL at.js ] 至使用Web SDK的頁面。

* [&#39;idMigrationEnabled&#39;](fundamentals/configuring-the-sdk.md#id-migration-enabled)
* [&#39;targetMigrationEnabled&#39;](fundamentals/configuring-the-sdk.md#targetMigrationEnabled)


>[!IMPORTANT]
>
>從at.js移轉至Web SDK時不支援下列Target功能：
> * [重新導向選件](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=en)
> * [CNAME和跨網域支援](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/?lang=en)


從at.js移轉至Web SDK後，您應移除 `targetMigrationEnabled` 選項。



