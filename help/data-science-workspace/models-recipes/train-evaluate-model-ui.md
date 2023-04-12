---
keywords: Experience Platform；培训和评估；数据科学工作区；热门主题；创建模型；创建培训运行
solution: Experience Platform
title: 在数据科学工作区用户界面中训练和评估模型
type: Tutorial
description: 在Adobe Experience Platform Data Science Workspace中，机器学习模型是通过合并适合模型意图的现有方法来创建的。 然后，对模型进行训练和评估，以通过微调其关联的超参数来优化其运行效率和效能。 方法可重复使用，这意味着可以使用单个方法创建多个模型并针对特定目的进行量身定制。
exl-id: 6f674cfa-c123-46a3-80e2-9342fe687976
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 2%

---

# 在数据科学工作区UI中培训和评估模型

在Adobe Experience Platform Data Science Workspace中，机器学习模型是通过合并适合模型意图的现有方法来创建的。 然后，对模型进行训练和评估，以通过微调其关联的超参数来优化其运行效率和效能。 方法可重复使用，这意味着可以使用单个方法创建多个模型并针对特定目的进行量身定制。

本教程将指导创建、培训和评估模型的步骤。

## 快速入门

要完成本教程，您必须具有 [!DNL Experience Platform]. 如果您在 [!DNL Experience Platform]，请在继续操作之前与系统管理员联系。

本教程需要现有的方法。 如果您没有方法，请按照 [在UI中导入打包的方法](./import-packaged-recipe-ui.md) 教程，然后再继续。

## 创建模型

在Experience Platform中，选择 **[!UICONTROL 模型]** 选项卡，然后选择“浏览”选项卡以查看现有模型。 选择 **[!UICONTROL 创建模型]** 在页面右上方附近，以开始创建模型。

![](../images/models-recipes/train-evaluate-ui/models_browse.png)

浏览现有处方列表，查找并选择用于创建模型的处方，然后选择 **[!UICONTROL 下一个]**.
![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

选择适当的输入数据集并选择 **[!UICONTROL 下一个]**. 这将设置模型的默认输入培训数据集。
![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

为模型提供名称并查看默认模型配置。 默认配置在方法创建过程中应用，通过双击这些值来检查和修改配置值。

要提供一组新配置，请选择 **[!UICONTROL 上传新配置]** 并将包含模型配置的JSON文件拖到浏览器窗口中。 选择 **[!UICONTROL 完成]** 创建模型。

>[!NOTE]
>
>配置是唯一的，并且特定于其预期的方法，这意味着零售销售方法的配置不适用于产品Recommendations方法。 请参阅 [参考](#reference) 部分，以了解零售销售方法配置列表。

![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## 创建培训运行

在Experience Platform中，选择 **[!UICONTROL 模型]** 选项卡，然后选择“浏览”选项卡以查看现有模型。 查找并选择附加到要训练的模型名称的超链接。

![](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

将列出所有现有培训运行及其当前培训状态。 对于使用 [!DNL Data Science Workspace] 用户界面中，使用默认配置和输入培训数据集自动生成并执行培训运行。

通过选择 **[!UICONTROL 火车]** 在“模型概述”页面的右上角附近。

![](../images/models-recipes/train-evaluate-ui/model_overview.png)

为培训运行选择培训输入数据集，然后选择 **[!UICONTROL 下一个]**.

![](../images/models-recipes/train-evaluate-ui/training_input.png)

将显示在模型创建期间提供的默认配置，通过双击这些值来相应地更改和修改这些配置。 选择 **[!UICONTROL 完成]** 创建并执行培训运行。

>[!NOTE]
>
>配置是唯一的，并且特定于其预期的方法，这意味着零售销售方法的配置不适用于产品Recommendations方法。 请参阅 [参考](#reference) 部分，以了解零售销售方法配置列表。

![](../images/models-recipes/train-evaluate-ui/training_configuration.png)


## 评估模型

在Experience Platform中，选择 **[!UICONTROL 模型]** 选项卡，然后选择“浏览”选项卡以查看现有模型。 查找并选择附加到要评估的模型名称的超链接。

![选择模型](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

将列出所有现有培训运行及其当前培训状态。 如果已完成多次培训运行，可以在模型评估图表中比较不同培训运行中的评估量度。 使用图形上方的下拉列表选择评估量度。

“平均绝对百分比误差”(MAPE)量度以误差百分比表示准确度。 这用于识别性能最佳的实验。 MAPE越低越好。

![培训运行概述](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

“精度”量度描述相关实例与总实例的百分比 *已检索* 实例。 精度可以看作随机选择的结果正确的概率。

![运行多个运行](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

选择特定培训运行可通过打开评估页面来提供该运行的详细信息。 此操作可在运行完成之前完成。 在评估页面上，您能够查看特定于培训运行的其他评估量度、配置参数和可视化图表。

![预览日志](../images/models-recipes/train-evaluate-ui/evaluate_training.png)

您还可以下载活动日志以查看运行的详细信息。 日志对于失败的运行来查看错误内容特别有用。

![活动日志](../images/models-recipes/train-evaluate-ui/activity_logs.png)

无法训练超参数，必须通过测试超参数的不同组合来优化模型。 重复此模型培训和评估过程，直到您到达一个优化的模型。

## 后续步骤

本教程将指导您在 [!DNL Data Science Workspace]. 在您到达优化模型后，可以使用培训的模型通过遵循 [在UI中对模型进行评分](./score-model-ui.md) 教程。

## 参考 {#reference}

### 零售销售方法配置

超参数决定模型的训练行为，修改超参数将影响模型的精度和精度：

| 超参数 | 描述 | 推荐范围 |
| --- | --- | --- |
| learning_rate | 学习率通过learning_rate缩小每个树的贡献。 learningrate和n估计量之间存在权衡。 | 0.1 |
| n_metiators | 要执行的提升阶段数。 渐变提升对过拟合相当稳健，因此，大量的渐变提升通常会获得更好的性能。 | 100 |
| max_depth | 单个回归估计器的最大深度。 最大深度限制树中的节点数。 调整此参数以获得最佳性能；最佳值取决于输入变量的交互。 | 3 |

其他参数可确定模型的技术属性：

| 参数键 | 类型 | 描述 |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | 字符串 | 以逗号分隔的输入架构属性列表。 |
| `ACP_DSW_TARGET_FEATURES` | 字符串 | 以逗号分隔的输出架构属性列表。 |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 布尔值 | 确定输入和输出功能是否可修改 |
| `tenantId` | 字符串 | 此ID可确保您创建的资源命名正确并包含在您的组织内。 [按照此处的步骤操作](../../xdm/api/getting-started.md#know-your-tenant_id) 以查找租户ID。 |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 字符串 | 用于培训模型的输入模式。 |
| `evaluation.labelColumn` | 字符串 | 用于评估可视化的列标签。 |
| `evaluation.metrics` | 字符串 | 用于评估模型的评估量度列表（以逗号分隔）。 |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 字符串 | 用于对模型进行评分的输出架构。 |
