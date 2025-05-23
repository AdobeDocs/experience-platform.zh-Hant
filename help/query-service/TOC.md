---
audience: user
user-guide-title: Adobe Experience Platform 查詢服務說明
breadcrumb-title: 查詢服務指南
user-guide-description: 使用標準 SQL 在 Experience Platform 的 Data Lake 中查詢資料。
feature: Queries
role: User,Developer
source-git-commit: 8b33d9231aeebd454fd614a81b356a9e971b757c
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 26%

---


# Adobe Experience Platform查詢服務 {#query}

- [查詢服務總覽](home.md)
- [查詢服務封裝](packaging.md)
- [查詢服務護欄](guardrails.md)
- 快速入門 {#get-started}
   - [先決條件](get-started/prerequisites.md)
- 資料蒸餾器 {#data-distiller}
   - [概觀](data-distiller/overview.md)
   - [授權使用情況](data-distiller/license-usage.md)
   - 衍生資料集 {#derived-datasets}
      - [概觀](data-distiller/derived-datasets/overview.md)
      - [使用SQL建立衍生資料集](data-distiller/derived-datasets/create-derived-datasets-with-sql.md)
      - [建立十等分衍生資料集](data-distiller/derived-datasets/decile-based-derived-attributes.md)
   - 用於擴展應用程式報告的 SQL 深入解析 {#sql-insights}
      - [概觀](data-distiller/sql-insights/overview.md)
      - [查詢專業模式](data-distiller/sql-insights/query-pro-mode.md)
      - [Accelerated Store概述](data-distiller/sql-insights/accelerated-store-overview.md)
      - [傳送加速的查詢](data-distiller/sql-insights/send-accelerated-queries.md)
      - [報表深入分析資料模型指南](data-distiller/sql-insights/reporting-insights-data-model.md)
   - AI/ML 功能管道 {#ml-feature-pipelines}
      - [概觀](data-distiller/ml-feature-pipelines/overview.md)
      - [連線到Jupyter Notebooks](data-distiller/ml-feature-pipelines/establish-connection.md)
      - [探索資料分析](data-distiller/ml-feature-pipelines/exploratory-analysis.md)
      - [ML的工程師功能](data-distiller/ml-feature-pipelines/feature-engineering.md)
      - [將資料匯出至ML環境](data-distiller/ml-feature-pipelines/export-data.md)
      - [AI/ML資料管道擴充端對端工作流程](data-distiller/ml-feature-pipelines/end-to-end-notebook-workflow.md)
   - [2025年高峰會會議](data-distiller/top-tips-to-maximize-value.md)
- 資料Distiller統計資料和機器學習 {#advanced-statistics}
   - [概觀](advanced-statistics/overview.md)
   - [功能工程](advanced-statistics/feature-engineering.md)
   - [模型](advanced-statistics/models.md)
   - [特徵轉換](advanced-statistics/feature-transformation.md)
   - 實作模型 {#implement-models}
      - [實作模型](advanced-statistics/implement-models/implement-models.md)
      - [迴歸](advanced-statistics/implement-models/regression.md)
      - [分類](advanced-statistics/implement-models/classification.md)
      - [叢集](advanced-statistics/implement-models/clustering.md)
   - 範例 {#examples}
      - [使用統計和機器學習進行機器人篩選](advanced-statistics/examples/statistics-and-ml-bot-filtering.md)
      - [使用SQL型Logistic回歸預測客戶流失](advanced-statistics/examples/predict-customer-churn.md)
- 資料Distiller受眾 {#data-distiller-audiences}
   - [使用SQL建置外部對象](data-distiller-audiences/overview.md)
- 範例 {#use-cases}
   - [概觀](use-cases/overview.md)
   - [捨棄的瀏覽](use-cases/abandoned-browse.md)
   - [歸因分析](use-cases/attribution-analysis.md)
   - [機器人篩選](use-cases/bot-filtering.md)
   - [使用統計和機器學習進行機器人篩選](use-cases/statistics-and-ml-bot-filtering-stub.md)
   - [建立事件的趨勢報表](use-cases/trended-report-of-events.md)
   - [同意分析](use-cases/consent-analysis.md)
   - [客戶期限值](use-cases/customer-lifetime-value.md)
   - [資料探索](./use-cases/data-exploration.md)
   - [基於十分位數的衍生資料集](use-cases/deciles-use-case.md)
   - [模糊比對](use-cases/fuzzy-match.md)
   - [列出使用者的頁面檢視](use-cases/list-visitor-sessions.md)
   - [依頁面檢視列出訪客](use-cases/visitors-by-number-of-page-views.md)
   - [使用SQL預測客戶流失](use-cases/predict-customer-churn-stub.md)
   - [傾向分數](use-cases/propensity-score.md)
   - [使用較高階函式擷取類似記錄](use-cases/retrieve-similar-records.md)
   - [從Analytics資料傳回並使用銷售變數](use-cases/merchandising-variables.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [檢視訪客的統計報表](use-cases/roll-up-report-of-a-visitor.md)
   - [網站和行動分析深入分析](use-cases/analytics-insights.md)
- 重要概念 {#key-concepts}
   - [使用巢狀資料結構](key-concepts/nested-data-structures.md)
   - [平面化巢狀資料結構](key-concepts/flatten-nested-data.md)
   - [匿名區塊](key-concepts/anonymous-block.md)
   - [內嵌範本](key-concepts/inline-templates.md)
   - [增量載入](key-concepts/incremental-load.md)
   - [重複資料刪除](key-concepts/deduplication.md)
   - [資料集範例](key-concepts/dataset-samples.md)
   - [資料集統計資料計算](key-concepts/dataset-statistics.md)
- 資料Distiller超立方體 {#hypercubes}
   - [使用超多維度資料集進行高效率的大資料分析](hypercubes/overview.md)
- 將用戶端連線至查詢服務 {#clients}
   - [使用者端連線概觀](clients/overview.md)
   - [SSL模式](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
   - [GitHub Copilot](./clients/github-copilot.md)
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
   - [將JWT移轉至OAuth認證](ui/migrate-jwt-to-oauth.md)
   - [從查詢結果產生輸出資料集](ui/create-datasets.md)
- 查詢服務API {#api}
   - [快速入門](api/getting-started.md)
   - [查詢](api/queries.md)
   - [連線參數](api/connection-parameters.md)
   - [排程](api/scheduled-queries.md)
   - [已排程查詢的執行](api/runs-scheduled-queries.md)
   - [查詢範本](api/query-templates.md)
   - [加速的查詢](api/accelerated-queries.md)
   - [警報訂閱](api/alert-subscriptions.md)
- 資料Distiller授權API {#auth-api}
   - [概觀](auth-api/overview.md)
   - [快速入門](auth-api/getting-started.md)
   - [IP存取](auth-api/ip-access.md)
   - [驗證](auth-api/validate.md)
- 資料治理 {#data-governance}
   - [概觀](data-governance/overview.md)
   - [稽核記錄指南](data-governance/audit-log-guide.md)
   - [臨時結構描述資料集中的身分](data-governance/ad-hoc-schema-identities.md)
   - [針對臨時結構描述的屬性型存取控制支援](./data-governance/ad-hoc-schema-labels.md)
- 最佳作法 {#best-practices}
   - [查詢執行](best-practices/writing-queries.md)
   - [資料資產組織](./best-practices/organize-data-assets.md)
- SQL 參照 {#sql}
   - [SQL概述](sql/overview.md)
   - [SQL語法](sql/syntax.md)
   - [Adobe定義的函式](sql/adobe-defined-functions.md)
   - [高階函式](sql/higher-order-functions.md)
   - [Spark SQL函式](sql/spark-sql-functions.md)
   - [中繼資料命令](sql/metadata.md)
   - [準備的陳述式](sql/prepared-statements.md)
- [常見問題](troubleshooting-guide.md)
- [IP位址允許清單](ip-address-allowlist.md)
- [API 參考資料](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Experience Platform 發行說明](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/release-notes/latest)
