---
title: 邊緣網路伺服器API概述
description: 了解 Edge Network 伺服器 API 及其使用方法。
seo-description: Learn what the Edge Network Server API is and how you can use it.
keywords: 資料收集；收集；Adobe Experience Platform邊緣網路；伺服器api;
exl-id: 46bd8798-d7f9-405b-9ca8-856ad4aa688c
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 15%

---

# 邊緣網路伺服器API概述 {#overview}

Adobe Experience Platform Edge Network 為客戶提供與任何 Adobe Experience Cloud 或 Adobe Experience Platform Edge 服務的最佳化互動方式。

的 [!DNL Edge Network Server API] 可用於各種資料收集、個性化、廣告和營銷使用案例。 的 [!DNL Server API] 可以用在伺服器上， [!DNL IoT] 設備、機頂盒和各種其他設備。

自 [!DNL Server API] 它不依賴任何庫來載入，它提供了與Adobe Experience Platform邊緣網路和受支援解決方案進行快速交互的方式。

C.C.的益處 [!DNL Server API] 體系結構包括：

* 減少了頁面負載時間
* 改進的延遲
* 第一方資料收集
* 簡化的服務端通信

的 [!DNL Server API] 支援通過兩個專用端點進行互動式和批處理資料收集：

1. 該互動式終點支援與Adobe Experience Platform和Adobe Experience Cloud服務的通信，這些服務支援高級細分、個性化和其他營銷使用案例。
2. 當需要裝載資料時，批端點將允許批發送請求，而不會從調用的應用程式接收響應。

的 [!DNL Server API] 支援以下類型的請求：

* 通過驗證的請求 [Adobe I/O](https://developer.adobe.com/)，使用新建 `server.adobedc.net` 端點。
* 未通過身份驗證的請求 `edge.adobedc.net` 端點。

這允許根據組織的隱私策略進行安全、經過身份驗證的敏感資料收集的使用案例。 除了驗證外，伺服器API還支援將資料流標籤為只接受通過API的已驗證通信。

觀看下面的視頻，瞭解Server API的簡化概述。

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
