---
keywords: Experience Platform；配置文件；实时客户配置文件；故障排除；API；统一配置文件；统一配置文件；配置文件；rtcp；启用配置文件；启用配置文件
title: Real-Time Customer Profile API指南
description: 实时客户个人资料API允许开发人员浏览和使用个人资料数据，包括查看个人资料、创建和更新合并策略、导出或示例个人资料数据，以及删除不再需要或添加错误的个人资料数据。 参阅本指南，了解如何使用 API 执行关键操作。
role: Developer
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 2%

---

# [!DNL Real-Time Customer Profile] API指南

通过[!DNL Real-Time Customer Profile]，您可以在Adobe Experience Platform中查看每个客户的整体视图。 [!DNL Profile]允许您将来自多个渠道（如在线、离线、CRM和第三方数据）的不同客户数据整合到一个统一视图中，并提供每个客户交互的可操作、带时间戳的帐户。

[!DNL Real-Time Customer Profile] API包括多个端点，如下所述。 有关详细信息，请访问各个端点指南，请参阅[快速入门指南](getting-started.md)，了解有关所需标头、读取示例API调用等的重要信息。

要查看所有可用的端点和CRUD操作，请访问[实时客户个人资料API参考swagger](https://www.adobe.com/go/profile-apis-en)。

有关在[!DNL Experience Platform] UI中使用[!DNL Real-Time Customer Profile]数据的指南，请参阅[配置文件用户指南](../ui/user-guide.md)。

## 计算属性 {#computed-attributes}

计算属性是用于将事件级数据聚合到配置文件级属性的函数。 这些函数是自动计算的，以便在分段、激活和个性化中使用它们。

每个计算属性都包含一个表达式（即“规则”），该表达式将评估传入的数据并将结果值存储在配置文件属性中。 这些计算可以帮助您轻松回答与生命周期购买价值、购买间隔时间或应用程序打开次数等相关的问题，而无需您在每次需要信息时手动执行复杂的计算。 然后，可以在配置文件中查看这些计算的属性值，将其用于创建受众，或通过多种不同的访问模式进行访问。

您可以使用`ca/attributes/`端点创建、查看、编辑和删除计算属性。 要了解如何使用计算属性，请参阅[计算属性概述](../computed-attributes/overview.md)。 对于API操作，请访问[计算属性API终结点指南](../computed-attributes/api.md)。

## 实体（[!DNL Profile]访问权限） {#entities}

通过Adobe Experience Platform，您可以使用RESTful API或用户界面访问[!DNL Real-Time Customer Profile]数据。 要了解如何使用API访问实体（通常称为“配置文件”），请按照[实体端点指南](entities.md)中所述的步骤操作。 要使用[!DNL Experience Platform] UI访问配置文件，请参阅[配置文件用户指南](../ui/user-guide.md)。

## 导出作业（[!DNL Profile]导出） {#profile-export}

可将[!DNL Real-Time Customer Profile]数据导出到数据集以供进一步处理，例如导出受众以供激活或导出配置文件属性以供报告。 受众的导出作业是[!DNL Adobe Experience Platform Segmentation Service] API的一部分，请阅读[分段导出作业终结点指南](../../profile/api/export-jobs.md)以了解详情。 有关如何创建和管理配置文件属性的导出作业的分步说明，请访问[导出作业端点指南](export-jobs.md)。

## 合并策略 {#merge-policies}

在[!DNL Experience Platform]中将来自多个源的数据聚集在一起时，合并策略是[!DNL Experience Platform]用来确定数据的优先顺序以及将合并哪些数据以创建单个客户配置文件的规则。 使用[!DNL Real-Time Customer Profile] API，您可以创建新的合并策略、管理现有策略并为组织设置默认合并策略。 要使用API处理合并策略，请访问[合并策略终结点指南](merge-policies.md)。

要了解有关合并策略及其在Experience Platform中的角色的更多信息，请从阅读[合并策略概述](../merge-policies/overview.md)开始。

## 预览样本状态（[!DNL Profile]预览） {#profile-preview}

当数据被摄取到Experience Platform中时，将运行示例作业以更新用户档案计数和其他实时客户档案数据相关量度。 此示例作业的结果可以使用实时客户个人资料API的`/previewsamplestatus`端点进行查看。 此端点还可用于同时按数据集和身份命名空间列出配置文件分发，以及生成多个报告，以了解您组织的配置文件存储的组成。  要开始使用`/profilepreviewstatus`终结点，请参阅[预览示例状态终结点指南](preview-sample-status.md)。

## 配置文件系统作业 {#profile-system-jobs}

引入到[!DNL Experience Platform]中的启用配置文件的数据存储在[!DNL Data Lake]以及[!DNL Real-Time Customer Profile]数据存储中。 有时候，可能有必要从配置文件存储中删除与数据集关联的配置文件数据，以便删除不再需要或添加错误的数据。 这需要使用API创建一个[!DNL Profile System Job]，也称为“[!DNL delete request]”，如果需要，可以修改、监视或删除它。 要了解如何使用[!DNL Real-Time Customer Profile] API中的`/system/jobs`端点处理删除请求，请按照[配置文件系统作业端点指南](profile-system-jobs.md)中所述的步骤操作。

## 更新用户档案属性 {#update-profile}

有时候，可能需要更新您组织的配置文件存储区中的数据。 例如，您可能需要更正记录或更改属性值。 这可以通过批量摄取完成，并且需要为启用了配置文件的数据集配置更新插入标记。 有关如何为属性更新配置数据集的更多信息，请参阅[为配置文件和更新插入](../../catalog/datasets/enable-upsert.md)启用数据集的教程。

## 后续步骤 {#next-steps}

若要开始使用[!DNL Real-Time Customer Profile] API进行调用，请阅读[入门指南](getting-started.md)，然后选择其中一个端点指南，以了解如何使用特定的[!DNL Profile]相关端点。 要使用[!DNL Experience Platform] UI处理[!DNL Profile]数据，请参阅[实时客户资料用户指南](../ui/user-guide.md)。
