---
keywords: Experience Platform;score a model;Data Science Workspace;popular topics;ui;scoring run;scoring results
solution: Experience Platform
title: 对模型(UI)进行评分
topic: Tutorial
description: '在Adobe Experience Platform数据科学工作区中评分可以通过将输入数据输入到现有训练好的模型中来实现。 然后，将评分结果作为新批存储在指定的输出数据集中并可查看。 '
translation-type: tm+mt
source-git-commit: c6c5ada52321b11543254f80399c38365f0fb9d7
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 0%

---


# 对模型(UI)进行评分

在Adobe Experience Platform, [!DNL Data Science Workspace] 可以通过将输入数据输入到现有的训练模型中来实现评分。 然后，将评分结果作为新批存储在指定的输出数据集中并可查看。

本教程演示了在用户界面中为模型评分所 [!DNL Data Science Workspace] 需的步骤。

## 入门指南

要完成本教程，您必须具有访问权限 [!DNL Experience Platform]。 如果您无权访问中的IMS组织，请在继 [!DNL Experience Platform]续操作之前与系统管理员联系。

本教程需要经过培训的模型。 如果您没有经过培训的模型，请按照 [培训并在UI教程中评估模型](./train-evaluate-model-ui.md) ，然后继续。

## 创建新的评分运行

使用先前完成和评估的培训运行中的优化配置创建评分运行。 模型的一组最佳配置通常通过查看培训运行评估指标来确定。

1. 找到最佳培训运行，以使用其配置进行评分。 通过单击所需的培训运行的名称来打开该培训运行。

2. 在“培训运行 **[!UICONTROL 评估]** ”选项卡中，单 **[!UICONTROL 击屏]** 幕右上方的“得分”按钮。 这将启动新的“运行 *评分”工作* 流。
   ![](../images/models-recipes/score/training_run_overview.png)

3. 选择输入评分数据集，然后单击“ **[!UICONTROL 下一步]**”。
   ![](../images/models-recipes/score/scoring_input.png)

4. 选择输出评分数据集，这是存储评分结果的专用输出数据集。 确认您的选择，然后单击“ **[!UICONTROL 下一步]**”。
   ![](../images/models-recipes/score/scoring_results.png)

5. 工作流中的最后一步会提示您配置评分运行。 这些配置由模型用于评分运行。
请注意，您将无法删除在“模型”创建过程中设置的继承参数。 您可以编辑或还原未继承的参数，方法是多次单击值，或者在将鼠标悬停在条目上方时单击还原图标。
   ![](../images/models-recipes/score/configuration.png)
检查并确认评分配置，并单 **[!UICONTROL 击]** “完成”以创建和执行评分运行。 您将进入“评 **[!UICONTROL 分运行]** ”选项卡，新的评分运行将显示状态。
   ![](../images/models-recipes/score/scoring_runs_tab.png)
评分运行将显示以下四种状态之一：挂起、完成、失败或正在运行，并会自动更新。 如果状态为“Completed”或“Failed”，请继续执行下一步。

## 视图评分结果

1. 查找用于评分运行的培训运行，并单击该名称以视图其“评估” **[!UICONTROL 页]** 。

2. 在培训运行评估页面顶部附近，单击“ **[!UICONTROL 评分运行]** ”选项卡以视图现有评分运行列表。 单击评分列表，在右列中视图其详细信息。
   ![](../images/models-recipes/score/view_details.png)

3. 如果所选得分运行的状态为“完成”或“失败”，则右列中 **[!UICONTROL 的视图活动日志]** 链接将处于活动状态。 单击链接以视图或下载执行日志。 如果评分运行失败，执行日志可以提供确定失败原因的有用信息。
   ![](../images/models-recipes/score/activity_logs.png)

4. 单击右 **[!UICONTROL 列中的预览评分结果]** “数据集”链接。 您将能够从评分运行中看到输出数据集的预览。
   ![](../images/models-recipes/score/preview_results.png)

5. 要获得完整的评分结果集，请单击右 **[!UICONTROL 列中的“评分结果]** ”数据集链接。

## 后续步骤

本教程指导您逐步使用中经过培训的模型对数据进行评分 [!DNL Data Science Workspace]。 按照教程， [在UI中将模型作为服务发布](./publish-model-service-ui.md) ，以便组织内的用户能够通过轻松访问机器学习服务来对数据进行评分。
