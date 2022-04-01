---
title: 邊緣網路伺服器API
description: 瞭解Adobe Experience Platform邊緣網路伺服器API是什麼以及如何使用它。
seo-description: Learn what the Adobe Experience Platform Edge Network Server API is and how you can use it.
keywords: 資料收集；收集；Adobe Experience Platform邊緣網路；伺服器api;
source-git-commit: 92b3a7bff576f72edc8628a850a2cdb9b43cb1c4
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---


# 邊緣網路伺服器API概述

Adobe Experience Platform邊緣網路為客戶與任何Adobe Experience Cloud或Adobe Experience Platform邊緣服務進行交互提供了優化的方式。

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

的 [!DNL Server API] 支援以下類型的請求：的 [!DNL Server API] 支援經驗證的請求 [Adobe I/O](https://developer.adobe.com/)，使用新建 `server.adobedc.net` 端點。

* 通過驗證的請求 [Adobe I/O](https://developer.adobe.com/)，使用新建 `server.adobedc.net` 端點。
* 未通過身份驗證的請求 `edge.adobedc.net` 端點。

這允許根據組織的隱私策略進行安全、經過身份驗證的敏感資料收集的使用案例。 除了驗證外，伺服器API還支援將資料流標籤為只接受通過API的已驗證通信。

觀看下面的視頻，瞭解Server API的簡化概述。

>[!VIDEO](https://video.tv.adobe.com/v/341448/)