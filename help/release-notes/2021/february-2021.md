---
title: Adobe Experience Platform 发行说明（2021 年 2 月）
description: Adobe Experience Platform 的 2021 年 2 月发行说明。
doc-type: release notes
last-update: February 24, 2021
author: ens70167
exl-id: 8c3142af-4021-4f7e-acbd-c5277dd188d1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 23%

---

# Adobe Experience Platform 发行说明

**发行日期： 2021年2月24日**

Adobe Experience Platform 的新功能：

- [(Beta)功能板](#dashboards)

Adobe Experience Platform 中现有功能的更新：

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## (Beta)功能板 {#dashboards}

Adobe Experience Platform提供了多个功能板，您可以通过这些功能板查看有关贵组织数据的重要信息，如在每日快照期间捕获的数据。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 配置文件、区段、目标和许可证使用情况仪表板(Beta) | **注意：功能板功能当前为测试版，并非对所有用户都可用。 文档和功能可能会发生变化。**<br/><br/>&#x200B;功能板提供有关您组织数据的现成报表，并直接内置到Experience Platform中的营销人员工作流程中。 这些仪表板无需额外的IT支持，也不需要通过额外的数据仓库设计和实施来导出和处理数据所需的时间和精力。 |

## [!DNL Data Science Workspace] {#dsw}

数据科学Workspace使用机器学习和人工智能从您的数据创建见解。 数据科学Workspace已集成到Adobe Experience Platform中，可帮助您在各个Adobe解决方案中使用您的内容和数据资产做出预测。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| JupyterLab EDA笔记本 | Jupyterlab现在提供探索数据分析(EDA) Python笔记本。 此笔记本旨在帮助您发现数据模式、检查数据健全度以及总结预测模型的相关数据。 有关详细信息，请参阅有关[探索预测模型的基于Web的数据](../../data-science-workspace/jupyterlab/eda-notebook.md)的教程。 |

有关Data Science Workspace的更多常规信息，请参阅[Data Science Workspace概述](../../data-science-workspace/home.md)。

## [!DNL Dataflows] {#dataflows}

在Adobe Experience Platform中，数据从各种源摄取，在Experience Platform中进行分析，并激活到各种目标。 Experience Platform通过提供数据流透明度，使跟踪这种潜在非线性数据流的过程更容易。

数据流是跨Experience Platform移动数据的数据作业的表示形式。 这些数据流在不同的服务中配置，有助于将数据从源连接器移动到目标数据集，然后由[!DNL Identity Service]和[!DNL Real-Time Customer Profile]使用它，最后激活到[!DNL Destinations]。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 新的监视仪表板 | 您现在可以使用监视仪表板实现跨服务透明度和对源数据摄取的可操作性洞察。 新的监视仪表板提供从[!DNL Data Lake]到[!DNL Identity Service]和到[!DNL Profile]的已处理数据的全面视图，同时还允许您监视摄取率、成功和失败。 有关详细信息，请参阅有关[在UI](../../dataflows/ui/monitor-sources.md)中监视源数据流的教程。 |

有关数据流的更多常规信息，请参阅[数据流概述](../../dataflows/home.md)。

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | [!DNL LinkedIn Matched Audiences]连接允许您在[!DNL LinkedIn]社交平台中激活受众。 |

有关目标的更多一般信息，请参阅[目标概述](../../destinations/home.md)。

## [!DNL Experience Data Model (XDM) System] {#xdm}

标准化和互操作性是[!DNL Experience Platform]背后的关键概念。 由Adobe驱动的[!DNL Experience Data Model] (XDM)致力于标准化客户体验数据并定义用于客户体验管理的架构。

XDM是一个公开记录的规范，旨在提高数字体验的强大功能。 它为任何应用程序提供通用结构和定义，以便与Adobe Experience Platform上的服务进行通信。 通过遵守XDM标准，所有客户体验数据都可以纳入到通用表示中，从而以更快、更集成的方式提供见解。 您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 已升级搜索UI | 改进搜索功能现在在[!UICONTROL 架构]工作区的[!UICONTROL 浏览]选项卡和[!DNL Schema Editor]中的架构字段组选择对话框中可用。<br><br>以前搜索词时，结果将仅包含名称与搜索查询匹配的XDM资源。 现在，除了名称与查询匹配的资源外，还将包含包含与术语匹配的各个属性的资源。 这允许您根据XDM资源包含的属性而不是资源名称来搜索这些资源。<br><br>有关详细信息，请参阅[浏览XDM资源](../../xdm/ui/explore.md)和[在UI中管理架构](../../xdm/ui/resources/schemas.md)上的文档。 |

有关XDM的更多常规信息，请参阅[XDM系统概述](../../xdm/home.md)。

## [!DNL Identity Service] {#identity}

提供相关的数字体验要求完全了解您的客户。 当您的客户数据分散在不同的系统中，导致每个客户似乎拥有多个“身份”时，就会更加困难。

Adobe Experience Platform [!DNL Identity Service]通过跨设备和系统桥接身份，允许您实时提供有影响力的个人数字体验，从而帮助您更好地了解客户及其行为。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 身份图查看器 | 利用身份图查看器，可验证和可视化在UI中拼合在一起的身份，从而改进调试和透明度。 有关详细信息，请参阅[身份图形查看器文档](../../identity-service/features/identity-graph-viewer.md)。 |

有关[!DNL Identity Service]的更多常规信息，请参阅[Identity Service概述](../../identity-service/home.md)。

## 实时客户轮廓 {#profile}

Adobe Experience Platform 使您能够为客户提供协调、一致且相关的体验，无论他们何时何地与您的品牌互动均是如此。利用实时客户轮廓，您可以看到每个客户的整体视图，其中结合来自多个渠道的数据，包括在线、离线、CRM 和第三方数据。[!DNL Profile]允许您将客户数据整合到一个统一视图中，并提供每个客户交互的带时间戳的可操作帐户。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 计算属性(Alpha) | ***注意：此功能当前为Alpha版，并非对所有用户都可用。 文档和功能可能会发生变化。*** <br/><br/>计算属性是用于将事件级数据聚合到配置文件级属性的函数。 然后，您可以在分段、激活和个性化中使用聚合。 这些函数的一些示例包括count、sum、average、min、max、true/false。 计算属性当前只能通过API使用。 |

有关实时客户个人资料的更多信息，包括用于使用[!DNL Profile]数据的教程和最佳实践，请从阅读[实时客户个人资料概述](../../profile/home.md)开始。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Experience Platform服务来构建、标记和增强这些数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新来源**

| 功能 | 描述 |
| --- | --- |
| [!DNL Google PubSub] | 您现在可以使用[!DNL Flow Service] API或用户界面将[!DNL Google PubSub]连接到[!DNL Experience Platform]。 有关详细信息，请参阅[[!DNL Google PubSub] 连接器概述](../../sources/connectors/cloud-storage/google-pubsub.md)。 |
| [!DNL Oracle Object Storage] | 您现在可以使用[!DNL Flow Service] API或用户界面将[!DNL Oracle Object Storage]连接到[!DNL Experience Platform]。 有关详细信息，请参阅[[!DNL Oracle Object Storage] 连接器概述](../../sources/connectors/cloud-storage/oracle-object-storage.md)。 |

有关源的更多常规信息，请参阅[源概述](../../sources/home.md)。
