---
title: 跟踪数据信号以生成客户生命周期值
description: 本指南提供了一个端到端演示，介绍如何将Data Distiller和用户定义的功能板与Real-time Customer Data Platform结合使用来测量和可视化客户生命周期值。
source-git-commit: 2346f2d9450bc24e10419c09ee3dbcfb35bd5778
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 0%

---

# 跟踪数据信号以生成客户生命周期值

您可以使用Real-time Customer Data Platform跟踪客户生命周期值(CLV)，并使用用户定义的功能板来显示该量度。 通过使用数据Distiller和用户定义的功能板，您可以衡量客户在整个客户关系中对贵公司的价值。 了解CLV有助于您制定业务战略，以赢取新客户，同时保留现有客户并保持利润率。

以下信息图描述了数据收集、操作、分析和操作的周期，这些周期可生成高性能数据以改进您的营销活动。

![从观察到分析到行动的往返数据信息图。](../images/use-cases/infographic-use-case-cycle.png)

此端到端用例演示了如何捕获和修改数据信号以计算客户生命周期值派生属性。 然后，这些派生属性可应用于您的Real-Time CDP配置文件数据，并可与用户定义的功能板一起使用，以构建用于分析的功能板。 通过Data Distiller，您可以扩展Real-Time CDP分析数据模型，并使用CLV派生属性和功能板分析来构建新区段，并将其激活到所需的目标。 然后，这些区段可用于创建高性能受众以支持您的下一个营销活动。

本指南旨在通过测量驱动CLV并在您的环境中实施类似用例的关键接触点中的数据信号，来帮助您更好地了解客户体验。 整个过程在下图中进行了总结。

![利用客户生命周期价值所需广泛步骤的信息图。](../images/use-cases/implementation-steps.png)

## 快速入门 {#getting-started}

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [查询服务](../home.md):提供用户界面和RESTful API，您可以在其中使用SQL查询来分析和扩充数据。
* [Segmentation Service](../../segmentation/home.md):允许您根据实时客户资料数据构建区段并生成受众。

## 先决条件

本指南要求您 [数据Distiller](../data-distiller/overview.md) SKU作为包产品的一部分。 如果您不确定自己是否拥有此功能，请咨询Adobe服务代表。

## 创建派生属性 {#create-derived-attribute}

建立CLV的第一步是根据从用户操作捕获的数据信号创建派生属性。 此特定用例在有关航空公司忠诚度计划的单独文档中捕获。 请参阅指南以了解如何 [使用查询服务创建基于文件的派生属性，以用于用户档案数据](./deciles-use-case.md). 在解释以下步骤的文件中提供了完整的示例和说明：

* 创建架构以允许分段存储。
* 使用查询服务创建文件。
* 生成数据集。
* 启用架构以在实时客户资料中使用。
* 创建标识命名空间并将其标记为主标识符。
* 创建查询以计算回顾期间的数据集。

## 扩展分析数据模型并计划更新 {#extend-data-model-and-set-refresh-schedule}

