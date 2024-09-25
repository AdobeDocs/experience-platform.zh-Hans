---
title: Adobe Experience Platform发行说明2024年9月
description: Adobe Experience Platform 2024年9月版发行说明。
source-git-commit: 1e9d16c53100c1ee930cf4bf5e9a9a5b6bd9c347
workflow-type: tm+mt
source-wordcount: '1975'
ht-degree: 27%

---

# Adobe Experience Platform 发行说明

**发行日期： 2024年9月24日**

Adobe Experience Platform现有功能和文档的更新：

- [警报](#alerts)
- [仪表板](#dashboards)
- [数据准备](#data-prep)
- [目标](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [身份服务](#identity-service)
- [查询服务](#query-service)
- [Segmentation Service](#segmentation-service)
- [源](#sources)

## 警报 {#alerts}

Experience Platform 允许您订阅各种平台活动的基于事件的警报。您可以通过平台用户界面中的 [!UICONTROL 警报] 选项卡订阅不同的警报规则，并可以选择在用户界面内或通过电子邮件通知接收警报消息。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 开发沙盒支持 | 您现在可以在生产沙盒和开发沙盒中[订阅警报](../../observability/alerts/ui.md)，从而实现所有环境的无缝监控。 |
| 电子邮件模板 | [电子邮件警报](../../observability/alerts/ui.md)现在包含详细的资产信息，确保您拥有所有关键详细信息且触手可及。 |
| 增强的自定义设置 | 您现在可以配置[警报阈值](../../observability/alerts/ui.md#alert-threshold)，以便根据您的特定需求为以下警报类型定制警报：<br><ul><li>区段作业延迟</li><li>区段导出延迟</li><li>目标流运行延迟</li><li>Identity服务流运行延迟</li><li>配置文件流运行延迟</li><li>源流量运行延迟</li><li>查询运行延迟</li><li>超出激活跳过率</li><li>超出源摄取错误率</ul> |
| 扩展的警报 | 审核事件信息警报现在可用于以下[警报规则](../../observability/alerts/rules.md)的订阅：<br><ul><li>受众创建</li><li>受众更新</li><li>受众删除</li><li>数据集创建</li><li>数据集更新</li><li>数据集删除</li><li>架构创建</li><li>架构更新</li><li>架构删除。 |

{style="table-layout:auto"}

有关警报的详细信息，请阅读[[!DNL Observability Insights] 概述](../../observability/home.md)。

## 仪表板 {#dashboards}

Experience Platform提供了多个功能板，通过该功能板可查看有关贵组织数据的重要见解，如在每日快照期间捕获的数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| Query Pro模式 — 全局过滤器升级 | 使用Query Pro模式的新日期过滤器增强分析。 使用SQL查询中的动态日期参数优化洞察，并按特定时间范围过滤数据。 通过直观的UI选择预设或自定义日期范围，使功能板与所有用户保持关联。 简化工作流、保持精确度并及时做出决策。 有关详细信息，请阅读有关创建日期过滤器](../../dashboards/data-distiller/query-pro-mode/filters/global-filter.md)的[指南。 |
| Query Pro模式 — 穿透钻取 | 利用Query Pro Mode的穿透钻取功能获得更深入的见解，并无缝地从高级别图表导航到详细仪表板。 使用此功能可毫不费力地从摘要转变为深入分析，并探索趋势、客户行为和KPI。 自动过滤直通和多级别钻取保持数据的一致性，确保顺利的探索。 简化工作流、保留上下文并加快决策速度。 有关详细信息，请阅读有关创建穿透钻取的[分步指南](../../dashboards/data-distiller/query-pro-mode/drill-through.md)。 |
| Query Pro模式 — 高级表属性 | 使用Query Pro Mode高级表属性来简化数据可视化，提高工作流效率和数据清晰度。 直接从自定义功能板向表添加自动排序、调整大小和分页。 对列进行排序，以排定关键数据的优先级，调整大小以获得最佳可读性，以及无缝导航大型数据集，而无需修改SQL查询。 阅读“[查看更多](../../dashboards/data-distiller/query-pro-mode/view-more.md)”指南以了解如何集成这些功能并提升您的数据洞察。 |

{style="table-layout:auto"}

有关仪表板的详细信息，包括如何授予访问权限和创建自定义构件，请首先阅读[仪表板概述](../../dashboards/home.md)。

## 数据准备 {#data-prep}

使用数据准备从 Experience Data Model (XDM) 映射数据并将数据映射到它、转换和验证数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| [!BADGE Beta]{type=Informational}新的数据准备函数以用于目标 | 您现在可以将以下数组函数用于“目标”用例：<ul><li>`array_to_string`</li><li>`filterArray`</li><li>`transformArray`</li><li>`flattenArray`</li></ul> 有关详细信息，请阅读[数据准备函数指南](../../data-prep/functions.md#arrays)。 |

{style="table-layout:auto"}

有关数据准备的详细信息，请参阅[数据准备概述](../../data-prep/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增或更新目标**{#new-updated-destinations}

| 目标 | 描述 |
| --- | --- |
| [Amazon广告](/help/destinations/catalog/advertising/amazon-ads.md) | 2024年9月版添加了映射选项，用于将`countryCode`参数导出到Amazon Ads中。 在[映射步骤](/help/destinations/catalog/advertising/amazon-ads.md#map)中使用`countryCode`提高您与Amazon的标识匹配率。 |

{style="table-layout:auto"}

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| --- | --- |
| [数据集导出](/help/destinations/ui/export-datasets.md)增强功能 | 2024年9月版的Experience Platform包括对数据集导出功能的多项增强，以更好地支持各种数据出口用例。 这些功能增强包括： <ul><li>新的数据文件夹可配置性选项，包括用于添加和删除子文件夹的选项。</li><li>新的导出选项，包括完整文件导出（一次）和指定结束日期的功能</li><li>注意：对于在9月版之前创建的所有数据集导出数据流，Adobe还引入了默认结束日期2025年5月1日。 对于这些数据流中的任一数据流，客户将需要手动更新数据流中的结束日期在结束日期之前，否则导出将在此日期停止。</li></ul> <br> ![Experience Platform用户界面的图像，该图像在计划步骤中突出显示“编辑计划和文件夹”选项。](../2024/assets/september/edit-schedule-folders.png "计划步骤中的“编辑计划和文件夹”选项。"){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

有关更多信息，请阅读[目标概述](../../destinations/home.md)。

## Experience Data Model (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Adobe Experience Platform 的数据提供通用结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 架构编辑器的增强功能 | 在架构编辑器中通过更新的关系工作流控制您的架构关系。 直接从Experience PlatformUI轻松更新或移除现有关系，使架构管理更顺畅、更直观。 调整引用架构并满怀信心地重命名关系，确保跨分段和其他关键过程无缝数据完整性。 要了解有关有效管理架构关系的更多信息，请参阅有关[在UI](../../xdm/tutorials/relationship-ui.md#create-a-relationship-field-group)中定义关系字段以及[B2B关系](../../xdm/tutorials/relationship-b2b.md#edit-a-b2b-schema-relationship)的指南。 |

{style="table-layout:auto"}

有关XDM的详细信息，请阅读[XDM系统概述](../../xdm/home.md)。

## 标识服务 {#identity-service}

使用 Adobe Experience Platform 标识服务通过跨设备和系统桥接标识，全面了解您的客户及其行为，助您实时提供有影响力的个人数字体验。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 标识图链接规则的可用性有限 | 身份图链接规则是Identity Service中的一套工具，可使用它们确保用户的准确个性化。 <ul><li>您现在可以使用[身份优化算法](../../identity-service/identity-graph-linking-rules/identity-optimization-algorithm.md)来确保身份图代表单个人员，从而防止在实时客户个人资料上不必要地合并身份。</li><li>配置[命名空间优先级](../../identity-service/identity-graph-linking-rules/namespace-priority.md)以定义各自命名空间的重要性并影响配置文件的形成和分段方式。</li><li>在UI](../../identity-service/identity-graph-linking-rules/graph-simulation.md)中使用[图形模拟工具来模拟具有不同配置的身份图形。</li><li>使用[身份设置界面](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md)指定您的唯一命名空间并为组织中的所有命名空间建立优先级。</li><li>有关图形数据的量度和趋势，请参阅[身份仪表板](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs)。</li></ul> 要尝试使用身份图关联规则，请联系您的Adobe客户团队以获取开发沙盒的访问权限。 |

**文档更新**

| 功能 | 描述 |
| --- | --- |
| 身份图链接规则疑难解答指南 | 阅读新的[身份图链接规则疑难解答指南](../../identity-service/identity-graph-linking-rules/troubleshooting.md)，了解您可以采取哪些方法和调试解决方案来解决使用身份图链接规则时可能遇到的常见问题。 |
| 身份图关联规则的常见问题解答 | 有关命名空间优先级、身份优化算法和身份图链接规则的其他方面的常见问题的解答列表，请阅读新的[身份图链接规则常见问题解答](../../identity-service/identity-graph-linking-rules/troubleshooting.md#frequently-asked-questions)。 |

{style="table-layout:auto"}

有关标识服务的更多信息，请参阅[标识服务概述](../../identity-service/home.md)。

## 查询服务 {#query-service}

查询服务允许您使用标准 SQL 查询 Adobe Experience Platform [!DNL data lake] 中的数据。您可以加入数据湖的任何数据集，并作为新数据集获取查询结果，以用于报表、Data Science Workspace，或将数据摄取到实时客户配置文件。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 数据Distiller受众 | 通过Experience Platform Data Distiller中的SQL Audience扩展，轻松创建、管理和激活受众。 使用直接来自数据湖的SQL命令定义受众区段，而不需要用户档案中的原始数据。 通过这种灵活的数据驱动方法，优化定位策略并自动将受众同步到基于文件的目标。 简化工作流，优化受众管理，并释放数据的全部潜力。 阅读有关使用SQL受众扩展](../../query-service/data-distiller-audiences/overview.md)提升受众策略的[指南。 |
| 数据Distiller统计数据 — 超多维数据集 | 使用超多维数据集优化大数据分析。 处理复杂的计算（如非重复计数和多维分析），无需重新处理历史数据。 以增量方式更新数据、简化工作流并缩短处理时间，同时保持准确性和效率。 获得更快、可扩展且经济高效的洞察信息，从而改变决策制定。 浏览有关使用超多维数据集](../../query-service/hypercubes.md)解锁高级分析的[指南。 |
| 查询编辑器对象浏览器 | 在查询编辑器中使用新的对象浏览器提高查询效率。 快速搜索、筛选和访问数据集，以更快地编写和优化查询。 利用实时模式更新和即时表元数据，您可以简化工作流、缩短导航时间并增强查询体验。 释放数据的潜力并优化分析。 有关详细信息，请阅读有关使用对象浏览器](../../query-service/ui/user-guide.md#object-browser)的[指南。 |
| 计算小时数 | 使用计划查询的新可见计算小时量度获得对资源使用情况的控制。 在查询执行级别查看计算小时数，以监视和优化CTAS/ITAS批处理查询的资源使用。 跟踪每次查询运行的开始时间、完成状态和计算时间。 轻松微调性能并降低成本。 有关如何最大限度地提高查询效率的信息，请阅读计算小时数](../../query-service/ui/query-schedules.md#compute-hours-at-job-level)上的[指南。 |

{style="table-layout:auto"}

若要了解有关查询服务的更多信息，请阅读[查询服务概述](../../query-service/home.md)。

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的配置文件子集。区段可以基于记录数据（例如人口统计信息）或代表客户与您的品牌互动的时间序列事件。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 统一搜索实施 | 现在，区段生成器中的搜索行为将使用统一搜索。 这样可在管理和搜索受众以重用区段成员资格时获得更强大的体验。 有关此更改的更多信息，请阅读[区段生成器指南](../../segmentation/ui/segment-builder.md#rule-builder-canvas)。 |

{style="table-layout:auto"}

有关[!DNL Segmentation Service]的详细信息，请阅读[分段概述](../../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

使用 Experience Platform 中的源从 Adobe 应用程序或第三方数据源引入数据。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| [!BADGE Beta]{type=Informative}支持在UI中进行加密数据摄取 | 您现在可以使用Experience Platform用户界面中的源工作区从云存储批处理源摄取加密数据。 阅读有关[在UI](../../sources/tutorials/ui/encryped-ingestion.md)中摄取加密数据的教程，以了解更多信息。 |
| [!DNL Snowflake Streaming]源的正式可用性 | [!DNL Snowflake Streaming]源现在处于GA状态。 使用此源将数据从您的[!DNL Snowflake]帐户流式传输到Experience Platform。 有关详细信息，请阅读[[!DNL Snowflake Streaming] 概述](../../sources/connectors/databases/snowflake-streaming.md)。 |
| 支持[!DNL Google BigQuery]中的服务帐户身份验证 | 您现在可以连接[!DNL Google BigQuery]帐户以Experience Platform使用服务帐户身份验证。 有关详细信息，请阅读[[!DNL Google BigQuery] 概述](../../sources/connectors/databases/bigquery.md#generate-your-google-bigquery-credentials)。<br> ![Experience Platform用户界面的图像，该图像在计划步骤中突出显示“编辑计划和文件夹”选项。Google BigQuery的](../2024/assets/september/service_auth.png "服务身份验证。"){width="250" align="center" zoomable="yes"} |
| 支持跳过样本数据预览 | 现在，在创建与以下源的源连接时，您可以选择跳过数据预览： <ul><li>[[!DNL Google BigQuery]](../../sources/tutorials/ui/create/databases/bigquery.md#skip-preview-of-sample-data)</li><li>[[!DNL Salesforce]](../../sources/tutorials/ui/create/crm/salesforce.md#skip-preview-of-sample-data)</li><li>[[!DNL Snowflake]](../../sources/tutorials/ui/create/databases/snowflake.md#skip-preview-of-sample-data)</li></ul> 您可以跳过数据预览，以规避在摄取大批量数据时可能发生的超时。 这样做可能会阻止自动验证计算字段和必填字段。 如果选择跳过数据预览，则可能必须在映射期间手动验证计算字段和必填字段。 |
| 支持在[!DNL SFTP]中禁用分块 | 您现在可以配置一个设置，该设置允许您禁用[!DNL SFTP]源中的分块。 请参阅 [[!DNL SFTP]  概述](../../sources/connectors/cloud-storage/sftp.md)，了解更多信息。 |

{style="table-layout:auto"}

有关更多信息，请阅读[源概述](../../sources/home.md)。
