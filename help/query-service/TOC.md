---
audience: user
user-guide-title: Adobe Experience Platform 查詢服務說明
breadcrumb-title: 查詢服務指南
user-guide-description: 使用標準 SQL 在 Experience Platform 的 Data Lake 中查詢資料。
feature: Queries
role: User,Developer
source-git-commit: 61b20f2a618ed4305351b2fe6ff771a45d759de1
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 19%

---


# Adobe Experience Platform查詢服務 {#query}

- [查詢服務總覽](home.md)
- [查詢服務封裝](packaging.md)
- [查詢服務護欄](guardrails.md)
- 開始使用 {#get-started}
   - [先決條件](get-started/prerequisites.md)
- 資料Distiller {#data-distiller}
   - [概觀](data-distiller/overview.md)
   - [授權使用情況](data-distiller/license-usage.md)
   - 衍生資料集 {#derived-datasets}
      - [概觀](data-distiller/derived-datasets/overview.md)
      - [使用SQL建立衍生資料集](data-distiller/derived-datasets/create-derived-datasets-with-sql.md)
      - [建立十等分衍生資料集](data-distiller/derived-datasets/decile-based-derived-attributes.md)
   - 延伸應用程式報表的可自訂分析 {#customizable-insights}
      - [概觀](data-distiller/customizable-insights/overview.md)
      - [傳送加速的查詢](data-distiller/customizable-insights/send-accelerated-queries.md)
      - [報表深入分析資料模型指南](data-distiller/customizable-insights/reporting-insights-data-model.md)
   - AI/ML功能管道 {#ml-feature-pipelines}
      - [概觀](data-distiller/ml-feature-pipelines/overview.md)
      - [連線到Jupyter Notebooks](data-distiller/ml-feature-pipelines/establish-connection.md)
      - [探索資料分析](data-distiller/ml-feature-pipelines/exploratory-analysis.md)
      - [ML的工程師功能](data-distiller/ml-feature-pipelines/feature-engineering.md)
      - [將資料匯出至ML環境](data-distiller/ml-feature-pipelines/export-data.md)
      - [AI/ML資料管道擴充端對端工作流程](data-distiller/ml-feature-pipelines/end-to-end-notebook-workflow.md)
- 使用案例 {#use-cases}
   - [概觀](use-cases/overview.md)
   - [捨棄的瀏覽](use-cases/abandoned-browse.md)
   - [歸因分析](use-cases/attribution-analysis.md)
   - [機器人篩選](use-cases/bot-filtering.md)
   - [建立事件的趨勢報表](use-cases/trended-report-of-events.md)
   - [同意分析](use-cases/consent-analysis.md)
   - [客戶期限值](use-cases/customer-lifetime-value.md)
   - [十等分衍生資料集](use-cases/deciles-use-case.md)
   - [模糊比對](use-cases/fuzzy-match.md)
   - [列出使用者的頁面檢視](use-cases/list-visitor-sessions.md)
   - [依頁面檢視列出訪客](use-cases/visitors-by-number-of-page-views.md)
   - [傾向分數](use-cases/propensity-score.md)
   - [使用較高階函式擷取類似記錄](use-cases/retrieve-similar-records.md)
   - [從Analytics資料傳回並使用銷售變數](use-cases/merchandising-variables.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [檢視訪客的統計報表](use-cases/roll-up-report-of-a-visitor.md)
   - [網站和行動分析深入分析](use-cases/analytics-insights.md)
- 重要概念{#key-concepts}
   - [使用巢狀資料結構](key-concepts/nested-data-structures.md)
   - [平面化巢狀資料結構](key-concepts/flatten-nested-data.md)
   - [匿名區塊](key-concepts/anonymous-block.md)
   - [內嵌範本](key-concepts/inline-templates.md)
   - [增量載入](key-concepts/incremental-load.md)
   - [重複資料刪除](key-concepts/deduplication.md)
   - [資料集範例](key-concepts/dataset-samples.md)
   - [資料集統計資料計算](key-concepts/dataset-statistics.md)
- 將使用者端連線至查詢服務 {#clients}
   - [使用者端連線概觀](clients/overview.md)
   - [SSL模式](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
   - [Jupyter Notebook](clients//jupyter-notebook.md)
   - [檢視器](clients/looker.md)
   - [Postico](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RStudio](clients/rstudio.md)
   - [Tableau](clients/tableau.md)
- 查詢服務UI {#ui}
   - [UI總覽](ui/overview.md)
   - [查詢編輯器使用手冊](ui/user-guide.md)
   - [查詢範本](ui/query-templates.md)
   - [參數化查詢](ui/parameterized-queries.md)
   - [查詢排程](ui/query-schedules.md)
   - [查詢記錄](ui/query-logs.md)
   - [監視已排程查詢](ui/monitor-queries.md)
   - [認證指南](ui/credentials.md)
   - [從查詢結果產生輸出資料集](ui/create-datasets.md)
- 查詢服務API端點 {#api}
   - [快速入門](api/getting-started.md)
   - [查詢](api/queries.md)
   - [連線參數](api/connection-parameters.md)
   - [時程表](api/scheduled-queries.md)
   - [已排程查詢的執行](api/runs-scheduled-queries.md)
   - [查詢範本](api/query-templates.md)
   - [加速的查詢](api/accelerated-queries.md)
   - [警報訂閱](api/alert-subscriptions.md)
- 資料控管 {#data-governance}
   - [概觀](data-governance/overview.md)
   - [稽核記錄指南](data-governance/audit-log-guide.md)
   - [臨時結構描述資料集中的身分](data-governance/ad-hoc-schema-identities.md)
   - [針對臨時結構描述的屬性型存取控制支援](./data-governance/ad-hoc-schema-labels.md)
- 最佳實務{#best-practices}
   - [查詢執行](best-practices/writing-queries.md)
   - [資料資產組織](./best-practices/organize-data-assets.md)
- SQL參考 {#sql}
   - [SQL概述](sql/overview.md)
   - [SQL語法](sql/syntax.md)
   - [Adobe定義的函式](sql/adobe-defined-functions.md)
   - [高階函式](sql/higher-order-functions.md)
   - [Spark SQL函式](sql/spark-sql-functions.md)
   - [中繼資料命令](sql/metadata.md)
   - [準備的陳述式](sql/prepared-statements.md)
- [常見問答](troubleshooting-guide.md)
- [IP位址允許清單](ip-address-allowlist.md)
- [API 參考資料](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Platform發行說明](https://experienceleague.adobe.com/en/docs/experience-platform/release-notes/latest)
