---
keywords: Experience Platform;home;popular topics;query service;Query service;joining datasets;joining dataset;
solution: Experience Platform
title: 加入資料集
topic: queries
translation-type: tm+mt
source-git-commit: f9749dbc5f2e3ac15be50cc5317ad60586b2c07e
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 3%

---


# 加入資料集

加入資料集可讓您將其他資料集的資料納入查詢中。 此範例使用自訂作業系統資料集將 `operatingsystemID` 值對應 `operatingsystem` 至。

資料集:
- your_analytics_table
- custom_operating_system_lookup

依頁面 `SELECT` 檢視次數建立前50個作業系統的陳述式。

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= ('2018-01-01') AND TIMESTAMP <= ('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

![影像](../images/queries/joining-datasets/select-operating-systems.png)