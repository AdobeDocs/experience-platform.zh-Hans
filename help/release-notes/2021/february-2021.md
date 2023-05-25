---
title: Adobe Experience Platform发行说明2021年2月
description: Adobe Experience Platform 2021年2月版发行说明。
doc-type: release notes
last-update: February 24, 2021
author: ens70167
exl-id: 8c3142af-4021-4f7e-acbd-c5277dd188d1
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发行日期：2021 年 2 月 24 日**

Adobe Experience Platform中的新增功能：

- [(Beta)功能板](#dashboards)

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## (Beta)功能板 {#dashboards}

Adobe Experience Platform提供了多个功能板，您可以通过该功能板查看有关贵组织数据的重要信息，如在每日快照期间捕获的数据。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 配置文件、区段、目标和许可证使用功能板（测试版） | **注意：功能板功能当前为测试版，并非对所有用户都可用。 文档和功能可能会发生变化。**<br/><br/>&#x200B;功能板提供有关组织数据的现成报告，并且直接内置到Platform中的营销人员工作流程中。 无需额外的IT支持，也不必花时间和精力通过额外的数据仓库设计和实施导出和处理数据，即可使用这些功能板。 |

## [!DNL Data Science Workspace] {#dsw}

数据科学工作区使用机器学习和人工智能从您的数据创建见解。 数据科学工作区集成到Adobe Experience Platform中，可帮助您跨Adobe解决方案使用内容和数据资源做出预测。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| JupyterLab EDA笔记本 | Jupyterlab现已提供Exploration Data Analysis (EDA) Python笔记本。 此笔记本旨在帮助您发现数据模式、检查数据健全度并总结预测模型的相关数据。 请参阅上的教程 [探索基于Web的数据以获取预测模型](../../data-science-workspace/jupyterlab/eda-notebook.md) 了解更多信息。 |

有关数据科学工作区的更多常规信息，请参阅 [数据科学工作区概述](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

在Adobe Experience Platform中，数据从各种来源摄取，在Experience Platform中进行分析，并激活到各种目的地。 Platform通过提供数据流透明性，使跟踪这种潜在非线性数据流的过程更加容易。

数据流是跨平台移动数据的数据作业的表示方法。这些数据流在不同的服务中配置，有助于将数据从源连接器移动到目标数据集，然后由使用 [!DNL Identity Service] 和 [!DNL Real-Time Customer Profile] 最终激活到 [!DNL Destinations].

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 新的监视仪表板 | 您现在可以使用监视仪表板实现跨服务透明度和对源数据摄取的可操作性洞察。 新的监视仪表板全面查看从处理过的数据 [!DNL Data Lake] 到 [!DNL Identity Service] 和 [!DNL Profile]，同时还允许您监控摄取率、成功和失败。 请参阅上的教程 [在UI中监控源数据流](../../dataflows/ui/monitor-sources.md) 了解更多信息。 |

有关数据流的更多常规信息，请参阅 [数据流概述](../../dataflows/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是与目标平台预建的集成，允许从Adobe Experience Platform无缝激活数据。 您可以使用目标为跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例激活已知和未知数据。

**新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | 此 [!DNL LinkedIn Matched Audiences] 连接允许您在中激活受众 [!DNL LinkedIn] 社交平台。 |

有关目标的更多常规信息，请参阅 [目标概述](../../destinations/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

标准化和互操作性是背后的关键概念 [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM)由Adobe驱动，致力于标准化客户体验数据并定义用于客户体验管理的架构。

XDM是一个公开记录的规范，旨在提高数字体验的强大功能。 它为任何应用程序提供通用结构和定义，以便与Adobe Experience Platform上的服务进行通信。 通过遵守XDM标准，所有客户体验数据都可以纳入到通用表示中，从而以更快、更集成的方式提供见解。 您可以从客户操作中获得有价值的见解，通过区段定义客户受众，并将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 已升级搜索UI | 现在，中提供了改进的搜索功能 [!UICONTROL 浏览] 在中选项卡 [!UICONTROL 架构] 工作区中的“架构字段组选择”对话框 [!DNL Schema Editor].<br><br>以前搜索术语时，结果将仅包含名称与搜索查询匹配的XDM资源。 现在，除了名称与查询匹配的资源外，还将包含包含与术语匹配的各个属性的资源。 这样，您就可以根据XDM资源包含的属性而不是资源名称来搜索这些资源。<br><br>查看文档 [探索XDM资源](../../xdm/ui/explore.md) 和 [管理架构](../../xdm/ui/resources/schemas.md) （在UI中）以了解更多信息。 |

有关XDM的更多常规信息，请参阅 [XDM系统概述](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

提供相关的数字体验需要全面了解您的客户。 当您的客户数据分散在不同的系统上，导致每个客户似乎都有多个“身份”时，就会使这一点变得更加困难。

Adobe Experience Platform [!DNL Identity Service] 通过跨设备和系统桥接身份，允许您实时提供有影响力的个人数字体验，帮助您更好地了解客户及其行为。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 身份图查看器 | 通过身份图查看器，您可以验证和可视化在UI中拼接在一起的身份，从而改进调试和透明度。 请参阅 [身份图查看器文档](../../identity-service/ui/identity-graph-viewer.md) 了解更多信息。 |

有关以下内容的更多常规信息： [!DNL Identity Service]，请参阅 [Identity服务概述](../../identity-service/home.md).

## 实时客户资料 {#profile}

通过Adobe Experience Platform，无论客户在何处或何时与您的品牌互动，您都可以为其推动协调、一致且相关的体验。 利用实时客户档案，您可以查看合并了来自多个渠道（包括在线、离线、CRM和第三方数据）的数据的每个单个客户的整体视图。 [!DNL Profile] 允许您将客户数据整合到一个统一的视图中，并提供每个客户交互的带时间戳的可操作帐户。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 计算属性(Alpha) | ***注意：此功能当前为Alpha版，并非对所有用户都可用。 文档和功能可能会发生变化。*** <br/><br/>计算属性是用于将事件级数据聚合到配置文件级属性的函数。 然后，您可以在分段、激活和个性化中使用聚合。 这些函数的一些示例包括count、sum、average、min、max、true/false。 计算属性当前只能通过API使用。 |

有关Real-Time Customer Profile的更多信息，包括有关使用的教程和最佳实践 [!DNL Profile] 数据，请首先阅读 [Real-time Customer Profile概述](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强这些数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)中摄取数据。

Experience Platform提供RESTful API和交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您进行身份验证并连接到外部存储系统和CRM服务，设置引入运行的时间，以及管理数据引入吞吐量。

**新源**

| 功能 | 描述 |
| --- | --- |
| [!DNL Google PubSub] | 您现在可以连接 [!DNL Google PubSub] 到 [!DNL Experience Platform] 使用 [!DNL Flow Service] API或用户界面。 请参阅 [[!DNL Google PubSub] 连接器概述](../../sources/connectors/cloud-storage/google-pubsub.md) 了解更多信息。 |
| [!DNL Oracle Object Storage] | 您现在可以连接 [!DNL Oracle Object Storage] 到 [!DNL Experience Platform] 使用 [!DNL Flow Service] API或用户界面。 请参阅 [[!DNL Oracle Object Storage] 连接器概述](../../sources/connectors/cloud-storage/oracle-object-storage.md) 了解更多信息。 |

有关源的更多常规信息，请参阅 [源概述](../../sources/home.md).
