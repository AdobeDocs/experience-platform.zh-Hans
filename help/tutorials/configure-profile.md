---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 实时客户用户档案教程
topic: tutorial
translation-type: tm+mt
source-git-commit: ee08f43400fa72abce95ed52aff879f954f4b4d6

---


# 配置实时客户用户档案和身份服务

为了为您的组织配置实时客户用户档案，您必须完成多个单独的工作流。 本文档概述了相关步骤，并提供了用于完成每个工作流程的教程的链接。 要进一步了解实时客户用户档案，请首先阅读用户档案概 [述](../profile/home.md)。

## 启用用户档案和身份模式

在将数据引入Adobe Experience Platform并用于创建实时客户用户档案之前，必须创建一个模式来提供要摄取的数据的结构，并且该模式必须启用以用于用户档案和Adobe Experience Platform Identity Service。 有关创建同时启用模式和标识服务的用户档案的分步说明，请参阅使用 [模式注册表API创建模式或使用模式生成器UI](../xdm/tutorials/create-schema-api.md) 创建模式的教程 [](../xdm/tutorials/create-schema-ui.md)。

## 为用户档案和标识配置数据集

要开始将数据引入用户档案，您必须拥有一个已正确配置以与实时客户用户档案和标识服务一起使用的数据集。 要开始，请按照配置数 [据集以进行用户档案和标识教程](../profile/tutorials/dataset-configuration.md)。

## 配置合并策略

Adobe Experience Platform使您能够将来自多个来源的数据整合在一起，并将其合并，以便了解每位客户的完整视图。 整合这些数据时，合并策略是平台用来确定数据的优先级以及将哪些数据合并以创建统一视图的规则。 使用RESTful API或用户界面，您可以创建新的合并策略、管理现有策略并为组织设置默认的合并策略。 要在平台UI中使用合并策略，请访问合 [并策略用户指南](../profile/ui/merge-policies.md)。 要使用实时客户用户档案API处理合并策略，请参阅合并策略开 [发人员指南](../profile/api/merge-policies.md)。

## 配置边缘投影

为了在多个渠道中实时为客户提供协调、一致和个性化的体验，需要随时随地提供正确的数据并在发生变化时不断更新。 Adobe Experience Platform通过使用所谓的边缘实现对数据的实时访问。 边缘是地理上放置的服务器，它存储数据并使应用程序可以很容易地访问它。 通过投影将数据路由到边缘，投影目标定义要向其发送数据的边缘，投影配置定义将在边缘上提供的特定信息。 有关详细信息以及要开始使用边缘，请参阅有关边缘预测的实时客户用户档案API [子指南](../profile/api/edge-projections.md)。

## 后续步骤

为组织配置实时客户用户档案后，您可以开始向单个客户用户档案添加数据，并根据特定客户属性创建受众细分。 要开始使用，请参阅以下教程：

* [将数据添加到实时客户用户档案](../profile/tutorials/add-profile-data.md)
* [创建区段](../segmentation/tutorials/create-a-segment.md)