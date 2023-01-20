---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；體驗事件查詢；體驗事件查詢；體驗事件查詢；體驗事件查詢；
title: 建立事件趨勢報表
description: 了解如何撰寫使用體驗事件來建立指定日期範圍內事件趨勢報表（依日期分組）的查詢。
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# 建立事件的趨勢報表

本檔案提供在特定日期範圍內按日建立事件趨勢報告所需的SQL範例。 使用Adobe Experience Platform Query Service，您可以撰寫使用 [!DNL Experience Events] 擷取各種使用案例。 體驗事件由Experience Data Model(XDM)ExperienceEvent類別表示，該類別會在使用者與網站或服務互動時擷取系統的不可變和非匯總快照。 體驗事件甚至可用於時域分析。 請參閱 [後續步驟區段](#next-steps) 對於涉及 [!DNL Experience Events] 來產生訪客報表。

報表可讓您存取Platform資料，以利貴組織的策略性業務分析。 透過這些報表，您可以透過各種方式檢查您的Platform資料、以簡單明瞭的格式顯示關鍵量度，並共用產生的深入分析。

XDM和 [!DNL Experience Events] 可在 [[!DNL XDM System] 概述](../../xdm/home.md). 將Query Service與 [!DNL Experience Events]，您就可以有效追蹤使用者的行為趨勢。 以下文檔提供了涉及 [!DNL Experience Events].

## 目標

下列範例會建立指定日期範圍內事件的趨勢報表，並依日期分組。 具體來說，此SQL範例將各種分析值總結為 `A`, `B`，和 `C`，然後總和一個月內parkas被檢視的次數。

在中找到的時間戳記欄 [!DNL Experience Event] 資料集為UTC格式。 範例使用 `from_utc_timestamp()` 函式，將時間戳記從UTC轉換為EDT，然後使用 `date_format()` 函式可將日期與其餘的時間戳記隔離。

```sql
SELECT 
date_format( from_utc_timestamp(timestamp, 'EDT') , 'yyyy-MM-dd') as Day,
SUM(web.webPageDetails.pageviews.value) as pageViews,
SUM(_experience.analytics.event1to100.event1.value) as A,
SUM(_experience.analytics.event1to100.event2.value) as B,
SUM(_experience.analytics.event1to100.event3.value) as C,
SUM(
    CASE 
    WHEN _experience.analytics.customDimensions.evars.evar1 = 'parkas' 
    THEN 1 
    ELSE 0 
    END) as viewedParkas
FROM your_analytics_table 
WHERE TIMESTAMP >= to_timestamp('2019-03-01') AND TIMESTAMP <= to_timestamp('2019-03-31')
GROUP BY Day 
ORDER BY Day ASC, pageViews DESC;
```

此查詢的結果如下所示。

```console
     Day     | pageViews |   A    |   B   |    C    | viewedParkas
-------------+-----------+--------+-------+---------+--------------
 2019-03-01  |   55317.0 | 8503.0 | 804.0 | 1578.0  |           73
 2019-03-02  |   55302.0 | 8600.0 | 854.0 | 1528.0  |           86
 2019-03-03  |   54613.0 | 8162.0 | 795.0 | 1568.0  |          100
 2019-03-04  |   54501.0 | 8479.0 | 832.0 | 1509.0  |          100
 2019-03-05  |   54941.0 | 8603.0 | 816.0 | 1514.0  |           73
 2019-03-06  |   54817.0 | 8434.0 | 855.0 | 1538.0  |           76
 2019-03-07  |   55201.0 | 8604.0 | 843.0 | 1517.0  |           64
 2019-03-08  |   55020.0 | 8490.0 | 849.0 | 1536.0  |           99
 2019-03-09  |   43186.0 | 6736.0 | 643.0 | 1150.0  |           52
 2019-03-10  |   48471.0 | 7542.0 | 772.0 | 1272.0  |           70
 2019-03-11  |   56307.0 | 8721.0 | 818.0 | 1571.0  |           81
 2019-03-12  |   55374.0 | 8653.0 | 843.0 | 1501.0  |           59
 2019-03-13  |   55046.0 | 8509.0 | 887.0 | 1556.0  |           65
 2019-03-14  |   55518.0 | 8551.0 | 848.0 | 1516.0  |           77
 2019-03-15  |   55329.0 | 8575.0 | 818.0 | 1607.0  |           96
 2019-03-16  |   55030.0 | 8651.0 | 815.0 | 1542.0  |           66
 2019-03-17  |   55143.0 | 8435.0 | 774.0 | 1572.0  |           65
 2019-03-18  |   54065.0 | 8211.0 | 816.0 | 1574.0  |          111
 2019-03-19  |   55097.0 | 8395.0 | 771.0 | 1498.0  |           86
 2019-03-20  |   55198.0 | 8472.0 | 863.0 | 1583.0  |           82
 2019-03-21  |   54978.0 | 8490.0 | 820.0 | 1580.0  |           83
 2019-03-22  |   55464.0 | 8561.0 | 820.0 | 1559.0  |           83
 2019-03-23  |   55384.0 | 8482.0 | 800.0 | 1139.0  |           82
 2019-03-24  |   55295.0 | 8594.0 | 841.0 | 1382.0  |           78
 2019-03-25  |   42069.0 | 6365.0 | 606.0 | 1509.0  |           62
 2019-03-26  |   49724.0 | 7629.0 | 724.0 | 1553.0  |           44
 2019-03-27  |   55111.0 | 8524.0 | 804.0 | 1524.0  |           94
 2019-03-28  |   55030.0 | 8439.0 | 822.0 | 1554.0  |           73
 2019-03-29  |   55281.0 | 8601.0 | 854.0 | 1580.0  |           73
 2019-03-30  |   55162.0 | 8538.0 | 846.0 | 1534.0  |           79
 2019-03-31  |   55437.0 | 8486.0 | 807.0 | 1649.0  |           68
 (31 rows)
```

## 後續步驟 {#next-steps}

閱讀本檔案，您就能更清楚了解如何搭配 [!DNL Experience Events] 來有效追蹤使用者的行為趨勢。

了解其他使用以訪客為基礎的使用案例 [!DNL Experience Events]，請閱讀下列檔案：

- [依頁面檢視次數擷取組織的訪客清單。](./visitors-by-number-of-page-views.md)
- [列出訪客先前的工作階段。](./list-visitor-sessions.md)
- [檢視訪客的統計報表。](./roll-up-report-of-a-visitor.md)
