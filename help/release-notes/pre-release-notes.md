---
title: Experience Platform预发行说明
description: Adobe Experience Platform最新发行说明预览。
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: acb8303673c3271794dcda87b149b473328a7a21
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 24%

---

# Adobe Experience Platform预发行说明

>[!IMPORTANT]
>
>本文档旨在作为当月发行说明的&#x200B;**预览**。 版本项目可能会发生更改，并且可能会在最终版本中添加或删除。

>[!TIP]
>
>有关其他 Adobe Experience Platform 应用程序的发行说明，请参阅以下文档：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/releases/pre-release-notes)
>- [联合受众构成](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hans/docs/real-time-cdp-collaboration/using/latest)

**发行日期：2026年1月**

Adobe Experience Platform 中新功能和现有功能的更新：

- [Agent Orchestrator](#agent-orchestrator)
- [目标](#destinations)
- [实时客户轮廓](#real-time-customer-profile)
- [架构](#schemas)
- [Segmentation Service](#segmentation-service)
- [源](#sources)

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator允许您构建和部署支持AI的代理，这些代理可以自动执行工作流并在多个渠道上与客户进行交互。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| Agent Orchestrator的试用动议 | Agent Orchestrator现在提供试用方案，允许客户在承诺完全购买之前探索和测试该服务。 这一先试后买选项使组织能够在自己的环境中评估Agent Orchestrator的功能，包括技能和编排功能。 该试用版提供了构建AI支持的代理以及了解如何将其集成到现有工作流中的实践体验。 |

{style="table-layout:auto"}

有关详细信息，请参阅[Agent Orchestrator文档](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator)。

## 目标 {#destinations}

[!DNL Destinations] 是预建的与目标平台的集成，可实现从 Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例。

**新增或更新的功能**

| 功能 | 描述 |
| --- | --- |
| 更新了Adobe Target目标的护栏限制 | 可以映射到单个Adobe Target目标的受众的最大数量已从50增至250。 这使Adobe Target与其他目标的标准受众限制保持一致，从而提供了更大的受众激活工作流灵活性。 客户现在可以将更多受众激活到Adobe Target目标，而无需创建多个数据流。 |

{style="table-layout:auto"}

有关更多信息，请阅读[目标概述](../destinations/home.md)。

## 实时客户轮廓 {#real-time-customer-profile}

实时客户配置文件允许您通过组合来自多个渠道的数据（包括在线、离线、CRM和第三方数据）来查看每个客户的整体视图。 用户档案允许您将客户数据整合到一个统一视图中，并提供每个客户交互的带时间戳的可操作帐户。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 流容量实施 | Experience Platform现在为Real-time Customer Profile和Identity Service强制执行流式处理吞吐量功能。 当客户超过其合同规定的流容量时，数据将以“先进先出”的方式排队和处理。 这可以确保可预测的系统性能，并防止容量违规影响数据摄取质量。 重要说明：超出容量时，流更新插入在数据湖中不可用，此强制实施不适用于具有Adobe Journey Optimizer许可证的客户，排队的数据将在容量可用时按顺序处理。 |
| 弃用Real-Time CDP Prime的API访问 | 现已为所有Real-Time CDP Prime客户弃用针对体验事件的API访问。 此更改会影响直接通过API查询体验事件的能力。 Real-Time CDP Ultimate客户可以通过正式的例外流程请求例外，以便在其用例需要时启用体验事件API访问。 此弃用可帮助优化系统性能，并遵循数据访问模式的最佳实践。 |
| 监测数据流运行 | 您现在可以在Profile中监视数据流运行的进度和就绪性。 |

{style="table-layout:auto"}

有关详细信息，请参阅 [[!DNL Real-Time Customer Profile]  概述](../profile/home.md)。

## 架构 {#schemas}

Experience Platform使用架构，以一致且可重用的方式描述数据结构。 通过在系统中以一致的方式定义数据，更容易保留含义并因此从数据中获取价值。 架构由一个基类以及零个或多个架构字段组组成。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 使用搜索、筛选、标记和文件夹实现架构库存现代化 | 架构浏览页面已进行现代化改造，可提供增强的组织和发现功能。 新增功能包括高级搜索和筛选选项，支持用户生成的标记和文件夹来组织架构，以及内联操作来简化工作流。 关键改进包括：更新了列（名称、类、数据集、身份、关系、启用配置文件、行为、架构类型、标记、创建日期、上次修改）、高级过滤器（显示配置文件、架构类型、类、具有任何标记、创建者、创建日期、修改日期、具有主身份、具有关系、主身份命名空间）、内联操作（编辑、删除、应用标签、为非关系架构创建数据集、管理标记、移动到文件夹、添加到包、复制JSON结构、下载示例文件）以及组织能力使用标记和文件夹的架构。 这些增强功能提供了对架构资源的全面可视性，并支持在沙盒级别进行更高效的架构管理。 |

有关详细信息，请参阅 [[!DNL Schemas]  概述](../xdm/home.md)。

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。受众可以基于记录型数据（如人口统计信息）或时间序列事件（代表客户与品牌的互动行为）进行构建。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 流式分段监控 | 流式客户细分的实时监控在沙盒、数据集和受众级别提供了评估率、延迟和数据质量量度的透明度。 该功能支持主动预警和可操作的洞察，以帮助数据工程师识别容量违规和摄取问题。监测指标包括评估率、P95摄取延迟以及接收、评估、失败和跳过的记录。 逐个数据集查看和逐个受众查看功能可全面查看符合条件或被取消资格的净新用户档案。 |
| 外部受众TTL刷新 | 外部受众（例如CSV上传）现在支持对生存时间(TTL)设置进行强制刷新功能。 此功能允许用户手动刷新外部受众的TTL过期，从而更好地控制受众生命周期管理。 这对于需要在初始TTL时间段后持续存在或需要重新激活而不重新上传数据的受众特别有用。 |

有关详细信息，请参阅 [[!DNL Segmentation Service]  概述](../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新源或已更新的源**

| 来源 | 描述 |
| --- | --- |
| [!DNL Oracle Eloqua] V2源 | 新的[!DNL Oracle Eloqua]源连接器现已可用，它取代了已弃用的连接器。 此更新的连接器增强了从[!DNL Oracle Eloqua]将数据摄取到Experience Platform中的功能和可靠性。 使用现有连接器的客户应迁移到新实施，因为现有连接将无法再正常运行。 新连接器支持连接到[!DNL Oracle Eloqua]并摄取营销自动化数据所需的所有设置和配置步骤。 |
| [!DNL Salesforce Marketing Cloud] V2源 | 新的[!DNL Salesforce Marketing Cloud]源连接器现已可用，它取代了已弃用的连接器。 此更新的连接器提高了性能，并为将数据从[!DNL Salesforce Marketing Cloud]摄取到Experience Platform提供了其他功能。 使用现有连接器的客户应过渡到新实施。 新连接器包含用于连接到[!DNL Salesforce Marketing Cloud]和摄取营销自动化数据的全面设置说明。 |

有关更多信息，请阅读[来源概述](../sources/home.md)。

