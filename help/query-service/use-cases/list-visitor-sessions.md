---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；體驗事件查詢；體驗事件查詢；體驗事件查詢；
title: 列出用戶的頁面視圖
description: 瞭解如何編寫使用「體驗事件」建立指定用戶已使用的最後100頁清單的查詢。
exl-id: d831910d-d3a4-4a5a-b897-b09f0546dab0
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 1%

---

# 列出用戶的頁面視圖

本文檔提供了列出指定用戶的頁面視圖所需的SQL示例。 使用Adobe Experience Platform查詢服務，可以編寫使用 [!DNL Experience Events] 以捕獲各種使用案例。 體驗事件由體驗資料模型(XDM)ExperienceEvent類表示，該類在用戶與網站或服務交互時捕獲系統的不可改變和非聚合快照。 體驗事件甚至可用於時域分析。 查看 [後續步驟部分](#next-steps) 更多涉及 [!DNL Experience Events] 生成訪問者報告。

有關XDM和 [!DNL Experience Events] 在 [[!DNL XDM System] 概述](../../xdm/home.md)。 通過將Query Service與 [!DNL Experience Events]，您可以有效跟蹤用戶間的行為趨勢。 以下文檔提供了涉及 [!DNL Experience Events]。

## 目標

以下示例列出了指定用戶已查看的最後100頁。

```sql
SELECT 
timestamp, 
web.webReferrer.type as referrerType, 
web.webReferrer.URL as referrer, 
web.webPageDetails.name as pageName, 
_experience.analytics.event1to100.event1.value as A, 
_experience.analytics.event1to100.event2.value as B, 
_experience.analytics.event1to100.event3.value as C, 
web.webPageDetails.pageviews.value as pageViews
FROM your_analytics_table 
WHERE endUserIds._experience.aaid.id = '457C3510571E5930-69AA721C4CBF9339' 
ORDER BY timestamp 
LIMIT 100;
```

此查詢的結果如下所示。

```console
      timestamp       |  referrerType  |                            referrer                                |                 pageName            |  A  |  B  |  C  | pageViews
----------------------+----------------+--------------------------------------------------------------------+-------------------------------------+-----+-----+-----+--------------
2019-11-08 17:15:28.0 | typed_bookmark |                                                                    |                                     |     |     |     |
2019-11-08 17:53:05.0 | social         | http://www.reddit.com                                              | Home                                |     |     |     |          1.0
2019-11-08 17:53:45.0 | typed_bookmark |                                                                    | Kids                                |     |     |     |          1.0
2019-11-08 19:22:34.0 | typed_bookmark |                                                                    |                                     |     |     |     |          
2019-11-08 20:01:12.0 | search_engine  | http://www.google.com/search?ie=UTF-8&q=laundry parkas&cid=sem:115 | Home                                |     |     |     |          1.0 
2019-11-08 20:01:57.0 | typed_bookmark |                                                                    | Kids                                |     |     |     |          1.0
2019-11-08 20:03:36.0 | typed_bookmark |                                                                    | Search Results                      | 1.0 |     |     |          1.0
2019-11-08 20:04:30.0 | typed_bookmark |                                                                    | Product Details: Pemmican Power Bar |     |     |     |          1.0
2019-11-08 20:05:27.0 | typed_bookmark |                                                                    | Shopping Cart: Cart Details         |     |     |     |          1.0
2019-11-08 20:06:07.0 | typed_bookmark |                                                                    | Shopping Cart: Shipping Information |     |     |     |          1.0
2019-11-08 20:07:02.0 | typed_bookmark |                                                                    | Shopping Cart: Billing Information  |     |     | 1.0 |          1.0
2019-11-08 20:07:52.0 | typed_bookmark |                                                                    | Shopping Cart: Order Review         |     |     |     |          1.0
2019-11-08 20:08:45.0 | typed_bookmark |                                                                    | Order Confirmation                  |     |     |     |          1.0
2019-11-08 20:09:24.0 | typed_bookmark |                                                                    | Home                                |     |     |     |          1.0
2019-11-08 20:10:03.0 | typed_bookmark |                                                                    | Editorial Page: Camping Essentials  |     |     |     |          1.0
2019-11-08 20:11:01.0 | typed_bookmark |                                                                    | Account Registration|Form           |     |     |     |          1.0
2019-11-08 20:11:38.0 | typed_bookmark |                                                                    | Seasonal Sale                       |     |     |     |          1.0
2019-11-08 20:12:10.0 | typed_bookmark |                                                                    | Blog: Iris Sagan                    |     |     |     |          1.0
2019-11-08 20:13:09.0 | typed_bookmark |                                                                    | Product Details: UltraTech Socks    |     |     |     |          1.0
2019-11-08 20:14:05.0 | typed_bookmark |                                                                    | Seasonal Sale                       |     |     |     |          1.0
```

## 後續步驟 {#next-steps}

通過閱讀此文檔，您可以更好地瞭解如何使用查詢服務 [!DNL Experience Events] 列出頁面視圖。

請參閱以下使用案例以瞭解其他基於訪問者的使用案例：

- [檢索按頁面視圖陣列織的訪問者清單。](./visitors-by-number-of-page-views.md)
- [查看訪問者的匯總報告。](./roll-up-report-of-a-visitor.md)
- [按天建立事件趨勢報告。](./trended-report-of-events.md)
