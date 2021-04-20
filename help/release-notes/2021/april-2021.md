---
title: Adobe Experience Platform 发行说明
description: Experience Platform 2021年4月21日发行说明。
doc-type: release notes
last-update: April 21, 2021
author: ens72741
translation-type: tm+mt
source-git-commit: 73ecf6e6f9796088e2d14f9dc3d9667104b22a8e
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 14%

---


# Adobe Experience Platform 发行说明

**发行日期：2021 年 4 月 21 日**

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允许数据工程师在体验数据模型(XDM)之间映射、转换和验证数据。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支持编辑现有数据流的映射 | 您现在可以更新现有数据流的映射集。 无法更新为一次性摄取计划的数据流的映射集。 HTTP API、Adobe Analytics、Adobe Audience Manager和[!DNL Marketo Engage]不支持此功能。 有关详细信息，请参阅有关[更新UI](../../sources/tutorials/ui/update-dataflows.md)中的源数据流的教程。 |
| 支持流摄取 | 现在，您可以在创建流源连接时使用数据准备函数。 有关详细信息，请参阅有关在UI](../../sources/tutorials/ui/create/streaming/http.md)中创建流源连接的教程。[ |

有关详细信息，请参阅[[!DNL Data Prep] 概述](../../data-prep/home.md)。

## [!DNL Intelligent Services] {#intelligent-services}

智能服务使营销分析师和从业人员能够在客户体验使用案例中利用人工智能和机器学习的强大功能。 这使营销分析师能够使用业务级配置设置特定于公司需求的预测，而无需数据科学专业知识。

### 客户人工智能

实时客户数据平台中提供的客户人工智能用于生成自定义倾向得分，如大规模订购和转化个别用户档案。 这无需通过将业务需求转变为机器学习问题、选择算法、培训或部署即可完成。

| 功能 | 描述 |
| ------- | ----------- |
| 支持Adobe Analytics数据 | 更新了功能，可通过Analytics源连接器支持Adobe Analytics数据集，无需ETL数据以符合消费者体验事件(CEE)模式。 |
| 支持Adobe Audience Manager数据 | 更新了功能，可通过Audience Manager源连接器支持Adobe Audience Manager数据集，无需ETL数据即可符合消费者体验事件(CEE)模式。 |
| 模型性能摘要 | 客户AI现在在服务实例分析页面中有一个[模型性能摘要选项卡](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics)。 “模型性能”选项卡显示所有实际转化率和客户流失率。 这使您能够解读和了解每个倾向桶中的情况。 |

有关受支持数据集的详细信息，请参阅[[!DNL Intelligent Services] 数据准备文档](../../intelligent-services/data-preparation.md)。

### Attribution AI

Attribution AI 用于将点数归因于导致转化事件的接触点。营销人员可利用此功能，促进量化客户旅程中每个营销接触点的营销影响。

| 功能 | 描述 |
| ------- | ----------- |
| 支持Adobe Analytics数据 | 更新了功能，可通过Analytics源连接器支持Adobe Analytics数据集，无需ETL数据以符合消费者体验事件(CEE)模式。 |

有关受支持数据集的详细信息，请参阅[[!DNL Intelligent Services] 数据准备文档](../../intelligent-services/data-preparation.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源收集数据，同时允许您使用平台服务构建、标记和增强该数据。 您可以从各种来源收集数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松为各种数据提供者设置源连接。 这些源连接允许您对外部存储系统和CRM服务进行身份验证并连接，设置获取运行的时间，以及管理数据获取吞吐量。

| 功能 | 描述 |
| ------- | ----------- |
| [!DNL Marketo Engage] （测试版） | 您现在可以使用UI创建[!DNL Marketo Engage]源连接，以将B2B数据引入平台，并使用连接到平台的应用程序保持此数据最新。 有关详细信息，请参阅[[!DNL Marketo Engage] 源连接器文档](../../sources/connectors/adobe-applications/marketo/marketo.md)。 |

要了解有关源的详细信息，请参阅[源概述](../../sources/home.md)。
