---
audience: user
user-guide-title: Adobe Experience Platform 查询服务帮助
breadcrumb-title: Query Service 指南
user-guide-description: 使用标准 SQL 在 Platform Data Lake 中查询数据。
feature: Queries
source-git-commit: df894d8b52aff3708aa06e73d4c5ba3e1e501f10
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 16%

---


# Adobe Experience Platform查询服务 {#query}

- [查询服务概述](home.md)
- [查询服务打包](packages.md)
- [查询服务护栏](guardrails.md)
- 数据Distiller {#data-distiller}
   - [许可证使用情况](data-distiller/licence-usage.md)
- 入门 {#get-started}
   - [先决条件](get-started/prerequisites.md)
- 使用案例{#use-cases}
   - [放弃浏览](use-cases/abandoned-browse.md)
   - [使用Adobe Target进行活动分析](use-cases/activity-analysis-with-adobe-target.md)
   - [归因分析](use-cases/attribution-analysis.md)
   - [机器人过滤](use-cases/bot-filtering.md)
   - [Web和移动分析分析](use-cases/analytics-insights.md)
- 查询服务API {#api}
   - [快速入门](api/getting-started.md)
   - [查询](api/queries.md)
   - [连接参数](api/connection-parameters.md)
   - [计划查询](api/scheduled-queries.md)
   - [针对计划查询运行](api/runs-scheduled-queries.md)
   - [查询模板](api/query-templates.md)
- 查询服务UI {#ui}
   - [UI概述](ui/overview.md)
   - [查询编辑器用户指南](ui/user-guide.md)
   - [查询模板](ui/query-templates.md)
   - [使用查询服务凭据](ui/credentials.md)
   - [从查询结果生成数据集](ui/create-datasets.md)
- 最佳实践 {#best-practices}
   - [查询执行的一般指导](best-practices/writing-queries.md)
   - [数据资产组织指南](./best-practices/organize-data-assets.md)
   - [使用嵌套数据结构](best-practices/nested-data-structures.md)
   - [扁平化嵌套数据结构](best-practices/flatten-nested-data.md)
   - [匿名块](best-practices/anonymous-block.md)
   - [增量加载](best-practices/incremental-load.md)
   - [重复数据删除](best-practices/deduplication.md)
- 派生属性 {#derived-attributes}
   - [概述](derived-attributes/overview.md)
   - [Deciles用例](derived-attributes/deciles-use-case.md)
- 示例查询 {#sample-queries}
   - [体验事件查询示例](sample-queries/experience-event.md)
   - [示例Adobe Analytics查询](sample-queries/adobe-analytics.md)
- SQL引用 {#sql}
   - [SQL概述](sql/overview.md)
   - [SQL语法](sql/syntax.md)
   - [Adobe定义的函数](sql/adobe-defined-functions.md)
   - [Spark SQL函数](sql/spark-sql-functions.md)
   - [元数据命令](sql/metadata.md)
   - [准备的陈述](sql/prepared-statements.md)
   - [数据集示例](sql/dataset-samples.md)
- 将客户端连接到查询服务 {#clients}
   - [客户端连接概述](clients/overview.md)
   - [SSL模式](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [数据库可视化工具](./clients/dbvisulaizer.md)
   - [朱佩特笔记本](clients//jupyter-notebook.md)
   - [Looker](clients/looker.md)
   - [波斯蒂科](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RStudio](clients/rstudio.md)
   - [塔布洛](clients/tableau.md)
- 数据管理 {#data-governance}
   - [概述](data-governance/overview.md)
   - [审核日志指南](data-governance/audit-log-guide.md)
   - [临时架构数据集中的身份](data-governance/ad-hoc-schema-identities.md)
   - [对临时架构的基于属性的访问控制支持](./data-governance/ad-hoc-schema-labels.md)
- [疑难解答指南](troubleshooting-guide.md)
- [API参考](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [平台发行说明](https://www.adobe.com/go/platform-release-notes-en)