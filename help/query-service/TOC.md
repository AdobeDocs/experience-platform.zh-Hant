---
audience: user
user-guide-title: Adobe Experience Platform 查詢服務說明
breadcrumb-title: 查詢服務指南
user-guide-description: 使用標準 SQL 在 平台 Data Lake 中查詢資料。
feature: Queries
source-git-commit: df894d8b52aff3708aa06e73d4c5ba3e1e501f10
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 17%

---


# Adobe Experience Platform查詢服務 {#query}

- [查詢服務概述](home.md)
- [查詢服務包裝](packages.md)
- [查詢服務護欄](guardrails.md)
- 資料Distiller {#data-distiller}
   - [授權使用](data-distiller/licence-usage.md)
- 開始使用 {#get-started}
   - [先決條件](get-started/prerequisites.md)
- 使用實例 {#use-cases}
   - [放棄的瀏覽](use-cases/abandoned-browse.md)
   - [使用Adobe Target進行活動分析](use-cases/activity-analysis-with-adobe-target.md)
   - [歸因分析](use-cases/attribution-analysis.md)
   - [機器人篩選](use-cases/bot-filtering.md)
   - [網頁和行動分析](use-cases/analytics-insights.md)
- 查詢服務API {#api}
   - [快速入門](api/getting-started.md)
   - [查詢](api/queries.md)
   - [連線參數](api/connection-parameters.md)
   - [排程查詢](api/scheduled-queries.md)
   - [針對排程查詢執行](api/runs-scheduled-queries.md)
   - [查詢範本](api/query-templates.md)
- 查詢服務UI {#ui}
   - [UI概述](ui/overview.md)
   - [查詢編輯器使用手冊](ui/user-guide.md)
   - [查詢範本](ui/query-templates.md)
   - [使用查詢服務憑據](ui/credentials.md)
   - [從查詢結果產生資料集](ui/create-datasets.md)
- 最佳做法 {#best-practices}
   - [查詢執行的一般指南](best-practices/writing-queries.md)
   - [資料資產組織指南](./best-practices/organize-data-assets.md)
   - [使用巢狀資料結構](best-practices/nested-data-structures.md)
   - [平面化巢狀資料結構](best-practices/flatten-nested-data.md)
   - [匿名塊](best-practices/anonymous-block.md)
   - [增量載入](best-practices/incremental-load.md)
   - [重複資料刪除](best-practices/deduplication.md)
- 衍生屬性 {#derived-attributes}
   - [總覽](derived-attributes/overview.md)
   - [Deciles使用案例](derived-attributes/deciles-use-case.md)
- 範例查詢 {#sample-queries}
   - [體驗事件查詢範例](sample-queries/experience-event.md)
   - [範例Adobe Analytics查詢](sample-queries/adobe-analytics.md)
- SQL參考 {#sql}
   - [SQL概述](sql/overview.md)
   - [SQL語法](sql/syntax.md)
   - [Adobe定義的函式](sql/adobe-defined-functions.md)
   - [Spark SQL函式](sql/spark-sql-functions.md)
   - [元資料命令](sql/metadata.md)
   - [準備的陳述](sql/prepared-statements.md)
   - [資料集範例](sql/dataset-samples.md)
- 將客戶端連接到查詢服務 {#clients}
   - [用戶端連線概觀](clients/overview.md)
   - [SSL模式](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [資料庫可視化工具](./clients/dbvisulaizer.md)
   - [朱佩特筆記型電腦](clients//jupyter-notebook.md)
   - [Looker](clients/looker.md)
   - [波斯蒂科](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RStudio](clients/rstudio.md)
   - [塔布洛](clients/tableau.md)
- 資料治理 {#data-governance}
   - [總覽](data-governance/overview.md)
   - [稽核記錄指南](data-governance/audit-log-guide.md)
   - [臨機結構資料集中的身分](data-governance/ad-hoc-schema-identities.md)
   - [臨機結構的基於屬性的訪問控制支援](./data-governance/ad-hoc-schema-labels.md)
- [疑難排解指南](troubleshooting-guide.md)
- [API 參考資料](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [平台發行說明](https://www.adobe.com/go/platform-release-notes-en)