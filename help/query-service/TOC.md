---
audience: user
user-guide-title: Adobe Experience Platform 查询服务帮助
breadcrumb-title: 查询服务指南
user-guide-description: 在 Experience Platform 中使用标准 SQL 查询数据湖中的数据。
feature: Queries
role: User,Developer
source-git-commit: 8b33d9231aeebd454fd614a81b356a9e971b757c
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 26%

---


# Adobe Experience Platform查询服务 {#query}

- [查询服务概述](home.md)
- [查询服务打包](packaging.md)
- [查询服务护栏](guardrails.md)
- 开始使用 {#get-started}
   - [先决条件](get-started/prerequisites.md)
- 数据蒸馏器 {#data-distiller}
   - [概述](data-distiller/overview.md)
   - [许可证使用](data-distiller/license-usage.md)
   - 派生数据集 {#derived-datasets}
      - [概述](data-distiller/derived-datasets/overview.md)
      - [使用SQL创建派生数据集](data-distiller/derived-datasets/create-derived-datasets-with-sql.md)
      - [创建基于十分位数的派生数据集](data-distiller/derived-datasets/decile-based-derived-attributes.md)
   - 用于扩展应用报告的 SQL Insights {#sql-insights}
      - [概述](data-distiller/sql-insights/overview.md)
      - [查询专业模式](data-distiller/sql-insights/query-pro-mode.md)
      - [Accelerated Store概述](data-distiller/sql-insights/accelerated-store-overview.md)
      - [发送加速查询](data-distiller/sql-insights/send-accelerated-queries.md)
      - [报表见解数据模型指南](data-distiller/sql-insights/reporting-insights-data-model.md)
   - AI/ML 功能管道 {#ml-feature-pipelines}
      - [概述](data-distiller/ml-feature-pipelines/overview.md)
      - [连接到Jupyter Notebooks](data-distiller/ml-feature-pipelines/establish-connection.md)
      - [探索性数据分析](data-distiller/ml-feature-pipelines/exploratory-analysis.md)
      - [ML的工程师功能](data-distiller/ml-feature-pipelines/feature-engineering.md)
      - [将数据导出到ML环境](data-distiller/ml-feature-pipelines/export-data.md)
      - [AI/ML数据管道扩充端到端工作流](data-distiller/ml-feature-pipelines/end-to-end-notebook-workflow.md)
   - [Summit 2025会议](data-distiller/top-tips-to-maximize-value.md)
- 数据Distiller统计和机器学习 {#advanced-statistics}
   - [概述](advanced-statistics/overview.md)
   - [特征工程](advanced-statistics/feature-engineering.md)
   - [模型](advanced-statistics/models.md)
   - [特征转换](advanced-statistics/feature-transformation.md)
   - 实施模型 {#implement-models}
      - [实施模型](advanced-statistics/implement-models/implement-models.md)
      - [回归](advanced-statistics/implement-models/regression.md)
      - [分类](advanced-statistics/implement-models/classification.md)
      - [聚类](advanced-statistics/implement-models/clustering.md)
   - 示例 {#examples}
      - [使用统计和机器学习进行机器人过滤](advanced-statistics/examples/statistics-and-ml-bot-filtering.md)
      - [使用基于SQL的Logistic回归预测客户流失](advanced-statistics/examples/predict-customer-churn.md)
- 数据Distiller受众 {#data-distiller-audiences}
   - [使用SQL构建外部受众](data-distiller-audiences/overview.md)
- 示例 {#use-cases}
   - [概述](use-cases/overview.md)
   - [已放弃的浏览](use-cases/abandoned-browse.md)
   - [归因分析](use-cases/attribution-analysis.md)
   - [机器人过滤](use-cases/bot-filtering.md)
   - [使用统计和机器学习介绍的机器人过滤](use-cases/statistics-and-ml-bot-filtering-stub.md)
   - [创建事件的趋势报表](use-cases/trended-report-of-events.md)
   - [同意分析](use-cases/consent-analysis.md)
   - [客户存留期值](use-cases/customer-lifetime-value.md)
   - [数据探索](./use-cases/data-exploration.md)
   - [基于十分位的派生数据集](use-cases/deciles-use-case.md)
   - [模糊匹配](use-cases/fuzzy-match.md)
   - [列出用户的页面查看次数](use-cases/list-visitor-sessions.md)
   - [按访客的页面查看次数列出访客](use-cases/visitors-by-number-of-page-views.md)
   - [使用SQL预测客户流失](use-cases/predict-customer-churn-stub.md)
   - [倾向性得分](use-cases/propensity-score.md)
   - [使用高阶函数检索类似记录](use-cases/retrieve-similar-records.md)
   - [从Analytics数据返回和使用促销变量](use-cases/merchandising-variables.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [查看访客的汇总报表](use-cases/roll-up-report-of-a-visitor.md)
   - [网站和移动分析洞察](use-cases/analytics-insights.md)
- 重要概念 {#key-concepts}
   - [使用嵌套数据结构](key-concepts/nested-data-structures.md)
   - [拼合嵌套数据结构](key-concepts/flatten-nested-data.md)
   - [匿名块](key-concepts/anonymous-block.md)
   - [内联模板](key-concepts/inline-templates.md)
   - [增量加载](key-concepts/incremental-load.md)
   - [重复数据删除](key-concepts/deduplication.md)
   - [数据集样本](key-concepts/dataset-samples.md)
   - [数据集统计信息计算](key-concepts/dataset-statistics.md)
- 数据Distiller超多维数据集 {#hypercubes}
   - [使用超多维数据集进行高效的大数据分析](hypercubes/overview.md)
- 将客户端连接到查询服务 {#clients}
   - [客户端连接概述](clients/overview.md)
   - [SSL模式](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
   - [GitHub Copilot](./clients/github-copilot.md)
   - [Jupyter Notebook](clients//jupyter-notebook.md)
   - [Looker](clients/looker.md)
   - [postico](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RStudio](clients/rstudio.md)
   - [表格](clients/tableau.md)
- 查询服务UI {#ui}
   - [UI概述](ui/overview.md)
   - [查询编辑器用户指南](ui/user-guide.md)
   - [查询模板](ui/query-templates.md)
   - [参数化查询](ui/parameterized-queries.md)
   - [查询计划](ui/query-schedules.md)
   - [查询日志](ui/query-logs.md)
   - [监测计划查询](ui/monitor-queries.md)
   - [凭据指南](ui/credentials.md)
   - [将JWT迁移到OAuth凭据](ui/migrate-jwt-to-oauth.md)
   - [从查询结果生成输出数据集](ui/create-datasets.md)
- 查询服务API {#api}
   - [快速入门](api/getting-started.md)
   - [查询](api/queries.md)
   - [连接参数](api/connection-parameters.md)
   - [计划](api/scheduled-queries.md)
   - [针对计划的查询运行](api/runs-scheduled-queries.md)
   - [查询模板](api/query-templates.md)
   - [加速查询](api/accelerated-queries.md)
   - [警报订阅](api/alert-subscriptions.md)
- 数据Distiller授权API {#auth-api}
   - [概述](auth-api/overview.md)
   - [快速入门](auth-api/getting-started.md)
   - [IP访问](auth-api/ip-access.md)
   - [验证](auth-api/validate.md)
- 数据治理 {#data-governance}
   - [概述](data-governance/overview.md)
   - [审核日志指南](data-governance/audit-log-guide.md)
   - [临时架构数据集中的身份](data-governance/ad-hoc-schema-identities.md)
   - [对临时架构的基于属性的访问控制支持](./data-governance/ad-hoc-schema-labels.md)
- 最佳实践 {#best-practices}
   - [查询执行](best-practices/writing-queries.md)
   - [数据资产组织](./best-practices/organize-data-assets.md)
- SQL 参考 {#sql}
   - [SQL概述](sql/overview.md)
   - [SQL语法](sql/syntax.md)
   - [Adobe定义的函数](sql/adobe-defined-functions.md)
   - [高阶函数](sql/higher-order-functions.md)
   - [Spark SQL函数](sql/spark-sql-functions.md)
   - [元数据命令](sql/metadata.md)
   - [准备的语句](sql/prepared-statements.md)
- [常见问题解答](troubleshooting-guide.md)
- [IP地址允许列表](ip-address-allowlist.md)
- [API 参考](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Experience Platform 发行说明](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/release-notes/latest)
