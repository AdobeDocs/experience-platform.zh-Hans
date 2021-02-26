---
title: Adobe Experience Platform 发行说明
description: Experience Platform 2021年2月24日发行说明。
doc-type: release notes
last-update: February 24, 2021
author: ens70167
translation-type: tm+mt
source-git-commit: efa06bec5af65240fdd586da4fd0439b8d1146b8
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 7%

---


# Adobe Experience Platform 发行说明

**发行日期：2021 年 2 月 24 日**

Adobe Experience Platform的新增功能：

- [（测试版）仪表板](#dashboards)

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## (Beta)仪表板{#dashboards}

Adobe Experience Platform提供了多个仪表板，通过这些视图，您可以有关组织数据的重要信息，这些信息在每日快照中捕获。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 用户档案、区段、目标和许可证使用仪表板（测试版） | **注意：仪表板功能当前处于测试阶段，并非所有用户都可用。文档和功能可能会发生变化。**<br/><br/>&#x200B;仪表板针对组织的数据提供开箱即用的报告，并直接内置于平台内的营销人员工作流程中。无需额外的IT支持，也无需花费时间和精力导出和处理仪表板，即可获得这些数据，同时还需要额外的数据仓库设计和实施。 |

## [!DNL Data Science Workspace] {#dsw}

数据科学工作区使用机器学习和人工智能从数据中创建洞察。 Data Science Workspace集成到Adobe Experience Platform中，可帮助您跨Adobe解决方案使用内容和数据资产进行预测。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| JupyterLab EDA笔记本 | 探索性数据分析(EDA)Python笔记本现已在Jupyterlab上市。 此笔记本旨在帮助您发现数据模式、检查数据完整性并汇总预测模型的相关数据。 有关详细信息，请参阅教程[探索基于Web的预测模型数据](../../data-science-workspace/jupyterlab/eda-notebook.md)。 |

有关Data Science Workspace的更多一般信息，请参阅[Data Science Workspace概述](../../data-science-workspace/home.md)。

## [!DNL Dataflows] {#dataflows}

在Adobe Experience Platform，数据是从各种来源中摄取的，在Experience Platform中分析，并激活到各种目的地。 平台通过为数据流提供透明度，使跟踪这种可能的非线性数据流的过程更加容易。

数据流是跨平台移动数据的数据作业的表示方法。这些数据流是跨不同服务配置的，有助于将数据从源连接器移动到目标数据集，然后由[!DNL Identity Service]和[!DNL Real-time Customer Profile]使用，最终激活到[!DNL Destinations]。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 新的监视仪表板 | 您现在可以使用监控仪表板实现跨服务透明度，并为源数据摄取提供切实可行的洞察。 新的监控仪表板提供了从[!DNL Data Lake]到[!DNL Identity Service]和[!DNL Profile]处理的数据的全面视图，同时还允许您监控摄取率、成功和失败。 有关详细信息，请参阅有关[在UI](../../dataflows/ui/monitor-sources.md)中监视源数据流的教程。 |

有关数据流的更多一般信息，请参阅[数据流概述](../../dataflows/home.md)。

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是预建的与目标平台的集成，允许从Adobe Experience Platform无缝激活数据。您可以使用目标来激活已知和未知的跨渠道营销活动、电子邮件活动、定向广告和许多其他用例的数据。

**新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](destinations/catalog/social/linkedin.md) | [!DNL LinkedIn Matched Audiences]连接允许您在[!DNL LinkedIn]社交平台中激活受众。 |

有关目标的更多常规信息，请参阅[目标概述](../../destinations/home.md)。

## [!DNL Experience Data Model (XDM) System] {#xdm}

标准化和互操作性是[!DNL Experience Platform]背后的关键概念。 [!DNL Experience Data Model] (XDM)由Adobe驱动，旨在实现客户体验数据标准化并定义客户体验管理模式。

