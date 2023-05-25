---
title: Adobe Experience Platform发行说明2021年4月
description: Adobe Experience Platform 2021年4月版发行说明。
doc-type: release notes
last-update: April 21, 2021
author: ens72741
exl-id: cc78e48a-3578-4c55-ae86-1946d62bddb9
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 12%

---

# Adobe Experience Platform 发行说明

**发布日期：2021 年 4 月 21 日**

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允许数据工程师映射、转换和验证数据到/传出体验数据模型(XDM)。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支持编辑现有数据流的映射 | 您现在可以更新现有数据流的映射集。 无法更新计划一次性摄取的数据流的映射集。 HTTP API、Adobe Analytics、Adobe Audience Manager和不支持此功能 [!DNL Marketo Engage]. 有关更多信息，请参阅以下教程： [在UI中更新源数据流](../../sources/tutorials/ui/update-dataflows.md). |
| 支持流式摄取 | 现在，您可以在创建流源连接时使用数据准备功能。 有关更多信息，请参阅以下教程： [在UI中创建流源连接](../../sources/tutorials/ui/create/streaming/http.md). |

欲知更多信息，请参见 [[!DNL Data Prep] 概述](../../data-prep/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

体验数据模型(XDM)是一种开源规范，旨在提高数字体验的强大功能。 它为任何应用程序提供通用结构和定义，以便与Adobe Experience Platform上的服务进行通信。 通过遵守XDM标准，所有客户体验数据都可以纳入到通用表示中，从而以更快、更集成的方式提供见解。 您可以从客户操作中获得有价值的见解，通过区段定义客户受众，并将客户属性用于个性化目的。

| 功能 | 描述 |
| --- | --- |
| 按行业列出的架构推荐 | 在架构编辑器UI中选择类和架构字段组时，您可以使用新筛选器根据特定行业查看推荐的标准组件。 请参阅相关文档 [行业数据模型](https://www.adobe.com/go/xdm-industry-erds-en) 以了解有关这些组件在不同行业用例中如何相互关联的更多信息。 |

## [!DNL Intelligent Services] {#intelligent-services}

智能服务可让营销分析师和从业人员在客户体验用例中利用人工智能和机器学习的强大功能。 借助此功能，营销分析人员可使用商业级别配置来设置特定于公司需求的预测，而无需具备数据科学专业知识。

### 客户人工智能

Real-time Customer Data Platform中提供的客户人工智能，用于生成自定义倾向分数，例如大规模单个用户档案的流失和转化率。 这无需通过将业务需求转变为机器学习问题、选择算法、培训或部署即可完成。

| 功能 | 描述 |
| ------- | ----------- |
| 支持Adobe Analytics数据 | 更新了功能，支持通过Analytics Source Connector的Adobe Analytics数据集，无需ETL您的数据以符合使用者体验事件(CEE)架构。 |
| 支持Adobe Audience Manager数据 | 更新了功能，支持通过Audience Manager源连接器的Adobe Audience Manager数据集，无需ETL您的数据以符合消费者体验事件(CEE)架构。 |
| 模型性能摘要 | Customer AI现在拥有 [模型性能摘要选项卡](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics) 在“服务实例分析”页面中。 模型性能选项卡显示所有实际转化率和客户流失率。 这使您能够破译并了解每个倾向桶中发生的情况。 |

有关受支持数据集的更多信息，请参阅 [[!DNL Intelligent Services] 数据准备文档](../../intelligent-services/data-preparation.md).

### 归因人工智能

Attribution AI 用于将点数归因于导致转化事件的接触点。营销人员可利用此功能，促进量化客户旅程中每个营销接触点的营销影响。

| 功能 | 描述 |
| ------- | ----------- |
| 支持Adobe Analytics数据 | 更新了功能，支持通过Analytics Source Connector的Adobe Analytics数据集，无需ETL您的数据以符合使用者体验事件(CEE)架构。 |

有关受支持数据集的更多信息，请参阅 [[!DNL Intelligent Services] 数据准备文档](../../intelligent-services/data-preparation.md).

## 分段服务 {#segmentation}

Adobe Experience Platform Segmentation Service提供了一个用户界面和RESTful API，允许您从构建区段和生成受众。 [!DNL Real-Time Customer Profile] 数据。 这些区段是在Platform上集中配置和维护的，因此任何Adobe应用程序都可以方便地访问它们。

[!DNL Segmentation Service] 通过描述用于区分客户群内可销售人员组的标准，来定义用户档案的特定子集。 区段可以基于记录数据（例如人口统计信息）或表示客户与您的品牌互动的时间系列事件。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 其他聚合函数 | 在区段生成器中添加了计数函数。 计数函数允许您计算指定事件的完成次数。 有关计数函数的更多信息，请参阅 [Segment Builder指南](../../segmentation/ui/segment-builder.md#count-functions) |

有关的详细信息 [!DNL Segmentation Service]，请参阅 [分段概述](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强这些数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)中摄取数据。

Experience Platform提供RESTful API和交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您进行身份验证并连接到外部存储系统和CRM服务，设置引入运行的时间，以及管理数据引入吞吐量。

| 功能 | 描述 |
| ------- | ----------- |
| [!DNL Marketo Engage] (Beta) | 您现在可以创建 [!DNL Marketo Engage] 源连接，使用UI将B2B数据传送到Platform，并使用与平台连接的应用程序使这些数据保持最新。 欲了解更多信息，请参见 [[!DNL Marketo Engage] 源连接器文档](../../sources/connectors/adobe-applications/marketo/marketo.md). |
| Beta版源迁移至GA | 以下源已从Beta版升级到GA版： <ul><li>[[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure EventHubs]](../../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../../sources/connectors/streaming/http.md)</li><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL Microsoft SQL Server]](../../sources/connectors/databases/sql-server.md)</li><li>[[!DNL Oracle]](../../sources/connectors/databases/oracle.md)</li></ul> |

要了解有关源的更多信息，请参阅 [源概述](../../sources/home.md).
