---
keywords: Experience Platform;计划模型；数据科学工作区；热门主题；计划评分；计划培训
solution: Experience Platform
title: 计划数据科学工作区UI中的模型
topic: tutorial
type: Tutorial
description: Adobe Experience Platform数据科学工作区允许您在机器学习服务上设置定期评分和培训运行。 自动化培训和评分流程可与数据中的模式保持同步，从而帮助保持和提高服务的长期效率。
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---


# 计划数据科学工作区UI中的模型

Adobe Experience Platform[!DNL Data Science Workspace]允许您在机器学习服务上设置计划评分和培训运行。 自动化培训和评分流程可与数据中的模式保持同步，从而帮助保持和提高服务的长期效率。

本教程将逐步通过[!UICONTROL 服务库]在现有服务上配置培训和评分计划。 它分为以下几个主要部分：

- [配置计划评分](#configure-scheduled-scoring)
- [配置计划培训](#configure-scheduled-training)

## 入门指南

要完成本教程，您必须具有对[!DNL Experience Platform]的访问权限。 如果您无权访问[!DNL Experience Platform]中的IMS组织，请在继续操作前与系统管理员联系。

本教程需要现有服务。 如果您没有可访问的服务可使用，则可以按照UI](./publish-model-service-ui.md)教程中的[将模型发布为服务来创建。

## 配置计划评分{#configure-scheduled-scoring}

模型评分可以配置为按计划自动进行。 创建服务后，您可以按照以下步骤配置和应用评分计划:

1. 在Adobe Experience Platform，单击左侧导航列中的&#x200B;**[!UICONTROL 服务]**&#x200B;选项卡以访问&#x200B;**[!DNL Service Gallery]**。 查找要计划计分运行的服务，然后单击&#x200B;**[!UICONTROL 打开]**&#x200B;以视图其&#x200B;**概述**页。
   ![](../images/models-recipes/schedule/click_to_open.png)

2. “概述”页显示服务的评分信息。 单击&#x200B;**[!UICONTROL 更新计划]**链接以配置评分计划。
   ![](../images/models-recipes/schedule/service_overview_score.png)

3. 为评分开始配置频率、计划日期、结束日期、输入数据集和输出数据集。 对配置感到满意后，单击&#x200B;**[!UICONTROL 创建]**以更新服务的评分计划。
   ![](../images/models-recipes/schedule/14_configure_scoring_schedule.png)

4. 您更新的评分计划显示在服务的&#x200B;**概述**页面中。
   ![](../images/models-recipes/schedule/service_with_scoring_schedule.png)


## 配置计划培训{#configure-scheduled-training}

在服务上配置计划的培训运行可确保机器学习模型更新为最新的数据模式。 每当计划的培训运行完成时，都会使用生成的培训模型来为服务提供动力，直到下一次计划的培训运行。

创建服务后，您可以按照以下步骤配置和应用培训计划:

1. 在Adobe Experience Platform，单击左侧导航列中的&#x200B;**[!UICONTROL 服务]**&#x200B;选项卡以访问&#x200B;**[!UICONTROL 服务库]**。 查找要计划培训运行的服务，然后单击&#x200B;**[!UICONTROL 打开]**&#x200B;以视图其&#x200B;**概述**页面。
   ![](../images/models-recipes/schedule/click_to_open.png)

2. “概述”页显示服务的培训信息。 单击&#x200B;**[!UICONTROL 更新计划]**链接以配置培训计划。
   ![](../images/models-recipes/schedule/service_overview_train.png)

3. 配置用于培训开始的频率、计划日期、结束日期和输入数据集。 对配置感到满意后，单击&#x200B;**[!UICONTROL 创建]**以更新服务的培训计划。
   ![](../images/models-recipes/schedule/12_configure_training_schedule.png)

4. 您更新的培训计划显示在服务的&#x200B;**概述**页面中。
   ![](../images/models-recipes/schedule/service_with_training_schedule.png)

## 后续步骤

通过遵循本教程，您成功地安排了在服务上运行自动化培训和评分，并完成了[!DNL Data Science Workspace]教程UI工作流程。 如果尚未执行此操作，请考虑[重新启动教程](./create-retails-sales-dataset.md)，然后按照API工作流创建、培训、得分和发布模型。
