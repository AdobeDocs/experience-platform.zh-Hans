---
keywords: Experience Platform;score a model;Data Science Workspace;popular topics
solution: Experience Platform
title: 对模型(UI)评分
topic: Tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# 对模型(UI)评分

在Adobe Experience Platform Data Science Workspace中，可通过将输入数据输入到现有培训模型中来获得评分。 然后，将评分结果作为新批存储在指定的输出数据集中并可查看。

本教程演示了在数据科学工作区用户界面中对模型评分所需的步骤。

## 入门指南

要完成本教程，您必须具有Experience Platform的访问权限。 如果您无权访问Experience Platform中的IMS组织，请在继续操作之前与系统管理员联系。

本教程需要经过培训的模型。 如果您没有经过培训的模型，请在继续之前， [按照UI教程中的培训并评估模型](./train-evaluate-model-ui.md) 。

## 创建新的评分运行

使用从先前完成和评估的培训运行中的优化配置创建评分运行。 模型的最佳配置集通常通过查看培训运行评估指标来确定。

1. 找到最佳培训运行，以使用其配置进行评分。 单击所需的培训运行名称以打开该培训运行。

2. 在“培训运行 **评估** ”选项卡中，单击屏幕右上 **方的** “得分”按钮。 这将启动新的“运行 **评分”工作流** 。
   ![](../images/models-recipes/score/training_run_overview.png)

3. 选择输入评分数据集，然后单击“下 **一步”**。
   ![](../images/models-recipes/score/scoring_input.png)

4. 选择输出评分数据集，这是存储评分结果的专用输出数据集。 确认您的选择，然后单击“ **下一步**”。
   ![](../images/models-recipes/score/scoring_results.png)

5. 工作流中的最后一步会提示您配置评分运行。 这些配置由“模型”用于评分运行。
请注意，您将无法删除在“模型”创建过程中设置的继承参数。 您可以编辑或还原未继承的参数，方法是多次单击值，或者在将鼠标悬停在条目上时单击还原图标。
   ![](../images/models-recipes/score/configuration.png)
检查并确认评分配置，然后单击 **完成** ，以创建并执行评分运行。 您将转到“评分运 **行”选项卡** ，新的评分运行将显示状态。
   ![](../images/models-recipes/score/scoring_runs_tab.png)
评分运行将显示以下四种状态之一：“待定”、“完成”、“失败”或“正在运行”，并会自动更新。 如果状态为“已完成”或“已失败”，请继续执行下一步。

## 视图评分结果

1. 查找用于评分运行的培训运行，然后单击该名称以视图其“评 **估** ”页。

2. 在培训运行评估页面顶部附近，单击“ **评分运行** ”选项卡以视图现有评分运行列表。 单击评分列表，将其详细信息视图到右列中。
   ![](../images/models-recipes/score/view_details.png)

3. 如果选定的评分运行状态为“完成”或“失败”，则右侧列中的 **** 视图活动日志链接将处于活动状态。 单击指向视图的链接或下载执行日志。 如果评分运行失败，执行日志可以提供确定失败原因的有用信息。
   ![](../images/models-recipes/score/activity_logs.png)

4. 单击右 **列中的预览评分结果数据集** 。 您将能够从评分运行中看到输出数据集的预览。
   ![](../images/models-recipes/score/preview_results.png)

5. 要获得完整的评分结果集，请单击右列中 **的“评分结果数据集** ”链接。

## 后续步骤

本教程向您介绍了使用数据科学工作区中经过培训的模型对数据进行评分的步骤。 按照教程，在 [UI中将模型作为服务发布](./publish-model-service-ui.md) ，以便组织内的用户通过提供对机器学习服务的轻松访问来得分数据。
