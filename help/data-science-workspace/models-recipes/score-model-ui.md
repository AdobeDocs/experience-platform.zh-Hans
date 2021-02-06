---
keywords: Experience Platform；对模型评分；数据科学工作区；热门主题；ui；评分运行；评分结果
solution: Experience Platform
title: 在数据科学工作区UI中对模型进行评分
topic: tutorial
type: Tutorial
description: '在Adobe Experience Platform数据科学工作区中评分可以通过将输入数据输入到现有训练好的模型中来实现。 然后，将评分结果作为新批存储在指定的输出数据集中并可查看。 '
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# 在数据科学工作区UI中对模型进行评分

Adobe Experience Platform[!DNL Data Science Workspace]的评分可以通过将输入数据输入到现有训练模型中来实现。 然后，将评分结果作为新批存储在指定的输出数据集中并可查看。

本教程演示了在[!DNL Data Science Workspace]用户界面中为模型评分所需的步骤。

## 入门指南

要完成本教程，您必须具有对[!DNL Experience Platform]的访问权限。 如果您无权访问[!DNL Experience Platform]中的IMS组织，请在继续操作前与系统管理员联系。

本教程需要经过培训的模型。 如果您没有经过培训的模型，请按照[培训并在UI](./train-evaluate-model-ui.md)教程中评估模型，然后继续。

## 创建新的评分运行

使用先前完成和评估的培训运行中的优化配置创建评分运行。 模型的一组最佳配置通常通过查看培训运行评估指标来确定。

1. 找到最佳培训运行，以使用其配置进行评分。 通过单击所需的培训运行的名称来打开该培训运行。

2. 在“培训运行&#x200B;**[!UICONTROL 评估]**”选项卡中，单击屏幕右上方的&#x200B;**[!UICONTROL 得分]**&#x200B;按钮。 这将启动新的&#x200B;**运行评分**工作流。
   ![](../images/models-recipes/score/training_run_overview.png)

3. 选择输入评分数据集，然后单击&#x200B;**[!UICONTROL 下一步]**。
   ![](../images/models-recipes/score/scoring_input.png)

4. 选择输出评分数据集，这是存储评分结果的专用输出数据集。 确认您的选择，然后单击&#x200B;**[!UICONTROL 下一步]**。
   ![](../images/models-recipes/score/scoring_results.png)

5. 工作流中的最后一步会提示您配置评分运行。 这些配置由模型用于评分运行。
请注意，您将无法删除在“模型”创建过程中设置的继承参数。 您可以编辑或还原未继承的参数，方法是多次单击值，或者在将鼠标悬停在条目上方时单击还原图标。
   ![](../images/models-recipes/score/configuration.png)
检查并确认评分配置，然后单 ****  击完成以创建和执行评分运行。您将进入&#x200B;**[!UICONTROL 评分运行]**选项卡，新的评分运行将显示状态。
   ![](../images/models-recipes/score/scoring_runs_tab.png)
评分运行将显示以下四种状态之一：挂起、完成、失败或正在运行，并会自动更新。如果状态为“Completed”或“Failed”，请继续执行下一步。

## 视图评分结果

1. 查找用于评分运行的培训运行，并单击该名称以视图其&#x200B;**[!UICONTROL 评估]**&#x200B;页面。

2. 在培训运行评估页面顶部附近，单击&#x200B;**[!UICONTROL 评分运行]**选项卡以视图现有评分运行列表。 单击评分列表，在右列中视图其详细信息。
   ![](../images/models-recipes/score/view_details.png)

3. 如果所选得分运行的状态为“完成”或“失败”，则右列中的&#x200B;**[!UICONTROL 视图活动日志]**链接将处于活动状态。 单击链接以视图或下载执行日志。 如果评分运行失败，执行日志可以提供确定失败原因的有用信息。
   ![](../images/models-recipes/score/activity_logs.png)

4. 单击右列中的&#x200B;**[!UICONTROL 预览评分结果数据集]**链接。 您将能够从评分运行中看到输出数据集的预览。
   ![](../images/models-recipes/score/preview_results.png)

5. 要获得完整的评分结果集，请单击右列中的&#x200B;**[!UICONTROL 评分结果数据集]**&#x200B;链接。

## 后续步骤

本教程向您逐步介绍如何使用[!DNL Data Science Workspace]中经过培训的模型对数据进行评分。 按照[在UI](./publish-model-service-ui.md)中将模型发布为服务上的教程，通过提供对机器学习服务的轻松访问，使组织内的用户能够对数据进行评分。
