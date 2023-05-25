---
keywords: Experience Platform；主页；热门主题；CJA；Journey Analytics；Customer Journey Analytics；Campaign Orchestration；编排；Customer Journey；Journey Orchestration；功能；地区
title: Adobe Experience Platform端到端示例工作流
description: 大致了解Adobe Experience Platform的基本端到端工作流程。
exl-id: 0a4d3b68-05a5-43ef-bf0d-5738a148aa77
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 3%

---

# Adobe Experience Platform端到端示例工作流

Adobe Experience Platform是市场上功能最强大、最灵活、最开放的系统，用于构建和管理可改善客户体验的完整解决方案。  Platform 让组织可以实现源自任何系统的客户数据和内容的集中化和标准化，并应用数据科学和机器学习来显著改进丰富的个性化体验的设计和交付。

Platform构建于RESTful API之上，向开发人员公开系统的全部功能，支持使用熟悉的工具轻松集成企业解决方案。 Platform允许您通过摄取客户数据、将数据分段到要定位的受众，并将这些受众激活到外部目标来获取客户的整体视图。 以下教程显示了一个端到端的工作流，其中显示了从通过源摄取到通过目标激活受众的所有步骤。

![Experience Platform端到端工作流](./images/end-to-end-tutorial/platform-end-2-end-workflow.png)

## 快速入门

此端到端工作流使用多个Adobe Experience Platform服务。 以下是此工作流中使用的服务列表，其中包含指向这些服务概述的链接：

