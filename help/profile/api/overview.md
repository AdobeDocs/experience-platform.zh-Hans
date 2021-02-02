---
keywords: Experience Platform;用户档案；实时客户用户档案；疑难解答；API；统一用户档案；统一用户档案；统一用户档案;;rtcp；启用用户档案；启用用户档案
title: 实时客户用户档案API开发人员指南
topic: guide
description: 实时用户档案API包括多个用于浏览和处理用户档案数据的端点，包括查看用户档案、创建和更新合并策略、导出或采样用户档案数据，以及删除您不再需要或错误地添加的用户档案数据。
translation-type: tm+mt
source-git-commit: 823d89ab37156e775a2879e3a2c91bfd911b83bb
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] API开发人员指南

[!DNL Real-time Customer Profile] 使您能够全面视图Adobe Experience Platform内每位客户。[!DNL Profile] 允许您将来自多个渠道（如在线、离线、CRM和第三方数据）的不同客户数据整合到一个统一的视图中，为每次客户互动提供可操作、有时间戳的帐户。

[!DNL Real-time Customer Profile] API包括多个端点，如下所述。 请访问各个端点指南获取详细信息，并参阅[快速入门指南](getting-started.md)以获取有关所需标头、读取示例API调用等的重要信息。

要视图所有可用端点和CRUD操作，请访问[实时客户用户档案API参考Swagger](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)。

有关在[!DNL Experience Platform] UI中使用[!DNL Real-time Customer Profile]数据的指南，请参阅[用户档案用户指南](../ui/user-guide.md)。

## (Alpha)计算属性{#computed-attributes}

>[!IMPORTANT]
>
>计算属性功能位于alpha中，并且不适用于所有用户。 文档和功能可能会更改。

通过计算属性，您可以根据其他值、计算和表达式自动计算字段的值。 计算属性在用户档案级别上操作，这意味着您可以跨所有记录和事件聚合值。 每个计算属性都包含一个表达式，即“规则”，用于评估传入的数据并将所得值存储在用户档案属性或事件中。 这些计算有助于您轻松回答与终身购买价值、购买间隔时间或应用程序打开次数等相关的问题，无需在每次需要信息时手动执行复杂的计算。 您可以使用`config/computedAttributes`端点创建、视图、编辑和删除计算属性。 要了解如何使用此端点，请访问[计算属性端点指南](computed-attributes.md)。

## 边缘投影{#edge-projections}

Adobe Experience Platform通过使数据易于在战略性位置的称为“边缘”的服务器上访问，实现客户体验的实时个性化。 [!DNL Real-time Customer Profile] API为通过称为“投影”的组件处理边提供端点。 这包括用于确定应将哪些数据投影到每个边缘的投影配置，以及用于定义将投影路由到何处的投影目标。 有关使用边缘投影的详细信息，请访问[投影配置和目标端点指南](edge-projections.md)。

## 实体（[!DNL Profile]访问）{#entities}

通过Adobe Experience Platform，您可以使用RESTful API或用户界面访问[!DNL Real-time Customer Profile]数据。 要了解如何使用API访问实体(更常称为“用户档案”)，请按照[entities endpoint guide](entities.md)中概述的步骤操作。 要使用[!DNL Platform] UI访问用户档案，请参阅[用户档案用户指南](../ui/user-guide.md)。

## 导出作业（[!DNL Profile]导出）{#profile-export}

[!DNL Real-time Customer Profile] 数据可以导出到数据集进行进一步处理，如导出受众段以用于激活或用户档案属性以进行报告。受众段的导出作业是[!DNL Adobe Experience Platform Segmentation Service] API的一部分，请阅读[分段导出作业终结点指南](../../profile/api/export-jobs.md)以了解更多。 有关如何创建和管理用户档案属性的导出作业的分步说明，请访问[导出作业终结点指南](export-jobs.md)。

## 合并策略{#merge-policies}

在[!DNL Experience Platform]中将来自多个源的数据整合在一起时，合并策略是[!DNL Platform]用来确定数据的优先级以及将哪些数据合并以创建单个客户用户档案的规则。 使用[!DNL Real-time Customer Profile] API，您可以创建新的合并策略、管理现有策略并为组织设置默认的合并策略。 要进一步了解如何使用API使用合并策略，请访问[合并策略端点指南](merge-policies.md)。

有关使用[!DNL Platform] UI处理合并策略的指南，请参阅[合并策略用户指南](../ui/merge-policies.md)。

## 预览示例状态([!DNL Profile]预览){#profile-preview}

当启用用户档案的数据被引入Experience Platform时，它被存储在用户档案数据存储中。 随着用户档案存储中记录数的增加或减少，将运行一个示例作业，该示例作业包括关于用户档案片段和合并用户档案在数据存储中的数量的信息。 使用用户档案API，您可以预览最新成功的示例，以及按数据集和身份命名空间列表用户档案分发。 要开始使用`/profilepreviewstatus`端点，请参阅[预览示例状态端点指南](preview-sample-status.md)。

## 用户档案系统作业{#profile-system-jobs}

引入[!DNL Platform]的启用用户档案的数据存储在[!DNL Data Lake]和[!DNL Real-time Customer Profile]数据存储中。 有时可能需要从[!DNL Profile]存储中删除数据集或批处理，以删除您不再需要或错误添加的数据。 这需要使用API创建[!DNL Profile System Job]（也称为“[!DNL delete request]”），如果需要，可以修改、监视或删除它。 要了解如何使用[!DNL Real-time Customer Profile] API中的`/system/jobs`端点处理删除请求，请按照[用户档案系统作业端点指南](profile-system-jobs.md)中所述的步骤操作。

## 后续步骤 {#next-steps}

要开始使用[!DNL Real-time Customer Profile] API进行调用，请阅读[入门指南](getting-started.md)，然后选择其中一个端点指南来了解如何使用特定的与[!DNL Profile]相关的端点。 要使用[!DNL Experience Platform] UI处理[!DNL Profile]用户档案，请参阅[实时客户数据用户指南](../ui/user-guide.md)。