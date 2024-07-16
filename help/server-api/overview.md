---
title: Edge Network伺服器API總覽
description: 了解 Edge Network 伺服器 API 及其使用方法。
exl-id: 46bd8798-d7f9-405b-9ca8-856ad4aa688c
source-git-commit: 041a1782442df5f08bb52e4e450734a51c7781ea
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 5%

---

# Edge Network伺服器API總覽 {#overview}

Adobe Experience PlatformEdge Network為客戶提供與任何Adobe Experience Cloud或Adobe Experience Platform Edge服務的最佳化互動方式。

[!DNL Edge Network Server API]可用於各種資料收集、個人化、廣告和行銷使用案例。 [!DNL Server API]可用於伺服器、[!DNL IoT]裝置、機上盒和各種其他裝置。

由於[!DNL Server API]不依賴任何程式庫來載入，因此可讓您以快如閃電的方式與Adobe Experience PlatformEdge Network和支援的解決方案互動。

[!DNL Server API]架構的優點包括：

* 縮短頁面載入時間
* 改善延遲
* 第一方資料收集
* 簡化服務間的伺服器端通訊

[!DNL Server API]透過兩個專用端點支援互動式和批次資料收集：

1. 互動式端點支援與Adobe Experience Platform和Adobe Experience Cloud服務的通訊，這些服務支援進階細分、個人化和其他行銷使用案例。
2. 當資料必須上線時，批次端點可允許批次傳送請求，而不會收到被呼叫之應用程式的回應。

[!DNL Server API]支援下列型別的要求：

* 已使用`server.adobedc.net`端點透過[Adobe Developer](https://developer.adobe.com/)驗證請求。
* 透過`edge.adobedc.net`端點進行的未驗證要求。

這可啟用使用案例，根據貴組織的隱私權政策，允許安全、經過驗證地收集敏感資料。 除了驗證以外，伺服器API支援標籤資料串流，以僅接受透過API的已驗證通訊。

請觀看以下影片，瞭解伺服器API的簡化概觀。

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
