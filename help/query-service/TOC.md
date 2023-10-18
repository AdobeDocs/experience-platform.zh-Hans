---
audience: user
user-guide-title: Adobe Experience Platform 查询服务帮助
breadcrumb-title: 查询服务指南
user-guide-description: 在 Experience Platform 中使用标准 SQL 查询数据湖中的数据。
feature: Queries
source-git-commit: 6c3c5e3a87773f9f58a5d61bd4bef19f4cdc2e96
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 18%

---


# Adobe Experience Platform查询服务 {#query}

- [查询服务概述](home.md)
- [查询服务打包](packages.md)
- [查询服务护栏](guardrails.md)
- 入门 {#get-started}
   - [先决条件](get-started/prerequisites.md)
- 数据Distiller {#data-distiller}
   - [概述](data-distiller/overview.md)
   - [许可证使用](data-distiller/license-usage.md)
   - 查询加速存储 {#query-accelerated-store}
      - [发送加速查询](data-distiller/query-accelerated-store/send-accelerated-queries.md)
      - [报表见解数据模型指南](data-distiller/query-accelerated-store/reporting-insights-data-model.md)
   - 派生属性 {#derived-attributes}
      - [概述](data-distiller/derived-attributes/overview.md)
      - [无缝SQL流](data-distiller/derived-attributes/seamless-sql-flow.md)
      - [创建基于十分位数的派生属性](data-distiller/derived-attributes/decile-based-derived-attributes.md)
   - AI/ML功能管道 {#ml-feature-pipelines}
      - [AI/ML功能管道](data-distiller/ml-feature-pipelines/overview.md)
      - [连接到Jupyter Notebooks](data-distiller/ml-feature-pipelines/establish-connection.md)
      - [探索性数据分析](data-distiller/ml-feature-pipelines/exploratory-analysis.md)
      - [ML的工程师功能](data-distiller/ml-feature-pipelines/feature-engineering.md)
      - [将数据导出到ML环境](data-distiller/ml-feature-pipelines/export-data.md)
      - [AI/ML数据管道扩充端到端工作流](data-distiller/ml-feature-pipelines/end-to-end-notebook-workflow.md)
- 用例 {#use-cases}
   - [已放弃的浏览](use-cases/abandoned-browse.md)
   - [归因分析](use-cases/attribution-analysis.md)
   - [机器人筛选](use-cases/bot-filtering.md)
   - [创建事件的趋势报表](use-cases/trended-report-of-events.md)
   - [同意分析](use-cases/consent-analysis.md)
   - [客户存留期值](use-cases/customer-lifetime-value.md)
   - [基于十分位数的派生属性](use-cases/deciles-use-case.md)
   - [模糊匹配](use-cases/fuzzy-match.md)
   - [列出用户的页面查看次数](use-cases/list-visitor-sessions.md)
   - [按访客的页面查看次数列出访客](use-cases/visitors-by-number-of-page-views.md)
   - [倾向分数](use-cases/propensity-score.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [从Analytics数据返回和使用促销变量](use-cases/merchandising-variables.md)
   - [查看访客的汇总报表](use-cases/roll-up-report-of-a-visitor.md)
   - [网站和移动分析洞察](use-cases/analytics-insights.md)
- 将客户端连接到查询服务 {#clients}
   - [客户端连接概述](clients/overview.md)
   - [SSL模式](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
   - [Jupyter Notebook](clients//jupyter-notebook.md)
   - [Looker](clients/looker.md)
   - [postico](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RStudio](clients/rstudio.md)
   - [Tableau](clients/tableau.md)
- 查询服务UI {#ui}
   - [UI概述](ui/overview.md)
   - [查询编辑器用户指南](ui/user-guide.md)
   - [查询模板](ui/query-templates.md)
   - [参数化查询（受限）](ui/parameterized-queries.md)
   - [查询计划](ui/query-schedules.md)
   - [查询日志](ui/query-logs.md)
   - [监测计划查询](ui/monitor-queries.md)
   - [凭据指南](ui/credentials.md)
   - [从查询结果生成输出数据集](ui/create-datasets.md)
- 查询服务API端点 {#api}
   - [快速入门](api/getting-started.md)
   - [查询](api/queries.md)
   - [连接参数](api/connection-parameters.md)
   - [时间表](api/scheduled-queries.md)
   - [针对计划的查询运行](api/runs-scheduled-queries.md)
   - [查询模板](api/query-templates.md)
   - [加速查询](api/accelerated-queries.md)
   - [警报订阅](api/alert-subscriptions.md)
- 数据治理 {#data-governance}
   - [概述](data-governance/overview.md)
   - [审核日志指南](data-governance/audit-log-guide.md)
   - [临时架构数据集中的身份](data-governance/ad-hoc-schema-identities.md)
   - [对临时架构的基于属性的访问控制支持](./data-governance/ad-hoc-schema-labels.md)
- 最佳实践 {#best-practices}
   - [查询执行](best-practices/writing-queries.md)
   - [数据资产组织](./best-practices/organize-data-assets.md)
- 基本概念 {#essential-concepts}
   - [使用嵌套数据结构](essential-concepts/nested-data-structures.md)
   - [拼合嵌套数据结构](essential-concepts/flatten-nested-data.md)
   - [匿名块](essential-concepts/anonymous-block.md)
   - [内联模板](essential-concepts/inline-templates.md)
   - [增量加载](essential-concepts/incremental-load.md)
   - [重复数据删除](essential-concepts/deduplication.md)
   - [数据集样本](essential-concepts/dataset-samples.md)
   - [数据集统计信息计算](essential-concepts/dataset-statistics.md)
- SQL引用 {#sql}
   - [SQL概述](sql/overview.md)
   - [SQL语法](sql/syntax.md)
   - [Adobe定义的函数](sql/adobe-defined-functions.md)
   - [Spark SQL函数](sql/spark-sql-functions.md)
   - [元数据命令](sql/metadata.md)
   - [准备的语句](sql/prepared-statements.md)
- [常见问题解答](troubleshooting-guide.md)
- [API 参考](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Platform发行说明](https://www.adobe.com/go/platform-release-notes_cn)
