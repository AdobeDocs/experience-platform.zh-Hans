---
keywords: Experience Platform；主页；热门主题；实时客户用户档案；身份服务；
solution: Experience Platform
title: 实时客户用户档案教程
topic: 教程
type: 教程
description: 本文档概述了所涉及的步骤，并提供了用于完成每个工作流程的教程的链接。
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---


# 配置 [!DNL Real-time Customer Profile]

要为您的组织配置[!DNL Real-time Customer Profile]，您需要完成多个单独的工作流。 本文档概述了所涉及的步骤，并提供了用于完成每个工作流程的教程的链接。

要了解有关[!DNL Real-time Customer Profile]的更多信息，请首先阅读[用户档案概述](../profile/home.md)。

## 实时客户用户档案UI概述

实时客户用户档案可以为每位客户创建整体视图，将来自多个渠道（包括在线、离线、CRM和第三方数据）的数据组合在一起。

**本指南将帮助您：**
- 了解[!UICONTROL 用户档案] UI和可用功能。
- 视图和管理用户档案数据。

要了解更多信息，请访问[实时客户用户档案用户指南](../profile/ui/user-guide.md)

## 实时客户用户档案API

实时客户用户档案API包括多个端点。 请阅读[实时客户用户档案API概述](../profile/api/overview.md)，了解有关每个可用端点及其使用案例的详细信息。

要了解更多信息并获取使用实时客户用户档案API执行CRUD操作所需的值，请访问[快速入门指南](../profile/api/getting-started.md)。

## 为[!DNL Profile]和[!DNL Identity]服务启用模式

在将数据引入Adobe Experience Platform并在创建[!DNL Real-time Customer Profiles]时使用之前，必须创建一个模式来提供要摄取的数据的结构，并且必须启用该模式以在[!DNL Profile]和Adobe Experience Platform [!DNL Identity Service]中使用。

**本指南将帮助您：**
- 浏览现有模式。
- 创建并命名模式。
- 添加和定义XDM混合。
- 将您的模式字段设置为标识字段。
- 为您的模式启用用户档案。

有关创建[!DNL Profile]和[!DNL Identity Service]已启用的模式的分步说明，请参阅有关使用模式注册表API](../xdm/tutorials/create-schema-api.md)或[使用模式 Builder UI](../xdm/tutorials/create-schema-ui.md)创建模式的教程。[

## 为[!DNL Profile]和[!DNL Identity]配置数据集

要开始将数据引入[!DNL Profile]中，您必须拥有已正确配置以与[!DNL Real-time Customer Profile]和[!DNL Identity Service]一起使用的数据集。

**本指南将帮助您：**
- 创建启用用户档案的数据集。
- 配置现有数据集。
- 将数据摄取到数据集中。
- 确认您的数据集已启用用户档案并且使用Identity Service。

要开始，请按照[的API教程，配置用户档案和Identity](../profile/tutorials/dataset-configuration.md)的数据集。

## 配置合并策略

Adobe Experience Platform使您能够将来自多个来源的数据整合在一起，并将其合并，以全面视图每位客户。 合并策略是[!DNL Platform]用来确定如何对数据进行优先级排序以及将哪些数据合并以创建统一视图的规则。

**本指南将帮助您：**
- 创建新的合并策略。
- 管理现有合并策略。
- 为您的组织设置默认合并策略。
- 了解合并策略违规。

要在[!DNL Platform] UI中使用合并策略，请访问[合并策略用户指南](../profile/ui/merge-policies.md)。 要使用实时客户用户档案API处理合并策略，请参阅[合并策略开发人员指南](../profile/api/merge-policies.md)。

## 配置边缘投影

为了实时为跨多个渠道的客户提供协调、一致和个性化的体验，需要随着变化随时提供并不断更新正确的数据。 Adobe [!DNL Experience Platform]通过使用所谓的边缘，可以实时访问数据。 边缘是一个地理上放置的服务器，它存储数据并使应用程序能够轻松访问它。 通过投影将数据路由到边缘，投影目标定义要向其发送数据的边缘，以及定义将在边缘上提供的特定信息的投影配置。

**本指南将帮助您：**
- 列表、创建、视图、更新和删除边缘投影目标。
- 列表并创建边缘投影配置。
- 了解选择器。

有关详细信息以及如何开始使用边缘，请参阅边缘投影的[!DNL Real-time Customer Profile] API [子指南](../profile/api/edge-projections.md)。

## 自定义用户档案数据在UI中的显示方式

在Experience Platform用户界面中，您可以视图客户实时用户档案数据并以客户用户档案的形式与其交互。 在UI中显示的用户档案信息已从多个用户档案片段合并到一起，以形成每个客户的单个视图。 这包括基本属性、链接身份和渠道首选项等详细信息。 用户档案中显示的默认字段也可以在组织级别进行更改，以显示首选用户档案属性。

**本指南将帮助您：**
- 对卡重新排序、调整大小、编辑和删除。
- 添加属性。
- 添加新卡。
- 恢复默认值。

要了解有关自定义用户档案数据的更多信息，请访问[用户档案自定义文档](../profile/ui/profile-customization.md)

## 后续步骤

为组织配置[!DNL Real-time Customer Profile]后，您可以开始向单个客户用户档案添加数据，并根据特定客户属性创建受众区段。 要开始使用，请参阅以下教程：

- [将数据添加到实时客户用户档案](../profile/tutorials/add-profile-data.md)
- [创建区段](../segmentation/tutorials/create-a-segment.md)