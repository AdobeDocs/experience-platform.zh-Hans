---
title: Adobe Experience Platform 发行说明（2020 年 9 月）
description: Adobe Experience Platform 2020 年 9 月发行说明。
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
exl-id: bf401f3a-b088-4cbd-9a64-224294b797b9
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 36%

---

# Adobe Experience Platform 发行说明

**发行日期： 2020年9月9日**

Adobe Experience Platform 中现有功能的更新：

- [数据治理](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## 数据治理 {#governance}

Adobe Experience Platform 数据治理是一系列策略和技术，用于管理客户数据并确保遵守适用于数据使用的法规、限制和政策。它在 Experience Platform 的 [!DNL Experience Platform] 各个层面中发挥着关键作用，包括编目、数据谱系、数据使用标记、数据访问策略和营销操作数据访问控制。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 数据集标签UI增强功能 | 若干新的排序和筛选控件已添加到数据集标签UI，以便更轻松地使用大型架构： <ul><li>根据完整架构路径，按字母顺序对字段排序。</li><li>对字段路径名执行部分搜索。</li><li>筛选没有标签、选定标签或标签类别的字段。</li></ul> |

有关该服务的更多信息，请参阅[数据管理概述](../../data-governance/home.md)。

## 目标 {#destinations}

在[Real-Time Customer Data Platform](../../rtcdp/overview.md)中，目标是与目标平台预先构建的集成，这些平台以无缝方式向这些合作伙伴激活数据。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| UX改进 | 用户可以访问内联表操作，以便更轻松地访问主要操作，例如添加数据、编辑计划和添加区段。 有关详细信息，请参阅[目标工作区](../../destinations/ui/destinations-workspace.md)文档。 |

要了解更多信息，请访问[目标概述](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights]允许您通过使用统计指标和事件通知来监控Adobe Experience Platform上的活动。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| Adobe I/O事件通知 | [!DNL Observability Insights]利用Adobe I/O Events为多个Experience Platform服务创建事件通知。 通知有效负载将发送到配置的webhook，然后您可以使用它来自动化后续下游进程。 |

有关该服务的更多信息，请参阅[[!DNL Observability Insights] 概述](../../observability/home.md)。

## [!DNL Privacy Service] {#privacy}

多项法律和组织规定赋予用户相应的权利，允许他们根据要求从数据存储中访问或删除其个人数据的权利。Adobe Experience Platform [!DNL Privacy Service] 提供 RESTful API 和用户界面，帮助您管理客户数据请求。借助 [!DNL Privacy Service]，您可以提交从 Adobe Experience Cloud 应用程序访问和删除个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支持 LGPD（巴西） | 现在可以根据巴西 [!DNL Lei Geral de Proteção de Dados] (LGPD) 法规创建隐私作业。这些任务会根据监管代码 `lgpd_bra` 进行追踪。 |

有关该服务的更多信息，请参阅 [Privacy Service 概述](../../privacy-service/home.md) 。

## 实时客户轮廓 {#profile}

Adobe Experience Platform 使您能够为客户提供协调、一致且相关的体验，无论他们何时何地与您的品牌互动均是如此。通过[!DNL Real-Time Customer Profile]，您可以查看合并来自多个渠道（包括在线、离线、CRM和第三方数据）的数据的每个单个客户的整体视图。 [!DNL Profile]允许您将不同的客户数据整合到一个统一视图中，并提供每个客户交互的带时间戳的可操作帐户。

| 功能 | 描述 |
| ------- | ----------- |
| 配置文件查看器 | Experience Platform UI中的配置文件查看器已更新，成为具有完全自定义的功能板。 用户现在可以选择执行以下任务： <ul><li>更新基本信息小部件中选定的标准和自定义属性。</li><li>创建、编辑和删除自定义构件</li><li>调整构件大小并重新排列构件</li></ul> |

有关[!DNL Real-Time Customer Profile]的更多信息，包括有关使用[!DNL Profile]数据的教程和最佳实践，请阅读[实时客户配置文件概述](../../profile/home.md)。

## Segmentation Service {#segmentation}

Adobe Experience Platform Segmentation Service提供了一个用户界面和RESTful API，允许您根据[!DNL Real-Time Customer Profile]数据构建区段并生成受众。 这些区段是在[!DNL Experience Platform]上集中配置和维护的，因此任何Adobe应用程序都可以轻松访问它们。

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。区段可以基于记录数据（例如人口统计信息）或代表客户与您的品牌互动的时间序列事件。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 导出作业 | 添加了标志，以允许将区段作为导出作业的一部分进行评估。 因此，用户可以在一个作业中同时运行分段和导出。 |
| 合并策略 | 可以在单个批次分段作业中包含多个合并策略。 |

有关[!DNL Segmentation Service]的详细信息，请参阅[分段概述](../../segmentation/home.md)

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强该数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

[!DNL Experience Platform]提供了一个RESTful API和一个交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 自动映射 | [!DNL Experience Platform]根据用户选择的目标架构或数据集，为数据摄取工作流程期间的自动映射提供智能推荐。 您可以手动调整灵活的自动映射规则以适合您的用例。 |
| UX改进 | 用户可以访问内联表操作，以便更轻松地访问主要操作，例如添加数据、编辑计划和添加区段。 有关详细信息，请参阅[监视数据流](../../sources/tutorials/ui/monitor.md)文档。 |

要了解有关源的更多信息，请参阅[源概述](../../sources/home.md)。
