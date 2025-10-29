---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；experienceevent查詢；experienceevent查詢；體驗事件查詢；
title: 檢視特定訪客的統計報表
description: 以下檔案提供在Adobe Experience Platform查詢服務中涉及Experience事件的查詢範例。
exl-id: 1348503f-65c1-41f9-b111-1284a49449a1
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 1%

---

# 檢視特定訪客的統計報表

本檔案提供了一個SQL範例，用來彙總特定使用者的多個分析屬性的資料，並在一個報表中一起檢視這些資料。 使用Adobe Experience Platform查詢服務，您可以撰寫使用[!DNL Experience Events]來擷取各種使用案例的查詢。 體驗事件由體驗資料模型(XDM) ExperienceEvent類別表示，可在使用者與網站或服務互動時，擷取系統不可變且非彙總的快照。 體驗事件甚至可用於時間網域分析。 請參閱[後續步驟一節](#next-steps)，瞭解更多涉及[!DNL Experience Events]產生訪客報表的使用案例。

有關XDM和[!DNL Experience Events]的更多資訊可在[[!DNL XDM System] 總覽](../../xdm/home.md)中找到。 結合查詢服務與[!DNL Experience Events]，您就能有效追蹤使用者之間的行為趨勢。 下列檔案提供涉及[!DNL Experience Events]的查詢範例。

## 目標

下列SQL範例顯示如何檢視指定使用者之各種分析值的彙總報表。

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
|----------------------------------+-----------+-------+-------+-------+--------------
457C3510571E5930-69AA721C4CBF9339 |     706.0 | 83.0  |  7.0  | 38.0  |          22
```

## 後續步驟 {#next-steps}

閱讀本檔案可讓您更瞭解如何搭配[!DNL Experience Events]使用查詢服務，以檢視指定使用者的分析值彙總報表。

請參閱下列使用案例，以瞭解其他以訪客為基礎的使用案例：

- [擷取按頁面檢視次陣列織的訪客清單。](./visitors-by-number-of-page-views.md)
- [列出訪客之前的工作階段。](./list-visitor-sessions.md)
- [依日期建立事件的趨勢報表。](./trended-report-of-events.md)
