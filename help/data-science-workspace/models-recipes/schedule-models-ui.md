---
keywords: Experience Platform;计划模型；数据科学工作区；热门主题；计划评分；计划培训
solution: Experience Platform
title: 计划数据科学工作区UI中的模型
topic: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace允许您在机器学习服务上设置计划的评分和培训运行。 自动化培训和评分流程有助于跟上数据中的模式，从而在一段时间内保持和提高服务的效率。
translation-type: tm+mt
source-git-commit: 8f5b7018a52d4c5860e03cec3108435ede8815f1
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---


# 计划数据科学工作区UI中的模型

Adobe Experience Platform [!DNL Data Science Workspace]允许您在机器学习服务上设置计划评分和培训运行。 自动化培训和评分流程有助于跟上数据中的模式，从而保持和提高服务的效率。

本教程将逐步介绍如何通过[!UICONTROL Service Gallery]在现有服务上配置培训和评分计划。 它分为以下几个主要部分：

- [配置计划评分](#configure-scheduled-scoring)
- [配置计划培训](#configure-scheduled-training)

## 入门指南

要完成本教程，您必须具有对[!DNL Experience Platform]的访问权限。 如果您无权访问[!DNL Experience Platform]中的IMS组织，请在继续操作之前与您的系统管理员联系。

本教程需要现有服务。 如果您没有可访问的服务可以使用，则可以按照[发布模型作为服务](./publish-model-service-ui.md)的教程创建一个。

## 配置计划评分{#configure-scheduled-scoring}

模型评分可以配置为按计划自动进行。 创建服务后，您可以按照以下步骤配置和应用评分计划:

在Adobe Experience Platform中，选择位于左侧导航列中的&#x200B;**[!UICONTROL Services]**&#x200B;选项卡以访问&#x200B;**[!DNL Service Gallery]**。 查找要计划计分运行的服务，并选择&#x200B;**[!UICONTROL Open]**&#x200B;以视图其&#x200B;**[!UICONTROL Overview]**&#x200B;页面。

![](../images/models-recipes/schedule/select_service.png)

“概述”页显示服务的评分信息。 选择&#x200B;**[!UICONTROL Update Schedule]**&#x200B;链接以配置评分计划。

![](../images/models-recipes/schedule/update_scoring.png)

为评分计划配置频率、开始日期、结束日期、输入数据集和输出数据集。 对配置满意后，选择&#x200B;**[!UICONTROL Create]**&#x200B;以更新服务的评分计划。

![](../images/models-recipes/schedule/set_scoring_schedule.png)

服务的&#x200B;**[!UICONTROL Overview]**&#x200B;页面中显示更新的评分计划。

![](../images/models-recipes/schedule/scoring_set.png)

## 配置计划培训{#configure-scheduled-training}

在服务上配置计划的培训运行可确保机器学习模型更新为最新的数据模式。 每当计划培训运行完成时，将使用生成的培训模型为服务提供动力，直到下次计划培训运行为止。

创建服务后，您可以按照以下步骤配置和应用培训计划:

在Adobe Experience Platform中，选择位于左侧导航列中的&#x200B;**[!UICONTROL Services]**&#x200B;选项卡以访问&#x200B;**[!UICONTROL Service Gallery]**。 查找要计划培训运行的服务，并选择&#x200B;**[!UICONTROL Open]**&#x200B;以视图其&#x200B;**[!UICONTROL Overview]**&#x200B;页。

![](../images/models-recipes/schedule/select_service.png)

“概述”页显示服务的培训信息。 选择&#x200B;**[!UICONTROL Update Schedule]**&#x200B;链接以配置培训计划。

![](../images/models-recipes/schedule/update_training.png)

配置用于培训计划的频率、开始日期、结束日期和输入数据集。 对配置满意后，选择&#x200B;**[!UICONTROL Create]**&#x200B;以更新服务的培训计划。

![](../images/models-recipes/schedule/set_training_schedule.png)

您更新的培训计划显示在服务的&#x200B;**[!UICONTROL Overview]**&#x200B;页面中。

![](../images/models-recipes/schedule/training_set.png)

## 后续步骤

通过完成本教程，您成功地安排了服务上的自动培训和评分运行，并完成了[!DNL Data Science Workspace]教程UI工作流程。 如果尚未执行此操作，请考虑[重新启动教程](./create-retails-sales-dataset.md)，然后按照API工作流创建、培训、得分和发布模型。
