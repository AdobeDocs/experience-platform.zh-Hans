---
keywords: Experience Platform;train and evaluate;Data Science Workspace;popular topics
solution: Experience Platform
title: 培训和评估模型(UI)
topic: Tutorial
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34

---


# 培训和评估模型(UI)

在Adobe Experience Platform Data Science Workspace中，机器学习模型是通过整合与模型意图相适应的现有“处方”来创建的。 然后，对模型进行训练和评估，通过微调其相关的超参数来优化其运行效率和功效。 菜谱是可重用的，这意味着可以使用单个菜谱创建多个模型并针对特定用途进行定制。

本教程将逐步介绍创建、培训和评估模型的步骤。

## 入门指南

要完成本教程，您必须具有Experience Platform的访问权限。 如果您无权访问Experience Platform中的IMS组织，请在继续操作前与系统管理员联系。

本教程需要现有的“菜谱”。 如果您没有菜谱，请按照UI教 [程中的导入打包的菜谱](./import-packaged-recipe-ui.md) ，然后继续。

## 创建模型

1. 在Adobe Experience Platform中，单击左 **[!UICONTROL Models]** 侧导航列中的链接以列表所有现有模型。 单 **[!UICONTROL Create Model]** 击页面右上方附近以开始“模型”(Model)创建过程。
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. 浏览现有菜谱的列表，找到并选择要用于创建模型的菜谱，然后单击 **[!UICONTROL Next]**。
   ![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

3. 选择适当的输入数据集并单击 **[!UICONTROL Next]**。 这将设置“模型”的默认输入培训数据集。
   ![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

4. 为“模型”提供名称并查看默认的“模型”配置。 在创建处方时应用了默认配置，通过多次单击这些值来检查和修改配置值。 要提供新的配置集，请单 **[!UICONTROL Upload New Config]** 击并将包含模型配置的JSON文件拖至浏览器窗口。 单 **[!UICONTROL Finish]** 击以创建模型。
   >[!NOTE]配置是唯一的，且特定于其预期的处方，这意味着零售销售处方的配置将不适用于产品推荐处方。 有关零售 [销售](#reference) 处方配置的列表，请参阅参考部分。

   ![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## 创建培训运行

1. 在Adobe Experience Platform中，单击左 **[!UICONTROL Models]** 侧导航列中的链接以列表所有现有模型。 查找并单击要培训的模型的名称。
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. 将列出所有具有当前培训状态的现有培训运行。 对于使用数据科学工作区用户界面创建的模型，将使用默认配置和输入培训数据集自动生成并执行培训运行。
   ![](../images/models-recipes/train-evaluate-ui/model_overview.png)

3. 单击“模型概述”页 **[!UICONTROL Train]** 面右上方附近，创建新的培训运行。
   ![](../images/models-recipes/train-evaluate-ui/training_input.png)

4. 为培训运行选择培训输入数据集并单击 **[!UICONTROL Next]**。
   ![](../images/models-recipes/train-evaluate-ui/training_configuration.png)

5. 在“模型”(Model)创建过程中提供的默认配置将显示出来，通过多次单击这些值，相应地更改和修改这些配置。 单击 **[!UICONTROL Finish]** 以创建并执行培训运行。
   >[!NOTE]配置是唯一的，且特定于其预期的处方，这意味着零售销售处方的配置将不适用于产品推荐处方。 有关零售 [销售](#reference) 处方配置的列表，请参阅参考部分。

   ![](../images/models-recipes/train-evaluate-ui/training_configuration.png)

## 评估模型

1. 在Adobe Experience Platform中，单击左 **[!UICONTROL Models]** 侧导航列中的链接以列表所有现有模型。 查找并单击要评估的模型的名称。
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. 将列出所有具有当前培训状态的现有培训运行。 对于多个已完成的培训运行，可以在模型评估图表中比较不同培训运行的评估指标，使用图表上方的下拉列表选择评估指标。

   平均绝对百分比误差(MAPE)度量以误差百分比表示精度。 这用于识别效果最佳的实验。 MAPE越低越好。

   ![](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

   “精确度”度量描述相关实例与检索到的实例总数的 *百分比* 。 精确度可以看作是随机选择的结果正确的概率。
   ![](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

   单击特定培训运行以视图该运行的详细信息。 甚至可以在运行完成之前完成此操作。 在“运行详细信息”页上，您可以看到特定于培训运行的其他评估指标、配置参数和可视化。 您还可以下载活动日志以查看运行的详细信息。 日志对于失败的运行来查看出错的内容尤为有用。
   ![](../images/models-recipes/train-evaluate-ui/activity_logs.png)

3. 无法训练超参数，必须通过测试不同的超参数组合来优化模型。 重复此模型培训和评估过程，直到您到达一个优化的模型。

## 后续步骤

本教程向您介绍了如何在数据科学工作区中创建、培训和评估模型。 到达优化模型后，您可以使用经过培训的模型，通过在UI教程中 [对模型评分来生成洞察](./score-model-ui.md) 。

## 参考 {#reference}

### 零售销售处方配置

超参数决定模型的训练行为，修改超参数将影响模型的准确性和精度：

| 超参数 | 描述 | 推荐范围 |
--- | --- | ---
| learning_rate | 学习率通过learning_rate缩减了每棵树的贡献。 学习率和n估计量之间存在权衡。 | 0.1 | [2 - 10] /估计器数 |
| n_mediators | 要执行的提升阶段数。 渐变提升对过拟合相当稳健，因此大数量通常会带来更好的性能。 | 100 | 100 - 1000 |
| max_depth | 单个回归估计器的最大深度。 最大深度限制树中的节点数。 调整此参数以获得最佳性能； 最佳值取决于输入变量的交互。 | 3 | 4 - 10 |

其他参数确定模型的技术属性：

| 参数键 | 类型 | 描述 |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | 字符串 | 列表以逗号分隔的输入模式属性。 |
| `ACP_DSW_TARGET_FEATURES` | 字符串 | 列表以逗号分隔的输出模式属性。 |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 布尔值 | 确定输入和输出功能是否可修改 |
| `tenantId` | 字符串 | 此ID可确保您创建的资源命名正确且包含在IMS组织中。 [按照此处的步骤](../../xdm/api/getting-started.md#know-your-tenant_id) ，查找您的租户ID。 |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 字符串 | 用于培训模型的输入模式。 |
| `evaluation.labelColumn` | 字符串 | 用于评估可视化的列标签。 |
| `evaluation.metrics` | 字符串 | 用于评估模型的评估指标的逗号分隔列表。 |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 字符串 | 用于对模型进行评分的输出模式。 |