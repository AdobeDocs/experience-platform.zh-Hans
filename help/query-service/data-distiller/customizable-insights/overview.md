---
title: 可自定义的分析
description: 了解用例、基本功能和使用Data Distiller开发可自定义的分析功能板的所需步骤。 了解Data Distiller中的可自定义分析功能如何增强透明度并获得不同维度（如用户档案、受众、营销活动、历程、权利和同意）的操作分析。
exl-id: f807d0fd-c8ec-42d4-96a0-5ffc5681943b
source-git-commit: bb95e0aa8ee92aee5a2f126d85e78308e652a061
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# 可自定义的分析

利用Data Distiller的可自定义见解，创建定制的报表数据模型以提取更深入的见解、优化策略并调整分析以满足特定业务需求。 使用可自定义的分析功能可跨维度（例如，用户档案、受众、营销活动、历程、权利和同意）增强透明度并从Adobe Experience Platform数据获得运营分析。 此功能提供了多功能、自适应解决方案，可定制贵组织的报表数据模型以符合您的特定业务需求。

要[可视化您的可自定义见解](../../../dashboards/data-distiller/overview.md)，您可以使用[查询专业模式](../../../dashboards/data-distiller/customizable-insights/query-pro-mode.md)通过自定义SQL查询进行复杂分析，并将您的数据转换为易于理解的图表。 使用Query Pro模式在功能板上创建定制的分析见解和可视化图表，并将您的分析下载为CSV文件以满足技术和非技术受众的需求。

本文档介绍了使用数据Distiller开发可自定义的分析功能板的用例、基本功能和所需步骤。

## 先决条件

本教程使用用户定义的功能板在Platform UI中可视化自定义数据模型中的数据。 有关此功能的更多信息，请参阅[用户定义的功能板文档](../../../dashboards/user-defined-dashboards.md)。

## 快速入门

要构建用于报表分析的自定义数据模型，并扩展包含扩充的Platform数据的Real-Time CDP数据模型，需要数据Distiller SKU。 请参阅与Data Distiller SKU相关的[打包](../../packaging.md)、[护栏](../../guardrails.md#query-accelerated-store)和[许可](../../data-distiller/license-usage.md)文档。 如果您没有Data Distiller SKU，请联系您的Adobe客户服务代表以了解更多信息。

## 可自定义的分析用例 {#use-cases}

以下是一些常见用例，可以通过Data Distiller中的可自定义分析来有效解决这些用例。

### 用户档案和受众使用情况透明度 {#usage-transparency}

**挑战：**&#x200B;如何按特定条件(如业务单位、忠诚度状态或客户存留期值(CLTV))划分关键绩效指标(KPI)。

**可自定义的分析解决方案：** Data Distiller支持在Adobe Experience Platform中扩展报表数据模型，从而促进[添加自定义配置文件属性，如CLTV](../../use-cases/customer-lifetime-value.md)或忠诚度状态。

### 同意异常跟踪 {#consent-anomaly-tracking}

**挑战：**&#x200B;如何将受众重叠和大小趋势线报告应用于电子邮件、短信和电话等渠道的自定义同意属性。

**可自定义的分析解决方案：**&#x200B;可以扩展报表数据模型以跟踪同意首选项随时间发生的变化。 这涉及构建其他事实和维度表以趋势化同意首选项并计划[增量数据刷新](../../key-concepts/incremental-load.md)。

### 优化受众分段策略 {#optimize-audience-segmentation-strategy}

**挑战：**&#x200B;如何将机器学习(ML)模型生成的倾向分数集成到其受众KPI报表中。

**可自定义的分析解决方案：**&#x200B;数据Distiller允许包含来自自定义ML模型的[倾向分数](../../use-cases/propensity-score.md)，从而便于在受众级别计算汇总分数。 然后，可以将此数据与标准KPI一起报告。

### 受众扩展 {#audience-expansion}

**挑战：**&#x200B;如何在受众重叠报表中获取不仅仅是个人资料计数，以及如何获取其他人口统计数据或偏好以指导受众扩展策略。

**可自定义的分析解决方案：**&#x200B;通过扩展报表数据模型，用户可以合并其他配置文件属性，用相关人口统计数据和首选项扩充受众重叠报表。

## 生成可自定义分析的关键功能 {#key-capabilities}

下图突出显示生成可自定义分析的几个基本功能。 这些功能包括：

1. **数据可视化：**&#x200B;结合趋势和条形图等可视化元素以全面查看数据趋势。
1. **功能板创作：**&#x200B;允许创建针对特定用例的自定义功能板，以提供更加个性化和更有针对性的分析体验。
1. **灵活的SQL数据建模：**&#x200B;使用通用的SQL数据建模方法，该方法允许用户无缝地组合和处理不同的数据集，增强适应性和分析深度。
1. **加速存储：**&#x200B;实施加速存储机制以通过SQL高效地提供聚合见解，从而确保简化和快速访问有价值的信息。
1. **BI连接：**&#x200B;促进与常用Business Intelligence(BI)工具(包括Power BI、Tableau、Looker和Apache Superset)的无缝集成。 该连接确保与多种BI环境兼容，使用户能够灵活地使用他们选择的工具进行深入分析和报告。

![数据Distiller可自定义分析的主要功能的可视表示形式。](../../images/data-distiller/customizable-insights/key-capabilities-of-customizable-insights.png)

## 创建可自定义分析的步骤 {#steps-to-create}

要在Data Distiller中开发可自定义的分析功能板，请按照以下分步说明进行操作。

1. **临时查询探索：**&#x200B;首先执行临时`SELECT`查询以探索数据湖上的原始数据。 这允许对实验进行实时、探索性的数据分析，并且验证查询结果未存储在数据湖中的数据。
1. **批处理查询利用率：**&#x200B;使用批处理查询[创建计划作业](../../api/scheduled-queries.md#create-a-new-scheduled-query)以生成分析汇总表，从而确保采用系统化和自动化的方法来处理数据。 批处理查询执行`INSERT TABLE AS SELECT`和`CREATE TABLE AS SELECT`查询以清理、形状、操作和扩充数据。 这些查询的结果存储在数据湖中。
1. **聚合分析加载：**&#x200B;将生成的聚合分析加载到加速存储中，并使用SQL测试查询，并确保数据检索的准确性和效率。 要了解如何[对加速存储](../../api/accelerated-queries.md)进行无状态查询，请参阅文档。
1. **访问和集成：**&#x200B;通过与Adobe Experience Platform [用户定义仪表板](../../../dashboards/user-defined-dashboards.md)或其他首选Business Intelligence(BI)工具集成，无缝访问存储在加速存储中的见解。 这些与第三方客户端的集成为用户提供了有凝聚力的直观体验。

![说明在Data Distiller中可自定义分析四个步骤的信息图表。](../../images/data-distiller/customizable-insights/steps-to-customizable-insights.png)

## 后续步骤

通过阅读本文档，您现在可以更好地了解用例、基本功能和使用Data Distiller开发可自定义的分析仪表板的必要步骤。 要继续了解如何创建定制的报表数据模型，请参阅[报表分析数据模型指南](./reporting-insights-data-model.md)。
