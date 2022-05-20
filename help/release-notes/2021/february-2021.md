---
title: Adobe Experience Platform发行说明2021年2月
description: 2021年2月版Adobe Experience Platform发行说明。
doc-type: release notes
last-update: February 24, 2021
author: ens70167
exl-id: 8c3142af-4021-4f7e-acbd-c5277dd188d1
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发行日期：2021 年 2 月 24 日**

Adobe Experience Platform的新增功能：

- [（测试版）功能板](#dashboards)

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## （测试版）功能板 {#dashboards}

Adobe Experience Platform提供了多个功能板，您可以通过这些功能板查看有关贵组织数据的重要信息（在每日快照期间捕获）。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 配置文件、区段、目标和许可证使用功能板（测试版） | **注意：功能板功能目前处于测试阶段，并非所有用户都能使用。 文档和功能可能会发生变化。**<br/><br/>&#x200B;功能板提供有关贵组织数据的现成报表，并直接内置到平台内的营销人员工作流程中。 这些功能板可用，无需额外的IT支持，也无需花费时间和精力，即可通过额外的数据仓库设计和实施导出和处理数据。 |

## [!DNL Data Science Workspace] {#dsw}

数据科学工作区使用机器学习和人工智能从您的数据中创建分析。 Data Science Workspace集成到Adobe Experience Platform中，可帮助您跨Adobe解决方案使用内容和数据资产进行预测。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| JupyterLab EDA笔记本 | 探索性数据分析(EDA)Python笔记本现已在Jupyterlab中提供。 本笔记本旨在帮助您发现数据模式、检查数据健全性并总结预测模型的相关数据。 请参阅 [浏览基于web的数据以建立预测模型](../../data-science-workspace/jupyterlab/eda-notebook.md) 以了解更多信息。 |

有关数据科学工作区的更多常规信息，请参阅 [数据科学工作区概述](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

在Adobe Experience Platform中，从各种来源摄取数据，在Experience Platform内进行分析，并激活到各种不同的目标。 Platform通过提供数据流的透明度，使跟踪这种潜在的非线性数据流的过程变得更加容易。

数据流是跨平台移动数据的数据作业的表示方法。这些数据流是跨不同的服务配置的，有助于将数据从源连接器移动到目标数据集，然后数据集会被利用 [!DNL Identity Service] 和 [!DNL Real-time Customer Profile] 最终激活 [!DNL Destinations].

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 新的监控仪表板 | 您现在可以使用监控仪表板实现跨服务透明度，并可为源数据摄取提供可操作的分析。 新的监控功能板提供了从 [!DNL Data Lake] to [!DNL Identity Service] 和 [!DNL Profile]，同时还允许您监控摄取率、成功和失败。 请参阅 [监控UI中的源数据流](../../dataflows/ui/monitor-sources.md) 以了解更多信息。 |

有关数据流的更多常规信息，请参阅 [数据流概述](../../dataflows/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是与目标平台的预建集成，可无缝激活来自Adobe Experience Platform的数据。 您可以使用目标来激活跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例的已知和未知数据。

**新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | 的 [!DNL LinkedIn Matched Audiences] 通过连接，可在 [!DNL LinkedIn] 社交平台。 |

有关目标的更多常规信息，请参阅 [目标概述](../../destinations/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

标准化和互操作性是其背后的关键概念 [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM)在Adobe的驱动下，努力标准化客户体验数据并定义客户体验管理架构。

XDM是一项公开记录的规范，旨在提高数字体验的强大功能。 它为任何与Adobe Experience Platform上的服务通信的应用程序提供了通用结构和定义。 通过遵循XDM标准，所有客户体验数据都可以整合到通用呈现形式中，以更快、更集成的方式提供洞察。 您可以从客户操作中获得有价值的分析，通过区段定义客户受众，以及将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 升级了搜索UI | 现在， [!UICONTROL 浏览] 选项卡 [!UICONTROL 模式] 工作区和架构字段组选择对话框(位于 [!DNL Schema Editor].<br><br>在以前搜索术语时，结果将仅包含名称与搜索查询匹配的XDM资源。 现在，除了名称与查询匹配的资源之外，还将包含包含与术语匹配的单个属性的资源。 这允许您根据XDM资源包含的属性而不是资源名称来搜索XDM资源。<br><br>请参阅 [浏览XDM资源](../../xdm/ui/explore.md) 和 [管理模式](../../xdm/ui/resources/schemas.md) ，以了解更多信息。 |

有关XDM的更多常规信息，请参阅 [XDM系统概述](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

提供相关的数字体验需要全面了解您的客户。 当客户数据在不同的系统中分散，导致每个客户似乎都具有多个“身份”时，这会使操作愈发困难。

Adobe Experience Platform [!DNL Identity Service] 通过跨设备和系统桥接身份，使您能够实时提供有影响的个人数字体验，从而帮助您更好地了解客户及其行为。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 身份图查看器 | 通过身份图查看器，您可以验证和可视化在UI中拼合在一起的身份，从而改进调试和透明度。 请参阅 [identity graph查看器文档](../../identity-service/ui/identity-graph-viewer.md) 以了解更多信息。 |

有关 [!DNL Identity Service]，请参阅 [Identity Service概述](../../identity-service/home.md).

## 实时客户个人资料 {#profile}

Adobe Experience Platform使您能够为客户在何处或何时与您的品牌进行交互，从而提供协调、一致的相关体验。 通过实时客户资料，您可以查看每个客户的整体视图，该视图将来自多个渠道的数据（包括在线、离线、CRM和第三方数据）进行整合。 [!DNL Profile] 允许您将客户数据整合到统一视图中，为每次客户交互提供一个可操作且带有时间戳的帐户。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 计算属性(Alpha) | ***注意：此功能当前位于alpha中，并非所有用户都可用。 文档和功能可能会发生变化。*** <br/><br/>计算属性是用于将事件级别数据聚合到配置文件级别属性中的函数。 然后，您可以在分段、激活和个性化中使用聚合。 这些函数的一些示例包括计数、总和、平均、最小、最大、true/false。 计算属性当前仅通过API可用。 有关更多信息，请参阅 [计算属性概述](../../profile/computed-attributes/overview.md). |

有关实时客户资料的更多信息，包括与 [!DNL Profile] 数据，请首先阅读 [实时客户资料概述](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**新来源**

| 功能 | 描述 |
| --- | --- |
| [!DNL Google PubSub] | 您现在可以连接 [!DNL Google PubSub] to [!DNL Experience Platform] 使用 [!DNL Flow Service] API或UI。 请参阅 [[!DNL Google PubSub] 连接器概述](../../sources/connectors/cloud-storage/google-pubsub.md) 以了解更多信息。 |
| [!DNL Oracle Object Storage] | 您现在可以连接 [!DNL Oracle Object Storage] to [!DNL Experience Platform] 使用 [!DNL Flow Service] API或UI。 请参阅 [[!DNL Oracle Object Storage] 连接器概述](../../sources/connectors/cloud-storage/oracle-object-storage.md) 以了解更多信息。 |

有关来源的更多常规信息，请参阅 [源概述](../../sources/home.md).
