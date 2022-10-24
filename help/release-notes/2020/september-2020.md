---
title: Adobe Experience Platform发行说明2020年9月
description: 2020年9月版Adobe Experience Platform发行说明。
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
exl-id: bf401f3a-b088-4cbd-9a64-224294b797b9
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发布日期：2020 年 9 月 9 日**

Adobe Experience Platform 现有功能的更新包括：

- [数据管理](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## 数据管理 {#governance}

Adobe Experience Platform数据管理是用于管理客户数据并确保符合适用于数据使用的法规、限制和策略的一系列策略和技术。 它在 [!DNL Experience Platform] 在不同级别，包括编目、数据谱系、数据使用标签、数据访问策略以及对营销操作数据的访问控制。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 数据集标签UI增强功能 | 数据集标签UI中新增了多个排序和过滤控件，以便更轻松地处理大型架构： <ul><li>根据完整架构路径，按字母顺序对字段排序。</li><li>对字段路径名称执行部分搜索。</li><li>筛选没有标签、选定标签或标签类别的字段。</li></ul> |

请参阅 [数据管理概述](../../data-governance/home.md) 以了解有关该服务的详细信息。

## 目标 {#destinations}

在 [Real-time Customer Data Platform](../../rtcdp/overview.md)，目标是与目标平台的预建集成，可无缝地向这些合作伙伴激活数据。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| UX改进 | 用户可以访问内联表操作，以更轻松地访问主操作，例如添加数据、编辑计划和添加区段。 请参阅 [目标工作区](../../destinations/ui/destinations-workspace.md) 文档以了解更多信息。 |

要了解更多信息，请访问 [目标概述](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] 允许您通过使用统计量度和事件通知来监控Adobe Experience Platform上的活动。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| Adobe I/O事件通知 | [!DNL Observability Insights] 利用Adobe I/O事件为多项Experience Platform服务创建事件通知。 通知负载会发送到配置的Webhook，然后您可以使用该Webhook自动执行进一步的下游流程。 |

请参阅 [[!DNL Observability Insights] 概述](../../observability/home.md) 以了解有关该服务的详细信息。

## [!DNL Privacy Service] {#privacy}

一些法律和组织法规允许用户根据请求从您的数据存储中访问或删除其个人数据。 Adobe Experience Platform [!DNL Privacy Service] 提供RESTful API和用户界面，帮助您管理来自客户的这些数据请求。 使用 [!DNL Privacy Service]，您可以提交从Adobe Experience Cloud应用程序访问和删除私有或个人客户数据的请求，以便自动遵守法律和组织隐私法规。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支持LGPD（巴西） | 如今，巴西可以在 [!DNL Lei Geral de Proteção de Dados] (LGPD)法规。 这些作业将根据法规代码进行跟踪 `lgpd_bra`. |

请参阅 [Privacy Service概述](../../privacy-service/home.md) 以了解有关该服务的详细信息。

## 实时客户个人资料 {#profile}

Adobe Experience Platform使您能够为客户在何处或何时与您的品牌进行交互，从而提供协调、一致的相关体验。 使用 [!DNL Real-time Customer Profile]，您可以看到每个客户的整体视图，该视图将来自多个渠道的数据（包括在线、离线、CRM和第三方数据）进行合并。 [!DNL Profile] 允许您将不同的客户数据整合到统一视图中，为每次客户互动提供一个可操作且带有时间戳的帐户。

| 功能 | 描述 |
| ------- | ----------- |
| 配置文件查看器 | Platform UI中的用户档案查看器已更新为具有完全自定义功能的功能板。 用户现在可以选择执行以下任务： <ul><li>更新基本信息小组件中选定的标准属性和自定义属性。</li><li>创建、编辑和删除自定义小组件</li><li>调整小组件大小和重新排列小组件</li></ul> |

有关 [!DNL Real-time Customer Profile]，包括使用的教程和最佳实践 [!DNL Profile] 数据，请阅读 [实时客户资料概述](../../profile/home.md).

## 分段服务 {#segmentation}

Adobe Experience Platform Segmentation Service提供了用户界面和RESTful API，允许您从 [!DNL Real-time Customer Profile] 数据。 这些区段在上集中配置和维护 [!DNL Platform]，以便任何Adobe应用程序都可轻松访问。

[!DNL Segmentation Service] 通过描述区分客户群中可销售人群的标准来定义特定的用户档案子集。 区段可以基于记录数据（如人口统计信息）或表示客户与您的品牌交互的时间序列事件。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 导出作业 | 已添加标记，以允许在导出作业中评估区段。 因此，用户可以在单个作业中同时运行分段和导出。 |
| 合并策略 | 单个批量分段作业中可以包含多个合并策略。 |

有关 [!DNL Segmentation Service]，请参阅 [分段概述](../../segmentation/home.md)

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用 [!DNL Platform] 服务。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

[!DNL Experience Platform] 提供了RESTful API和交互式UI，让您能够轻松为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 自动映射 | [!DNL Platform] 根据用户选择的目标架构或数据集，在数据摄取工作流期间为自动映射提供智能推荐。 您可以手动调整灵活的自动映射规则以适合您的用例。 |
| UX改进 | 用户可以访问内联表操作，以更轻松地访问主操作，例如添加数据、编辑计划和添加区段。 请参阅 [监控数据流](../../sources/tutorials/ui/monitor.md) 文档以了解更多信息。 |

要进一步了解源，请参阅 [源概述](../../sources/home.md).
