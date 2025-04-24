---
title: Adobe Experience Platform Web Software Development Kit (SDK)概覽
description: 瞭解如何使用Adobe Experience Platform Web SDK將Experience Platform功能整合至您的網站。
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 1%

---

# Adobe Experience Platform Web SDK {#overview}

Adobe Experience Platform Web SDK是使用者端的JavaScript資料庫，可讓Adobe Experience Cloud客戶透過Adobe Experience Platform Edge Network與其服務互動。

您可以透過兩種方式實作Web SDK：

* [Web SDK標籤延伸模組](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)。 如需詳細資訊，請參閱教學課程，瞭解如何使用Web SDK[實作Adobe Experience Cloud](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hant)。
* 使用[Web SDK JavaScript資料庫](install/library.md)手動實作。

本指南包含如何使用Web Experience Cloud JavaScript程式庫和標籤擴充功能與SDK解決方案互動的指示。

## Experience Platform Edge Network {#edge-network}



Experience Platform Web SDK是Adobe Experience Platform Edge Network的一部分，其中包括：

* **[Experience Platform Web SDK](#overview)**：簡化Adobe技術部署的JavaScript程式庫和標籤擴充功能。
* **[Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/)**：新部署方法的v5行動SDK延伸。
* **[Edge Network API](https://developer.adobe.com/data-collection-apis/docs/api/)**：用於資料收集、個人化、廣告和行銷使用案例的伺服器端API。 您可以在伺服器、IoT裝置、機上盒和其他裝置上使用它。

Edge Network提供低延遲資料收集、可插拔式運算，以及所有可定址管道的快速資料啟用。 它提供適用於網路、行動和伺服器端通道的單一整合SDK，將資料傳送至共同的Adobe網域(`adobedc.net`)，並接收資料和體驗傳送的單一裝載。

在伺服器端，統一的邊緣閘道和通用平台服務架構可簡化新功能的部署，同時具備下列優點：

* 減少客戶實現價值的時間；
* 結束對「點」整合的需求；
* 相較於舊程式庫，提升效能；
* 降低營運成本；
* 加快創新速度；
* 為Adobe客戶創造持續的競爭優勢。

整合的邊緣系統可讓您管理所有管道的廣告、行銷和個人化行銷活動。 它可減少總擁有成本並支援各種資料型別，讓您對應資料模型以搭配多個Experience Cloud產品使用。

## 影片概觀 {#video}

請觀看以下影片，瞭解Adobe Experience Platform [!DNL Web SDK]和[!DNL Edge Network]的概觀。

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## 由網頁SDK取代的程式庫 {#sdks}

Web SDK是從頭開始建立的新開放原始碼資料庫，可整合現有資料庫的功能。 它解決標籤引發順序、版本不一致和相依性管理的問題，提供新的[開放原始碼](https://github.com/adobe/alloy)方式以實作[!DNL Experience Cloud]。

Web SDK已取代：

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

它也會引入新的端點，簡化對Adobe解決方案的HTTP請求。 之前，`Visitor.js`、`AT.js`、`DIL.js`和`AppMeasurement.js`需要多次呼叫。 現在，單一呼叫可以擷取ID、擷取[!DNL Target]體驗、傳送資料至[!DNL Audience Manager]，以及傳遞資料至Adobe Experience Platform。

觀看以下影片以檢視Adobe Experience Platform [!DNL Web SDK]和[!DNL Edge Network]的實際運作情況，使用單一呼叫將資料傳送至[!DNL Experience Platform]、[!DNL Analytics]、[!DNL Audience Manager]和[!DNL Target]。

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## 從現有程式庫移轉至Web SDK {#migrating-to-web-sdk}

Adobe提供簡化的升級路徑，可簡化您從[現有資料庫](#sdks)移轉至Web SDK的程式。 您可以個別移轉網站的每個頁面，而不需要一次移轉整個網站。 您可以在部分頁面上使用Web SDK，而在其他頁面上則保留現有程式庫，以逐步轉換。

### 將`AT.js`移轉至Web SDK的考量事項 {#considerations}

在使用`AT.js`將頁面移轉至Web SDK之前，請啟用下列Web SDK組態選項，以確保在頁面之間導覽時維持訪客設定檔。

* [&#39;idMigrationEnabled&#39;](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [&#39;targetMigrationEnabled&#39;](/help/web-sdk/commands/configure/targetmigrationenabled.md)

>[!IMPORTANT]
>
>從`at.js`移轉至Web SDK時不支援下列Target功能：
>
>* [重新導向選件](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html)
>* [CNAME和跨網域支援](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

從`AT.js`移轉至Web SDK後，請從您的設定中移除`targetMigrationEnabled`選項。
