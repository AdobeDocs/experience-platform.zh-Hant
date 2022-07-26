---
audience: user
user-guide-title: Adobe Experience Platform 查詢服務說明
breadcrumb-title: 查詢服務指南
user-guide-description: 使用標準 SQL 在 平台 Data Lake 中查詢資料。
feature: Queries
source-git-commit: 1fe657ac698dd4fcce84902d85b582a9ed7fd4ac
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 18%

---


# Adobe Experience Platform查詢服務 {#query}

- [查詢服務概述](home.md)
- [查詢服務的護欄](guardrails.md)
- 開始使用 {#get-started}
   - [先決條件](get-started/prerequisites.md)
- 使用實例 {#use-cases}
   - [已放棄瀏覽](use-cases/abandoned-browse.md)
   - [活動分析與Adobe Target](use-cases/activity-analysis-with-adobe-target.md)
   - [歸因分析](use-cases/attribution-analysis.md)
   - [機器人過濾](use-cases/bot-filtering.md)
   - [Web和移動分析洞見](use-cases/analytics-insights.md)
- 查詢服務API {#api}
   - [快速入門](api/getting-started.md)
   - [查詢](api/queries.md)
   - [連接參數](api/connection-parameters.md)
   - [計畫查詢](api/scheduled-queries.md)
   - [運行計畫查詢](api/runs-scheduled-queries.md)
   - [查詢模板](api/query-templates.md)
- 查詢服務UI {#ui}
   - [UI概述](ui/overview.md)
   - [查詢編輯器使用手冊](ui/user-guide.md)
   - [查詢模板](ui/query-templates.md)
   - [使用查詢服務憑據](ui/credentials.md)
   - [從查詢結果生成資料集](ui/create-datasets.md)
- 最佳做法 {#best-practices}
   - [查詢執行的一般指導](best-practices/writing-queries.md)
   - [資料資產組織指南](./best-practices/organize-data-assets.md)
   - [使用嵌套資料結構](best-practices/nested-data-structures.md)
   - [拼合嵌套資料結構](best-practices/flatten-nested-data.md)
   - [匿名塊](best-practices/anonymous-block.md)
   - [增量載入](best-practices/incremental-load.md)
   - [重複資料消除](best-practices/deduplication.md)
- 派生屬性 {#derived-attributes}
   - [總覽](derived-attributes/overview.md)
   - [Deciles用例](derived-attributes/deciles-use-case.md)
- 示例查詢 {#sample-queries}
   - [體驗事件查詢示例](sample-queries/experience-event.md)
   - [示例Adobe Analytics查詢](sample-queries/adobe-analytics.md)
- SQL引用 {#sql}
   - [SQL概述](sql/overview.md)
   - [SQL語法](sql/syntax.md)
   - [Adobe定義函式](sql/adobe-defined-functions.md)
   - [Spark SQL函式](sql/spark-sql-functions.md)
   - [元資料命令](sql/metadata.md)
   - [準備的陳述](sql/prepared-statements.md)
- 將客戶端連接到查詢服務 {#clients}
   - [客戶端連接概述](clients/overview.md)
   - [SSL模式](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [資料庫可視化工具](./clients/dbvisulaizer.md)
   - [看](clients/looker.md)
   - [波斯蒂科](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RStudio](clients/rstudio.md)
   - [塔布洛](clients/tableau.md)
- 資料治理 {#data-governance}
   - [總覽](data-governance/overview.md)
   - [審核日誌指南](data-governance/audit-log-guide.md)
   - [ad hoc模式資料集中的標識](data-governance/ad-hoc-schema-identities.md)
   - [基於屬性的訪問控制支援ad hoc模式](./data-governance/ad-hoc-schema-labels.md)
- [故障排除指南](troubleshooting-guide.md)
- [API 參考資料](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [平台發行說明](https://www.adobe.com/go/platform-release-notes-en)