---
keywords: Experience Platform；配置文件；实时客户配置文件；故障诊断；API；统一配置文件；统一配置文件；配置文件；rtcp；启用配置文件；启用配置文件
title: 实时客户资料API指南
description: 实时客户配置文件API允许开发人员探索和使用配置文件数据，包括查看配置文件、创建和更新合并策略、导出或采样配置文件数据，以及删除不再需要或错误添加的配置文件数据。 请阅读本指南，了解如何使用API执行关键操作。
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: b2ae2b4ca2efe606aa148e06ca988a6285bedfee
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] API指南

[!DNL Real-time Customer Profile] 使您能够在Adobe Experience Platform中全面了解每个客户。[!DNL Profile] 允许您将来自多个渠道（如在线、离线、CRM和第三方数据）的不同客户数据整合到一个统一视图中，为每次客户交互提供一个可操作且带有时间戳的帐户。

[!DNL Real-time Customer Profile] API包含多个端点，如下所述。 有关详细信息，请访问各个端点指南，并参阅[快速入门指南](getting-started.md) ，以了解有关所需标头、读取示例API调用等的重要信息。

要查看所有可用的端点和CRUD操作，请访问[实时客户配置文件API引用Swagger](https://www.adobe.com/go/profile-apis-en)。

有关在[!DNL Experience Platform] UI中使用[!DNL Real-time Customer Profile]数据的指南，请参阅[配置文件用户指南](../ui/user-guide.md)。

## (Alpha)计算属性 {#computed-attributes}

>[!IMPORTANT]
>
>计算属性功能位于Alpha中，并非所有用户都可用。 文档和功能可能会发生更改。

计算属性是用于将事件级别数据聚合到配置文件级别属性中的函数。 这些函数会自动计算，以便在分段、激活和个性化期间使用。

每个计算属性都包含一个表达式，即“规则”，用于计算传入数据并将结果值存储在配置文件属性中。 这些计算有助于您轻松回答与生命周期购买值、购买间隔时间或应用程序打开次数等相关的问题，而无需您每次需要信息时都手动执行复杂的计算。 然后，可以在配置文件中查看这些计算出的属性值，用于创建区段，或通过许多不同的访问模式访问这些属性值。

您可以使用`config/computedAttributes`端点创建、查看、编辑和删除计算属性。 要了解如何使用计算属性，请参阅[计算属性概述](../computed-attributes/overview.md)。 有关API操作，请访问[计算属性API端点指南](../computed-attributes/ca-api.md)。

## 边缘投影 {#edge-projections}

Adobe Experience Platform通过使数据能够在战略位置称为“边缘”的服务器上轻松访问，从而实现客户体验的实时个性化。 [!DNL Real-time Customer Profile] API通过名为“projections”的组件为使用边缘提供了端点。 这包括用于确定应将哪些数据投影到每个边缘的投影配置，以及用于定义投影路由位置的投影目标。 有关使用边缘投影的详细信息，请访问[投影配置和目标端点指南](edge-projections.md)。

## 实体（[!DNL Profile]访问） {#entities}

通过Adobe Experience Platform，您可以使用RESTful API或用户界面访问[!DNL Real-time Customer Profile]数据。 要了解如何使用API访问实体（通常称为“profiles”），请按照[entities endpoint guide](entities.md)中所述的步骤操作。 要使用[!DNL Platform] UI访问用户档案，请参阅[配置文件用户指南](../ui/user-guide.md)。

## 导出作业（[!DNL Profile]导出） {#profile-export}

[!DNL Real-time Customer Profile] 数据可导出到数据集以进行进一步处理，如导出受众区段以进行激活或配置文件属性以进行报告。受众区段的导出作业是[!DNL Adobe Experience Platform Segmentation Service] API的一部分，请阅读[分段导出作业端点指南](../../profile/api/export-jobs.md)以了解更多信息。 有关如何为配置文件属性创建和管理导出作业的分步说明，请访问[导出作业端点指南](export-jobs.md)。

## 合并策略 {#merge-policies}

在[!DNL Experience Platform]中将来自多个源的数据汇集在一起时，合并策略是[!DNL Platform]用来确定数据优先级和合并哪些数据以创建单个客户配置文件的规则。 使用[!DNL Real-time Customer Profile] API，您可以创建新的合并策略、管理现有策略，并为组织设置默认的合并策略。 要使用API处理合并策略，请访问[合并策略端点指南](merge-policies.md)。

要进一步了解合并策略及其在Platform中的角色，请首先阅读[合并策略概述](../merge-policies/overview.md)。

## 预览示例状态（[!DNL Profile]预览） {#profile-preview}

将数据摄取到Platform后，将运行一个示例作业以更新用户档案计数和其他与实时客户档案数据相关的量度。 此示例作业的结果可以使用`/previewsamplestatus`端点（实时客户资料API的一部分）查看。 此端点还可用于按数据集和身份命名空间列出配置文件分配，以及生成多个报表，以便查看您组织的配置文件存储的组成。  要开始使用`/profilepreviewstatus`端点，请参阅[预览示例状态端点指南](preview-sample-status.md)。

## 配置文件系统作业 {#profile-system-jobs}

被摄取到[!DNL Platform]的启用了配置文件的数据会存储在[!DNL Data Lake]和[!DNL Real-time Customer Profile]数据存储中。 有时可能需要从[!DNL Profile]存储中删除数据集或批处理，以删除您不再需要或错误添加的数据。 这需要使用API创建[!DNL Profile System Job]（也称为“[!DNL delete request]”），如果需要，可以修改、监视或删除该API。 要了解如何使用[!DNL Real-time Customer Profile] API中的`/system/jobs`端点处理删除请求，请按照[配置文件系统作业端点指南](profile-system-jobs.md)中所述的步骤操作。

## 后续步骤 {#next-steps}

要开始使用[!DNL Real-time Customer Profile] API进行调用，请阅读[入门指南](getting-started.md)，然后选择其中一个端点指南，以了解如何使用与[!DNL Profile]相关的特定端点。 要使用[!DNL Experience Platform] UI处理[!DNL Profile]数据，请参阅[实时客户资料用户指南](../ui/user-guide.md)。
