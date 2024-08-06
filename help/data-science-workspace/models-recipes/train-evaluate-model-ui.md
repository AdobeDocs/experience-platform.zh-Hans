---
keywords: Experience Platform；训练和评估；数据科学Workspace；热门主题；创建模型；创建训练运行
solution: Experience Platform
title: 在数据科学Workspace UI中培训和评估模型
type: Tutorial
description: 在Adobe Experience Platform数据科学Workspace中，机器学习模型通过合并适用于模型意图的现有方法而创建。 然后对该模型进行训练和评估，以通过微调其相关的超参数来优化其运行效率和功效。 配方可重复使用，这意味着只需一个配方，即可创建多个模型并根据特定目的对其进行定制。
exl-id: 6f674cfa-c123-46a3-80e2-9342fe687976
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 1%

---

# 在数据科学Workspace UI中培训和评估模型

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

在Adobe Experience Platform数据科学Workspace中，机器学习模型通过合并适用于模型意图的现有方法而创建。 然后对该模型进行训练和评估，以通过微调其相关的超参数来优化其运行效率和功效。 配方可重复使用，这意味着只需一个配方，即可创建多个模型并根据特定目的对其进行定制。

本教程将逐步介绍创建、训练和评估模型的步骤。

## 快速入门

要完成本教程，您必须拥有[!DNL Experience Platform]的访问权限。 如果您在[!DNL Experience Platform]中无权访问某个组织，请在继续操作之前与系统管理员联系。

本教程需要现有方法。 如果您没有方法，请按照[在UI中导入打包的方法](./import-packaged-recipe-ui.md)教程中的说明继续操作。

## 创建模型

在Experience Platform中，选择位于左侧导航栏中的&#x200B;**[!UICONTROL 模型]**&#x200B;选项卡，然后选择“浏览”选项卡以查看现有模型。 选择页面右上角附近的&#x200B;**[!UICONTROL 创建模型]**&#x200B;以开始创建模型。

![](../images/models-recipes/train-evaluate-ui/models_browse.png)

浏览现有配方列表，查找并选择用于创建模型的配方，然后选择&#x200B;**[!UICONTROL 下一步]**。
![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

选择适当的输入数据集，然后选择&#x200B;**[!UICONTROL 下一步]**。 这将为模型设置默认输入培训数据集。
![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

提供模型的名称并查看默认模型配置。 在创建处方期间应用了默认配置，通过双击这些值来审阅和修改配置值。

若要提供一组新的配置，请选择&#x200B;**[!UICONTROL 上传新配置]**，然后将包含模型配置的JSON文件拖动到浏览器窗口中。 选择&#x200B;**[!UICONTROL 完成]**&#x200B;以创建模型。

>[!NOTE]
>
>配置是唯一的，并且特定于其预期方法，这意味着零售方法配置不适用于产品Recommendations方法。 有关零售方法配置的列表，请参阅[引用](#reference)部分。

![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## 创建训练运行

在Experience Platform中，选择位于左侧导航栏中的&#x200B;**[!UICONTROL 模型]**&#x200B;选项卡，然后选择“浏览”选项卡以查看现有模型。 查找并选择附加到要训练的模型名称的超链接。

![](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

列出所有现有训练运行及其当前训练状态。 对于使用[!DNL Data Science Workspace]用户界面创建的模型，使用默认配置和输入训练数据集自动生成并执行训练运行。

通过选择模型概述页面右上角附近的&#x200B;**[!UICONTROL 训练]**&#x200B;来创建新的训练运行。

![](../images/models-recipes/train-evaluate-ui/model_overview.png)

为训练运行选择训练输入数据集，然后选择&#x200B;**[!UICONTROL 下一步]**。

![](../images/models-recipes/train-evaluate-ui/training_input.png)

模型创建期间提供的默认配置将显示出来，通过双击值可相应地更改和修改这些配置。 选择&#x200B;**[!UICONTROL 完成]**&#x200B;以创建和执行训练运行。

>[!NOTE]
>
>配置是唯一的，并且特定于其预期方法，这意味着零售方法配置不适用于产品Recommendations方法。 有关零售方法配置的列表，请参阅[引用](#reference)部分。

![](../images/models-recipes/train-evaluate-ui/training_configuration.png)


## 评估模型

在Experience Platform中，选择位于左侧导航栏中的&#x200B;**[!UICONTROL 模型]**&#x200B;选项卡，然后选择浏览选项卡以查看现有模型。 查找并选择附加到要评估的模型名称的超链接。

![选择模型](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

列出所有现有训练运行及其当前训练状态。 对于多个已完成的训练运行，可以在模型评估图表中跨不同的训练运行比较评估指标。 使用图表上方的下拉列表选择评估量度。

平均绝对百分比误差(MAPE)度量以误差百分比表示精度。 这用于识别最佳性能试验。 MAPE越低越好。

![培训运行概述](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

“精度”度量描述了相关实例与总共&#x200B;*个检索实例*&#x200B;的百分比之比。 精度可以看作是随机选择结果正确的可能性。

![正在运行多个运行](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

通过选择特定的训练运行，可通过打开评估页面来提供运行的详细信息。 甚至可以在运行完成之前完成此操作。 在评估页面上，您可以看到特定于训练运行的其他评估指标、配置参数和可视化图表。

![预览日志](../images/models-recipes/train-evaluate-ui/evaluate_training.png)

您还可以下载活动日志以查看运行的详细信息。 日志对于失败运行以查看错误情况特别有用。

![活动日志](../images/models-recipes/train-evaluate-ui/activity_logs.png)

不能训练超参数，必须通过测试不同超参数的组合来优化模型。 重复此模型训练和评估过程，直到到达优化模型为止。

## 后续步骤

本教程将指导您在[!DNL Data Science Workspace]中创建、培训和评估模型。 到达优化模型后，可以使用经过训练的模型生成见解，方法是按照[在UI中对模型评分](./score-model-ui.md)教程进行操作。

## 参考 {#reference}

### 零售方式配置

超参数决定了模型的训练行为，修改超参数将会影响模型的精度和精度：

| 超参数 | 描述 | 建议的范围 |
| --- | --- | --- |
| learning_rate | 学习率通过learning_rate减小每个树的贡献。 学习速率和n估算之间存在一种权衡。 | 0.1 |
| n_estimators | 要执行的提升阶段数。 梯度提升算法对于过拟合有很好的鲁棒性，因此大量梯度提升算法通常可以获得更好的性能。 | 100 |
| max_depth | 单个回归估计值的最大深度。 最大深度限制树中的节点数。 调整此参数以获得最佳性能；最佳值取决于输入变量的交互作用。 | 3 |

其它参数可确定模型的技术属性：

| 参数键 | 类型 | 描述 |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | 字符串 | 逗号分隔的输入架构属性列表。 |
| `ACP_DSW_TARGET_FEATURES` | 字符串 | 逗号分隔的输出架构属性列表。 |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 布尔值 | 确定输入和输出功能是否可修改 |
| `tenantId` | 字符串 | 此ID可确保正确存储您创建的资源，并将其包含在您的组织中。 [按照此处](../../xdm/api/getting-started.md#know-your-tenant_id)的步骤查找您的租户ID。 |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 字符串 | 用于训练模型的输入架构。 |
| `evaluation.labelColumn` | 字符串 | 评估可视化图表的列标签。 |
| `evaluation.metrics` | 字符串 | 用于评估模型的评估指标列表（以逗号分隔）。 |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 字符串 | 用于对模型评分的输出架构。 |
