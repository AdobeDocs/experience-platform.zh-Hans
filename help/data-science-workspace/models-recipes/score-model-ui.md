---
keywords: Experience Platform；对模型进行评分；Data Science Workspace；热门主题；UI；评分运行；评分结果
solution: Experience Platform
title: 在数据科学工作区UI中对模型进行评分
type: Tutorial
description: 在Adobe Experience Platform Data Science Workspace中，通过将输入数据馈送到现有培训的模型中，可以获得评分。 然后，将评分结果存储并作为新批次在指定的输出数据集中查看。
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---

# 在数据科学工作区UI中对模型进行评分

在Adobe Experience Platform得分 [!DNL Data Science Workspace] 可通过将输入数据输入到现有训练模型中来实现。 然后，将评分结果存储并作为新批次在指定的输出数据集中查看。

本教程演示了在 [!DNL Data Science Workspace] 用户界面。

## 快速入门

要完成本教程，您必须具有 [!DNL Experience Platform]. 如果您在 [!DNL Experience Platform]，请在继续操作之前与系统管理员联系。

本教程需要经过培训的模型。 如果您没有经过培训的模型，请按照 [在用户界面中训练和评估模型](./train-evaluate-model-ui.md) 教程，然后再继续。

## 创建新的评分运行

使用先前完成和评估的培训运行中的优化配置创建评分运行。 模型的最佳配置集通常通过查看培训运行评估量度来确定。

找到最佳培训运行，以使用其配置进行评分。 然后，通过选择附加到其名称的超链接，打开所需的培训运行。

![选择培训运行](../images/models-recipes/score/select-run.png)

从培训班开始 **[!UICONTROL 评估]** 选项卡，选择 **[!UICONTROL 得分]** 位于屏幕右上方。 开始新的评分工作流。

![](../images/models-recipes/score/training_run_overview.png)

选择输入评分数据集，然后选择 **[!UICONTROL 下一个]**.

![](../images/models-recipes/score/scoring_input.png)

选择输出评分数据集，这是存储评分结果的专用输出数据集。 确认您的选择并选择 **[!UICONTROL 下一个]**.

![](../images/models-recipes/score/scoring_results.png)

工作流中的最后一步会提示您配置评分运行。 这些配置由模型用于进行评分运行。
请注意，您不能删除在模型创建期间设置的继承参数。 您可以通过双击值或在将鼠标悬停在条目上时选择还原图标，来编辑或还原未继承的参数。

![配置](../images/models-recipes/score/configuration.png)

查看并确认评分配置，然后选择 **[!UICONTROL 完成]**  创建并执行评分运行。 您会被定向到 **[!UICONTROL 评分运行]** 选项卡和新评分运行 **[!UICONTROL 待定]** 状态。

![打分运行选项卡](../images/models-recipes/score/scoring_runs_tab.png)

可以使用以下状态之一显示评分运行：
- 待定
- 完成
- 失败
- 正在运行

状态会自动更新。 如果状态为，请继续执行下一步 **[!UICONTROL 完成]** 或 **[!UICONTROL 失败]**.

## 查看评分结果

要查看评分结果，请首先选择培训运行。

![选择培训运行](../images/models-recipes/score/select-run.png)

您将被重定向到培训运行 **[!UICONTROL 评估]** 页面。 在培训运行评估页面顶部附近，选择 **[!UICONTROL 评分运行]** 选项卡，以查看现有评分运行的列表。

![评估页面](../images/models-recipes/score/view_scoring_runs.png)

接下来，选择打分运行以查看运行详细信息。

![运行详细信息](../images/models-recipes/score/view_details.png)

如果所选评分运行的状态为“完成”或“失败”，则 **[!UICONTROL 查看活动日志]** 链接可用。 如果评分运行失败，执行日志可提供用于确定失败原因的有用信息。 要下载执行日志，请选择 **[!UICONTROL 查看活动日志]**.

![选择查看日志](../images/models-recipes/score/view_logs.png)

的 **[!UICONTROL 查看活动日志]** 弹出窗口。 选择一个URL以自动下载关联的日志。

![](../images/models-recipes/score/activity_logs.png)

您还可以选择通过选择  **[!UICONTROL 预览评分结果数据集]**.

![选择预览结果](../images/models-recipes/score/view_results.png)

提供了输出数据集的预览。

![预览结果](../images/models-recipes/score/preview_results.png)

对于整套评分结果，请选择 **[!UICONTROL 评分结果数据集]** 链接。

## 后续步骤

本教程将指导您完成使用 [!DNL Data Science Workspace]. 请阅读本教程 [在UI中发布模型为服务](./publish-model-service-ui.md) 通过提供对机器学习服务的轻松访问，让组织内的用户对数据进行评分。
