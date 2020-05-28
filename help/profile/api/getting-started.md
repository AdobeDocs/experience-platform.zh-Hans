---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 实时客户用户档案API开发人员指南
topic: guide
translation-type: tm+mt
source-git-commit: 8449681a7fd0fc5dccf4837a1e8e512f1e2f2601
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 0%

---


# 实时客户用户档案API开发人员指南

实时客户用户档案使您能够在Adobe Experience Platform中全面了解每位客户。 用户档案允许您将来自多个渠道（如在线、离线、CRM和第三方数据）的不同客户数据整合到一个统一的视图中，为每次客户互动提供一个具有可操作性、时间戳记的帐户。

## 入门指南 {#getting-started}

使用实时用户档案API，您可以针对用户档案资源执行基本的CRUD操作，如配置计算属性、访问实体、导出用户档案数据以及删除不需要的数据集或批。

使用此开发人员指南需要对处理用户档案数据时涉及的各种Adobe Experience Platform服务进行有效的了解。 在开始使用实时客户用户档案API之前，请查阅以下服务的文档：

* [实时客户用户档案](../home.md): 根据来自多个来源的汇总数据，实时提供统一的客户用户档案。
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): 通过跨设备和系统桥接身份，更好地视图客户及其行为。
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): 允许您根据实时受众数据构建用户档案细分。
* [体验数据模型(XDM)](../../xdm/home.md): 平台组织客户体验数据的标准化框架。
* [沙箱](../../sandboxes/home.md): Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和改进数字体验应用程序。

以下各节提供了成功调用用户档案API端点时需要了解的其他信息。

### 读取示例API调用

实时客户用户档案API文档提供示例API调用，以演示如何正确设置请求格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用的部分。

### 所需的标题

API文档还要求您完成身份验证教 [程](../../tutorials/authentication.md) ，以便成功调用平台端点。 完成身份验证教程后，将为Experience Platform API调用中的每个所需标头提供值，如下所示：

* 授权： 承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都与特定虚拟沙箱相隔离。 对平台API的请求需要一个标头，它指定操作将在中进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

请求主体中具有有效负荷的所有请求（如POST、PUT和PATCH调用）都必须包含标 `Content-Type` 头。 在每个呼叫参数中提供特定于每个呼叫的已接受值。

## (Alpha)计算属性

>[!IMPORTANT]
>计算的属性功能位于alpha中，并非所有用户都可用。 文档和功能可能会更改。

通过计算属性，您可以根据其他值、计算和表达式自动计算字段的值。 计算属性在用户档案级别上操作，这意味着您可以跨所有记录和事件聚合值。

每个计算属性都包含一个表达式，即“规则”，用于评估传入的数据，并将结果值存储在用户档案属性或事件中。 这些计算有助于您轻松回答与终身购买价值、购买间隔时间或应用程序打开次数等相关的问题，无需在每次需要信息时手动执行复杂的计算。

您可以使用端点创建、视图、编辑和删除计算属 `config/computedAttributes` 性。 要了解如何使用这些端点，请访 [问计算属性子指南](computed-attributes.md)。

## 边缘投影

Adobe Experience Platform通过使数据易于在战略性位置称为“边缘”的服务器上访问，实现客户体验的实时个性化。 实时客户用户档案API为通过称为“预测”的组件处理边缘提供端点。 这包括用于确定应将哪些数据投影到每个边缘的投影配置，以及用于定义将投影路由到何处的投影目标。

有关使用边缘投影的详细信息，请访 [问边缘投影子指南](edge-projections.md)。

## 实体

通过Adobe Experience Platform，您可以使用RESTful API或用户界面访问实时客户用户档案数据。 要了解如何使用API访问实体(更常称为“用户档案”)，请遵循实体子指南 [中概述的步骤](entities.md)。

## 合并策略

在Experience Platform中将多个来源的数据整合在一起时，合并策略是平台用来确定数据的优先级和合并哪些数据以创建单个客户用户档案的规则。

使用实时客户用户档案API，您可以创建新的合并策略、管理现有策略并为组织设置默认的合并策略。 要进一步了解如何使用API使用合并策略，请访 [问合并策略子指南](merge-policies.md)。

有关使用平台UI处理合并策略的指南，请参阅合 [并策略用户指南](../ui/merge-policies.md)。

## 用户档案系统作业

引入平台的数据存储在数据湖和实时客户用户档案数据存储中。 有时可能需要从用户档案库中删除数据集或批处理，以删除您不再需要或错误添加的数据。 这需要使用API创建用户档案系统作业（称为“删除请求”），如果需要，也可以进行修改、监视或删除。

要了解如何使用实时客户用户档案API中 `/system/jobs` 的端点处理删除请求，请按照用户档案系统作业子指 [南中概述的步骤操作](profile-system-jobs.md)。

## 后续步骤

要开始使用实时客户用户档案API进行调用，请选择其中一个子指南来了解如何使用特定的用户档案相关端点。 要进一步了解如何使用平台UI处理用户档案数据，请 [参阅实时客户用户档案用户指南](../ui/user-guide.md)。