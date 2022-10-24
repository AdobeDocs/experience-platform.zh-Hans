---
title: Adobe Experience Platform发行说明2021年4月
description: 2021年4月版Adobe Experience Platform发行说明。
doc-type: release notes
last-update: April 21, 2021
author: ens72741
exl-id: cc78e48a-3578-4c55-ae86-1946d62bddb9
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 10%

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

[!DNL Data Prep] 允许数据工程师在体验数据模型(XDM)之间映射、转换和验证数据。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支持编辑现有数据流的映射 | 您现在可以更新现有数据流的映射集。 您无法更新计划一次性摄取的数据流的映射集。 HTTP API、Adobe Analytics、Adobe Audience Manager和 [!DNL Marketo Engage]. 有关更多信息，请参阅 [在UI中更新源数据流](../../sources/tutorials/ui/update-dataflows.md). |
| 支持流式引入 | 现在，您可以在创建流源连接时使用数据准备函数。 有关更多信息，请参阅 [在UI中创建流源连接](../../sources/tutorials/ui/create/streaming/http.md). |

有关详细信息，请参阅 [[!DNL Data Prep] 概述](../../data-prep/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

体验数据模型(XDM)是一项开源规范，旨在提高数字体验的功能。 它为任何与Adobe Experience Platform上的服务通信的应用程序提供了通用结构和定义。 通过遵循XDM标准，可以将所有客户体验数据纳入到通用的表示形式中，以更快、更集成的方式提供洞察。 您可以从客户操作中获得有价值的分析，通过区段定义客户受众，以及将客户属性用于个性化目的。

| 功能 | 描述 |
| --- | --- |
| 按行业划分的模式建议 | 在架构编辑器UI中选择类和架构字段组时，您可以使用新的过滤器根据您的特定行业查看推荐的标准组件。 请参阅 [行业数据模型](https://www.adobe.com/go/xdm-industry-erds-en) 有关不同行业用例中这些组件如何彼此关联的更多信息。 |

## [!DNL Intelligent Services] {#intelligent-services}

“智能服务”使营销分析师和从业人员能够在客户体验用例中利用人工智能和机器学习的强大功能。 这允许营销分析人员使用业务级别配置来设置特定于公司需求的预测，而无需具备数据科学专业知识。

### 客户人工智能

Real-time Customer Data Platform中提供的Customer AI用于生成自定义倾向得分，例如个人档案的大规模流失率和转化。 这无需通过将业务需求转变为机器学习问题、选择算法、培训或部署即可完成。

| 功能 | 描述 |
| ------- | ----------- |
| 支持Adobe Analytics数据 | 更新了功能，以便通过Analytics源连接器支持Adobe Analytics数据集，而无需对数据执行ETL操作，以符合消费者体验事件(CEE)架构。 |
| 支持Adobe Audience Manager数据 | 更新了功能，可通过Audience Manager源连接器支持Adobe Audience Manager数据集，而无需对数据执行ETL操作，以符合消费者体验事件(CEE)架构。 |
| 模型性能摘要 | 客户人工智能现在具有 [模型性能摘要选项卡](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics) 在服务实例分析页面中。 “模型性能”选项卡显示所有实际的转化率和流失率。 这样，您就可以解密并了解每个倾向存储段中所发生的情况。 |

有关受支持数据集的更多信息，请参阅 [[!DNL Intelligent Services] 数据准备文档](../../intelligent-services/data-preparation.md).

### 归因人工智能

Attribution AI 用于将点数归因于导致转化事件的接触点。营销人员可利用此功能，促进量化客户旅程中每个营销接触点的营销影响。

| 功能 | 描述 |
| ------- | ----------- |
| 支持Adobe Analytics数据 | 更新了功能，以便通过Analytics源连接器支持Adobe Analytics数据集，而无需对数据执行ETL操作，以符合消费者体验事件(CEE)架构。 |

有关受支持数据集的更多信息，请参阅 [[!DNL Intelligent Services] 数据准备文档](../../intelligent-services/data-preparation.md).

## 分段服务 {#segmentation}

Adobe Experience Platform Segmentation Service提供了用户界面和RESTful API，允许您从 [!DNL Real-time Customer Profile] 数据。 这些区段在平台上进行集中配置和维护，使任何Adobe应用程序都可轻松访问它们。

[!DNL Segmentation Service] 通过描述区分客户群中可销售人群的标准来定义特定的用户档案子集。 区段可以基于记录数据（如人口统计信息）或表示客户与您的品牌交互的时间序列事件。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 其他聚合函数 | 区段生成器中已添加计数函数。 利用计数函数，可计算指定事件完成的次数。 有关计数函数的更多信息，请参阅 [区段生成器指南](../../segmentation/ui/segment-builder.md#count-functions) |

有关 [!DNL Segmentation Service]，请参阅 [分段概述](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

| 功能 | 描述 |
| ------- | ----------- |
| [!DNL Marketo Engage] （测试版） | 您现在可以创建 [!DNL Marketo Engage] 源连接使用UI将B2B数据引入平台，并使用与平台连接的应用程序保持此数据最新。 有关更多信息，请参阅 [[!DNL Marketo Engage] 源连接器文档](../../sources/connectors/adobe-applications/marketo/marketo.md). |
| 测试版源迁移至GA | 以下来源已从测试版提升为正式发布： <ul><li>[[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure EventHubs]](../../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../../sources/connectors/streaming/http.md)</li><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL Microsoft SQL Server]](../../sources/connectors/databases/sql-server.md)</li><li>[[!DNL Oracle]](../../sources/connectors/databases/oracle.md)</li></ul> |

要进一步了解源，请参阅 [源概述](../../sources/home.md).
