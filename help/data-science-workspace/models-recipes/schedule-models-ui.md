---
keywords: Experience Platform;schedule a model;Data Science Workspace;popular topics
solution: Experience Platform
title: 计划模型(UI)
topic: Tutorial
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34

---


# 计划模型(UI)

Adobe Experience Platform Data Science Workspace允许您在机器学习服务上设置定期评分和培训运行。 自动化培训和评分流程可与数据中的模式保持同步，从而帮助保持和提高服务的长期效率。

本教程逐步介绍如何通过服务库在现有服务上配置培训和评 *分计划*。 它分为以下几个主要部分：

- [配置计划评分](#configure-scheduled-scoring)
- [配置计划培训](#configure-scheduled-training)

## 入门指南

要完成本教程，您必须具有Experience Platform的访问权限。 如果您无权访问Experience Platform中的IMS组织，请在继续操作前与系统管理员联系。

本教程需要现有服务。 如果您没有可访问的服务可以使用，则可以按照UI教程中的“将模型 [发布为服务”创建一个服务](./publish-model-service-ui.md) 。

## 配置计划评分 {#configure-scheduled-scoring}

模型评分可以配置为按计划自动进行。 创建服务后，您可以按照以下步骤配置和应用评分计划:

1. 在Adobe Experience Platform中，单击左 **[!UICONTROL Services]** 侧导航列中的选项卡以访问服 *务库*。 查找要计划评分运行的服务，并单击以 **[!UICONTROL Open]** 视图其 *概述* 页。
   ![](../images/models-recipes/schedule/click_to_open.png)

2. “概述”页显示服务的评分信息。 单击链 **[!UICONTROL Update Schedule]** 接以配置评分计划。
   ![](../images/models-recipes/schedule/service_overview_score.png)

3. 为评分开始配置频率、计划日期、结束日期、输入数据集和输出数据集。 对配置感到满意后，单击 **[!UICONTROL Create]** 以更新服务的评分计划。
   ![](../images/models-recipes/schedule/14_configure_scoring_schedule.png)

4. 更新的评分计划显示在服务的概述 *页* 。
   ![](../images/models-recipes/schedule/service_with_scoring_schedule.png)


## 配置计划培训 {#configure-scheduled-training}

在服务上配置计划的培训运行可确保机器学习模型更新为最新的数据模式。 每当计划的培训运行完成时，都会使用生成的培训模型来为服务提供动力，直到下一次计划的培训运行。

创建服务后，您可以按照以下步骤配置和应用培训计划:

1. 在Adobe Experience Platform中，单击左 **[!UICONTROL Services]** 侧导航列中的选项卡以访问服 *务库*。 查找要计划培训运行的服务，然后单击以 **[!UICONTROL Open]** 视图其 *概述* 页。
   ![](../images/models-recipes/schedule/click_to_open.png)

2. “概述”页显示服务的培训信息。 单击链 **[!UICONTROL Update Schedule]** 接以配置培训计划。
   ![](../images/models-recipes/schedule/service_overview_train.png)

3. 配置用于培训开始的频率、计划日期、结束日期和输入数据集。 对配置感到满意后，单击 **[!UICONTROL Create]** 以更新服务的培训计划。
   ![](../images/models-recipes/schedule/12_configure_training_schedule.png)

4. 更新的培训计划显示在服务的概述 *页面* 。
   ![](../images/models-recipes/schedule/service_with_training_schedule.png)

## 后续步骤

通过遵循本教程，您成功地安排了在服务上运行自动化培训和评分，并完成了数据科学工作区教程UI工作流程。 如果您尚未这样做，请考虑重 [新启动教程](./create-retails-sales-dataset.md) ，然后按照API工作流创建、培训、得分和发布模型。
