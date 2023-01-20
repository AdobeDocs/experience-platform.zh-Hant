---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；體驗事件查詢；體驗事件查詢；體驗事件查詢；體驗事件查詢；
title: 列出使用者的頁面檢視
description: 了解如何撰寫使用體驗事件的查詢，以建立指定使用者已使用的最近100個頁面的清單。
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 1%

---

# 列出使用者的頁面檢視

本文檔提供了列出指定用戶的頁面視圖所需的SQL示例。 使用Adobe Experience Platform Query Service，您可以撰寫使用 [!DNL Experience Events] 擷取各種使用案例。 體驗事件由Experience Data Model(XDM)ExperienceEvent類別表示，該類別會在使用者與網站或服務互動時擷取系統的不可變和非匯總快照。 體驗事件甚至可用於時域分析。 請參閱 [後續步驟區段](#next-steps) 對於涉及 [!DNL Experience Events] 來產生訪客報表。

XDM和 [!DNL Experience Events] 可在 [[!DNL XDM System] 概述](../../xdm/home.md). 將Query Service與 [!DNL Experience Events]，您就可以有效追蹤使用者的行為趨勢。 以下文檔提供了涉及 [!DNL Experience Events].

## 目標

下列範例列出指定使用者檢視的最近100個頁面。

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

閱讀本檔案，您就能更清楚了解如何搭配 [!DNL Experience Events] 將頁面檢視列為指定的使用者。

請參閱下列使用案例，了解其他以訪客為基礎的使用案例：

- [依頁面檢視次數擷取組織的訪客清單。](./visitors-by-number-of-page-views.md)
- [檢視訪客的統計報表。](./roll-up-report-of-a-visitor.md)
- [依日建立事件的趨勢報表。](./trended-report-of-events.md)
