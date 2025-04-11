---
keywords: Experience Platform；发布模型；数据科学Workspace；热门主题；为服务评分
solution: Experience Platform
title: 在数据科学Workspace UI中发布模型即服务
type: Tutorial
description: Adobe Experience Platform Data Science Workspace允许您发布经过培训和评估的模型即服务，从而使贵组织内的用户无需创建自己的模型即可对数据进行评分。
exl-id: ebbec1b1-20d3-43b5-82d3-89c79757625a
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 4%

---

# 在 Data Science Workspace UI 中将模型发布为服务 {#publish-a-model-as-a-service}

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

>[!CONTEXTUALHELP]
>id="platform_intelligentservices_publishmodel"
>title="将模型发布为服务"
>abstract=""

Adobe Experience Platform Data Science Workspace允许您发布经过培训和评估的模型即服务，从而使贵组织内的用户无需创建自己的模型即可对数据进行评分。

## 快速入门

要完成本教程，您必须拥有[!DNL Experience Platform]的访问权限。 如果您无权访问[!DNL Experience Platform]中的组织，请在继续之前与系统管理员交谈。

本教程要求现有模型能够成功运行训练。 如果您没有可发布的模型，请按照[培训教程在UI](./train-evaluate-model-ui.md)教程中评估模型，然后再继续。

如果您希望使用Sensei机器学习API发布模型，请参阅[API教程](./publish-model-service-api.md)。

## 发布模型 {#publish-a-model}

在Adobe Experience Platform中，选择位于左侧导航列中的&#x200B;**[!UICONTROL 模型]**，然后选择&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡以列出所有现有模型。 选择要作为服务发布的模型的名称。

![](../images/models-recipes/publish-model/browse_model.png)

选择模型概述页面右上角附近的&#x200B;**[!UICONTROL 发布]**&#x200B;以启动服务创建过程。

![](../images/models-recipes/publish-model/view_training.png)

输入所需的服务名称并提供服务说明（可选），完成后，选择&#x200B;**[!UICONTROL 下一步]**。

![](../images/models-recipes/publish-model/configure_training.png)

列出了模型的所有成功训练运行。 新服务将从选定的训练运行继承训练和评分配置。

![](../images/models-recipes/publish-model/select_training_run.png)

选择&#x200B;**[!UICONTROL 完成]**&#x200B;以创建服务，并重定向到&#x200B;**[!UICONTROL 服务库]**&#x200B;以显示所有可用的服务，包括新创建的服务。

![](../images/models-recipes/publish-model/service_gallery.png)

## 使用服务计分 {#access-a-service}

在Adobe Experience Platform中，选择位于左侧导航列中的&#x200B;**[!UICONTROL 服务]**&#x200B;选项卡以访问&#x200B;**[!UICONTROL 服务库]**。 查找要使用的服务，然后选择&#x200B;**[!UICONTROL 打开]**。

![](../images/models-recipes/publish-model/open_service.png)

在服务概述页面中，选择&#x200B;**[!UICONTROL 得分]**。

![](../images/models-recipes/publish-model/score_service.png)

为评分运行选择适当的输入数据集，然后选择&#x200B;**[!UICONTROL 下一步]**。 系统会要求您对评分数据集执行相同的步骤。 选择输入和输出数据集后，即可更新配置。

![](../images/models-recipes/publish-model/select_datasets.png)

创建服务后，它会继承默认的评分配置。 您可以查看这些配置，并根据需要通过双击值来调整它们。 对配置感到满意后，选择&#x200B;**[!UICONTROL 完成]**&#x200B;以开始评分运行。

![](../images/models-recipes/publish-model/scoring_configs.png)

在服务的&#x200B;**概述**&#x200B;页面上，将显示新评分作业及其进度的详细信息。 作业完成后，**[!UICONTROL 得分]**&#x200B;容器中的&#x200B;**[!UICONTROL 最近]**&#x200B;标头将更新。

![](../images/models-recipes/publish-model/pending_scoring.png)

## 后续步骤 {#next-steps}

通过完成本教程，您已成功将模型发布为可访问服务，并通过[!UICONTROL 服务库]使用新服务对数据进行评分。 继续下一教程，了解如何[安排服务的自动培训和评分运行](./schedule-models-ui.md)。
