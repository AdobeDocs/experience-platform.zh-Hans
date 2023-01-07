---
keywords: Experience Platform；主页；热门主题；CJA;journey analytics；客户历程分析；促销活动编排；编排；客户历程；历程；历程编排；功能；区域
title: Adobe Experience Platform端到端示例工作流
description: 了解Adobe Experience Platform的基本端到端工作流程（高级）。
exl-id: 0a4d3b68-05a5-43ef-bf0d-5738a148aa77
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 3%

---

# Adobe Experience Platform端到端示例工作流

Adobe Experience Platform是市场上功能最强大、最灵活、最开放的系统，用于构建和管理可推动客户体验的完整解决方案。  Platform 让组织可以实现源自任何系统的客户数据和内容的集中化和标准化，并应用数据科学和机器学习来显著改进丰富的个性化体验的设计和交付。

基于RESTful API，Platform向开发人员提供了系统的完整功能，支持使用熟悉的工具轻松集成企业解决方案。 Platform允许您通过以下方式获得客户的整体视图：摄取客户数据，将数据分段到要定位的受众，并将这些受众激活到外部目标。 以下教程将演示一个端到端工作流，其中显示了从通过源摄取到通过目标激活受众的所有步骤。

![Experience Platform端到端工作流](./images/end-to-end-tutorial/platform-end-2-end-workflow.png)

## 快速入门

此端到端工作流使用多个Adobe Experience Platform服务。 以下是此工作流中使用的服务列表，其概述链接包括：

