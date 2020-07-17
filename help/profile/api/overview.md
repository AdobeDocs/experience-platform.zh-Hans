---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 实时客户用户档案API开发人员指南
topic: guide
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] API开发人员指南

[!DNL Real-time Customer Profile] 使您能够在Adobe Experience Platform内全面了解每位客户。 [!DNL Profile] 允许您将来自多个渠道（如在线、离线、CRM和第三方数据）的不同客户数据整合到一个统一的视图中，为每次客户互动提供可操作、有时间戳的帐户。

该API [!DNL Real-time Customer Profile] 包括多个端点，如下所述。 请访问各个端点指南获取详细信息，并参 [阅入门指南](getting-started.md) ，获取有关所需标头、读取示例API调用等的重要信息。

要视图所有可用端点和CRUD操作，请参 [阅实时用户档案API参考Swagger](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)。

## (Alpha)计算属性

>[!IMPORTANT]
>
>
>计算的属性功能位于alpha中，并非所有用户都可用。 文档和功能可能会更改。

通过计算属性，您可以根据其他值、计算和表达式自动计算字段的值。 计算属性在用户档案级别上操作，这意味着您可以跨所有记录和事件聚合值。 每个计算属性都包含一个表达式，即“规则”，用于评估传入的数据，并将结果值存储在用户档案属性或事件中。 这些计算有助于您轻松回答与终身购买价值、购买间隔时间或应用程序打开次数等相关的问题，无需在每次需要信息时手动执行复杂的计算。 您可以使用端点创建、视图、编辑和删除计算属 `config/computedAttributes` 性。 要了解如何使用此端点，请访问计算 [属性端点指南](computed-attributes.md)。

## 边缘投影

Adobe Experience Platform通过使数据易于在战略性位置称为“边缘”的服务器上访问，实现客户体验的实时个性化。 API [!DNL Real-time Customer Profile] 为通过称为“投影”的组件处理边提供端点。 这包括用于确定应将哪些数据投影到每个边缘的投影配置，以及用于定义将投影路由到何处的投影目标。 有关使用边缘投影的详细信息，请访问投 [影配置和目标端点指南](edge-projections.md)。

## 实体(用户档案访问) {#entities}

通过Adobe Experience Platform，您可 [!DNL Real-time Customer Profile] 以使用RESTful API或用户界面访问数据。 要了解如何使用API访问实体(更常称为“用户档案”)，请遵循实体端点指南中 [概述的步骤](entities.md)。 要使用UI访问用户档案, [!DNL Platform] 请参阅“用户档案 [用户指南”](../ui/user-guide.md)。

## 合并策略

当将多个来源的数据整合到 [!DNL Experience Platform]一起时，合并策略是确定 [!DNL Platform] 数据的优先级以及将哪些数据合并以创建单个客户用户档案的规则。 使用 [!DNL Real-time Customer Profile] API，您可以创建新的合并策略、管理现有策略并为组织设置默认的合并策略。 要进一步了解如何使用API使用合并策略，请访问合 [并策略端点指南](merge-policies.md)。

有关使用UI处理合并策略的指 [!DNL Platform] 南，请参阅合 [并策略用户指南](../ui/merge-policies.md)。

## 用户档案系统作业

所摄取的 [!DNL Platform] 数据被存储 [!DNL Data Lake] 在数据存储 [!DNL Real-time Customer Profile] 器中。 有时可能需要从商店中删除数据集或批 [!DNL Profile] 量，以删除您不再需要或错误添加的数据。 这需要使用API创 [!DNL Profile System Job]建一个称为“[!DNL delete request]”的API，该API也可以根据需要进行修改、监视或删除。 要了解如何使用API中的端点处 `/system/jobs` 理删除请 [!DNL Real-time Customer Profile] 求，请按照用户档案系统作业端点指 [南中概述的步骤操作](profile-system-jobs.md)。

## 后续步骤

要开始使用API进行调 [!DNL Real-time Customer Profile] 用，请阅读 [入门指南](getting-started.md) ，然后选择一个端点指南，以了解如何使用特定的 [!DNL Profile]相关端点。 要进一步了解如何 [!DNL Profile] 使用UI [!DNL Platform] 处理数据，请 [参阅实时客户用户档案用户指南](../ui/user-guide.md)。