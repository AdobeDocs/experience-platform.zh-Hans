---
keywords: Experience Platform；演练；数据科学工作区；热门主题
solution: Experience Platform
title: 数据科学工作区演练
topic: Walkthrough
description: 此文档为Adobe Experience Platform数据科学工作区提供了演练。 具体来说，数据科学家将通过的一般工作流程来解决使用机器学习的问题。
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '1716'
ht-degree: 0%

---


# [!DNL Data Science Workspace] 漫游

此文档为Adobe Experience Platform[!DNL Data Science Workspace]提供了一个演练。 本教程概述了一般数据科学家工作流程，以及他们如何使用机器学习来解决问题。

## 先决条件

- 注册的Adobe ID帐户
   - Adobe ID帐户必须已添加到有权访问Adobe Experience Platform和[!DNL Data Science Workspace]的组织。

## 零售用例

在当前市场中，零售商要保持竞争力，面临着许多挑战。 零售商的主要关注点之一是决定产品的最优定价，并预测销售趋势。 利用准确的预测模型，零售商将能够找到需求与定价策略之间的关系并做出优化的定价决策，从而最大化销售和收入。

## 数据科学家的解决方案

数据科学家的解决方案是利用零售商提供的丰富历史信息，预测未来趋势并优化定价决策。 本演练使用过去的销售数据来训练机器学习模型，并使用该模型来预测未来的销售趋势。 利用此功能，您可以生成洞察以帮助实现最佳定价更改。

此概述反映了数据科学家在获取数据集和创建模型以预测每周销售额时所经历的步骤。 本教程介绍Adobe Experience Platform[!DNL Data Science Workspace]上的“Sample Retail Sales Notebook（零售销售笔记本示例）”中的以下部分：

