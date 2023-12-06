---
solution: Experience Platform
title: Media Edge API
description: Media Edge API概述
exl-id: 55c952de-caab-4301-acf2-f7b64cebbb1c
source-git-commit: 034498e662ed55112f22751d44cf3ecf75d38d61
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 3%

---

# Media Edge API總覽

Media Edge API建立在Adobe Experience Platform上，可在的架構中提供媒體事件追蹤資料 [XDM結構描述](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html#:~:text=Experience%20Data%20Model%20(XDM)%2C,the%20power%20of%20digital%20experiences). Media Analytics客戶可藉此使用下列功能：

* 替換為 [Adobe Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=zh-Hant)，客戶可以取得持續時間、開始和停止的近乎即時、精細的詳細資料，以評估和合併媒體量度。 從Adobe Analytics移轉的客戶可在Adobe Customer Journey Analytics中使用所有報表量度。

* 替換為 [Adobe Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=zh-Hant)，客戶可使用媒體使用情況資料豐富其即時設定檔。

* 替換為 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=zh-Hant)，客戶可最佳化全通路行銷活動，並透過媒體使用訊號將歷程自動化。


## 最佳化媒體追蹤資料流程

兩者 [Media Collection API](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-overview.html#media-tracking-data-flows) 和Media Edge API以RESTful服務的形式提供媒體追蹤資料。 但使用Media Edge服務的優點如下：

* 這是將XDM結構描述併入資料流程的最簡單方式。

* 呼叫會從媒體播放器直接導向至 [Experience Platform Edge Network](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=zh-Hant).

* 它只要使用最少量的跨伺服器呼叫，就能有效率地追蹤媒體事件。

下表顯示適用於各種Media Analytics案例的可能Adobe API服務：

| 使用案例 | API服務 |
| -------- | ----------- |
| Adobe Experience Platform解決方案 | 媒體邊緣 |
| Real-Time CDP +Customer Journey Analytics | 媒體邊緣 |
| Adobe Analytics + Adobe Experience Platform解決方案 | 媒體邊緣 |
| 僅限Adobe Analytics （已追蹤） | 媒體收集 |

>[!NOTE]
>
> Analytics的Media Collection API服務仍會接收XDM資料，但並未針對Media Edge服務進行最佳化。 視從Media Player傳送的資料而定，某些僅限Analytics的資料也可以透過Media Edge API服務路由。

下圖顯示兩個API服務的資料流程：

![Media Analytics資料流程](../assets/edge-api-dataflow.png)

## 後續步驟

* 如需使用Media Edge API的詳細資訊，請參閱 [快速入門檔案](getting-started.md).

* 如需使用Platform Edge的詳細資訊，請參閱 [使用Experience Platform Edge安裝Media Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/implementation-edge.html).
