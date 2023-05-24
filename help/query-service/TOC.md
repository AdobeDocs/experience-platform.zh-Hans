---
audience: user
user-guide-title: Adobe Experience Platform 查询服务帮助
breadcrumb-title: 查询服务指南
user-guide-description: 在 Experience Platform 中使用标准 SQL 查询数据湖中的数据。
feature: Queries
source-git-commit: adf8da46d09c60b86df16493043efeacbdd24fe2
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 17%

---


# Adobe Experience Platform查詢服務 {#query}

- [查詢服務總覽](home.md)
- [查詢服務封裝](packages.md)
- [查詢服務護欄](guardrails.md)
- 入门 {#get-started}
   - [先决条件](get-started/prerequisites.md)
- 資料Distiller {#data-distiller}
   - [概述](data-distiller/overview.md)
   - [许可证使用](data-distiller/license-usage.md)
   - 查詢加速存放區 {#query-accelerated-store}
      - [傳送加速的查詢](data-distiller/query-accelerated-store/send-accelerated-queries.md)
      - [報表深入分析資料模型指南](data-distiller/query-accelerated-store/reporting-insights-data-model.md)
   - 衍生屬性 {#derived-attributes}
      - [概述](data-distiller/derived-attributes/overview.md)
      - [順暢的SQL流程](data-distiller/derived-attributes/seamless-sql-flow.md)
      - [建立十等分衍生屬性](data-distiller/derived-attributes/decile-based-derived-attributes.md)
- 用例 {#use-cases}
   - [捨棄的瀏覽](use-cases/abandoned-browse.md)
   - [歸因分析](use-cases/attribution-analysis.md)
   - [機器人篩選](use-cases/bot-filtering.md)
   - [建立事件的趨勢報表](use-cases/trended-report-of-events.md)
   - [客戶期限值](use-cases/customer-lifetime-value.md)
   - [十等分衍生屬性](use-cases/deciles-use-case.md)
   - [模糊比對](use-cases/fuzzy-match.md)
   - [列出使用者的頁面檢視](use-cases/list-visitor-sessions.md)
   - [依訪客的頁面檢視列出訪客](use-cases/visitors-by-number-of-page-views.md)
   - [傾向分數](use-cases/propensity-score.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [從Analytics資料傳回並使用銷售變數](use-cases/merchandising-variables.md)
   - [檢視訪客的統計報表](use-cases/roll-up-report-of-a-visitor.md)
   - [網頁和行動分析深入分析](use-cases/analytics-insights.md)
- 將使用者端連線至查詢服務 {#clients}
   - [使用者端連線概觀](clients/overview.md)
   - [SSL模式](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
   - [Jupyter Notebook](clients//jupyter-notebook.md)
   - [Looker](clients/looker.md)
   - [Postico](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RStudio](clients/rstudio.md)
   - [Tableau](clients/tableau.md)
- 查詢服務UI {#ui}
   - [UI總覽](ui/overview.md)
   - [查詢編輯器使用手冊](ui/user-guide.md)
   - [查詢範本](ui/query-templates.md)
   - [查詢排程](ui/query-schedules.md)
   - [查詢記錄](ui/query-logs.md)
   - [監視排定的查詢](ui/monitor-queries.md)
   - [認證指南](ui/credentials.md)
   - [從查詢結果產生輸出資料集](ui/create-datasets.md)
- 查詢服務API端點 {#api}
   - [快速入门](api/getting-started.md)
   - [查询](api/queries.md)
   - [連線引數](api/connection-parameters.md)
   - [時程表](api/scheduled-queries.md)
   - [針對排定的查詢執行](api/runs-scheduled-queries.md)
   - [查詢範本](api/query-templates.md)
   - [加速的查詢](api/accelerated-queries.md)
   - [警報訂閱](api/alert-subscriptions.md)
- 数据治理 {#data-governance}
   - [概述](data-governance/overview.md)
   - [稽核記錄指南](data-governance/audit-log-guide.md)
   - [臨時結構描述資料集中的身分](data-governance/ad-hoc-schema-identities.md)
   - [針對臨時結構描述的屬性型存取控制支援](./data-governance/ad-hoc-schema-labels.md)
- 最佳实践 {#best-practices}
   - [查詢執行](best-practices/writing-queries.md)
   - [資料資產組織](./best-practices/organize-data-assets.md)
- 基本概念 {#essential-concepts}
   - [使用巢狀資料結構](essential-concepts/nested-data-structures.md)
   - [平面化巢狀資料結構](essential-concepts/flatten-nested-data.md)
   - [匿名區塊](essential-concepts/anonymous-block.md)
   - [增量載入](essential-concepts/incremental-load.md)
   - [重複資料刪除](essential-concepts/deduplication.md)
   - [資料集範例](essential-concepts/dataset-samples.md)
- SQL參考 {#sql}
   - [SQL概述](sql/overview.md)
   - [SQL語法](sql/syntax.md)
   - [Adobe定義的函式](sql/adobe-defined-functions.md)
   - [Spark SQL函式](sql/spark-sql-functions.md)
   - [中繼資料命令](sql/metadata.md)
   - [準備的陳述式](sql/prepared-statements.md)
- [常见问题解答](troubleshooting-guide.md)
- [API參考](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Platform發行說明](https://www.adobe.com/go/platform-release-notes_cn)
