---
keywords: Experience Platform；media edge；熱門主題；日期範圍
solution: Experience Platform
title: Media Edge API
description: Media Edge API概述。
exl-id: null
source-git-commit: f040ba6d1403da4212fe279e32316bac995905b2
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 5%

---


# Media Edge API總覽

Media Edge API建立在Adobe Experience Platform (AEP)上，可在的架構中提供媒體事件追蹤資料 [XDM結構描述](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=en#:~:text=Experience%20Data%20Model%20(XDM)%2C,the%20power%20of%20digital%20experiences). Media Analytics客戶可以使用此功能來使用下列功能：

* 替換為 [Customer Journey Analytics(CJA)](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=zh-Hant)，客戶可獲得持續時間、開始和停止的近乎即時、精細的詳細資訊，以評估和合併媒體量度。 從Adobe Analytics移轉的客戶可在CJA中使用所有報告量度。

* 替換為 [Adobe Real-time Customer Data Platform (CDP)](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html)，客戶可使用媒體使用資料擴充其即時設定檔。

* 替換為 [Adobe Journey Optimizer (AJO)](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=en)，客戶可最佳化全通路行銷活動，並透過媒體使用訊號將歷程自動化。


## 最佳化媒體追蹤資料流程

兩者 [媒體收集](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-overview.html?lang=en&amp;media-tracking-data-flows) API和Media Edge API以RESTful服務的形式提供媒體追蹤資料。 但是使用Media Edge服務有以下優點：

* 這是將XDM結構描述併入資料流程的最簡單方式。

* 呼叫會從媒體播放器直接導向至 [Experience Edge Platform Network](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=en).

* 最有效率地追蹤媒體事件。

下表呈現各種媒體分析案例適用的最佳Adobe API服務：

| 使用案例 | 平台 | API服務 |
| -------- | ------ | ---------- |
| CJA | AEP | 媒體邊緣 |
| CDP + CJA | AEP | 媒體邊緣 |
| Analytics + CJA | AEP | 媒體邊緣 |
| 舊版分析 | 不適用 | 媒體收集 |

>[!NOTE]
>
> Analytics的Media Collection API服務仍會接收XDM資料，但並未針對Media Edge服務進行最佳化。 根據從Media Player傳送的資料，某些Analytics專用資料也可以透過Media Edge API服務路由。

下圖顯示兩個API服務的資料流程：


![Media Analytics資料流程](../assets/edge-api-dataflow.png)


如需使用Media Edge API的詳細資訊，請參閱快速入門檔案。

如需使用Platform Edge的詳細資訊，請參閱 [使用Experience Platform邊緣安裝Media Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/implementation-edge.html?lang=en).




