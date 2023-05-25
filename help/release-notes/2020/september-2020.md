---
title: Adobe Experience Platform发行说明2020年9月
description: Adobe Experience Platform 2020年9月版发行说明。
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
exl-id: bf401f3a-b088-4cbd-9a64-224294b797b9
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发布日期：2020 年 9 月 9 日**

Adobe Experience Platform 现有功能的更新包括：

- [数据治理](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## 数据治理 {#governance}

Adobe Experience Platform数据管理是用于管理客户数据并确保遵守适用于数据使用的法规、限制和策略的一系列策略和技术。 它在以下方面发挥着关键作用 [!DNL Experience Platform] 在不同的级别，包括编目、数据谱系、数据使用标签、数据访问策略和对营销活动数据的访问控制。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 数据集标签UI增强功能 | 已将多个新的排序和筛选控件添加到数据集标签UI，以便更轻松地使用大型架构： <ul><li>根据完整架构路径按字母顺序对字段排序。</li><li>对字段路径名执行部分搜索。</li><li>筛选没有标签、选定标签或标签类别的字段。</li></ul> |

请参阅 [数据治理概述](../../data-governance/home.md) 以了解有关该服务的更多信息。

## 目标 {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md)，目标是预先构建的与目标平台的集成，可无缝地向这些合作伙伴激活数据。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| UX改进 | 用户可以访问内联表操作，以便更轻松地访问主要操作，例如添加数据、编辑计划和添加区段。 请参阅 [目标工作区](../../destinations/ui/destinations-workspace.md) 文档，以了解更多信息。 |

要了解更多信息，请访问 [目标概述](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] 允许您通过使用统计指标和事件通知来监控Adobe Experience Platform上的活动。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| Adobe I/O事件通知 | [!DNL Observability Insights] 利用Adobe I/O事件为多个Experience Platform服务创建事件通知。 通知有效负载将发送到配置的webhook，然后您可以使用它来自动化进一步的下游进程。 |

请参阅 [[!DNL Observability Insights] 概述](../../observability/home.md) 以了解有关该服务的更多信息。

## [!DNL Privacy Service] {#privacy}

一些法律和组织法规授予用户权利，允许他们根据请求从您的数据存储中访问或删除其个人数据。 Adobe Experience Platform [!DNL Privacy Service] 提供RESTful API和用户界面，以帮助您管理来自客户的数据请求。 替换为 [!DNL Privacy Service]，您可以提交从Adobe Experience Cloud应用程序访问和删除私人或个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支持LGPD（巴西） | 现在，隐私工作可以在巴西的 [!DNL Lei Geral de Proteção de Dados] (LGPD)法规。 这些作业根据法规代码进行跟踪 `lgpd_bra`. |

请参阅 [Privacy Service概述](../../privacy-service/home.md) 以了解有关该服务的更多信息。

## 实时客户资料 {#profile}

通过Adobe Experience Platform，无论客户在何处或何时与您的品牌互动，您都可以为其推动协调、一致且相关的体验。 替换为 [!DNL Real-Time Customer Profile]，您可以看到合并了来自多个渠道（包括在线、离线、CRM和第三方数据）的数据的每个客户的整体视图。 [!DNL Profile] 允许您将不同的客户数据整合到一个统一的视图中，并提供每个客户交互的可操作、带时间戳的帐户。

| 功能 | 描述 |
| ------- | ----------- |
| 配置文件查看器 | 平台UI中的配置文件查看器已更新为带有完全自定义的功能板。 用户现在可以选择执行以下任务： <ul><li>更新基本信息小部件中选定的标准和自定义属性。</li><li>创建、编辑和删除自定义构件</li><li>调整构件大小并重新排列构件</li></ul> |

有关的详细信息 [!DNL Real-Time Customer Profile]，包括有关使用的教程和最佳实践 [!DNL Profile] 数据，请阅读 [Real-time Customer Profile概述](../../profile/home.md).

## 分段服务 {#segmentation}

Adobe Experience Platform Segmentation Service提供了一个用户界面和RESTful API，允许您从构建区段和生成受众。 [!DNL Real-Time Customer Profile] 数据。 这些区段集中配置并维护于 [!DNL Platform]，便于任何Adobe应用程序访问。

[!DNL Segmentation Service] 通过描述用于区分客户群内可销售人员组的标准，来定义用户档案的特定子集。 区段可以基于记录数据（例如人口统计信息）或表示客户与您的品牌互动的时间系列事件。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 导出作业 | 添加了一个标志，以允许将区段作为导出作业的一部分进行评估。 因此，用户可以在单个作业中运行分段和导出。 |
| 合并策略 | 可以在单个批量分段作业中包含多个合并策略。 |

有关的详细信息 [!DNL Segmentation Service]，请参阅 [分段概述](../../segmentation/home.md)

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用来构建、标记和增强这些数据 [!DNL Platform] 服务。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)中摄取数据。

[!DNL Experience Platform] 提供了一个RESTful API和一个交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您进行身份验证并连接到外部存储系统和CRM服务，设置引入运行的时间，以及管理数据引入吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 自动映射 | [!DNL Platform] 根据用户选择的目标架构或数据集，在数据摄取工作流期间为自动映射提供智能推荐。 您可以手动调整灵活的自动映射规则以适合您的用例。 |
| UX改进 | 用户可以访问内联表操作，以便更轻松地访问主要操作，例如添加数据、编辑计划和添加区段。 请参阅 [监测数据流](../../sources/tutorials/ui/monitor.md) 文档，以了解更多信息。 |

要了解有关源的更多信息，请参阅 [源概述](../../sources/home.md).
