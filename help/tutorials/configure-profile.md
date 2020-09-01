---
keywords: Experience Platform;home;popular topics;Real-time Customer Profile;Identity Service;
solution: Experience Platform
title: 实时客户用户档案教程
topic: tutorial
description: 本文档概述了涉及的步骤，并提供了用于完成每个工作流程的教程的链接。
translation-type: tm+mt
source-git-commit: d3ece56d10b1940a5992906a65a50ffe2f7e4346
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# 配置 [!DNL Real-time Customer Profile] 和 [!DNL Identity Service]

为了为您的 [!DNL Real-time Customer Profile] 组织进行配置，您需要完成多个单独的工作流。 本文档概述了涉及的步骤，并提供了用于完成每个工作流程的教程的链接。 要了解有关的更 [!DNL Real-time Customer Profile]多信息，请首先阅读 [用户档案概述](../profile/home.md)。

## 为和启用模式 [!DNL Profile] 功能 [!DNL Identity]

在将数据引入Adobe Experience Platform并用于创建之前，必 [!DNL Real-time Customer Profiles]须创建模式，以提供将要摄取的数据的结构，并且必须启用该模式以在 [!DNL Profile] 和Adobe Experience Platform使 [!DNL Identity Service]用。 有关创建同时启用模式和的分步说 [!DNL Profile] 明 [!DNL Identity Service]，请参阅使用模式注册 [表API创建模式或使用](../xdm/tutorials/create-schema-api.md) 模式生成器UI创建模式的教程 [](../xdm/tutorials/create-schema-ui.md)。

## 为和配置数 [!DNL Profile] 据集 [!DNL Identity]

要开始向中 [!DNL Profile]摄取数据，您必须拥有已正确配置以与和一起使用的 [!DNL Real-time Customer Profile] 数据集 [!DNL Identity Service]。 要开始，请按照配置 [数据集以进行用户档案和身份教程](../profile/tutorials/dataset-configuration.md)。

## 配置合并策略

Adobe Experience Platform使您能够将来自多个来源的数据整合在一起，以便全面视图每位客户。 将数据整合在一起时，合并策略是确定 [!DNL Platform] 数据的优先级以及合并哪些数据以创建统一视图的规则。 使用REST风格的API或用户界面，您可以创建新的合并策略、管理现有策略并为组织设置默认的合并策略。 要在UI中使用合并策 [!DNL Platform] 略，请访问合 [并策略用户指南](../profile/ui/merge-policies.md)。 要使用实时客户用户档案API处理合并策略，请参阅合并策 [略开发人员指南](../profile/api/merge-policies.md)。

## 配置边缘投影

为了跨多个渠道为客户实时提供协调、一致、个性化的体验，需要随时提供正确的数据，并在发生变化时不断更新。 Adobe [!DNL Experience Platform] 通过使用所谓的边缘实现对数据的实时访问。 边缘是一个地理上放置的服务器，它存储数据并使应用程序能够方便地访问它。 数据通过投影被路由到边缘，投影目标定义要向其发送数据的边缘，投影配置定义要在边缘上提供的特定信息。 有关详细信息以及如何开始使用边缘，请参 [!DNL Real-time Customer Profile] 阅 [边缘投影的API子指南](../profile/api/edge-projections.md)。

## 后续步骤

为组织配置 [!DNL Real-time Customer Profile] 后，您可以开始向单个客户用户档案添加数据，并根据特定客户属性创建受众细分。 要开始使用，请参阅以下教程：

* [将数据添加到实时客户用户档案](../profile/tutorials/add-profile-data.md)
* [创建区段](../segmentation/tutorials/create-a-segment.md)