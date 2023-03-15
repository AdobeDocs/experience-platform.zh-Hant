---
title: 邊緣網路伺服器API概述
description: 了解 Edge Network 伺服器 API 及其使用方法。
seo-description: Learn what the Edge Network Server API is and how you can use it.
keywords: 資料收集；收集；Adobe Experience Platform Edge Network；伺服器api;
exl-id: 46bd8798-d7f9-405b-9ca8-856ad4aa688c
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 15%

---

# 邊緣網路伺服器API概述 {#overview}

Adobe Experience Platform Edge Network 為客戶提供與任何 Adobe Experience Cloud 或 Adobe Experience Platform Edge 服務的最佳化互動方式。

此 [!DNL Edge Network Server API] 可用於各種資料收集、個人化、廣告和行銷使用案例。 此 [!DNL Server API] 可用於伺服器， [!DNL IoT] 裝置、機上盒和各種其他裝置。

由於 [!DNL Server API] 不需仰賴任何程式庫來載入，它提供快速的方式，與Adobe Experience Platform邊緣網路和支援的解決方案互動。

此 [!DNL Server API] 架構包括：

* 縮短頁面載入時間
* 改善延遲
* 第一方資料收集
* 簡化的服務端通訊

此 [!DNL Server API] 透過兩個專用端點支援互動式和批次資料收集：

1. 互動式端點支援與Adobe Experience Platform和Adobe Experience Cloud服務的通訊，這些服務支援進階細分、個人化和其他行銷使用案例。
2. 當需要上架資料時，批次端點將允許以批次方式傳送請求，而不會收到呼叫之應用程式的回應。

此 [!DNL Server API] 支援下列類型的要求：

* 透過驗證的請求 [Adobe I/O](https://developer.adobe.com/)，使用新 `server.adobedc.net` 端點。
* 透過 `edge.adobedc.net` 端點。

這可讓您根據組織的隱私權原則，啟用安全、經過驗證的敏感資料收集使用案例。 除了驗證外，伺服器API支援標示資料流，以僅接受透過API進行的已驗證通訊。

請觀看以下影片，以簡化伺服器API的概觀。

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
