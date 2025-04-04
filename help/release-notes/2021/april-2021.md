---
title: Adobe Experience Platform 发行说明（2021 年 4 月）
description: Adobe Experience Platform 的 2021 年 4 月发行说明。
doc-type: release notes
last-update: April 21, 2021
author: ens72741
exl-id: cc78e48a-3578-4c55-ae86-1946d62bddb9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 33%

---

# Adobe Experience Platform 发行说明

**发行日期： 2021年4月21日**

Adobe Experience Platform 中现有功能的更新：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep]允许数据工程师映射、转换和验证与Experience Data Model (XDM)之间的数据。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支持编辑现有数据流的映射 | 您现在可以更新现有数据流的映射集。 无法更新计划一次性摄取的数据流的映射集。 HTTP API、Adobe Analytics、Adobe Audience Manager和[!DNL Marketo Engage]不支持此功能。 有关详细信息，请参阅有关[在UI](../../sources/tutorials/ui/update-dataflows.md)中更新源数据流的教程。 |
| 支持流式摄取 | 现在，在创建流源连接时，可以使用数据准备功能。 有关详细信息，请参阅有关[在UI](../../sources/tutorials/ui/create/streaming/http.md)中创建流源连接的教程。 |

有关详细信息，请参阅[[!DNL Data Prep] 概述](../../data-prep/home.md)。

## [!DNL Experience Data Model (XDM)] {#xdm}

体验数据模型(XDM)是一种开源规范，旨在提高数字体验的强大功能。 它为任何应用程序提供通用结构和定义，以便与Adobe Experience Platform上的服务进行通信。 通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

| 功能 | 描述 |
| --- | --- |
| 按行业划分的架构推荐 | 在架构编辑器UI中选择类和架构字段组时，您可以使用新筛选器根据特定行业查看推荐的标准组件。 请参阅有关[行业数据模型](https://www.adobe.com/go/xdm-industry-erds-en)的文档，以详细了解这些组件在不同行业用例中如何相互关联。 |

## [!DNL Intelligent Services] {#intelligent-services}

智能服务可让营销分析师和从业人员在客户体验用例中利用人工智能和机器学习的功能。 借助此功能，营销分析人员可使用商业级别配置来设置特定于公司需求的预测，而无需具备数据科学专业知识。

### 客户人工智能

Real-Time Customer Data Platform中提供的客户人工智能，用于生成自定义倾向分数，如个人档案大规模的流失和转化情况。 这无需通过将业务需求转变为机器学习问题、选择算法、培训或部署即可完成。

| 功能 | 描述 |
| ------- | ----------- |
| 支持Adobe Analytics数据 | 更新了功能，以通过Analytics Source Connector支持Adobe Analytics数据集，无需ETL您的数据以符合消费者体验事件(CEE)架构。 |
| 支持Adobe Audience Manager数据 | 更新了功能，以通过Adobe Audience Manager源连接器支持Audience Manager数据集，无需ETL您的数据以符合消费者体验事件(CEE)架构。 |
| 模型性能摘要 | Customer AI现在在服务实例分析页面中有一个[模型性能摘要选项卡](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics)。 模型性能选项卡显示所有实际转化率和客户流失率。 这使您能够破译并了解每个倾向区间中发生的变化。 |

有关支持的数据集的更多信息，请参阅[[!DNL Intelligent Services] 数据准备文档](../../intelligent-services/data-preparation.md)。

### 归因人工智能

Attribution AI 用于将点数归因于导致转化事件的接触点。营销人员可利用此功能，促进量化客户历程中每个营销接触点的营销影响。

| 功能 | 描述 |
| ------- | ----------- |
| 支持Adobe Analytics数据 | 更新了功能，以通过Analytics Source Connector支持Adobe Analytics数据集，无需ETL您的数据以符合消费者体验事件(CEE)架构。 |

有关支持的数据集的更多信息，请参阅[[!DNL Intelligent Services] 数据准备文档](../../intelligent-services/data-preparation.md)。

## Segmentation Service {#segmentation}

Adobe Experience Platform Segmentation Service提供了一个用户界面和RESTful API，允许您根据[!DNL Real-Time Customer Profile]数据构建区段并生成受众。 这些区段在Experience Platform上集中配置和维护，可供任何Adobe应用程序轻松访问。

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。区段可以基于记录数据（例如人口统计信息）或代表客户与您的品牌互动的时间序列事件。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 其他聚合函数 | 在区段生成器中添加了计数函数。 计数函数允许您计算指定事件的完成次数。 有关计数函数的更多信息，请参阅[区段生成器指南](../../segmentation/ui/segment-builder.md#count-functions)的计数函数部分 |

有关 [!DNL Segmentation Service] 的详细信息，请查看[分段概述](../../segmentation/home.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Experience Platform服务来构建、标记和增强这些数据。 您可以从各种来源获取数据，例如 Adobe 应用程序、基于云的存储、第三方软件和 CRM 系统。

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

| 功能 | 描述 |
| ------- | ----------- |
| [!DNL Marketo Engage] (Beta) | 您现在可以使用UI创建[!DNL Marketo Engage]源连接以将B2B数据引入Experience Platform，并使用与Experience Platform连接的应用程序使这些数据保持最新。 有关详细信息，请参阅[[!DNL Marketo Engage] 源连接器文档](../../sources/connectors/adobe-applications/marketo/marketo.md)。 |
| Beta源迁移到GA | 以下源已从Beta版升级到GA版： <ul><li>[[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure EventHubs]](../../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../../sources/connectors/streaming/http.md)</li><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL Microsoft SQL Server]](../../sources/connectors/databases/sql-server.md)</li><li>[[!DNL Oracle]](../../sources/connectors/databases/oracle.md)</li></ul> |

要了解有关源的更多信息，请参阅[源概述](../../sources/home.md)。
