---
title: Adobe Experience Platform 发行说明（2024 年 9 月）
description: Adobe Experience Platform 2024 年 9 月发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 059ed53ace6d54a0c0fb406c2f0379588fea2c44
workflow-type: tm+mt
source-wordcount: '2149'
ht-degree: 84%

---

# Adobe Experience Platform 发行说明

**发行日期：2024 年 9 月 24 日**

Adobe Experience Platform 中现有功能和文档的更新：

- [Adobe Experience Platform 发行说明](#adobe-experience-platform-release-notes)
   - [警报 {#alerts}](#alerts-alerts)
   - [仪表板{#dashboards}](#dashboards-dashboards)
   - [数据准备{#data-prep}](#data-prep-data-prep)
   - [目标 {#destinations}](#destinations-destinations)
   - [体验数据模型(XDM) {#xdm}](#experience-data-model-xdm-xdm)
   - [标识服务{#identity-service}](#identity-service-identity-service)
   - [查询服务{#query-service}](#query-service-query-service)
   - [分段服务{#segmentation-service}](#segmentation-service-segmentation-service)
   - [源 {#sources}](#sources-sources)

## 警报 {#alerts}

Experience Platform 允许您订阅各种平台活动的基于事件的警报。您可以通过平台用户界面中的 [!UICONTROL 警报] 选项卡订阅不同的警报规则，并可以选择在用户界面内或通过电子邮件通知接收警报消息。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 开发沙盒支持 | 您现在可以在生产和开发沙盒中 [订阅警报](../../observability/alerts/ui.md) ，从而实现在所有环境中的无缝监控。 |
| 电子邮件模板 | [电子邮件提醒](../../observability/alerts/ui.md) 现在包含详细的资产信息，确保您随时掌握所有关键详细信息。 |
| 增强定制 | 您现在可以配置 [警报阈值](../../observability/alerts/ui.md#alert-threshold) ，从而提供更大的灵活性，根据您的特定需求定制以下警报类型的警报：<br><ul><li>区段作业延迟</li><li>区段导出延迟</li><li>目标流量运行延迟</li><li>标识服务流量运行延迟</li><li>轮廓流量运行延迟</li><li>源流量运行延迟</li><li>查询运行延迟</li><li>激活跳过率超出范围</li><li>源引入错误率超出范围</ul> |
| 扩展警报 | 现可订阅以下 [警报规则](../../observability/alerts/rules.md)的审核事件信息警报：<br><ul><li>受众创建</li><li>受众更新</li><li>受众删除</li><li>数据集创建</li><li>数据集更新</li><li>数据集删除</li><li>架构创建</li><li>架构更新</li><li>架构删除 |

{style="table-layout:auto"}

有关警报的更多信息，请阅读[[!DNL Observability Insights] 概述](../../observability/home.md)。

## 仪表板 {#dashboards}

Experience Platform 提供了多个仪表板，您可以通过这些仪表板查看在每日快照中摄取的有关您组织数据的重要洞察。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| “许可证使用情况”插件表 | 通过核心产品和加载项的专用表格精细地了解许可证使用情况，并管理您的平台资源。 在沙盒级别使用穿透钻取视图跟踪和分析每个核心产品的关键量度。 附加量度与核心产品量度无缝集成，提供了使用情况的全面视图。 增强的可见性可帮助您优化许可证管理，并使资源与组织需求相匹配。 有关详细信息，请参阅[[!UICONTROL 许可证使用情况]仪表板指南](../../dashboards/guides/license-usage.md#overview-tab)。 |
| Query Pro Mode - 全局过滤器升级 | 使用 Query Pro Mode 的新日期过滤器增强分析。使用 SQL 查询中的动态日期参数来细化洞察，并按特定时间范围过滤数据。通过直观的用户界面选择预设或自定义日期范围，确保仪表板与所有用户的相关性。简化工作流程、保持精确度并及时做出决策。请阅读 [创建日期过滤器的指南](../../dashboards/data-distiller/query-pro-mode/filters/global-filter.md)，了解更多信息。 |
| Query Pro Mode - 深入钻取 | 使用 Query Pro Mode 的深入探究功能解锁更深入的洞察，并无缝地从高级图表导航到详细的仪表板。使用此功能可以轻松地从摘要转向深入分析，并探索趋势、客户行为和 KPI。自动过滤器传递和多级钻取保持数据一致，确保顺利探索。简化工作流程、保留背景并加快决策。请阅读 [有关创建钻取的分步指南](../../dashboards/data-distiller/query-pro-mode/drill-through.md) 以了解更多信息。 |
| Query Pro Mode - 高级表属性 | 使用 Query Pro Mode 高级表属性来简化数据可视化、增强工作流效率并提高数据清晰度。直接从自定义仪表板向表格添加自动排序、调整大小和分页功能。对列进行排序以确定关键数据的优先级、调整大小以获得最佳可读性，并无缝浏览大型数据集而无需修改 SQL 查询。请阅读“[查看更多](../../dashboards/data-distiller/query-pro-mode/view-more.md)”指南，了解如何集成这些功能并提升您的数据洞察力。 |
| 总数据量 | “平均配置文件丰富度”量度已替换为“总数据量”量度。 总数据量是指可用于实时客户档案以进行参与和个性化工作流的可用数据总量。 有关此更改的详细信息，请参阅[总数据卷指南](../../landing/license-usage-and-guardrails/total-data-volume.md)。 |

{style="table-layout:auto"}

有关仪表板的详细信息，包括如何授予访问权限和创建自定义构件，请首先阅读[仪表板概述](../../dashboards/home.md)。

## 数据准备 {#data-prep}

使用数据准备从 Experience Data Model (XDM) 映射数据并将数据映射到它、转换和验证数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| [!BADGE Beta]{type=Informative} 可用于目标的新数据准备功能 | 现在，您可以将以下数组函数用于目标用例：<ul><li>`array_to_string`</li><li>`filterArray`</li><li>`transformArray`</li><li>`flattenArray`</li></ul> 有关详细信息，请阅读[数据准备函数指南](../../data-prep/functions.md#arrays)。 |

{style="table-layout:auto"}

有关数据准备的详细信息，请参阅[数据准备概述](../../data-prep/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增或更新目标**{#new-updated-destinations}

| 目标 | 描述 |
| --- | --- |
| [Amazon 广告](/help/destinations/catalog/advertising/amazon-ads.md) | 2024 年 9 月的版本添加了将 `countryCode` 参数导出到 Amazon Ads 的映射选项。`countryCode` 在 [映射步骤](/help/destinations/catalog/advertising/amazon-ads.md#map) 中使用，以提高您与亚马逊的标识匹配率。 |

{style="table-layout:auto"}

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| --- | --- |
| [数据集导出](/help/destinations/ui/export-datasets.md) 增强功能 | Experience Platform 2024 年 9 月发布的版本对数据集导出功能进行了多项增强，以更好地支持各种数据传出用例。这些功能增强包括： <ul><li>新的数据文件夹可配置选项，包括添加和删除子文件夹的选项。</li><li>新的导出选项包括完整文件导出（一次）以及指定结束日期的功能</li><li>注意：Adobe 还为 9 月版本之前创建的所有数据集导出数据流引入了 2025 年 5 月 1 日的默认结束日期。对于任何这些数据流，客户都需要在结束日期之前手动更新数据流中的结束日期，否则导出将在此日期停止。</li></ul> <br> ![Experience Platform 用户界面图像突出显示了计划步骤中的编辑计划和文件夹选项。](../2024/assets/september/edit-schedule-folders.png "在计划步骤中编辑计划和文件夹选项。"){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

有关更多信息，请阅读[目标概述](../../destinations/home.md)。

## Experience Data Model (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Adobe Experience Platform 的数据提供通用结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| Schema Editor 的增强功能 | 使用 Schema Editor 中更新的关系工作流来控制您的模式关系。直接从 Experience Platform UI 轻松更新或删除现有关系，使模式管理更顺畅、更直观。调整参考模式并自信地重命名关系，确保跨分段和其他关键流程的无缝数据完整性。要了解有关有效管理模式关系的更多信息，请参阅有关 [在 UI 中定义关系字段](../../xdm/tutorials/relationship-ui.md#create-a-relationship-field-group) 和 [B2B 关系](../../xdm/tutorials/relationship-b2b.md#edit-a-b2b-schema-relationship)的指南。 |

{style="table-layout:auto"}

有关 XDM 更多信息，请阅读[XDM 系统概述](../../xdm/home.md)。

## 标识服务 {#identity-service}

使用 Adobe Experience Platform 标识服务通过跨设备和系统桥接标识，全面了解您的客户及其行为，助您实时提供有影响力的个人数字体验。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 标识图链接规则的可用性有限 | 身份图链接规则是Identity Service中的一套工具，可使用它们确保用户的准确个性化。 <ul><li>您现在可以使用[身份优化算法](../../identity-service/identity-graph-linking-rules/identity-optimization-algorithm.md)来确保身份图代表单个人员，从而防止在实时客户个人资料上不必要地合并身份。</li><li>配置[命名空间优先级](../../identity-service/identity-graph-linking-rules/namespace-priority.md)以定义各自命名空间的重要性并影响配置文件的形成和分段方式。</li><li>在UI](../../identity-service/identity-graph-linking-rules/graph-simulation.md)中使用[图形模拟工具来模拟具有不同配置的身份图形。</li><li>使用[身份设置界面](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md)指定您的唯一命名空间并为组织中的所有命名空间建立优先级。</li><li>有关图形数据的量度和趋势，请参阅[身份仪表板](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs)。</li></ul> 要尝试使用身份图关联规则，请联系您的Adobe客户团队以获取开发沙盒的访问权限。 |

**文档更新**

| 功能 | 描述 |
| --- | --- |
| 标识图链接规则故障排除指南 | 阅读新的 [标识图链接规则故障排除指南](../../identity-service/identity-graph-linking-rules/troubleshooting.md)，了解您可以采取的方法和调试解决方案，以解决使用标识图链接规则时可能遇到的常见问题。 |
| 标识图链接规则常见问题解答 | 阅读新的 [标识图链接规则常见问题解答](../../identity-service/identity-graph-linking-rules/troubleshooting.md#frequently-asked-questions)，获取有关命名空间优先级、标识优化算法和标识图链接规则其他方面的常见问题的解答列表。 |

{style="table-layout:auto"}

有关标识服务的更多信息，请参阅[标识服务概述](../../identity-service/home.md)。

## 查询服务 {#query-service}

查询服务允许您使用标准 SQL 查询 Adobe Experience Platform [!DNL data lake] 中的数据。您可以加入数据湖的任何数据集，并作为新数据集获取查询结果，以用于报表、Data Science Workspace，或将数据摄取到实时客户配置文件。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| Data Distiller 受众 | 使用 Experience Platform 的 Data Distiller 中的 SQL 受众扩展轻松创建、管理和激活受众。直接从数据湖中使用 SQL 命令定义受众群体，无需在配置文件中使用原始数据。通过这种灵活的数据驱动方法，优化定位策略并自动将受众同步到基于文件的目的地。简化工作流程，优化受众管理并充分发挥数据的潜力。阅读 [有关使用 SQL 受众扩展的指南](../../query-service/data-distiller-audiences/overview.md) 来提升您的受众策略。 |
| Data Distiller Statistics - 超立方体 | 使用超立方体优化大数据分析。处理复杂的计算（例如不同计数和多维分析），无需重新处理历史数据。逐步更新数据，简化工作流程并缩短处理时间，同时保持准确性和效率。获得更快、可扩展且经济高效的洞察力，从而改变决策。探索 [超立方体使用指南](../../query-service/hypercubes/overview.md)，解锁高级分析。 |
| Query Editor Object 浏览器 | 使用查询编辑器中的新对象浏览器提高查询效率。快速搜索、过滤和访问数据集以更快地编写和优化查询。通过实时模式更新和即时表元数据，您可以简化工作流程、缩短导航时间并增强查询体验。释放数据潜力并优化分析。若要了解更多信息，请阅读有关[使用对象浏览器](../../query-service/ui/user-guide.md#object-browser)的指南。 |
| 计算小时数 | 使用新显示的计划查询的计算小时数指标来控制资源使用情况。在查询执行级别查看计算小时数，以监控和优化 CTAS/ITAS 批量查询的资源使用情况。跟踪每次查询运行的开始时间、完成状态和计算时间。轻松微调性能并降低成本。阅读 [计算小时数指南](../../query-service/ui/query-schedules.md#compute-hours-at-job-level) 了解有关如何最大限度提高查询效率的信息。 |

{style="table-layout:auto"}

要详细了解查询服务，请阅读[查询服务概述](../../query-service/home.md)。

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的配置文件子集。区段可以基于记录数据（例如人口统计信息）或代表客户与您的品牌互动的时间序列事件。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 流式分段标准更新 | 从2024年9月版开始，更新了受众有资格进行流式客户细分的标准。 有关这些更改的详细信息，请参阅[流式分段资格标准更新](../../segmentation/eligibility-criteria-update.md)。 |
| 统一搜索实施 | Segment Builder 中的搜索行为现在将使用统一搜索。这样，在管理和搜索可供重复用于细分成员身份的受众时，可以获得更强大的体验。有关此更改的更多信息，请阅读[区段生成器指南](../../segmentation/ui/segment-builder.md#rule-builder-canvas)。 |

{style="table-layout:auto"}

有关 [!DNL Segmentation Service] 的更多信息，请参阅[分段概述](../../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

使用 Experience Platform 中的源从 Adobe 应用程序或第三方数据源引入数据。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| [!BADGE Beta]{type=Informative} 支持在 UI 中导入加密数据 | 您现在可以使用 Experience Platform 用户界面中的源工作区从云存储批处理源中提取加密数据。请阅读教程 [在 UI 中提取加密数据](../../sources/tutorials/ui/encryped-ingestion.md)，了解更多信息。 |
| [!DNL Snowflake Streaming]源的正式可用性 | [!DNL Snowflake Streaming] 源现在处于 GA。 使用此源将数据从您的[!DNL Snowflake]帐户流式传输到到 Experience Platform。请参阅 [[!DNL Snowflake Streaming] 概述](../../sources/connectors/databases/snowflake-streaming.md)，了解更多信息。 |
| 支持服务帐户身份验证 [!DNL Google BigQuery] | 现在您可以连接您的 [!DNL Google BigQuery] 使用服务帐户身份验证将帐户添加到 Experience Platform。有关详细信息，请参阅 [[!DNL Google BigQuery] 概述](../../sources/connectors/databases/bigquery.md#generate-your-google-bigquery-credentials)。<br> ![Experience Platform 用户界面图像突出显示了计划步骤中的编辑计划和文件夹选项。](../2024/assets/september/service_auth.png "Google BigQuery 的服务身份验证。"){width="250" align="center" zoomable="yes"} |
| 支持跳过示例数据预览 | 现在，您可以选择在与以下源创建源连接时跳过数据预览： <ul><li>[[!DNL Google BigQuery]](../../sources/tutorials/ui/create/databases/bigquery.md#skip-preview-of-sample-data)</li><li>[[!DNL Salesforce]](../../sources/tutorials/ui/create/crm/salesforce.md#skip-preview-of-sample-data)</li><li>[[!DNL Snowflake]](../../sources/tutorials/ui/create/databases/snowflake.md#skip-preview-of-sample-data)</li></ul> 您可以跳过数据预览以避免在提取大批量数据时可能出现的超时。这样做可能会阻止计算字段和必填字段的自动验证。如果您选择跳过数据预览，那么您可能必须在映射期间手动验证计算字段和必填字段。 |
| 支持在[!DNL SFTP]中禁用分块 | 您现在可以配置一个设置，允许您禁用 [!DNL SFTP] 来源。请参阅 [[!DNL SFTP]  概述](../../sources/connectors/cloud-storage/sftp.md)，了解更多信息。 |

{style="table-layout:auto"}

有关更多信息，请阅读[源概述](../../sources/home.md)。
