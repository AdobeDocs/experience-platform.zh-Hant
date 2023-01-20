---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；體驗事件查詢；體驗事件查詢；體驗事件查詢；體驗事件查詢；
title: 檢視特定訪客的統計報表
description: 下列檔案提供與Adobe Experience Platform Query Service中的Experience Events有關的查詢範例。
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 1%

---

# 檢視特定訪客的統計報表

本檔案提供SQL範例，用於匯總特定使用者從多個分析屬性收集的資料，並在一份報表中一併查看該資料。 使用Adobe Experience Platform Query Service，您可以撰寫使用 [!DNL Experience Events] 擷取各種使用案例。 體驗事件由Experience Data Model(XDM)ExperienceEvent類別表示，該類別會在使用者與網站或服務互動時擷取系統的不可變和非匯總快照。 體驗事件甚至可用於時域分析。 請參閱 [後續步驟區段](#next-steps) 對於涉及 [!DNL Experience Events] 來產生訪客報表。

XDM和 [!DNL Experience Events] 可在 [[!DNL XDM System] 概述](../../xdm/home.md). 將Query Service與 [!DNL Experience Events]，您就可以有效追蹤使用者的行為趨勢。 以下文檔提供了涉及 [!DNL Experience Events].

## 目標

以下SQL示例說明如何查看指定用戶的各種分析值的匯總報告。

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

閱讀本檔案，您就能更清楚了解如何搭配 [!DNL Experience Events] 檢視指定使用者之analytics值的匯總報表。

請參閱下列使用案例，了解其他以訪客為基礎的使用案例：

- [依頁面檢視次數擷取組織的訪客清單。](./visitors-by-number-of-page-views.md)
- [列出訪客先前的工作階段。](./list-visitor-sessions.md)
- [依日建立事件的趨勢報表。](./trended-report-of-events.md)