XDM是一个公开存档的规范，旨在提高数字体验的强大功能。 它为任何与Adobe Experience Platform上的服务通信的应用程序提供了通用结构和定义。 通过遵守XDM标准，所有客户体验数据都可以整合到以更快、更集成的方式提供洞察的常见表现形式中。 您可以从客户行动中获得宝贵的洞察，通过细分定义客户受众，并将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 升级的搜索UI | 现在，在[!UICONTROL 模式]工作区的[!UICONTROL 浏览]选项卡和[!DNL Schema Editor]的混音选择对话框中，可使用改进的搜索功能。<br><br>在以前搜索术语时，结果将仅包含名称与搜索查询匹配的XDM资源。现在，除了名称与查询匹配的资源外，还将包括包含与术语匹配的单个属性的资源。 这允许您根据XDM资源包含的属性而不是资源名称搜索XDM资源。<br><br>有关更多信息，请 [参阅有关](../../xdm/ui/explore.md) 在UI中 [探索](../../xdm/ui/resources/schemas.md) XDM资源和管理架构的文档。 |

有关XDM的更多一般信息，请参阅[XDM系统概述](../../xdm/home.md)。

## [!DNL Identity Service] {#identity}

提供相关的数字体验需要全面了解客户。 当客户数据在不同系统之间碎片化，导致每个客户似乎具有多个“身份”时，这就变得更加困难。

Adobe Experience Platform [!DNL Identity Service]通过跨设备和系统连接身份，帮助您实时提供有影响力的个性化数字体验，从而更好地视图客户及其行为。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 标识图查看器 | 通过标识图查看器，您可以验证和可视化在UI中拼接在一起的身份，从而改进调试和透明度。 有关详细信息，请参阅[标识图查看器文档](../../identity-service/ui/identity-graph-viewer.md)。 |

有关[!DNL Identity Service]的更多一般信息，请参阅[Identity Service概述](../../identity-service/home.md)。

## 实时客户资料 {#profile}

Adobe Experience Platform使您能够在客户与您的品牌互动的任何地方或何时为其提供协调一致的相关体验。 通过实时客户用户档案，您可以了解每位客户的整体视图，该客户整合了来自多个渠道的数据，包括在线、离线、CRM和第三方数据。 [!DNL Profile] 允许您将客户数据整合到一个统一的视图中，为每次客户互动提供一个可操作且有时间戳的帐户。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 计算属性(Alpha) | ***注意：此功能当前位于alpha中，并且并非所有用户都可用。文档和功能可能会发生变化。*** <br/><br/>计算属性是用于将事件级数据聚合为用户档案级属性的函数。然后，您可以在细分、激活和个性化中使用聚合。 这些函数的一些示例包括count、sum、average、min、max、true/false。 计算属性当前仅通过API可用。 有关详细信息，请参阅[计算属性概述](../../profile/computed-attributes/overview.md)。 |

有关实时客户用户档案的更多信息（包括使用[!DNL Profile]数据的教程和最佳实践），请首先阅读[实时客户用户档案概述](../../profile/home.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源收集数据，同时允许您使用平台服务构建、标记和增强该数据。 您可以从各种来源收集数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松为各种数据提供者设置源连接。 这些源连接允许您对外部存储系统和CRM服务进行身份验证并连接，设置获取运行的时间，以及管理数据获取吞吐量。

**新来源**

| 功能 | 描述 |
| --- | --- |
| [!DNL Google PubSub] | 您现在可以使用[!DNL Flow Service] API或UI将[!DNL Google PubSub]连接到[!DNL Experience Platform]。 有关详细信息，请参阅[[!DNL Google PubSub] 连接器概述](../../sources/connectors/cloud-storage/google-pubsub.md)。 |
| [!DNL Oracle Object Storage] | 您现在可以使用[!DNL Flow Service] API或UI将[!DNL Oracle Object Storage]连接到[!DNL Experience Platform]。 有关详细信息，请参阅[[!DNL Oracle Object Storage] 连接器概述](../../sources/connectors/cloud-storage/oracle-object-storage.md)。 |

有关源的更多一般信息，请参阅[源概述](../../sources/home.md)。