- [[!DNL Experience Data Model (XDM)]](../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Platform] 组织客户体验数据。 为了更好地利用分段，请确保您的数据被摄取为用户档案和事件，并符合 [数据建模的最佳实践](../xdm/schema/best-practices.md).
- [[!DNL Identity Service]](../identity-service/home.md)：通过跨设备和系统桥接身份，让您全面了解客户及其行为。
- [源](../sources/home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下方式构建、标记和增强传入数据： [!DNL Platform] 服务。
- [[!DNL Segmentation Service]](../segmentation/home.md)： [!DNL Segmentation Service] 允许您划分存储于 [!DNL Experience Platform] 将个人（如客户、潜在客户、用户或组织）关联到较小的组中。
- [[!DNL Real-Time Customer Profile]](../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
- [数据集](../catalog/datasets/overview.md)：用于数据持久化的存储和管理结构 [!DNL Experience Platform].
- [目标](../destinations/home.md)：目标是与常用应用程序预构建的集成，允许从Platform无缝激活数据，用于跨渠道营销活动、电子邮件活动、定向广告和许多其他用例。

## 创建 XDM 架构

将数据摄取到Platform之前，必须首先创建一个XDM架构来描述该数据的结构。 在下一步摄取数据时，您会将传入数据映射到此架构。 要了解如何创建示例XDM架构，请阅读以下教程： [使用架构编辑器创建架构](../xdm/tutorials/create-schema-ui.md).

上述教程将演示如何为架构设置标识字段。 标识字段表示可用于标识与记录或时间序列事件相关的个人人员的字段。 标识字段是在Platform中构建客户标识图的关键组件，最终影响Real-time Customer Profile如何将不同的数据片段合并到一起，从而获得客户的完整视图。 有关如何在Platform中查看身份图的更多详细信息，请参阅关于的教程 [如何使用身份图查看器](../identity-service/ui/identity-graph-viewer.md).

您需要启用架构以便在Real-time Customer Profile中使用，以便可以根据您的架构从数据构建客户配置文件。 请参阅以下部分： [为配置文件启用架构](../xdm/ui/resources/schemas.md#profile) 有关更多信息，请参阅架构UI指南。

## 将数据摄取到Platform

创建XDM架构后，您可以开始将数据引入系统。

所有带入Platform的数据都会在摄取时存储到单独的数据集中。 数据集是映射到特定XDM架构的数据记录集合。 在可以使用您的数据之前， [!DNL Real-Time Customer Profile]，必须专门配置相关数据集。 有关如何为配置文件启用数据集的完整说明，请参阅 [数据集UI指南](../catalog/datasets/user-guide.md#enable-profile) 和 [数据集配置API教程](../profile/tutorials/dataset-configuration.md). 配置数据集后，您可以开始将数据摄取到其中。

Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种源中摄取数据，如 Adobe 应用程序、基于云的存储、数据库和许多其他源。例如，您可以使用来摄取数据 [Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md). 有关可用源的完整列表，请参见 [源连接器概述](../sources/home.md).

如果您使用Amazon S3作为源连接器，则可以按照以下任一API教程中的说明进行操作： [创建Amazon S3连接器](../sources/tutorials/api/create/cloud-storage/s3.md) 或上的用户界面教程 [创建Amazon S3连接器](../sources/tutorials/ui/create/cloud-storage/s3.md) 以了解如何在连接器内创建、连接和摄取数据。

有关源连接器的更多详细说明，请阅读 [源连接器概述](../sources/home.md). 要了解有关流服务的更多信息，请阅读 [流服务API参考](https://www.adobe.io/experience-platform-apis/references/flow-service/).

通过源连接器将您的数据引入Platform并存储在启用了配置文件的数据集后，系统会根据您在XDM架构中配置的身份数据自动创建客户配置文件。

首次将数据上载到新数据集时，或者在设置新的ETL流程或数据源时，建议仔细检查数据，以确保数据已正确上载，并且生成的配置文件包含预期的数据。 有关如何在Platform UI中访问客户配置文件的更多信息，请参阅 [Real-Time Customer Profile用户界面指南](../profile/ui/user-guide.md). 有关如何使用Real-time Customer Profile API访问用户档案的详细信息，请参阅以下指南： [使用实体端点](../profile/api/entities.md).

## 评估数据

从摄取的数据成功生成用户档案后，可以使用分段评估数据。 区段是定义个人资料存储中由一部分人共享的特定属性或行为的过程，以便从客户群中区分出可销售的一组人。 要了解有关分段的更多信息，请阅读 [分段服务概述](../segmentation/home.md).

### 创建区段定义

要开始使用此功能，您必须创建一个区段定义来群集客户，以创建目标受众。 区段定义是可用于定义要定位的受众的规则集合。 要创建区段定义，您可以按照有关使用的 [区段生成器](../segmentation/ui/segment-builder.md) 或上的API教程 [创建区段](../segmentation/tutorials/create-a-segment.md).

创建区段定义后，请确保记下区段定义ID。

### 评估区段定义

创建区段定义后，您可以创建区段作业以将该区段评估为一次性实例，也可以创建计划以持续评估该区段。

要根据需求评估区段定义，您可以创建区段任务。 区段作业是一个异步进程，它会根据引用的区段定义和合并策略创建新的受众区段。 合并策略是Platform使用的一组规则，可确定将使用哪些数据来创建客户配置文件，以及当源之间存在差异时，将优先考虑哪些数据。 要了解如何使用合并策略，请参阅 [合并策略UI指南](../profile/merge-policies/ui-guide.md).

创建并评估区段作业后，您可以获取有关区段的信息，例如受众规模或处理过程中可能发生的错误。 要了解如何创建区段作业（包括您需要提供的所有详细信息），请阅读 [区段作业开发人员指南](../segmentation/api/segment-jobs.md).

要持续评估区段定义，您可以创建和启用计划。 计划是一种可用于在指定时间每天自动运行一次区段作业的工具。 要了解如何创建和启用计划，您可以按照 [计划端点](../segmentation/api/schedules.md).

## 导出评估的数据

在创建一次性区段作业或持续计划后，您可以创建区段导出作业以将结果导出到数据集，也可以将结果导出到目标。 以下部分提供了有关这两种选项的指南。

### 将评估的数据导出到数据集

在创建一次性区段作业或持续计划后，您可以通过创建区段导出作业来导出结果。 区段导出作业是一种异步任务，用于将有关所评估受众的信息发送到数据集。

在创建导出作业之前，必须首先创建一个数据集以将数据导出到。 要了解如何创建数据集，请阅读以下部分： [创建目标数据集](../segmentation/tutorials/evaluate-a-segment.md#create-dataset) 在关于评估区段的教程中，确保您在创建区段后记下数据集ID。 创建数据集后，您可以创建导出作业。 要了解如何创建导出作业，您可以按照 [导出作业端点](../segmentation/api/export-jobs.md).

### 将评估的数据导出到目标

或者，在创建一次性区段作业或持续计划后，您可以将结果导出到目标。 目标是一个端点，例如外部服务上的Adobe应用程序，可以在其中激活和交付受众。 有关可用目标的完整列表，请参阅 [目标目录](../destinations/catalog/overview.md).

有关如何将数据激活到批处理或电子邮件营销目标的说明，请参阅 [如何使用Platform UI将受众数据激活到批量配置文件导出目标](../destinations/ui/activate-batch-profile-destinations.md) 和 [有关如何使用流服务API连接到批处理目标和激活数据的指南](../destinations/api/connect-activate-batch-destinations.md).

## 监控您的Platform数据活动

Platform允许您跟踪如何使用数据流处理数据，数据流表示跨Platform的各种组件移动数据的作业。 这些数据流在不同的服务中配置，有助于将数据从源连接器移动到目标数据集，然后由使用 [!DNL Identity Service] 和 [!DNL Real-Time Customer Profile] 最终被激活到目标之前。 监控仪表板为您提供了数据流历程的可视表示形式。 要了解如何在Platform UI中监测数据流，请参阅上的教程 [监控源的数据流](../dataflows/ui/monitor-sources.md) 和 [监控目标的数据流](../dataflows/ui/monitor-destinations.md).

您还可以通过使用统计指标和事件通知来监控Platform活动 [!DNL Observability Insights]. 您可以通过Platform UI订阅警报通知，或将其发送到配置的webhook。 有关如何从Experience PlatformUI查看、启用、禁用和订阅可用警报的更多详细信息，请参阅 [[!UICONTROL 警报] UI指南](../observability/alerts/ui.md). 有关如何通过Webhook接收警报的详细信息，请参阅 [订阅Adobe I/O事件通知](../observability/alerts/subscribe.md).

## 后续步骤

通过阅读本教程，您已大致了解了适用于Platform的简单端到端流程。 要了解有关Adobe Experience Platform的更多信息，请阅读 [平台概述](./home.md). 要了解有关使用平台UI和平台API的更多信息，请阅读 [Platform UI指南](./ui-guide.md) 和 [平台API指南](./api-guide.md) 的量度。
