---
keywords: Experience Platform；配置文件；实时客户配置文件；故障排除；API；统一配置文件；统一配置文件；配置文件；rtcp；启用配置文件；启用配置文件
title: Real-Time Customer Profile API指南
description: 实时客户个人资料API允许开发人员浏览和使用个人资料数据，包括查看个人资料、创建和更新合并策略、导出或示例个人资料数据，以及删除不再需要或添加错误的个人资料数据。 参阅本指南，了解如何使用API执行关键操作。
role: Developer
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] API指南

[!DNL Real-Time Customer Profile] 使您能够在Adobe Experience Platform中查看每个客户的整体视图。 [!DNL Profile] 允许您将来自多个渠道（如在线、离线、CRM和第三方数据）的不同客户数据整合到一个统一视图中，并提供每个客户交互的带时间戳的可操作帐户。

此 [!DNL Real-Time Customer Profile] API包括多个端点，如下所述。 有关详细信息，请参阅各个端点指南，并参阅 [快速入门指南](getting-started.md) 有关所需标头的重要信息，请阅读示例API调用等。

要查看所有可用的端点和CRUD操作，请访问 [实时客户个人资料API参考Swagger](https://www.adobe.com/go/profile-apis-en).

有关使用指南 [!DNL Real-Time Customer Profile] 中的数据 [!DNL Experience Platform] UI，请参阅 [配置文件用户指南](../ui/user-guide.md).

## [!BADGE 测试版]{type=Informative}计算属性 {#computed-attributes}

>[!IMPORTANT]
>
计算属性功能处于测试阶段，并非对所有用户都可用。 文档和功能可能会发生更改。

计算属性是用于将事件级数据聚合到配置文件级属性的函数。 这些函数是自动计算的，以便在分段、激活和个性化中使用它们。

每个计算属性都包含一个表达式（即“规则”），该表达式将评估传入的数据并将结果值存储在配置文件属性中。 这些计算可以帮助您轻松回答与生命周期购买价值、购买间隔时间或应用程序打开次数等相关的问题，而无需您在每次需要信息时手动执行复杂的计算。 然后，可以在配置文件中查看这些计算的属性值，将其用于创建受众，或通过多种不同的访问模式进行访问。

您可以使用创建、查看、编辑和删除计算属性 `ca/attributes/` 端点。 要了解如何使用计算属性，请参阅 [计算属性概述](../computed-attributes/overview.md). 对于API操作，请访问 [计算属性API端点指南](../computed-attributes/api.md).

## 实体([!DNL Profile] access) {#entities}

通过Adobe Experience Platform，您可以 [!DNL Real-Time Customer Profile] 数据使用RESTful API或用户界面。 要了解如何使用API访问实体（通常称为“用户档案”），请按照 [实体端点指南](entities.md). 要使用访问用户档案，请执行以下操作 [!DNL Platform] UI，请参阅 [配置文件用户指南](../ui/user-guide.md).

## 导出作业([!DNL Profile] export) {#profile-export}

[!DNL Real-Time Customer Profile] 可将数据导出到数据集以供进一步处理，例如导出受众以供激活或导出配置文件属性以供报告。 受众的导出作业是 [!DNL Adobe Experience Platform Segmentation Service] API，请阅读 [分段导出作业端点指南](../../profile/api/export-jobs.md) 了解更多信息。 有关如何创建和管理配置文件属性的导出作业的分步说明，请访问 [导出作业端点指南](export-jobs.md).

## 合并策略 {#merge-policies}

将来自多个源的数据汇集到中时 [!DNL Experience Platform]，合并策略是指 [!DNL Platform] 使用确定数据的优先顺序以及将合并哪些数据以创建各个客户配置文件。 使用 [!DNL Real-Time Customer Profile] API之外，您还可以创建新的合并策略、管理现有策略以及为组织设置默认合并策略。 要使用API处理合并策略，请访问 [合并策略端点指南](merge-policies.md).

要了解有关合并策略及其在Platform中的角色的更多信息，请从阅读 [合并策略概述](../merge-policies/overview.md).

## 预览示例状态([!DNL Profile] 预览) {#profile-preview}

当数据被摄取到Platform中时，将运行示例作业以更新用户档案计数和其他实时客户档案数据相关量度。 可以使用查看此示例作业的结果 `/previewsamplestatus` 端点，实时客户资料API的一部分。 此端点还可用于同时按数据集和身份命名空间列出配置文件分发，以及生成多个报告，以了解您组织的配置文件存储的组成。  要开始使用 `/profilepreviewstatus` 端点，请参阅 [预览示例状态终结点指南](preview-sample-status.md).

## 配置文件系统作业 {#profile-system-jobs}

已摄取到的启用配置文件的数据 [!DNL Platform] 存储在 [!DNL Data Lake] 以及 [!DNL Real-Time Customer Profile] 数据存储。 有时候，可能有必要从配置文件存储中删除与数据集关联的配置文件数据，以便删除不再需要或添加错误的数据。 这需要使用API创建 [!DNL Profile System Job]，也称为“[!DNL delete request]“”，可根据需要修改、监视或删除这些变量。 要了解如何使用删除请求，请执行以下操作 `/system/jobs` 中的端点 [!DNL Real-Time Customer Profile] API，请按照 [配置文件系统作业端点指南](profile-system-jobs.md).

## 更新用户档案属性 {#update-profile}

有时候，可能需要更新您组织的配置文件存储区中的数据。 例如，您可能需要更正记录或更改属性值。 这可以通过批量摄取完成，并且需要为启用了配置文件的数据集配置更新插入标记。 有关如何配置数据集以进行属性更新的更多信息，请参阅的教程 [为配置文件和更新插入启用数据集](../../catalog/datasets/enable-upsert.md).

## 后续步骤 {#next-steps}

要开始使用 [!DNL Real-Time Customer Profile] API，阅读 [快速入门指南](getting-started.md) 然后选择其中一个端点指南，以了解如何使用特定的 [!DNL Profile] — 相关端点。 使用 [!DNL Profile] 数据使用 [!DNL Experience Platform] UI，请参阅 [Real-time Customer Profile用户指南](../ui/user-guide.md).
