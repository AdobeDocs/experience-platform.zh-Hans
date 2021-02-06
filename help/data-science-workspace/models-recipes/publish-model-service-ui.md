---
keywords: Experience Platform；发布模型；数据科学工作区；热门主题；为服务评分
solution: Experience Platform
title: 在数据科学工作区UI中发布模型作为服务
topic: tutorial
type: Tutorial
description: Adobe Experience Platform数据科学工作区允许您将经过培训和评估的模型作为服务发布，使您的IMS组织内的用户无需创建自己的模型即可对数据进行评分。
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---


# 在数据科学工作区UI中发布模型作为服务

Adobe Experience Platform数据科学工作区允许您将经过培训和评估的模型作为服务发布，使您的IMS组织内的用户无需创建自己的模型即可对数据进行评分。

## 入门指南

要完成本教程，您必须具有对[!DNL Experience Platform]的访问权限。 如果您无权访问[!DNL Experience Platform]中的IMS组织，请在继续操作前与系统管理员联系。

本教程要求现有模型能够成功运行培训。 如果您没有可发布的模型，请按照[培训，在继续之前，在UI](./train-evaluate-model-ui.md)教程中评估模型。

如果您希望使用Sensei机器学习API发布模型，请参阅[API教程](./publish-model-service-api.md)。

## 发布型号{#publish-a-model}

1. 在Adobe Experience Platform，单击左侧导航列中的&#x200B;**[!UICONTROL Models]**链接以列表所有现有型号。 查找并单击要作为服务发布的模型的名称。
   ![](../images/models-recipes/publish-model/1_browse_model.png)
2. 单击“模型概述”页右上方的&#x200B;**[!UICONTROL 发布]**以开始服务创建过程。
   ![](../images/models-recipes/publish-model/2_view_training_runs.png)
3. 输入服务的所需名称并（可选）提供服务说明，完成后单击&#x200B;**[!UICONTROL 下一步]**。
   ![](../images/models-recipes/publish-model/3_configure_service.png)
4. 列出了“模型”的所有成功培训运行。 新服务将从所选培训运行继承培训和评分配置。
   ![](../images/models-recipes/publish-model/4_select_training_run.png)
5. 单击&#x200B;**[!UICONTROL 完成]**&#x200B;以创建服务并重定向到&#x200B;**[!UICONTROL 服务库]**以显示所有可用服务，包括新创建的服务。
   ![](../images/models-recipes/publish-model/service_gallery.png)

## 使用服务{#access-a-service}进行得分

1. 在Adobe Experience Platform，单击左侧导航列中的&#x200B;**[!UICONTROL 服务]**&#x200B;选项卡以访问&#x200B;**[!UICONTROL 服务库]**。 查找您希望使用的服务，然后单击&#x200B;**[!UICONTROL 得分]**。
   ![](../images/models-recipes/publish-model/click_to_score.png)
2. 为评分运行选择适当的输入数据集，然后单击&#x200B;**[!UICONTROL 下一步]**。
   ![](../images/models-recipes/publish-model/6_scoring_input.png)
3. 为评分结果选择适当的输出数据集，然后单击&#x200B;**[!UICONTROL 下一步]**。
   ![](../images/models-recipes/publish-model/7_scoring_output.png)
4. 创建服务后，它会继承默认的评分配置。 您可以查看这些配置，并根据需要通过多次单击这些值来调整它们。 对配置感到满意后，单击&#x200B;**[!UICONTROL 完成]**开始计分运行。
   ![](../images/models-recipes/publish-model/8_scoring_configure.png)
5. 在服务的&#x200B;**概述**&#x200B;页面上，将显示新评分作业及其进度的详细信息。 作业完成后，将更新&#x200B;**[!UICONTROL Scorning]**&#x200B;容器中的&#x200B;**[!UICONTROL Most Recent]**标头。
   ![](../images/models-recipes/publish-model/score_pending.png)

## 后续步骤 {#next-steps}

通过本教程，您成功地将模型发布为可访问的服务，并通过[!UICONTROL 服务库]使用新服务对数据进行了计分。 继续下一个教程，了解如何[计划在服务](./schedule-models-ui.md)上运行的自动化培训和评分。
