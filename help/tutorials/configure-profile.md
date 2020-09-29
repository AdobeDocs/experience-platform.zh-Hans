---
keywords: Experience Platform;home;popular topics;Real-time Customer Profile;Identity Service;
solution: Experience Platform
title: 实时客户用户档案教程
topic: tutorial
type: Tutorial
description: 本文档概述了涉及的步骤，并提供了用于完成每个工作流程的教程的链接。
translation-type: tm+mt
source-git-commit: 844ef4a0131e41d3a7a3da319ccf7f8d5cf1f40d
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 0%

---


# 配置 [!DNL Real-time Customer Profile] 和 [!DNL Identity Service]

为了为您的 [!DNL Real-time Customer Profile] 组织进行配置，您需要完成多个单独的工作流。 本文档概述了涉及的步骤，并提供了用于完成每个工作流程的教程的链接。

要了解有关的更 [!DNL Real-time Customer Profile]多信息，请首先阅读 [用户档案概述](../profile/home.md)。

## 实时客户用户档案UI概述

实时客户用户档案可以为您的每位客户创建整体视图，将来自多个渠道（包括在线、离线、CRM和第三方数据）的数据相结合。

**本指南将帮助您：**
- 了解 [!UICONTROL 用户档案] UI和可用功能。
- 视图和管理用户档案数据。

要了解更多信息，请访 [问实时客户用户档案用户指南](../profile/ui/user-guide.md)

## 实时客户用户档案API

实时客户用户档案API包括多个端点。 用户档案允许您将来自多个渠道（如在线、离线、CRM和第三方数据）的不同客户数据整合到一个统一的视图中，为每次客户互动提供一个具有可操作性、时间戳记的帐户。 请阅读实 [时客户用户档案API概述](../profile/api/overview.md) ，以了解有关每个可用端点及其使用案例的更多信息。

**提供以下API开发人员指南：**
- [计算属性(alpha) ](../profile/api/computed-attributes.md) -了解计算属性的用例以及如何配置、访问、更新和删除计算属性。
- [边缘投影](../profile/api/edge-projections.md) -了解如何创建、视图、更新、删除和列表投影目标。 此文档还包含有关列出和创建投影配置的信息，并提供了使用选择器的示例。
- [实体(用户档案访问](../profile/api/entities.md) )-了解如何按身份或身份列表访问用户档案数据。 此外，了解如何使用身份访问多个用户档案的时间序列事件、按身份访问单个用户档案以及访问多个模式实体。
- [导出作业(用户档案导出](../profile/api/export-jobs.md) )-了解如何创建、视图、监视和取消导出作业。
- [合并策略](../profile/api/merge-policies.md) -了解合并策略的组件以及如何访问、创建、更新和删除合并策略。
- [预览样本状态(用户档案预览](../profile/api/preview-sample-status.md) )-了解如何视图上一个样本状态、按数据集分配列表用户档案和按命名空间分配列表用户档案。
- [用户档案系统作业(删除请求](../profile/api/profile-system-jobs.md) )-了解如何在用户档案商店中视图、创建和删除数据集或批处理的删除请求。

要了解更多信息并获取使用实时客户用户档案API执行CRUD操作所需的值，请访问入 [门指南](../profile/api/getting-started.md)。

## 启用模式 [!DNL Profile] 和服 [!DNL Identity] 务

在将数据引入Adobe Experience Platform并用于创建之前，必 [!DNL Real-time Customer Profiles]须创建模式，以提供将要摄取的数据的结构，并且必须启用该模式以在 [!DNL Profile] 和Adobe Experience Platform使 [!DNL Identity Service]用。

**本指南将帮助您：**
- 浏览现有模式。
- 创建并命名模式。
- 添加和定义XDM混合。
- 将您的模式字段设置为标识字段。
- 为您的用户档案启用模式。

有关创建同时启用模式和的分步说 [!DNL Profile] 明 [!DNL Identity Service]，请参阅使用模式注册 [表API创建模式或使用](../xdm/tutorials/create-schema-api.md) 模式生成器UI创建模式的教程 [](../xdm/tutorials/create-schema-ui.md)。

## 为和配置数 [!DNL Profile] 据集 [!DNL Identity]

要开始向中 [!DNL Profile]摄取数据，您必须拥有已正确配置以与和一起使用的 [!DNL Real-time Customer Profile] 数据集 [!DNL Identity Service]。

**本指南将帮助您：**
- 创建启用用户档案的数据集。
- 配置现有数据集。
- 将数据摄取到数据集中。
- 确认您的数据集已启用用户档案并使用Identity Service。

要开始，请按照API教程 [为用户档案和标识配置数据集](../profile/tutorials/dataset-configuration.md)。

## 配置合并策略

Adobe Experience Platform使您能够将来自多个来源的数据整合在一起，以便全面视图每位客户。 将数据整合在一起时，合并策略是确定 [!DNL Platform] 数据的优先级以及合并哪些数据以创建统一视图的规则。

**本指南将帮助您：**
- 创建新的合并策略。
- 管理现有合并策略。
- 为组织设置默认的合并策略。
- 了解合并策略违规。

要在UI中使用合并策 [!DNL Platform] 略，请访问合 [并策略用户指南](../profile/ui/merge-policies.md)。 要使用实时客户用户档案API处理合并策略，请参阅合并策 [略开发人员指南](../profile/api/merge-policies.md)。

## 配置边缘投影

为了跨多个渠道为客户实时提供协调、一致、个性化的体验，需要随时提供正确的数据，并在发生变化时不断更新。 Adobe [!DNL Experience Platform] 通过使用所谓的边缘实现对数据的实时访问。 边缘是一个地理上放置的服务器，它存储数据并使应用程序能够方便地访问它。 数据通过投影被路由到边缘，投影目标定义要向其发送数据的边缘，投影配置定义要在边缘上提供的特定信息。

**本指南将帮助您：**
- 列表、创建、视图、更新和删除边缘投影目标。
- 列表并创建边缘投影配置。
- 了解选择器。

有关详细信息以及如何开始使用边缘，请参 [!DNL Real-time Customer Profile] 阅 [边缘投影的API子指南](../profile/api/edge-projections.md)。

## 自定义用户档案数据在UI中的显示方式

在Experience Platform用户界面中，您可以视图实时客户用户档案数据并以客户用户档案的形式与其交互。 在UI中显示的用户档案信息已从多个用户档案片段合并到一起，以形成每个客户的单个视图。 这包括基本属性、链接身份和渠道首选项等详细信息。 用户档案中显示的默认字段也可以在组织级别进行更改，以显示首选用户档案属性。

**本指南将帮助您：**
- 重新排序、调整大小、编辑和删除卡。
- 添加属性。
- 添加新卡。
- 恢复默认值。

要了解有关自定义用户档案数据的更多信息，请访问 [用户档案自定义文档](../profile/ui/profile-customization.md)

## 后续步骤

为组织配置 [!DNL Real-time Customer Profile] 后，您可以开始向单个客户用户档案添加数据，并根据特定客户属性创建受众细分。 要开始使用，请参阅以下教程：

- [将数据添加到实时客户用户档案](../profile/tutorials/add-profile-data.md)
- [创建区段](../segmentation/tutorials/create-a-segment.md)