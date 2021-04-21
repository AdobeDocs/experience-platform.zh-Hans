---
keywords: Experience Platform；培训和评估；数据科学工作区；热门主题；创建模型；创建培训运行
solution: Experience Platform
title: 在数据科学工作区用户界面中训练和评估模型
topic-legacy: tutorial
type: Tutorial
description: 在Adobe Experience Platform Data Science Workspace中，通过合并适合模型意图的现有菜谱来创建机器学习模型。 然后，对模型进行训练和评估，通过微调其相关的超参数来优化其运行效率和效能。 菜谱是可重用的，这意味着可以使用单个菜谱创建多个模型并针对特定用途进行定制。
exl-id: 6f674cfa-c123-46a3-80e2-9342fe687976
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 1%

---

# 在数据科学工作区用户界面中培训和评估模型

在Adobe Experience Platform Data Science Workspace中，通过合并适合模型意图的现有菜谱来创建机器学习模型。 然后，对模型进行训练和评估，通过微调其相关的超参数来优化其运行效率和效能。 菜谱是可重用的，这意味着可以使用单个菜谱创建多个模型并针对特定用途进行定制。

本教程将逐步介绍创建、培训和评估模型的步骤。

## 入门指南

要完成本教程，您必须具有对[!DNL Experience Platform]的访问权限。 如果您无权访问[!DNL Experience Platform]中的IMS组织，请在继续操作之前与您的系统管理员联系。

本教程需要现有的菜谱。 如果您没有菜谱，请按照UI](./import-packaged-recipe-ui.md)教程中的[导入打包菜谱，然后继续。

## 创建模型

在Experience Platform中，选择左侧导航中的&#x200B;**[!UICONTROL Models]**&#x200B;选项卡，然后选择浏览选项卡以视图现有模型。 选择页面右上角的&#x200B;**[!UICONTROL Create Model]**&#x200B;以开始模型创建过程。

![](../images/models-recipes/train-evaluate-ui/models_browse.png)

浏览现有菜谱的列表，找到并选择用于创建模型的菜谱，然后选择&#x200B;**[!UICONTROL Next]**。
![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

选择适当的输入数据集，然后选择&#x200B;**[!UICONTROL Next]**。 这将设置“模型”的默认输入培训数据集。
![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

为“模型”(Model)提供名称并查看默认“模型”(Model)配置。 在创建处方时应用了默认配置，通过多次单击这些值来复查和修改配置值。

要提供一组新的配置，请选择&#x200B;**[!UICONTROL Upload New Config]**，然后将包含Model配置的JSON文件拖到浏览器窗口中。 选择&#x200B;**[!UICONTROL Finish]**&#x200B;以创建模型。

>[!NOTE]
>
>配置是唯一的，且特定于其预期的方法，这意味着零售销售方法的配置将不适用于产品Recommendations方法。 有关零售销售方法配置的列表，请参阅[reference](#reference)部分。

![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## 创建培训运行

在Experience Platform中，选择左侧导航中的&#x200B;**[!UICONTROL Models]**&#x200B;选项卡，然后选择浏览选项卡以视图现有模型。 查找并选择附加到要训练的模型名称的超链接。

![](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

将列出所有具有其当前培训状态的现有培训运行。 对于使用[!DNL Data Science Workspace]用户界面创建的模型，将自动生成培训运行，并使用默认配置和输入培训数据集执行培训运行。

通过选择“模型概述”页右上角的&#x200B;**[!UICONTROL Train]**&#x200B;来创建新的培训运行。

![](../images/models-recipes/train-evaluate-ui/model_overview.png)

为培训运行选择培训输入数据集，然后选择&#x200B;**[!UICONTROL Next]**。

![](../images/models-recipes/train-evaluate-ui/training_input.png)

在“模型”(Model)创建过程中提供的默认配置会显示出来，通过按住多次单击这些值，相应地更改和修改这些配置。 选择&#x200B;**[!UICONTROL Finish]**&#x200B;以创建并执行培训运行。

>[!NOTE]
>
>配置是唯一的，且特定于其预期的方法，这意味着零售销售方法的配置将不适用于产品Recommendations方法。 有关零售销售方法配置的列表，请参阅[reference](#reference)部分。

![](../images/models-recipes/train-evaluate-ui/training_configuration.png)


## 评估模型

在Experience Platform中，选择左侧导航中的&#x200B;**[!UICONTROL Models]**&#x200B;选项卡，然后选择浏览选项卡以视图现有模型。 查找并选择附加到要评估的模型名称的超链接。

![选择模型](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

将列出所有具有其当前培训状态的现有培训运行。 对于多个已完成的培训运行，可以在模型评估图表中比较不同培训运行中的评估量度。 使用图表上方的下拉列表选择评估量度。

“平均绝对百分比错误(MAPE)”量度以误差的百分比表示准确性。 这用于识别效果最佳的实验。 MAPE越低越好。

![培训运行概述](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

“精度”量度描述相关实例与已检索的&#x200B;**&#x200B;实例总数的百分比。 精确度可以看作是随机选择的结果正确的概率。

![运行多个运行](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

选择特定培训运行会打开评估页，提供该运行的详细信息。 甚至在运行完成之前也可以执行此操作。 在评估页面上，您可以查看特定于培训运行的其他评估量度、配置参数和可视化。

![预览日志](../images/models-recipes/train-evaluate-ui/evaluate_training.png)

您还可以下载活动日志以查看运行的详细信息。 日志对于失败的运行来查看错误内容尤为有用。

![活动日志](../images/models-recipes/train-evaluate-ui/activity_logs.png)

无法训练超参数，必须通过测试不同的超参数组合来优化模型。 重复此模型培训和评估过程，直到您到达一个优化的模型。

## 后续步骤

本教程向您介绍了如何在[!DNL Data Science Workspace]中创建、培训和评估模型。 到达优化的模型后，您可以使用经过培训的模型生成洞察，方法是遵循UI](./score-model-ui.md)教程中的[对模型评分。

## 参考 {#reference}

### 零售销售方法配置

超参数决定了模型的训练行为，修改超参数将影响模型的精度和精度：

| 超参数 | 描述 | 推荐范围 |
--- | --- | ---
| learning_rate | 学习率通过learning_rate缩小了每棵树的贡献。 学习率和n估计量之间存在着权衡。 | 0.1 | [2 - 10] /估计数 |
| n_maitors | 要执行的提升阶段数。 渐变提升对过拟合相当稳健，因此大量渐变通常会产生更好的性能。 | 100 | 100 - 1000 |
| max_depth | 单个回归估计器的最大深度。 最大深度限制了树中的节点数。 调整此参数以获得最佳性能；最佳值取决于输入变量的交互。 | 3 | 4 - 10 |

其他参数确定模型的技术属性：

| 参数键 | 类型 | 描述 |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | 字符串 | 列表以逗号分隔的输入模式属性。 |
| `ACP_DSW_TARGET_FEATURES` | 字符串 | 列表以逗号分隔的输出模式属性。 |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 布尔值 | 确定输入和输出特征是否可修改 |
| `tenantId` | 字符串 | 此ID可确保您创建的资源命名正确并包含在您的IMS组织中。 [请按照以下](../../xdm/api/getting-started.md#know-your-tenant_id) 步骤查找您的租户ID。 |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 字符串 | 用于培训模型的输入模式。 |
| `evaluation.labelColumn` | 字符串 | 用于评估可视化的列标签。 |
| `evaluation.metrics` | 字符串 | 以逗号分隔的评估量度列表，用于评估模型。 |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 字符串 | 用于对模型进行评分的输出模式。 |