接下来，您必须构建自定义数据模型或扩展现有Adobe Real-Time CDP数据模型，以便与CLV报表分析互动。 请参阅相关文档以了解如何 [通过查询服务构建报表分析数据模型，以与加速存储数据和用户定义的功能板一起使用](../data-distiller/query-accelerated-store/reporting-insights-data-model.md#build-a-reporting-insights-data-model). 本教程涵盖以下步骤：

* 使用数据Distiller创建报告分析的模型。
* 创建表、关系和填充数据。
* 查询报表分析数据模型。
* 使用Real-Time CDP分析数据模型扩展您的数据模型。
* 创建维度表以扩展报表分析模型。
* 查询扩展的加速存储报告分析数据模型

请参阅Real-time Customer Data Platform分析数据模型文档，以了解如何 [自定义SQL查询模板，以便为营销和关键绩效指标(KPI)用例创建Real-Time CDP报表](../../dashboards/cdp-insights-data-model.md).

确保设置计划以定期刷新自定义数据模型。 这可确保根据需要将数据作为摄取管道的一部分返回，并填充用户定义的功能板。 请参阅 [计划查询指南](../ui/query-schedules.md#create-schedule) 了解如何设置计划。

## 构建功能板以捕获分析 {#build-a-custom-dashboard}

现在，您已创建自定义数据模型，接下来可以使用自定义查询和用户定义的功能板来显示数据。 有关如何操作的完整指南，请参阅用户定义的功能板概述 [构建自定义功能板](../../dashboards/user-defined-dashboards.md). UI指南包含有关以下内容的详细信息：

* 如何创建小组件。
* 如何使用小组件编辑器。

下面显示了使用非文件存储段的自定义CLV小组件示例。

![基于十年的自定义CLTV小组件的集合。](../images/use-cases/deciles-user-defined-dashboard.png)

## 创建和激活区段以构建高性能受众 {#create-and-activate-segments}

下一步是根据实时客户资料数据生成区段并生成受众。 请参阅区段生成器UI指南，以了解如何 [在平台中创建和激活区段](../../segmentation/ui/segment-builder.md). 该指南提供了有关如何执行以下操作的章节：

* 使用属性、事件和现有受众的组合作为构建基块来创建区段定义。
* 使用规则生成器画布和容器来控制区段规则执行的顺序。
* 查看潜在受众的估计值，以便根据需要调整区段定义。
* 为计划分段启用所有区段定义。
* 为流分段启用指定的区段定义。

或者，还有 [区段生成器视频教程](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) 可获取更多信息。

## 为电子邮件促销活动激活您的区段 {#activate-segment-for-campaign}

生成区段后，您便可以将其激活到目标。 平台支持各种电子邮件服务提供商(ESP)，使您能够管理电子邮件营销活动，如发送促销电子邮件活动。

检查 [电子邮件营销目标概述](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/overview.html?lang=en#connect-destination) (例如， [Oracle雄辩](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/oracle-eloqua-api.html?lang=en) 页面)。

## 查看营销活动返回的分析数据 {#post-campaign-data-analysis}

来自源的数据现在可以 [增量处理](../essential-concepts/incremental-load.md) 作为加速数据存储中数据模型的计划刷新的一部分。 客户的任何响应事件都可以在发生时或批量摄取到Adobe Experience Platform中。 根据您的设置或源连接器，您的数据模型可能每天刷新一次或多次。 请参阅 [批量摄取API概述](../../ingestion/batch-ingestion/api-overview.md) 或 [流摄取概述](../../ingestion/streaming-ingestion/overview.md) 以了解更多信息。

更新数据模型后，您的自定义功能板小组件会提供有意义的信号，以便您测量和可视化客户生命周期值。

![一个自定义小组件，用于显示根据其客户群和电子邮件促销活动打开的电子邮件数量。](../images/use-cases/post-activation-and-email-response-kpis.png)

为您的自定义分析提供了各种可视化选项。

![营销活动存储段小组件打开的电子邮件。](../images/use-cases/email-opened-by-campaign-buckets.png)

这些洞察反过来也可以帮助您针对后续促销活动制定业务策略。

![四个自定义小组件的集合，用于详细描述电子邮件促销活动的结果。](../images/use-cases/example-widgets.png)

## 后续步骤

通过阅读本文档，您应该更好地了解如何使用Real-time Customer Data Platform来跟踪和可视化客户生命周期值(CLV)量度。 要进一步了解通过查询服务和Experience Platform满足的许多业务用例，建议您阅读以下文档：

* [放弃浏览用例的端到端示例，演示了查询服务的多功能性和优势。](./abandoned-browse.md)
* [如何使用查询服务和机器学习从真正的在线网站访客流量中确定和过滤机器人活动](./bot-filtering.md)
* [如何对平台数据执行匹配，该数据通过大致匹配您选择的字符串来组合来自多个数据集的结果。](./fuzzy-match.md)

<!-- "Data signals are actions taken by consumers while online that offer clues about intent that can be acted upon. This includes anything from visiting a website to filling out a change of address or clicking an ad."  -->

<!-- "Customer touchpoints are your brand's points of customer contact, from start to finish." -->
