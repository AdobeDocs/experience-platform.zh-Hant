---
audience: user
user-guide-title: Adobe Experience Platform 查詢服務說明
breadcrumb-title: 查詢服務指南
user-guide-description: 使用標準 SQL 在 Experience Platform 的 Data Lake 中查詢資料。
feature: Queries
source-git-commit: adf8da46d09c60b86df16493043efeacbdd24fe2
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 18%

---


# Adobe Experience Platform查詢服務 {#query}

- [查詢服務概述](home.md)
- [查詢服務打包](packages.md)
- [查詢服務護欄](guardrails.md)
- 開始使用 {#get-started}
   - [先決條件](get-started/prerequisites.md)
- 資料Distiller {#data-distiller}
   - [總覽](data-distiller/overview.md)
   - [授權使用情況](data-distiller/license-usage.md)
   - 查詢加速儲存 {#query-accelerated-store}
      - [發送加速查詢](data-distiller/query-accelerated-store/send-accelerated-queries.md)
      - [《報告見解資料模型指南》](data-distiller/query-accelerated-store/reporting-insights-data-model.md)
   - 派生屬性 {#derived-attributes}
      - [總覽](data-distiller/derived-attributes/overview.md)
      - [無縫SQL流](data-distiller/derived-attributes/seamless-sql-flow.md)
      - [建立基於十位數的派生屬性](data-distiller/derived-attributes/decile-based-derived-attributes.md)
- 使用案例 {#use-cases}
   - [已放棄瀏覽](use-cases/abandoned-browse.md)
   - [歸因分析](use-cases/attribution-analysis.md)
   - [機器人過濾](use-cases/bot-filtering.md)
   - [建立事件趨勢報告](use-cases/trended-report-of-events.md)
   - [客戶生存期價值](use-cases/customer-lifetime-value.md)
   - [基於Decile的派生屬性](use-cases/deciles-use-case.md)
   - [模糊匹配](use-cases/fuzzy-match.md)
   - [列出用戶的頁面視圖](use-cases/list-visitor-sessions.md)
   - [按其頁面視圖列出訪問者](use-cases/visitors-by-number-of-page-views.md)
   - [傾向得分](use-cases/propensity-score.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [從分析資料返回和使用促銷變數](use-cases/merchandising-variables.md)
   - [查看訪問者的匯總報告](use-cases/roll-up-report-of-a-visitor.md)
   - [Web和移動分析洞見](use-cases/analytics-insights.md)
- 將客戶端連接到查詢服務 {#clients}
   - [客戶端連接概述](clients/overview.md)
   - [SSL模式](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [資料庫可視化器](./clients/dbvisulaizer.md)
   - [朱佩特筆記本](clients//jupyter-notebook.md)
   - [看](clients/looker.md)
   - [波斯蒂科](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RStudio](clients/rstudio.md)
   - [塔布洛](clients/tableau.md)
- 查詢服務UI {#ui}
   - [UI概述](ui/overview.md)
   - [查詢編輯器使用手冊](ui/user-guide.md)
   - [查詢模板](ui/query-templates.md)
   - [查詢計畫](ui/query-schedules.md)
   - [查詢日誌](ui/query-logs.md)
   - [監視計畫查詢](ui/monitor-queries.md)
   - [憑據指南](ui/credentials.md)
   - [從查詢結果生成輸出資料集](ui/create-datasets.md)
- 查詢服務API終結點 {#api}
   - [快速入門](api/getting-started.md)
   - [查詢](api/queries.md)
   - [連接參數](api/connection-parameters.md)
   - [計畫](api/scheduled-queries.md)
   - [運行計畫查詢](api/runs-scheduled-queries.md)
   - [查詢模板](api/query-templates.md)
   - [加速查詢](api/accelerated-queries.md)
   - [警報訂閱](api/alert-subscriptions.md)
- 資料治理 {#data-governance}
   - [總覽](data-governance/overview.md)
   - [審核日誌指南](data-governance/audit-log-guide.md)
   - [ad hoc模式資料集中的標識](data-governance/ad-hoc-schema-identities.md)
   - [基於屬性的訪問控制支援ad hoc模式](./data-governance/ad-hoc-schema-labels.md)
- 最佳做法 {#best-practices}
   - [查詢執行](best-practices/writing-queries.md)
   - [資料資產組織](./best-practices/organize-data-assets.md)
- 基本概念 {#essential-concepts}
   - [使用嵌套資料結構](essential-concepts/nested-data-structures.md)
   - [拼合嵌套資料結構](essential-concepts/flatten-nested-data.md)
   - [匿名塊](essential-concepts/anonymous-block.md)
   - [增量載入](essential-concepts/incremental-load.md)
   - [重複資料消除](essential-concepts/deduplication.md)
   - [資料集示例](essential-concepts/dataset-samples.md)
- SQL引用 {#sql}
   - [SQL概述](sql/overview.md)
   - [SQL語法](sql/syntax.md)
   - [Adobe定義函式](sql/adobe-defined-functions.md)
   - [Spark SQL函式](sql/spark-sql-functions.md)
   - [元資料命令](sql/metadata.md)
   - [準備的陳述](sql/prepared-statements.md)
- [常見問答](troubleshooting-guide.md)
- [API 參考資料](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [平台發行說明](https://www.adobe.com/go/platform-release-notes_tw)
