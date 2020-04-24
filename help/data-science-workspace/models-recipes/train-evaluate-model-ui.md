---
keywords: Experience Platform;train and evaluate;Data Science Workspace;popular topics
solution: Experience Platform
title: 培训和评估模型(UI)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# 培训和评估模型(UI)

在Adobe Experience Platform Data Science Workspace中，机器学习模型是通过整合符合模型意图的现有菜谱而创建的。 然后，对模型进行训练和评估，以通过微调其相关的超参数来优化其运行效率和效能。 菜谱是可重用的，这意味着可以使用单个菜谱创建多个模型并根据特定用途进行定制。

本教程将逐步介绍创建、培训和评估模型的步骤。

## 入门指南

要完成本教程，您必须具有Experience Platform的访问权限。 如果您无权访问Experience Platform中的IMS组织，请在继续操作之前与系统管理员联系。

本教程需要现有的“菜谱”。 如果您没有菜谱，请在继续之前， [请按照UI教程中的导入打包的菜谱](./import-packaged-recipe-ui.md) 。

## 创建模型

1. 在Adobe Experience Platform中，单击左侧导 **航列中的** “模型”链接以列表所有现有模型。 单 **击页面右上方附近的“创建模型** ”(Create Model)，开始“模型”(Model)创建过程。
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. 浏览现有菜谱的列表，查找并选择要用于创建模型的菜谱，然后单击“下 **一步”**。
   ![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

3. 选择适当的输入数据集，然后单击“下 **一步”**。 这将设置“模型”的默认输入培训数据集。
   ![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

4. 为“模型”(Model)提供名称并查看默认的“模型”(Model)配置。 在菜谱创建过程中应用了默认配置，通过多次单击这些值来检查和修改配置值。 要提供一组新配置，请单击“上 **传新配置”** ，然后将包含“模型”配置的JSON文件拖入浏览器窗口。 单击 **“完成** ”(Finish)以创建“模型”(Model)。
   >[!NOTE]配置是唯一的，且特定于其预期的菜谱，这意味着零售销售菜谱的配置将不适用于产品推荐菜谱。 有关“零 [售列表](#reference) ”配置的，请参阅参考部分。

   ![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## 创建培训运行

1. 在Adobe Experience Platform中，单击左侧导 **航列中的** “模型”链接以列表所有现有模型。 查找并单击要培训的模型的名称。
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. 将列出所有具有其当前培训状态的现有培训运行。 对于使用Data Science Workspace用户界面创建的模型，系统会使用默认配置和输入培训数据集自动生成并执行培训运行。
   ![](../images/models-recipes/train-evaluate-ui/model_overview.png)

3. 单击“模型”概述页面右上 **角附近的** “培训”，创建新的培训运行。
   ![](../images/models-recipes/train-evaluate-ui/training_input.png)

4. 为培训运行选择培训输入数据集，然后单击“下 **一步”**。
   ![](../images/models-recipes/train-evaluate-ui/training_configuration.png)

5. 在“模型”(Model)创建过程中提供的默认配置会显示出来，通过多次单击这些值，相应地更改和修改这些配置。 单击 **完成** ，创建并执行培训运行。
   >[!NOTE]配置是唯一的，且特定于其预期的菜谱，这意味着零售销售菜谱的配置将不适用于产品推荐菜谱。 有关“零 [售列表](#reference) ”配置的，请参阅参考部分。

   ![](../images/models-recipes/train-evaluate-ui/training_configuration.png)

## 评估模型

1. 在Adobe Experience Platform中，单击左侧导 **航列中的** “模型”链接以列表所有现有模型。 查找并单击要计算的模型的名称。
   ![](../images/models-recipes/train-evaluate-ui/models_browse.png)

2. 将列出所有具有其当前培训状态的现有培训运行。 在“模型”评估图表中，可以对多个已完成的培训运行进行比较评估指标，然后使用图表上方的下拉列表选择评估指标。

   “平均绝对百分比误差”(MAPE)度量以误差的百分比表示准确度。 这用于识别效果最佳的实验。 MAPE越低，越好。

   ![](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

   “精确度”度量描述相关实例与检索到的实例总数的百分 *比* 。 精确度可以看作是随机选择的结果正确的概率。
   ![](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

   单击特定培训运行以视图该运行的详细信息。 即使在运行完成之前，也可以执行此操作。 在运行详细信息页面上，您可以查看特定于培训运行的其他评估指标、配置参数和可视化。 您还可以下载活动日志以查看运行的详细信息。 日志对于失败的运行特别有用，以查看出错的内容。
   ![](../images/models-recipes/train-evaluate-ui/activity_logs.png)

3. 无法训练超参数，必须通过测试不同的超参数组合来优化模型。 重复此模型培训和评估过程，直到您到达优化的模型。

## 后续步骤

本教程向您介绍了在数据科学工作区中创建、培训和评估模型的过程。 到达优化模型后，您可以使用经过培训的模型，通过在UI教程中的模型得分 [来生成洞察](./score-model-ui.md) 。

## 参考 {#reference}

### 零售销售菜谱配置

超参数决定模型的训练行为，修改超参数将影响模型的准确度和精度：

| 超参数 | 描述 | 推荐范围 |
--- | --- | ---
| learning_rate | 学习率通过learning_rate缩小每个树的贡献。 学习率和n估计量之间存在权衡。 | 0.1 | [2 - 10] /估计器数 |
| n_metiators | 要执行的提升阶段数。 渐变提升对过拟合相当稳健，因此大数目通常会带来更好的性能。 | 100 | 100 - 1000 |
| max_depth | 单个回归估计器的最大深度。 最大深度限制树中的节点数。 调整此参数以获得最佳性能；最佳值取决于输入变量的交互。 | 3 | 4 - 10 |

其他参数确定模型的技术属性：

| 参数键 | 类型 | 描述 |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | 字符串 | 列表以逗号分隔的输入模式属性。 |
| `ACP_DSW_TARGET_FEATURES` | 字符串 | 列表以逗号分隔的输出模式属性。 |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Boolean | 确定输入和输出功能是否可修改 |
| `tenantId` | 字符串 | 此ID可确保您创建的资源命名正确并包含在IMS组织中。 [请按照此处的步骤](../../xdm/api/getting-started.md#know-your-tenant-id) ，查找您的租户ID。 |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 字符串 | 用于培训模型的输入模式。 |
| `evaluation.labelColumn` | 字符串 | 用于评估可视化的列标签。 |
| `evaluation.metrics` | 字符串 | 用于评估模型的评估指标的以逗号分隔的列表。 |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 字符串 | 用于对模型进行评分的输出模式。 |