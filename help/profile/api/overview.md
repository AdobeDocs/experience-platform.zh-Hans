---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 实时客户用户档案API开发人员指南
topic: guide
translation-type: tm+mt
source-git-commit: fd6516d1c1d3792b41de65d0f44d78af1124ccc7
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# 实时客户用户档案API开发人员指南

实时用户档案使您能够全面视图Adobe Experience Platform内每位客户。 用户档案允许您将来自多个渠道（如在线、离线、CRM和第三方数据）的不同客户数据整合到一个统一的视图中，为每次客户互动提供一个具有可操作性、时间戳记的帐户。

实时客户用户档案API包括多个端点，如下所述。 请访问各个端点指南获取详细信息，并参 [阅入门指南](getting-started.md) ，获取有关所需标头、读取示例API调用等的重要信息。

要视图所有可用端点和CRUD操作，请参 [阅实时用户档案API参考Swagger](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)。

## (Alpha)计算属性

>[!IMPORTANT]
>计算的属性功能位于alpha中，并非所有用户都可用。 文档和功能可能会更改。

通过计算属性，您可以根据其他值、计算和表达式自动计算字段的值。 计算属性在用户档案级别上操作，这意味着您可以跨所有记录和事件聚合值。 每个计算属性都包含一个表达式，即“规则”，用于评估传入的数据，并将结果值存储在用户档案属性或事件中。 这些计算有助于您轻松回答与终身购买价值、购买间隔时间或应用程序打开次数等相关的问题，无需在每次需要信息时手动执行复杂的计算。 您可以使用端点创建、视图、编辑和删除计算属 `config/computedAttributes` 性。 要了解如何使用此端点，请访问计算 [属性端点指南](computed-attributes.md)。

## 边缘投影

Adobe Experience Platform通过使数据易于在战略性位置称为“边缘”的服务器上访问，实现客户体验的实时个性化。 实时客户用户档案API为通过称为“预测”的组件处理边缘提供端点。 这包括用于确定应将哪些数据投影到每个边缘的投影配置，以及用于定义将投影路由到何处的投影目标。 有关使用边缘投影的详细信息，请访问投 [影配置和目标端点指南](edge-projections.md)。

## 实体

通过Adobe Experience Platform，您可以使用RESTful API或用户界面访问实时客户用户档案数据。 要了解如何使用API访问实体(更常称为“用户档案”)，请遵循实体端点指南中 [概述的步骤](entities.md)。 要使用平台UI访问用户档案，请参阅 [用户档案用户指南](../ui/user-guide.md)。

## 合并策略

在Experience Platform中整合来自多个来源的数据时，合并策略是平台用来确定数据的优先级和合并数据以创建单个客户用户档案的规则。 使用实时客户用户档案API，您可以创建新的合并策略、管理现有策略并为组织设置默认的合并策略。 要进一步了解如何使用API使用合并策略，请访问合 [并策略端点指南](merge-policies.md)。

有关使用平台UI处理合并策略的指南，请参阅合 [并策略用户指南](../ui/merge-policies.md)。

## 用户档案系统作业

引入平台的数据存储在数据湖和实时客户用户档案数据存储中。 有时可能需要从用户档案库中删除数据集或批处理，以删除您不再需要或错误添加的数据。 这需要使用API创建用户档案系统作业（称为“删除请求”），如果需要，也可以进行修改、监视或删除。 要了解如何使用实时客户用户档案API中 `/system/jobs` 的端点处理删除请求，请遵循用户档案系统作业端点指南 [中概述的步骤](profile-system-jobs.md)。

## 后续步骤

要开始使用实时客户用户档案API进行调用，请阅读 [入门指南](getting-started.md) ，然后选择端点指南之一，以了解如何使用特定的用户档案相关端点。 要进一步了解如何使用平台UI处理用户档案数据，请 [参阅实时客户用户档案用户指南](../ui/user-guide.md)。