- [设置](#setup)
- [浏览数据](#exploring-data)
- [功能工程](#feature-engineering)
- [培训和验证](#training-and-verification)

### [!DNL Data Science Workspace]中的笔记本

在Adobe Experience PlatformUI中，从&#x200B;**[!UICONTROL 数据科学]**&#x200B;选项卡中选择&#x200B;**[!UICONTROL 笔记本]**，以转到[!UICONTROL 笔记本]概述页面。 在此页中，选择[!DNL JupyterLab]选项卡以启动[!DNL JupyterLab]环境。 [!DNL JupyterLab]的默认登陆页是&#x200B;**[!UICONTROL 启动器]**。

![](./images/walkthrough/notebooks.png)

![](./images/walkthrough/jupyterlab_launcher.png)

本教程使用[!DNL JupyterLab Notebooks]中的[!DNL Python] 3来显示如何访问和浏览数据。 在“启动器”页面中提供了示例笔记本。 **[!UICONTROL 零售销售]**&#x200B;示例笔记本在以下示例中使用。

### 设置 {#setup}

打开零售销售笔记本后，您应首先加载工作流程所需的库。 以下列表对后面步骤示例中使用的每个库进行了简短描述。

- **跳跃**:为大型、多维阵列和矩阵添加支持的科学计算库
- **熊猫**:优惠用于数据处理和分析的数据结构和操作的库
- **matplotlib.pyplot**:绘制库，在绘制时提供类似MATLAB的体验
- **西博恩** :基于matplotlib的高层界面数据可视化库
- **sklearn**:具有分类、回归、支持向量和聚类算法的机器学习库
- **警告**:控制警告消息的库

### 浏览数据{#exploring-data}

#### 加载数据

加载库后，您可以开始查看数据。 下面的[!DNL Python]代码使用熊猫&#39; `DataFrame`数据结构和[read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv)函数将[!DNL Github]上托管的CSV读入熊猫数据框：

![](./images/walkthrough/read_csv.png)

熊猫的DataFrame数据结构是一种二维标记数据结构。 要快速查看数据的尺寸，可使用`df.shape`。 这会返回表示DataFrame的维度的元组：

![](./images/walkthrough/df_shape.png)

最后，您可以预览数据的外观。 可以使用`df.head(n)`视图DataFrame的前一行`n`:

![](./images/walkthrough/df_head.png)

#### 统计摘要

我们可以利用[!DNL Python's]熊猫库来获取每个属性的数据类型。 以下调用的输出将提供有关每个列的条目数和数据类型的信息：

```PYTHON
df.info()
```

![](./images/walkthrough/df_info.png)

此信息非常有用，因为了解每列的数据类型将使我们能够了解如何处理数据。

现在我们来看统计摘要。 只显示数字数据类型，因此不会输出`date`、`storeType`和`isHoliday`:

```PYTHON
df.describe()
```

![](./images/walkthrough/df_describe.png)

通过这种方法，您可以看到每个特征有6435个实例。 此外，还给出了平均、标准偏差(std)、最小、最大和间隔等统计信息。 这给出了有关数据偏差的信息。 在下一节中，您将重点介绍可视化功能，这些功能与这些信息配合使用，以便我们全面了解您的数据。

查看`store`的最小值和最大值，您可以看到有45个数据表示的唯一存储。 还有`storeTypes`可区分存储区。 通过执行以下操作，可以看到`storeTypes`的分布：

![](./images/walkthrough/df_groupby.png)

这意味着22个存储区的`storeType A`,17个为`storeType B`,6个为`storeType C`。

#### 可视化数据

既然您了解了数据框架值，您就希望用可视化来补充这一点，使事情更清晰、更容易地识别模式。 这些图在将结果传送到受众时也很有用。

#### 单变量图

单变量图是单个变量的图。 用于可视化数据的通用单变量图是方框图和晶须图。

使用以前的零售数据集，您可以为45家商店及其每周销售量生成包装盒和晶须图。 该图使用`seaborn.boxplot`函数生成。

![](./images/walkthrough/box_whisker.png)

用方框和晶须图显示数据的分布。 出图的外线显示上和下四分位图，而框跨越四分位图范围。 框中的线标记中间值。 高于上四分之一或下四分之一的任何数据点都标记为圆。 这些点被视为异常值。

接下来，您可以按时绘制每周的销售情况。 您将仅显示第一个商店的输出。 笔记本中的代码生成6个图，对应于我们数据集中45个商店中的6个。

![](./images/walkthrough/weekly_sales.png)

通过此图表，您可以比较2年内的每周销售额。 随着时间推移，销售高峰和低谷很容易出现。

#### 多变量图

多变量图用于查看变量之间的交互。 通过可视化，数据科学家可以发现变量之间是否存在关联或模式。 常用的多变量图是相关矩阵。 利用相关矩阵，用相关系数量化多变量之间的依赖关系。

使用相同的零售数据集，您可以生成相关矩阵。

![](./images/walkthrough/correlation_1.png)

注意中间对角线。 这表明，在比较变量本身时，它具有完全正相关性。 强正相关度将接近1，弱正相关度将接近0。 负相关性与负系数呈逆趋势显示。

### 功能工程{#feature-engineering}

在本节中，功能工程用于通过执行以下操作来修改您的零售数据集：

- 添加周和年列
- 将storeType转换为指示符变量
- 将isHoliday转换为数字变量
- 预测每周下周的销售

#### 添加周和年列

日期的当前格式(`2010-02-05`)可能很难区分每周的数据。 因此，您应将日期转换为包含周和年。

![](./images/walkthrough/date_to_week_year.png)

现在，周和日期如下：

![](./images/walkthrough/date_week_year.png)

#### 将storeType转换为指示符变量

接下来，您要将storeType列转换为表示每个`storeType`的列。 有3种存储类型(`A`、`B`、`C`)，您要从中创建3个新列。 在每个列中设置的值是布尔值，其中根据`storeType`的值设置“1”，其他2列的值设置为`0`。

![](./images/walkthrough/storeType.png)

当前`storeType`列已删除。

#### 将isHoliday转换为数字类型

下一步修改是将`isHoliday`布尔值更改为数字表示。

![](./images/walkthrough/isHoliday.png)

#### 预测每周下周的销售

现在，您希望将之前和未来每周的销售添加到每个数据集。 可以通过偏移`weeklySales`来实现。 此外，还计算`weeklySales`差。 这是通过减去`weeklySales`与上周的`weeklySales`来完成的。

![](./images/walkthrough/weekly_past_future.png)

由于您正在向前偏移`weeklySales`数据45个数据集，向后偏移45个数据集以创建新列，因此前45个数据点和后45个数据点都有NaN值。 您可以使用`df.dropna()`函数从数据集中删除这些点，该函数删除所有具有NaN值的行。

![](./images/walkthrough/dropna.png)

修改后的数据集摘要如下所示：

![](./images/walkthrough/df_info_new.png)

### 培训和验证{#training-and-verification}

现在，是时候创建一些数据模型，选择哪个模型在预测未来销售方面表现最佳。 您将评估以下5种算法：

- 线性回归
- 决策树
- 随机森林
- 渐变提升
- K邻居

#### 将数据集拆分为培训和测试子集

您需要一种方法来了解模型能够预测值的准确程度。 此评估可通过分配部分数据集以用作验证，而其余数据集则用作培训数据来完成。 由于`weeklySalesAhead`是`weeklySales`的实际未来值，您可以使用它来评估模型在预测值时的准确性。 拆分操作如下所示：

![](./images/walkthrough/split_data.png)

您现在有`X_train`和`y_train`来准备模型，并有`X_test`和`y_test`以供以后评估。

#### 专题检查算法

在本节中，您将所有算法声明到名为`model`的数组中。 接下来，您对此数组进行迭代，对于每个算法，使用`model.fit()`输入培训数据，该数据创建模型`mdl`。 使用此模型，您可以使用`X_test`数据预测`weeklySalesAhead`。

![](./images/walkthrough/training_scoring.png)

对于评分，您使用预测值`weeklySalesAhead`与`y_test`数据中实际值之间的平均百分比差。 由于您希望将预测与实际结果之间的差异降至最低，因此，梯度提升回归器是效果最佳的模型。

#### 可视化预测

最后，使用实际的每周销售额值可视化您的预测模型。 蓝线表示实际数字，绿色表示使用渐变提升的预测。 以下代码生成6个图，表示数据集中45个商店中的6个。 此处仅显示`Store 1`:

![](./images/walkthrough/visualize_prediction.png)

## 后续步骤

此文档涵盖了用于解决零售销售问题的一般数据科学家工作流程。 总结：

- 加载工作流程所需的库。
- 载入库后，您可以使用统计摘要、可视化和图形开始查看数据。
- 接下来，使用功能工程对您的零售数据集进行修改。
- 最后，创建数据模型并选择预测未来销售效果最佳的模型。

准备就绪后，请阅读[JupyterLab用户指南](./jupyterlab/overview.md)开始Adobe Experience Platform数据科学工作区中的笔记本电脑概览。 此外，如果您有兴趣了解模型和方法，请阅读[零售销售模式和数据集](./models-recipes/create-retails-sales-dataset.md)教程进行开始。 本教程为您准备后续的数据科学工作区教程，可在数据科学工作区[教程页面](../tutorials/data-science-workspace.md)中查看。