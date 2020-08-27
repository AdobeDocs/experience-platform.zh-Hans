---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics;score a service
solution: Experience Platform
title: 将模型发布为服务(UI)
topic: Tutorial
description: Adobe Experience Platform数据科学工作区允许您将经过培训和评估的模型作为服务发布，使您的IMS组织内的用户无需创建自己的模型即可对数据进行评分。
translation-type: tm+mt
source-git-commit: 7615476c4b728b451638f51cfaa8e8f3b432d659
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---


# 将模型发布为服务(UI)

Adobe Experience Platform数据科学工作区允许您将经过培训和评估的模型作为服务发布，使您的IMS组织内的用户无需创建自己的模型即可对数据进行评分。

## 入门指南

要完成本教程，您必须具有访问权限 [!DNL Experience Platform]。 如果您无权访问中的IMS组织，请在继 [!DNL Experience Platform]续操作之前与系统管理员联系。

本教程要求现有模型能够成功运行培训。 如果您没有可发布的模型，请按照 [培训并在UI教程中评估模型](./train-evaluate-model-ui.md) ，然后继续。

如果您希望使用Sensei机器学习API发布模型，请参阅 [API教程](./publish-model-service-api.md)。

## 发布模型 {#publish-a-model}

1. 在Adobe Experience Platform，单击左 **[!UICONTROL 侧导航]** 列中的“模型”链接以列表所有现有的“模型”。 查找并单击要作为服务发布的模型的名称。
   ![](../images/models-recipes/publish-model/1_browse_model.png)
2. 单击 **[!UICONTROL “模型]** ”概述页面右上角附近的“发布”，以开始服务创建过程。
   ![](../images/models-recipes/publish-model/2_view_training_runs.png)
3. 输入服务的所需名称并（可选）提供服务说明，完成后单击 **[!UICONTROL 下]** 一步。
   ![](../images/models-recipes/publish-model/3_configure_service.png)
4. 列出了“模型”的所有成功培训运行。 新服务将从所选培训运行继承培训和评分配置。
   ![](../images/models-recipes/publish-model/4_select_training_run.png)
5. 单击 **[!UICONTROL “完成]** ”以创建服务并重定向到服务 **[!UICONTROL 库]** ，以显示所有可用的服务，包括新创建的服务。
   ![](../images/models-recipes/publish-model/service_gallery.png)

## 使用服务得分 {#access-a-service}

1. 在Adobe Experience Platform，单击 **[!UICONTROL 左侧]** 导航列中的“服务”选项卡以访 *[!UICONTROL 问服务库]*。 查找您希望使用的服务，然后单击“ **[!UICONTROL 得分]**”。
   ![](../images/models-recipes/publish-model/click_to_score.png)
2. 为评分运行选择适当的输入数据集，然后单击“下 **[!UICONTROL 一步]**”。
   ![](../images/models-recipes/publish-model/6_scoring_input.png)
3. 为评分结果选择适当的输出数据集，然后单击“下 **[!UICONTROL 一步]**”。
   ![](../images/models-recipes/publish-model/7_scoring_output.png)
4. 创建服务后，它会继承默认的评分配置。 您可以查看这些配置，并根据需要通过多次单击这些值来调整它们。 对配置感到满意后，单击“ **[!UICONTROL 完成]** ”开始评分运行。
   ![](../images/models-recipes/publish-model/8_scoring_configure.png)
5. 在服务的概 *述页* ，将显示新评分作业及其进度的详细信息。 作业完成后，将更 **[!UICONTROL 新“最近]** ”评分作业。
   ![](../images/models-recipes/publish-model/score_pending.png)

## 后续步骤 {#next-steps}

通过本教程，您成功地将模型发布为可访问的服务，并使用新服务通过服务库对数据 *[!UICONTROL 进行计分]*。 继续下一个教程，了解如何 [计划服务上的自动培训和评分](./schedule-models-ui.md)。
