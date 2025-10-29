---
keywords: Experience Platform；为模型评分；数据科学Workspace；热门主题；ui；评分运行；评分结果
solution: Experience Platform
title: 在数据科学Workspace UI中为模型评分
type: Tutorial
description: 在Adobe Experience Platform数据科学Workspace中，可通过将输入数据馈送到现有的已训练模型来实现评分。 评分结果将作为新批次存储在指定的输出数据集中并可供查看。
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 1%

---

# 在数据科学Workspace UI中为模型评分

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

通过将输入数据馈送到现有的经过训练的模型，可以达到Adobe Experience Platform [!DNL Data Science Workspace]中的得分。 评分结果将作为新批次存储在指定的输出数据集中并可供查看。

本教程演示了在[!DNL Data Science Workspace]用户界面中为模型评分所需的步骤。

## 快速入门

要完成本教程，您必须拥有[!DNL Experience Platform]的访问权限。 如果您无权访问[!DNL Experience Platform]中的组织，请在继续之前与系统管理员交谈。

本教程需要一个经过培训的模型。 如果您没有经过培训的模型，请按照[培训并在UI](./train-evaluate-model-ui.md)教程中评估模型，然后再继续。

## 创建新的评分运行

评分运行是使用先前完成并评估的训练运行中的优化配置创建的。 模型的最佳配置集通常通过查看训练运行评估指标来确定。

找到最佳训练运行，以使用其配置进行评分。 然后，通过选择附加到其名称的超链接来打开所需的训练运行。

![选择训练运行](../images/models-recipes/score/select-run.png)

从训练运行&#x200B;**[!UICONTROL Evaluation]**&#x200B;选项卡中，选择位于屏幕右上角的&#x200B;**[!UICONTROL Score]**。 新的评分工作流开始。

![](../images/models-recipes/score/training_run_overview.png)

选择输入评分数据集并选择&#x200B;**[!UICONTROL Next]**。

![](../images/models-recipes/score/scoring_input.png)

选择输出评分数据集，这是存储评分结果的专用输出数据集。 确认您的选择并选择&#x200B;**[!UICONTROL Next]**。

![](../images/models-recipes/score/scoring_results.png)

工作流的最后一步会提示您配置评分运行。 模型将这些配置用于评分运行。
请注意，不能移除在创建模型期间设置的继承参数。 您可以编辑或还原非继承的参数，方法是双击该值或在将鼠标悬停在条目上时选择还原图标。

![配置](../images/models-recipes/score/configuration.png)

查看并确认评分配置并选择&#x200B;**[!UICONTROL Finish]**&#x200B;以创建并执行评分运行。 您被定向到&#x200B;**[!UICONTROL Scoring Runs]**&#x200B;选项卡，并显示状态为&#x200B;**[!UICONTROL Pending]**&#x200B;的新评分运行。

![评分运行选项卡](../images/models-recipes/score/scoring_runs_tab.png)

评分运行可以显示为以下状态之一：

- 待处理
- 完成
- 失败
- 正在运行

状态会自动更新。 如果状态为&#x200B;**[!UICONTROL Complete]**&#x200B;或&#x200B;**[!UICONTROL Failed]**，则继续执行下一步。

## 查看评分结果

要查看评分结果，请从选择训练运行开始。

![选择训练运行](../images/models-recipes/score/select-run.png)

您将被重定向到训练运行&#x200B;**[!UICONTROL Evaluation]**&#x200B;页面。 在训练运行评估页面顶部附近，选择&#x200B;**[!UICONTROL Scoring Runs]**&#x200B;选项卡以查看现有评分运行的列表。

![评估页](../images/models-recipes/score/view_scoring_runs.png)

接下来，选择一个评分运行以查看运行详细信息。

![运行详细信息](../images/models-recipes/score/view_details.png)

如果选定的评分运行的状态为“完成”或“失败”，则提供&#x200B;**[!UICONTROL View Activity Logs]**&#x200B;链接。 如果评分运行失败，执行日志可提供有用的信息来确定失败原因。 要下载执行日志，请选择&#x200B;**[!UICONTROL View Activity Logs]**。

![选择查看日志](../images/models-recipes/score/view_logs.png)

出现&#x200B;**[!UICONTROL View activity logs]**&#x200B;弹出框。 选择一个URL以自动下载关联的日志。

![](../images/models-recipes/score/activity_logs.png)

您还可以通过选择&#x200B;**[!UICONTROL Preview scoring results dataset]**&#x200B;来查看评分结果。

![选择预览结果](../images/models-recipes/score/view_results.png)

提供了输出数据集的预览。

![预览结果](../images/models-recipes/score/preview_results.png)

对于完整的评分结果集，请选择在右列中找到的&#x200B;**[!UICONTROL Scoring Results Dataset]**&#x200B;链接。

## 后续步骤

本教程将指导您完成在[!DNL Data Science Workspace]中使用经过训练的模型为数据评分的步骤。 按照有关[在UI中发布模型即服务](./publish-model-service-ui.md)的教程进行操作，通过提供对机器学习服务的轻松访问，允许组织内的用户评分数据。
