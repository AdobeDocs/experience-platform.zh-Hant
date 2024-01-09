---
title: Adobe Experience Platform Web軟體開發套件(SDK)概覽
description: 瞭解如何使用Adobe Experience Platform Web SDK將Platform功能整合至您的網站。
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: a8b1aa87ecd85c530188e520db2f17136a63ae44
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 1%

---


# Adobe Experience Platform Web SDK {#overview}

>[!IMPORTANT]
>
>在2024年4月底，Adobe Experience Platform Web SDK將會移除所有版本Internet Explorer的支援。

Adobe Experience Platform Web Software Development Kit (SDK)是使用者端的JavaScript程式庫，可讓Adobe Experience Cloud的客戶透過Adobe Experience Platform Edge Network與其服務互動。 Adobe提供兩種實作Web SDK的方法：

* 使用手動實作 `alloy.js` JavaScript程式庫。 本使用手冊提供此實作方法的檔案。
* 此 [Web SDK標籤擴充功能](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). 另請參閱 [使用Web SDK教學課程實作Adobe Experience Cloud](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hant) 以取得詳細資訊。

## Experience Platform Edge Network {#edge-network}

Experience Platform Web SDK是構成Adobe Experience Platform Edge Network的工具集合的一部分。 Edge Network包含下列元件：

* **[Experience PlatformWeb SDK](#overview)：** JavaScript SDK和標籤擴充功能可大幅簡化Adobe技術的部署。
* **[Experience Platform行動SDK](https://developer.adobe.com/client-sdks/home/)：** v5行動SDK的擴充功能，可讓客戶使用新的部署方法
* **[Experience Platform Edge Network伺服器API](../server-api/overview.md)：** 可用於各種資料收集、個人化、廣告和行銷使用案例的API。 伺服器API可用於伺服器、IoT裝置、機上盒和各種其他裝置。

Edge Network是低延遲資料收集、可插拔式運算，以及跨所有可定址通道快速啟用資料的架構。 它為每個管道（JavaScript、行動裝置、伺服器端）提供單一整合SDK，好將資料傳送至通用Adobe網域(`adobedc.net`)並接收單一裝載，以傳回資料和體驗傳送。

在伺服器端，統一的邊緣閘道和通用平台服務架構可協助您輕鬆將新功能部署至此即時運算環境中。 此架構特色：

* 減少客戶實現價值的時間
* 結束對「點」整合的需求
* 相較於舊程式庫，提升效能
* 降低成本
* 加快創新速度
* 為Adobe客戶創造持續的競爭優勢

單一整合的邊緣系統可讓客戶管理其跨所有頻道的廣告、行銷或個人化行銷活動，作為整合式體驗。 它也能讓Adobe以較低的總體擁有成本為客戶提供服務。 Edge系統可容納大部分型別的資料，讓您對應自己的資料模型，以供多個Experience Cloud產品擷取。

## 影片概述 {#video}

下列影片會概略介紹Adobe Experience Platform [!DNL Web SDK] 和Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## 以Web SDK取代的程式庫 {#sdks}

Web SDK不僅僅是現有程式庫的包裝函式。 這是一個新的程式庫，從頭開始撰寫，以合併現有程式庫的功能。 其目的在於結束標籤必須依正確順序引發的挑戰、與程式庫版本設定挑戰的不一致，以及更好的相依性管理。 這是一種實作的新方法 [!DNL Experience Cloud] 確實如此 [開放原始碼](https://github.com/adobe/alloy).

Web SDK會取代下列SDK：

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

除了新程式庫之外，還有新的端點可簡化HTTP請求以Adobe解決方案。 之前， `Visitor.js` 傳送封鎖呼叫給訪客ID服務，然後 `AT.js` 已傳送電話給Adobe Target， `DIL.js` 傳送呼叫至Adobe Audience Manager，最後 `AppMeasurement.js` 已傳送呼叫至Adobe Analytics。 此新程式庫和端點可以擷取ID、擷取 [!DNL Target] 體驗，傳送資料至 [!DNL Audience Manager]，並透過單一呼叫將資料傳遞至Adobe Experience Platform。

下列影片示範Adobe Experience Platform [!DNL Web SDK] 和Adobe Experience Platform [!DNL Edge Network] 執行中。 影片範例使用單一呼叫來Adobe，將資料傳送至 [!DNL Experience Platform]， [!DNL Analytics]， [!DNL Audience Manager]、和 [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## 從現有程式庫移轉至Web SDK {#migrating-to-web-sdk}

若要簡化您的移轉作業，請利用 [現有程式庫](#sdks) Adobe為Web SDK提供簡化的升級途徑。 此路徑可讓您將網站的每個個別頁面移轉至Web SDK，而不需要一次移轉整個網站。 現有程式庫位於其他頁面時，您可以在指定頁面上使用Web SDK。 準備就緒後，您就可以移轉這些其他頁面。

### 移轉 `AT.js` Web SDK考量事項 {#considerations}

移轉使用的頁面之前 `AT.js` 若要使用Web SDK，請務必啟用下列Web SDK設定選項。 這些選項可確保從以下頁面導覽時保留訪客設定檔： `AT.js` 至使用Web SDK的頁面。

* [&#39;idMigrationEnabled&#39;](fundamentals/configuring-the-sdk.md#id-migration-enabled)
* [&#39;targetMigrationEnabled&#39;](fundamentals/configuring-the-sdk.md#targetMigrationEnabled)


>[!IMPORTANT]
>
>從at.js移轉至Web SDK時不支援下列Target功能：
>
>* [重新導向選件](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html)
>* [CNAME和跨網域支援](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

從移轉之後 `AT.js` 至Web SDK，移除 `targetMigrationEnabled` 選項。
