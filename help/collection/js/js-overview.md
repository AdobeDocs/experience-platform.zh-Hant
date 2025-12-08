---
title: Web SDK JavaScript程式庫概觀
description: 使用JavaScript將資料傳送至Adobe Experience Platform Edge Network。
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 7f932e9868e84cf8abdaa6cf0b2da5bac837234d
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# Web SDK JavaScript程式庫概觀

**Adobe Experience Platform Web SDK**&#x200B;是使用者端的JavaScript資料庫，可讓您將資料傳送至Adobe Experience Platform Edge Network。 本指南會記錄Web SDK JavaScript程式庫(`alloy.js`)實作路徑，包括核心概念、安裝、設定和命令。 如需資料收集UI中的網頁SDK標籤擴充功能，請參閱[網頁SDK標籤擴充功能](/help/tags/extensions/client/web-sdk/overview.md)。

網頁SDK會以與解決方案無關的方式(XDM)傳送資料至Experience Platform Edge Network，接著將資料對應至解決方案特定的格式和目的地，並即時傳送。

## Experience Platform Edge Network {#edge-network}

Adobe Experience Platform Edge Network提供低延遲資料收集、可插拔式運算，以及所有可定址管道的快速資料啟用。 它提供適用於網路、行動和伺服器端通道的單一整合SDK，將資料傳送至共同的Adobe網域(`adobedc.net`)，並接收資料和體驗傳送的單一裝載。

在伺服器端，統一的邊緣閘道和通用平台服務架構可簡化新功能的部署，同時具備下列優點：

* 減少客戶實現價值的時間；
* 結束對「點」整合的需求；
* 相較於舊程式庫，提升效能；
* 降低營運成本；
* 加快創新速度；
* 為Adobe客戶創造持續的競爭優勢。

整合的邊緣系統可讓您管理所有管道的廣告、行銷和個人化行銷活動。 它可減少總擁有成本並支援各種資料型別，讓您對應資料模型以搭配多個Experience Cloud產品使用。

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## 由網頁SDK取代的程式庫 {#sdks}

Web SDK是從頭開始建立的開放原始碼程式庫，可整合現有程式庫的功能。 它可解決標籤引發順序、版本不一致和相依性管理的問題，提供一種實作許多Experience Cloud產品的方法。 Web SDK取代了下列服務的資料收集：

* Adobe Experience Platform訪客ID服務(`Visitor.js`)
* Adobe Analytics (`AppMeasurement.js`)
* Adobe Target (`AT.js`)
* Adobe Audience Manager (`DIL.js`)
* Adobe Media Analytics
* Adobe Advertising

它也會引入新的端點，簡化對Adobe解決方案的HTTP請求。 之前，每個資料收集程式庫都需要進行多次呼叫。 現在，單一呼叫可以擷取ID、擷取[!DNL Target]體驗、傳送資料至[!DNL Audience Manager]，以及傳遞資料至Adobe Experience Platform。

## 從現有程式庫移轉至Web SDK {#migrating-to-web-sdk}

Adobe提供簡化的升級路徑，可簡化從任何現有程式庫移轉至Web SDK的程式。 您可以個別移轉網站的每個頁面，而不需要一次移轉整個網站。 您可以在部分頁面上使用Web SDK，而在其他頁面上則保留現有程式庫，以逐步轉換。
