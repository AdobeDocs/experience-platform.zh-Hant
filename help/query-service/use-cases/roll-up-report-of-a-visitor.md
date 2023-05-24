---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；體驗事件查詢；體驗事件查詢；體驗事件查詢；
title: 查看特定訪問者的匯總報告
description: 以下文檔提供了涉及Adobe Experience Platform查詢服務中的體驗事件的查詢示例。
exl-id: 1348503f-65c1-41f9-b111-1284a49449a1
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 1%

---

# 查看特定訪問者的匯總報告

本文檔提供了一個SQL示例，用於從特定用戶的多個分析屬性中聚合資料，並在一個報告中一起查看該資料。 使用Adobe Experience Platform查詢服務，可以編寫使用 [!DNL Experience Events] 以捕獲各種使用案例。 體驗事件由體驗資料模型(XDM)ExperienceEvent類表示，該類在用戶與網站或服務交互時捕獲系統的不可改變和非聚合快照。 體驗事件甚至可用於時域分析。 查看 [後續步驟部分](#next-steps) 更多涉及 [!DNL Experience Events] 生成訪問者報告。

有關XDM和 [!DNL Experience Events] 在 [[!DNL XDM System] 概述](../../xdm/home.md)。 通過將Query Service與 [!DNL Experience Events]，您可以有效跟蹤用戶間的行為趨勢。 以下文檔提供了涉及 [!DNL Experience Events]。

## 目標

以下SQL示例說明如何查看指定用戶的各種分析值的聚合報告。

```sql
SELECT 
endUserIds._experience.aaid.id, 
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
WHERE endUserIds._experience.aaid.id = '457C3510571E5930-69AA721C4CBF9339' 
GROUP BY endUserIds._experience.aaid.id
ORDER BY pageViews DESC;
```

查詢結果顯示在下表中。

```console
               id                 | pageViews |   A   |   B   |   C   | viewedParkas
----------------------------------+-----------+-------+-------+-------+--------------
457C3510571E5930-69AA721C4CBF9339 |     706.0 | 83.0  |  7.0  | 38.0  |          22
```

## 後續步驟 {#next-steps}

通過閱讀此文檔，您可以更好地瞭解如何使用查詢服務 [!DNL Experience Events] 查看指定用戶的分析值的聚合報告。

請參閱以下使用案例以瞭解其他基於訪問者的使用案例：

- [檢索按頁面視圖陣列織的訪問者清單。](./visitors-by-number-of-page-views.md)
- [列出訪問者以前的會話。](./list-visitor-sessions.md)
- [按天建立事件趨勢報告。](./trended-report-of-events.md)
