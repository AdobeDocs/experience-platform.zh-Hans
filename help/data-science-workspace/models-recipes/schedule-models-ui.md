---
keywords: Experience Platform；计划模型；数据科学Workspace；热门主题；计划得分；计划训练
solution: Experience Platform
title: 在数据科学Workspace UI中计划模型
type: Tutorial
description: Adobe Experience Platform数据科学Workspace允许您在机器学习服务上设置计划的评分和训练运行。 自动化培训和评分过程有助于通过及时跟踪数据中的模式来维护和改进服务的效率。
exl-id: 51f6f328-7c63-4de1-9184-2ba526bb82e2
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# 在数据科学Workspace UI中计划模型

Adobe Experience Platform [!DNL Data Science Workspace]允许您在机器学习服务上设置计划的评分和训练运行。 自动化培训和评分过程有助于通过及时跟踪数据中的模式来维护和改善服务的效率。

本教程介绍通过[!UICONTROL 服务库]在现有服务上配置培训和评分计划的步骤。 它分为以下主要部分：

- [配置计划评分](#configure-scheduled-scoring)
- [配置计划培训](#configure-scheduled-training)

## 快速入门

要完成本教程，您必须拥有[!DNL Experience Platform]的访问权限。 如果您无权访问[!DNL Experience Platform]中的组织，请在继续之前与系统管理员交谈。

本教程需要现有的服务。 如果您没有可访问的服务，则可以按照有关[将模型发布为服务](./publish-model-service-ui.md)的教程创建一个可访问的服务。

## 配置计划评分 {#configure-scheduled-scoring}

模型评分可以配置为按计划自动进行。 创建服务后，您可以按照以下步骤配置并应用评分计划：

在Adobe Experience Platform中，选择位于左侧导航列中的&#x200B;**[!UICONTROL 服务]**&#x200B;选项卡以访问&#x200B;**[!DNL Service Gallery]**。 查找要计划评分运行的服务，然后选择&#x200B;**[!UICONTROL 打开]**&#x200B;以查看其&#x200B;**[!UICONTROL 概述]**&#x200B;页面。

![](../images/models-recipes/schedule/select_service.png)

“概述”页面显示服务的评分信息。 选择&#x200B;**[!UICONTROL 更新计划]**&#x200B;链接以配置评分计划。

![](../images/models-recipes/schedule/update_scoring.png)

为评分计划配置频率、开始日期、结束日期、输入数据集和输出数据集。 对配置感到满意后，选择&#x200B;**[!UICONTROL 创建]**&#x200B;以更新服务的评分计划。

![](../images/models-recipes/schedule/set_scoring_schedule.png)

更新的评分计划将显示在服务的&#x200B;**[!UICONTROL 概述]**&#x200B;页面中。

![](../images/models-recipes/schedule/scoring_set.png)

## 配置计划培训 {#configure-scheduled-training}

配置在服务上运行的计划训练，可确保机器学习模型更新为最新的数据模式。 每当计划的培训运行完成后，就会使用生成的经过培训的模型为服务供电，直到下一次计划的培训运行。

创建服务后，您可以按照以下步骤配置并应用培训计划：

在Adobe Experience Platform中，选择位于左侧导航列中的&#x200B;**[!UICONTROL 服务]**&#x200B;选项卡以访问&#x200B;**[!UICONTROL 服务库]**。 查找要安排培训运行的服务，然后选择&#x200B;**[!UICONTROL 打开]**&#x200B;以查看其&#x200B;**[!UICONTROL 概述]**&#x200B;页面。

![](../images/models-recipes/schedule/select_service.png)

“概述”页面显示服务的培训信息。 选择&#x200B;**[!UICONTROL 更新计划]**&#x200B;链接以配置培训计划。

![](../images/models-recipes/schedule/update_training.png)

配置用于训练计划的频率、开始日期、结束日期和输入数据集。 对配置感到满意后，选择&#x200B;**[!UICONTROL 创建]**&#x200B;以更新服务的培训计划。

![](../images/models-recipes/schedule/set_training_schedule.png)

更新的培训计划将显示在服务的&#x200B;**[!UICONTROL 概述]**&#x200B;页面中。

![](../images/models-recipes/schedule/training_set.png)

## 后续步骤

通过学习本教程，您已成功安排了在服务上运行自动培训和评分，并完成了[!DNL Data Science Workspace]教程UI工作流。 如果您尚未这样做，请考虑[重新启动教程](./create-retails-sales-dataset.md)，然后按照API工作流创建、训练、评分和发布模型。
