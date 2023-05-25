---
keywords: Experience Platform；配置文件；实时客户配置文件；故障排除；API；统一配置文件；统一配置文件；配置文件；rtcp；启用配置文件；启用配置文件
title: Real-Time Customer Profile API指南
description: 实时客户个人资料API允许开发人员浏览和使用个人资料数据，包括查看个人资料、创建和更新合并策略、导出或示例个人资料数据，以及删除不再需要或添加错误的个人资料数据。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 1%

---

# [!DNL Real-Time Customer Profile] API指南

[!DNL Real-Time Customer Profile] 使您能够在Adobe Experience Platform中查看每个客户的整体视图。 [!DNL Profile] 允许您将来自多个渠道（如在线、离线、CRM和第三方数据）的不同客户数据整合到一个统一视图中，从而为每次客户交互提供一个带有时间戳的可操作帐户。

此 [!DNL Real-Time Customer Profile] API包括多个端点，如下所述。 有关详细信息，请访问各个端点指南，并参阅 [快速入门指南](getting-started.md) 有关所需标头的重要信息，请阅读示例API调用等。

要查看所有可用的端点和CRUD操作，请访问 [Real-Time Customer Profile API参考swagger](https://www.adobe.com/go/profile-apis-en).

有关使用的指南 [!DNL Real-Time Customer Profile] 中的数据 [!DNL Experience Platform] UI，请参阅 [配置文件用户指南](../ui/user-guide.md).

<!-- ## (Alpha) Computed attributes {#computed-attributes}

>[!IMPORTANT]
>
>Computed attribute functionality is in alpha and is not available to all users. Documentation and functionality are subject to change.

Computed attributes are functions used to aggregate event-level data into profile-level attributes. These functions are automatically computed so that they can be used across segmentation, activation, and personalization.

Each computed attribute contains an expression, or "rule", that evaluates incoming data and stores the resulting value in a profile attribute. These computations help you to easily answer questions related to things like lifetime purchase value, time between purchases, or number of application opens, without requiring you to manually perform complex calculations each time the information is needed. These computed attribute values can then be viewed in a profile, used to create a segment, or accessed through a number of different access patterns.

You can create, view, edit, and delete computed attributes using the `config/computedAttributes` endpoint. To learn how to use computed attributes, refer to the [computed attributes overview](../computed-attributes/overview.md). For API operations, visit the [computed attributes API endpoint guide](../computed-attributes/ca-api.md). -->

## 边缘投影 {#edge-projections}

Adobe Experience Platform通过在名为“边缘”的具有战略意义的服务器上轻松访问数据，实现了客户体验的实时个性化。 此 [!DNL Real-Time Customer Profile] API通过名为“投影”的组件提供处理边缘的端点。 这包括确定应该投影到每个边缘的投影配置，以及定义投影路由位置的投影目的地。 有关使用Edge Projection的详细信息，请访问 [投影配置和目标端点指南](edge-projections.md).

## 实体([!DNL Profile] access) {#entities}

通过Adobe Experience Platform，您可以访问 [!DNL Real-Time Customer Profile] 数据使用RESTful API或用户界面。 要了解如何使用API访问实体（通常称为“用户档案”），请按照 [实体端点指南](entities.md). 要使用访问用户档案，请 [!DNL Platform] UI，请参阅 [配置文件用户指南](../ui/user-guide.md).

## 导出作业([!DNL Profile] export) {#profile-export}

[!DNL Real-Time Customer Profile] 可将数据导出到数据集以供进一步处理，例如导出受众区段以供激活，或导出配置文件属性以供报告。 导出受众区段的作业是 [!DNL Adobe Experience Platform Segmentation Service] API，请参阅 [分段导出作业端点指南](../../profile/api/export-jobs.md) 了解更多信息。 有关如何创建和管理配置文件属性的导出作业的分步说明，请访问 [导出作业端点指南](export-jobs.md).

## 合并策略 {#merge-policies}

将来自多个源的数据汇集到中时 [!DNL Experience Platform]，合并策略是指 [!DNL Platform] 使用确定数据的优先顺序以及将合并哪些数据以创建单个客户配置文件。 使用 [!DNL Real-Time Customer Profile] API中，您可以创建新的合并策略、管理现有策略以及为组织设置默认合并策略。 要使用API使用合并策略，请访问 [合并策略端点指南](merge-policies.md).

要了解有关合并策略及其在Platform中的角色的更多信息，请从阅读 [合并策略概述](../merge-policies/overview.md).

## 预览示例状态([!DNL Profile] preview) {#profile-preview}

当数据被摄取到Platform中时，将运行一个示例作业来更新用户档案计数和其他与实时客户档案数据相关的量度。 可以使用查看此示例作业的结果 `/previewsamplestatus` 端点，实时客户个人资料API的一部分。 此端点还可用于按数据集和身份命名空间列出配置文件分发，以及生成多个报告，以了解贵组织的配置文件存储区的组成。  要开始使用 `/profilepreviewstatus` 端点，请参阅 [预览示例状态终结点指南](preview-sample-status.md).

## 配置文件系统作业 {#profile-system-jobs}

已摄取到的启用配置文件的数据 [!DNL Platform] 存储在 [!DNL Data Lake] 以及 [!DNL Real-Time Customer Profile] 数据存储。 有时候，可能有必要从以下位置删除数据集或批次： [!DNL Profile] 存储以删除您不再需要或添加错误的数据。 这需要使用API创建 [!DNL Profile System Job]，也称为“[!DNL delete request]&quot;，可根据需要修改、监视或删除它们。 要了解如何使用删除请求 `/system/jobs` 中的端点 [!DNL Real-Time Customer Profile] API，请按照 [配置文件系统作业端点指南](profile-system-jobs.md).

## 更新配置文件属性 {#update-profile}

有时候，可能需要更新您组织的配置文件存储区中的数据。 例如，您可能需要更正记录或更改属性值。 这可以通过批量摄取完成，并且需要为启用了配置文件的数据集配置更新插入标记。 有关如何为属性更新配置数据集的更多信息，请参阅的教程 [为配置文件和更新插入启用数据集](../../catalog/datasets/enable-upsert.md).

## 后续步骤 {#next-steps}

要开始使用 [!DNL Real-Time Customer Profile] API，请阅读 [快速入门指南](getting-started.md) 然后选择其中一个端点指南，了解如何使用特定的 [!DNL Profile] — 相关端点。 使用 [!DNL Profile] 数据使用 [!DNL Experience Platform] UI，请参阅 [Real-time Customer Profile用户指南](../ui/user-guide.md).
