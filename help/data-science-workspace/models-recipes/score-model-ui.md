---
keywords: Experience Platform；为模型得分；数据科学工作区；热门主题；ui；得分运行；得分结果
solution: Experience Platform
title: 在数据科学工作区UI中为模型打分
topic-legacy: tutorial
type: Tutorial
description: 通过将输入数据输入到现有培训模型中，可以在Adobe Experience Platform数据科学工作区中获得评分。 然后，将评分结果作为新批存储在指定的输出数据集中并可查看。
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---

# 在数据科学工作区UI中为模型打分

通过将输入数据输入到现有的训练模型中，可以在Adobe Experience Platform[!DNL Data Science Workspace]中获得评分。 然后，将评分结果作为新批存储在指定的输出数据集中并可查看。

本教程演示了在[!DNL Data Science Workspace]用户界面中对模型评分所需的步骤。

## 入门指南

要完成本教程，您必须具有对[!DNL Experience Platform]的访问权限。 如果您无权访问[!DNL Experience Platform]中的IMS组织，请在继续操作之前与您的系统管理员联系。

本教程需要经过培训的模型。 如果您没有经过培训的模型，请按照[培训并在UI](./train-evaluate-model-ui.md)教程中评估模型，然后继续。

## 创建新得分运行

使用先前完成和评估的培训运行中的优化配置创建得分运行。 模型的一组最佳配置通常通过查看培训运行评估量度来确定。

找到最佳培训运行，以使用其配置进行评分。 然后，通过选择附加到其名称的超链接来打开所需的培训运行。

![选择培训运行](../images/models-recipes/score/select-run.png)

从培训运行&#x200B;**[!UICONTROL Evaluation]**&#x200B;选项卡中，选择位于屏幕右上角的&#x200B;**[!UICONTROL Score]**。 开始新的评分工作流。

![](../images/models-recipes/score/training_run_overview.png)

选择输入评分数据集，然后选择&#x200B;**[!UICONTROL Next]**。

![](../images/models-recipes/score/scoring_input.png)

选择输出评分数据集，这是存储评分结果的专用输出数据集。 确认您的选择，然后选择&#x200B;**[!UICONTROL Next]**。

![](../images/models-recipes/score/scoring_results.png)

工作流中的最后一步会提示您配置得分运行。 这些配置由模型用于评分运行。
请注意，您不能删除在创建模型时设置的继承参数。 您可以编辑或还原未继承的参数，方法是单击值或在将鼠标悬停在条目上方时选择还原图标。

![配置](../images/models-recipes/score/configuration.png)

查看并确认评分配置，然后选择&#x200B;**[!UICONTROL Finish]**&#x200B;以创建并执行评分运行。 您将转到&#x200B;**[!UICONTROL Scoring Runs]**&#x200B;选项卡，并显示状态为&#x200B;**[!UICONTROL Pending]**&#x200B;的新得分运行。

![“计分运行”](../images/models-recipes/score/scoring_runs_tab.png)

可以使用以下状态之一显示评分运行：
- 待定
- 完成
- 失败
- 正在运行

状态会自动更新。 如果状态为&#x200B;**[!UICONTROL Complete]**&#x200B;或&#x200B;**[!UICONTROL Failed]**，请继续执行下一步。

## 视图评分结果

要视图得分结果，请通过选择培训运行进行开始。

![选择培训运行](../images/models-recipes/score/select-run.png)

您将被重定向到培训运行&#x200B;**[!UICONTROL Evaluation]**&#x200B;页面。 在培训运行评估页面顶部附近，选择&#x200B;**[!UICONTROL Scoring Runs]**&#x200B;选项卡以视图现有得分运行的列表。

![评估页](../images/models-recipes/score/view_scoring_runs.png)

然后，选择一个评分运行以视图运行详细信息。

![运行详细信息](../images/models-recipes/score/view_details.png)

如果选定的评分运行状态为“完成”或“失败”，则&#x200B;**[!UICONTROL View Activity Logs]**&#x200B;链接可用。 如果评分运行失败，执行日志可以提供用于确定失败原因的有用信息。 要下载执行日志，请选择&#x200B;**[!UICONTROL View Activity Logs]**。

![选择视图日志](../images/models-recipes/score/view_logs.png)

出现&#x200B;**[!UICONTROL View activity logs]**&#x200B;弹出窗口。 选择一个URL以自动下载关联的日志。

![](../images/models-recipes/score/activity_logs.png)

您还可以选择&#x200B;**[!UICONTROL Preview scoring results dataset]**&#x200B;视图您的评分结果。

![选择预览结果](../images/models-recipes/score/view_results.png)

提供输出数据集的预览。

![预览结果](../images/models-recipes/score/preview_results.png)

要获得完整的评分结果集，请选择右列中的&#x200B;**[!UICONTROL Scoring Results Dataset]**&#x200B;链接。

## 后续步骤

本教程向您介绍了使用[!DNL Data Science Workspace]中经过培训的模型对数据进行评分的步骤。 请按照[中的教程，在UI](./publish-model-service-ui.md)中将模型发布为服务，以便通过提供对机器学习服务的轻松访问，让组织内的用户能够对数据进行评分。