- [[!DNL Experience Data Model (XDM)]](../xdm/home.md):标准化框架， [!DNL Platform] 组织客户体验数据。 为了最好地利用分段，请确保根据 [数据建模最佳实践](../xdm/schema/best-practices.md).
- [[!DNL Identity Service]](../identity-service/home.md):通过跨设备和系统桥接身份，全面了解客户及其行为。
- [源](../sources/home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
- [[!DNL Segmentation Service]](../segmentation/home.md): [!DNL Segmentation Service] 允许您将存储在 [!DNL Experience Platform] 与属于较小群组的个人（例如客户、潜在客户、用户或组织）相关。
- [[!DNL Real-Time Customer Profile]](../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
- [数据集](../catalog/datasets/overview.md):中数据持久性的存储和管理结构 [!DNL Experience Platform].
- [目标](../destinations/home.md):目标是与常用应用程序的预建集成，允许从平台无缝激活数据以用于跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例。

## 创建 XDM 架构

在将数据摄取到平台中之前，必须先创建一个XDM架构以描述该数据的结构。 在下一步中摄取数据时，您会将传入数据映射到此架构。 要了解如何创建XDM模式示例，请阅读 [使用模式编辑器创建模式](../xdm/tutorials/create-schema-ui.md).

上述教程将演示如何为架构设置标识字段。 标识字段表示一个字段，可用于标识与记录或时间系列事件相关的个人人员。 身份字段是在Platform中构建客户身份图形的关键组件，这最终会影响实时客户资料如何将不同的数据片段合并在一起，以获得客户的完整视图。 有关如何在Platform中查看身份图形的更多详细信息，请参阅 [如何使用身份图查看器](../identity-service/ui/identity-graph-viewer.md).

您需要启用架构以在实时客户用户档案中使用，以便能够根据您的架构根据数据构建客户用户档案。 请参阅 [为用户档案启用模式](../xdm/ui/resources/schemas.md#profile) 有关更多信息，请参阅架构UI指南。

## 将数据摄取到平台

创建XDM架构后，您便可以开始将数据导入系统。

引入Platform的所有数据都会在摄取时存储到单个数据集。 数据集是映射到特定XDM架构的数据记录集合。 在数据可供使用之前 [!DNL Real-Time Customer Profile]，则必须专门配置相关数据集。 有关如何为配置文件启用数据集的完整说明，请参阅 [数据集UI指南](../catalog/datasets/user-guide.md#enable-profile) 和 [数据集配置API教程](../profile/tutorials/dataset-configuration.md). 配置数据集后，您可以开始向其中摄取数据。

Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种源中摄取数据，如 Adobe 应用程序、基于云的存储、数据库和许多其他源。例如，您可以使用 [Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md). 可在 [源连接器概述](../sources/home.md).

如果您使用Amazon S3作为源连接器，则可以按照 [创建Amazon S3连接器](../sources/tutorials/api/create/cloud-storage/s3.md) 或上的UI教程 [创建Amazon S3连接器](../sources/tutorials/ui/create/cloud-storage/s3.md) 了解如何在连接器中创建、连接和摄取数据。

有关源连接器的更多详细说明，请阅读 [源连接器概述](../sources/home.md). 要了解有关流量服务（源所基于的API）的更多信息，请阅读 [流量服务API参考](https://www.adobe.io/experience-platform-apis/references/flow-service/).

在通过源连接器将数据引入Platform并存储到启用了配置文件的数据集中后，系统会根据您在XDM架构中配置的身份数据自动创建客户配置文件。

首次将数据上传到新数据集时，或在设置新的ETL流程或数据源时，建议仔细检查数据，以确保数据已正确上传，并且生成的配置文件包含您预期的数据。 有关如何在Platform UI中访问客户用户档案的更多信息，请参阅 [Real-Time Customer Profile UI指南](../profile/ui/user-guide.md). 有关如何使用实时客户用户档案API访问用户档案的详细信息，请参阅 [使用实体端点](../profile/api/entities.md).

## 评估数据

从摄取的数据成功生成用户档案后，即可使用分段来评估数据。 区段是定义由个人子集与用户档案存储共享的特定属性或行为的过程，以便将可销售的人群与客户群区分开来。 要了解有关分段的更多信息，请阅读 [分段服务概述](../segmentation/home.md).

### 创建区段定义

要开始使用，您必须创建一个区段定义来将客户聚类，以创建目标受众。 区段定义是规则的集合，您可以使用这些规则定义要定位的受众。 要创建区段定义，您可以按照UI指南中有关使用 [区段生成器](../segmentation/ui/segment-builder.md) 或上的API教程 [创建区段](../segmentation/tutorials/create-a-segment.md).

创建区段定义后，请确保记住区段定义ID。

### 评估区段定义

创建区段定义后，您可以创建区段作业以作为一次性实例来评估区段，也可以创建计划以持续评估区段。

要按需评估区段定义，您可以创建区段任务。 区段作业是一个异步流程，可根据引用的区段定义和合并策略创建新的受众区段。 合并策略是一组规则，Platform使用这些规则来确定将使用哪些数据来创建客户配置文件，以及当源之间存在差异时，将按优先顺序排列哪些数据。 要了解如何使用合并策略，请参阅 [合并策略UI指南](../profile/merge-policies/ui-guide.md).

创建和评估区段作业后，您可以获取有关该区段的信息，如受众的大小或处理过程中可能发生的错误。 要了解如何创建区段作业（包括您需要提供的所有详细信息），请阅读 [区段作业开发人员指南](../segmentation/api/segment-jobs.md).

要持续评估区段定义，您可以创建并启用计划。 计划是一种工具，可用于在指定的时间每天自动运行一次区段作业。 要了解如何创建和启用计划，您可以按照 [计划终结点](../segmentation/api/schedules.md).

## 导出评估的数据

创建一次性区段作业或持续计划后，您可以创建区段导出作业以将结果导出到数据集，或将结果导出到目标。 以下各节提供了有关这两个选项的指导。

### 将评估的数据导出到数据集

创建一次性区段作业或持续计划后，可以通过创建区段导出作业导出结果。 区段导出作业是将评估受众的相关信息发送到数据集的异步任务。

在创建导出作业之前，必须先创建数据集以将数据导出到。 要了解如何创建数据集，请阅读 [创建目标数据集](../segmentation/tutorials/evaluate-a-segment.md#create-dataset) 在有关评估区段的教程中，确保在创建数据集ID后记下该数据集ID。 创建数据集后，您可以创建导出作业。 要了解如何创建导出作业，您可以按照 [导出作业端点](../segmentation/api/export-jobs.md).

### 将评估的数据导出到目标

或者，在创建一次性区段作业或正在进行的计划后，您可以将结果导出到目标。 目标是可在其中激活和传递受众的端点，例如外部服务上的Adobe应用程序。 可在 [目标目录](../destinations/catalog/overview.md).

有关如何将数据激活到批量营销目标或电子邮件营销目标的说明，请参阅 [如何使用Platform UI激活受众数据以批量导出配置文件目标](../destinations/ui/activate-batch-profile-destinations.md) 和 [关于如何使用流量服务API连接到批处理目标和激活数据的指南](../destinations/api/connect-activate-batch-destinations.md).

## 监控平台数据活动

Platform允许您通过使用数据流跟踪数据的处理方式，数据流是跨Platform各个组件移动数据的作业的表示形式。 这些数据流是跨不同的服务配置的，有助于将数据从源连接器移动到目标数据集，然后数据集会被利用 [!DNL Identity Service] 和 [!DNL Real-Time Customer Profile] 最终激活到目标之前。 监控仪表板可直观地呈现数据流的历程。 要了解如何在Platform UI中监视数据流，请参阅 [监控源的数据流](../dataflows/ui/monitor-sources.md) 和 [监控目标数据流](../dataflows/ui/monitor-destinations.md).

您还可以通过使用 [!DNL Observability Insights]. 您可以通过Platform UI订阅警报通知，或将其发送到配置的WebHook。 有关如何从Experience PlatformUI查看、启用、禁用和订阅可用警报的更多详细信息，请参阅 [[!UICONTROL 警报] UI指南](../observability/alerts/ui.md). 有关如何通过Web挂接接收警报的详细信息，请参阅 [订阅Adobe I/O事件通知](../observability/alerts/subscribe.md).

## 后续步骤

通过阅读本教程，您大致了解了适用于Platform的简单端到端流程。 要了解有关Adobe Experience Platform的更多信息，请阅读 [平台概述](./home.md). 要了解有关使用Platform UI和Platform API的更多信息，请阅读 [Platform UI指南](./ui-guide.md) 和 [Platform API指南](./api-guide.md) 分别进行。
