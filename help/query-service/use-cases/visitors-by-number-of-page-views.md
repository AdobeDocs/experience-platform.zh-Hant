---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；體驗事件查詢；體驗事件查詢；體驗事件查詢；
title: 按訪問者的頁面視圖數列出訪問者
description: 瞭解如何編寫使用「體驗事件」來檢索按頁面視圖陣列織的訪問者清單的查詢。
exl-id: 6e8eed0c-838e-4cd0-ae8c-453114fbf4ea
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 1%

---

# 按訪問者的頁面視圖數列出訪問者

本文檔提供了檢索按頁面視圖陣列織的訪問者清單所需的SQL示例。 使用Adobe Experience Platform查詢服務，可以編寫使用 [!DNL Experience Events] 以捕獲各種使用案例。 體驗事件由體驗資料模型(XDM)ExperienceEvent類表示，該類在用戶與網站或服務交互時捕獲系統的不可改變和非聚合快照。 體驗事件甚至可用於時域分析。 查看 [後續步驟部分](#next-steps) 更多涉及 [!DNL Experience Events] 生成訪問者報告。

有關XDM和 [!DNL Experience Events] 在 [[!DNL XDM System] 概述](../../xdm/home.md)。 通過將Query Service與 [!DNL Experience Events]，您可以有效跟蹤用戶間的行為趨勢。 以下文檔提供了涉及 [!DNL Experience Events]。

## 目標

以下示例建立一個報告，其中列出了已查看最多頁面的用戶的10個ID。

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

通過閱讀此文檔，您可以更好地瞭解如何使用查詢服務 [!DNL Experience Events] 列出已查看最多頁面的用戶。

請參閱以下使用案例以瞭解其他基於訪問者的使用案例：

- [列出訪問者以前的會話。](./list-visitor-sessions.md)
- [查看訪問者的匯總報告。](./roll-up-report-of-a-visitor.md)
- [按天建立事件趨勢報告。](./trended-report-of-events.md)
