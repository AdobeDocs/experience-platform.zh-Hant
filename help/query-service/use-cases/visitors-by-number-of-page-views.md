---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；體驗事件查詢；體驗事件查詢；體驗事件查詢；體驗事件查詢；
title: 依訪客的頁面檢視次數列出訪客
description: 了解如何撰寫使用體驗事件來擷取依頁面檢視次陣列織之訪客清單的查詢。
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 1%

---

# 依訪客的頁面檢視次數列出訪客

本檔案提供擷取依頁面檢視次陣列織之訪客清單所需的SQL範例。 使用Adobe Experience Platform Query Service，您可以撰寫使用 [!DNL Experience Events] 擷取各種使用案例。 體驗事件由Experience Data Model(XDM)ExperienceEvent類別表示，該類別會在使用者與網站或服務互動時擷取系統的不可變和非匯總快照。 體驗事件甚至可用於時域分析。 請參閱 [後續步驟區段](#next-steps) 對於涉及 [!DNL Experience Events] 來產生訪客報表。

XDM和 [!DNL Experience Events] 可在 [[!DNL XDM System] 概述](../../xdm/home.md). 將Query Service與 [!DNL Experience Events]，您就可以有效追蹤使用者的行為趨勢。 以下文檔提供了涉及 [!DNL Experience Events].

## 目標

下列範例會建立報表，列出檢視次數最多頁面之使用者的10個ID。

```sql
SELECT 
endUserIds._experience.aaid.id, 
SUM(web.webPageDetails.pageviews.value) as pageViews 
FROM your_analytics_table
GROUP BY endUserIds._experience.aaid.id 
ORDER BY pageViews DESC
LIMIT 10;
```

查詢結果顯示在下表中。

```console
               id                  | pageViews
-----------------------------------+-----------
 457C3510571E5930-69AA721C4CBF9339 |     706.0
 776F85658792C017-6491FE6570382A01 |     700.0
 6BEC9C6AB52E779F-28F5B023113F2C85 |     654.0
 1C0CCFB2DC63611E-6E4A4D4142AEB613 |     642.0
 112EE9A6F3BE29D1-514A6C355A2C9EF6 |     629.0
 CCC75A0E6AC7F2FA-11D58515D370F626 |     624.0
 749F850A44153120-3710C53FA2162349 |     614.0
 2B668C6DDDAF0C505-92EDCC072F7CDDA |     587.0
 7EB7257335935320-101921AF45111FE6 |     586.0
 5F4759CA80DCA9C9-2C0DA93D80D9DBFA |     586.0
(10 rows)
```

## 後續步驟 {#next-steps}

閱讀本檔案，您就能更清楚了解如何搭配 [!DNL Experience Events] 列出檢視次數最多頁面的使用者。

請參閱下列使用案例，了解其他以訪客為基礎的使用案例：

- [列出訪客先前的工作階段。](./list-visitor-sessions.md)
- [檢視訪客的統計報表。](./roll-up-report-of-a-visitor.md)
- [依日建立事件的趨勢報表。](./trended-report-of-events.md)
