---
keywords: Experience Platform；演练；数据科学工作区；热门主题
solution: Experience Platform
title: 数据科学工作区演练
topic-legacy: Walkthrough
description: 本文档提供了Adobe Experience Platform数据科学工作区的演练。 具体来说，数据科学家将通过的通用工作流程来使用机器学习来解决问题。
exl-id: d814846e-52a9-46c6-831a-3399241959f2
source-git-commit: 7d98340e7949aadc744513415c4fc7469efd2403
workflow-type: tm+mt
source-wordcount: '1695'
ht-degree: 0%

---

# [!DNL Data Science Workspace] 演练

本文档提供了Adobe Experience Platform [!DNL Data Science Workspace]的演练。 本教程概述了通用的数据科学家工作流程，以及他们如何使用机器学习来解决问题。

## 先决条件

- 已注册的Adobe ID帐户
   - 必须已将Adobe ID帐户添加到具有Adobe Experience Platform和[!DNL Data Science Workspace]访问权限的组织。

## 零售用例

零售商在保持当前市场竞争力方面面临许多挑战。 该零售商的主要关注点之一是确定产品的最佳定价并预测销售趋势。 借助准确的预测模型，零售商将能够找到需求与定价策略之间的关系，并做出优化的定价决策以最大限度地提高销售和收入。

## 数据科学家的解决方案

数据科学家的解决方案是利用零售商提供的丰富历史信息，预测未来趋势并优化定价决策。 此演练使用过去的销售数据来训练机器学习模型，并使用该模型来预测未来销售趋势。 借助此功能，您可以生成分析以帮助进行最佳定价更改。

此概述反映了数据科学家获取数据集并创建模型以预测每周销售额的步骤。 本教程涵盖Adobe Experience Platform [!DNL Data Science Workspace]上零售销售笔记本示例中的以下部分：

- [设置](#setup)
- [浏览数据](#exploring-data)
- [特征工程](#feature-engineering)
- [培训和验证](#training-and-verification)

### [!DNL Data Science Workspace]中的笔记本

在Adobe Experience Platform UI的&#x200B;**[!UICONTROL Data Science]**&#x200B;选项卡中，选择&#x200B;**[!UICONTROL Notebooks]**，以转到[!UICONTROL Notebooks]概述页面。 在此页面中，选择[!DNL JupyterLab]选项卡以启动[!DNL JupyterLab]环境。 [!DNL JupyterLab]的默认登陆页面是&#x200B;**[!UICONTROL Launcher]**。

![](./images/walkthrough/notebooks.png)

![](./images/walkthrough/jupyterlab_launcher.png)

本教程使用[!DNL JupyterLab Notebooks]中的[!DNL Python] 3来显示如何访问和浏览数据。 在“启动器”页面中，提供了示例笔记本。 下面提供的示例中使用了&#x200B;**[!UICONTROL 零售销售]**&#x200B;示例笔记本。

### 设置 {#setup}

打开零售销售笔记本后，您应该首先加载工作流所需的库。 以下列表对后续步骤的示例中使用的每个库进行了简短描述。

- **numpy**:科学的计算库，可增加对大型多维阵列和矩阵的支持
- **熊猫**:提供用于数据处理和分析的数据结构和操作的库
- **matplotlib.pyplot**:绘图库，在绘制时提供类似于MATLAB的体验
- **西博恩** :基于matplotlib的高级界面数据可视化库
- **sklearn**:具有分类、回归、支持向量和聚类算法的机器学习库
- **警告**:控制警告消息的库

### 浏览数据{#exploring-data}

#### 加载数据

加载库后，您可以开始查看数据。 以下[!DNL Python]代码使用pantics&#39; `DataFrame`数据结构和[read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv)函数将[!DNL Github]上托管的CSV读入到pantics DataFrame中：

![](./images/walkthrough/read_csv.png)

熊猫的DataFrame数据结构是一种二维标记数据结构。 要快速查看数据的维度，您可以使用`df.shape`。 这会返回一个表示DataFrame维度的元组：

![](./images/walkthrough/df_shape.png)

最后，您可以预览数据的外观。 可以使用`df.head(n)`查看DataFrame的前`n`行：

![](./images/walkthrough/df_head.png)

#### 统计摘要

利用[!DNL Python's] pantics库获取每个属性的数据类型。 以下调用的输出将提供有关每个列的条目数和数据类型的信息：

```PYTHON
df.info()
```

![](./images/walkthrough/df_info.png)

此信息非常有用，因为了解每列的数据类型将使我们能够了解如何处理数据。

现在，我们来看一下统计摘要。 将只显示数字数据类型，因此将不输出`date`、`storeType`和`isHoliday`:

```PYTHON
df.describe()
```

![](./images/walkthrough/df_describe.png)

通过此，您可以看到每个特征有6435个实例。 此外，还给出了平均值、标准差(std)、最小值、最大值和四分位数等统计信息。 这会提供有关数据偏差的信息。 在下一部分中，您将转到可视化图表，该可视化图表与此信息结合使用，以便我们完全了解您的数据。

通过查看`store`的最小值和最大值，您可以看到有45个唯一存储区来存储数据。 还有`storeTypes`可区分存储区。 通过执行以下操作，可以看到`storeTypes`的分布：

![](./images/walkthrough/df_groupby.png)

这表示22个存储区的数量为`storeType A`,17个存储区的数量为`storeType B`,6个存储区的数量为`storeType C`。

#### 可视化数据

现在，您已了解数据框架值，接下来想要使用可视化图表来补充这些值，以便更清晰、更轻松地识别模式。 在将结果传递给受众时，这些图表也非常有用。

#### 单变量图

单变量图是单个变量的图。 用于显示数据的常见单变量图是框图和晶须图。

使用之前的零售数据集，您可以为45家商店及其每周销售额中的每家，生成方框和须条图。 使用`seaborn.boxplot`函数生成图。

![](./images/walkthrough/box_whisker.png)

用盒状和晶须状图显示数据的分布。 出图的外线显示上四分位点和下四分位点，而框跨越四分位点范围。 框中的线条表示中间值。 超过上四分位数或下四分位数1.5倍的任何数据点都标记为圆。 这些点被视为异常值。

接下来，你可以按时绘制每周的销售情况。 您将仅显示第一个存储的输出。 笔记本中的代码会生成6个图，对应于我们数据集中45个存储中的6个。

![](./images/walkthrough/weekly_sales.png)

通过此图表，您可以比较2年内的每周销售额。 随着时间的推移，销售高峰和低谷模式很容易出现。

#### 多变量图表

多变量图用于查看变量之间的交互。 通过可视化，数据科学家可以查看变量之间是否存在任何关联或模式。 使用的常见多变量图表是关联矩阵。 利用相关矩阵，利用相关系数量化多个变量之间的依赖关系。

使用相同的零售数据集，您可以生成关联矩阵。

![](./images/walkthrough/correlation_1.png)

请注意中间对角线。 这表明，在比较变量本身时，它具有完全正相关。 强正相关度将接近1，而弱关联度将接近0。 负相关显示，负系数显示逆趋势。

### 特征工程{#feature-engineering}

在此部分中，功能工程用于通过执行以下操作来修改您的零售数据集：

- 添加周和年列
- 将storeType转换为指示器变量
- 将isHoliday转换为数值变量
- 预测下周的销售

#### 添加周和年列

日期的当前格式(`2010-02-05`)可能会很难区分每周的数据。 因此，您应将日期转换为包含周和年。

![](./images/walkthrough/date_to_week_year.png)

现在，周和日期如下：

![](./images/walkthrough/date_week_year.png)

#### 将storeType转换为指示器变量

接下来，要将storeType列转换为表示每个`storeType`的列。 有3种存储类型(`A`、`B`、`C`)，您要从中创建3个新列。 在每个值中设置的值是一个布尔值，其中根据`storeType`的值设置“1”，并根据其他2列的`0`的值设置“1”。

![](./images/walkthrough/storeType.png)

将删除当前的`storeType`列。

#### 将isHoliday转换为数字类型

下一个修改是将`isHoliday`布尔值更改为数字表示形式。

![](./images/walkthrough/isHoliday.png)

#### 预测下周的销售

现在，您希望向每个数据集添加以前和未来的每周销售量。 您可以通过偏移`weeklySales`来执行此操作。 此外，还会计算`weeklySales`差。 这是通过减去前一周的`weeklySales`中的`weeklySales`来完成的。

![](./images/walkthrough/weekly_past_future.png)

由于您正在向前偏移`weeklySales`数据45个数据集，向后偏移45个数据集以创建新列，因此前45个和后45个数据点具有NaN值。 您可以使用`df.dropna()`函数从数据集中删除这些点，该函数会删除所有具有NaN值的行。

![](./images/walkthrough/dropna.png)

修改后数据集的摘要如下所示：

![](./images/walkthrough/df_info_new.png)

### 培训和验证{#training-and-verification}

现在，是时候创建一些数据模型，并选择哪种模型在预测未来销售方面表现最佳。 您将评估以下5种算法：

- 线性回归
- 决策树
- 随机森林
- 渐变提升
- K个邻居

#### 将数据集拆分到培训和测试子集

您需要一种方法来了解模型能够预测值的准确程度。 此评估可通过以下方法完成：分配部分数据集以用作验证，其余数据集则用作培训数据。 由于`weeklySalesAhead`是`weeklySales`的实际未来值，因此可以使用它来评估模型在预测值方面的准确度。 拆分操作如下所示：

![](./images/walkthrough/split_data.png)

现在，您有`X_train`和`y_train`来准备模型，并有`X_test`和`y_test`供以后评估。

#### 现场检查算法

在此部分中，将所有算法声明到名为`model`的数组中。 接下来，您遍历此数组，并针对每个算法，使用`model.fit()`输入培训数据，该数据创建一个模型`mdl`。 使用此模型，可以使用`X_test`数据预测`weeklySalesAhead`。

![](./images/walkthrough/training_scoring.png)

对于评分，您将采用预测的`weeklySalesAhead`与`y_test`数据中实际值之间的平均百分比差。 由于您希望将预测与实际结果之间的差异降至最低，因此，“渐变提升回归”(Gradient Boosting Reversessor)是性能最佳的模型。

#### 可视化预测

最后，使用实际的每周销售值来可视化您的预测模型。 蓝线表示实际数字，绿线表示使用渐变提升进行的预测。 以下代码会生成6个图，这些图表示数据集中45个存储中的6个。 此处仅显示`Store 1`:

![](./images/walkthrough/visualize_prediction.png)

## 后续步骤

本文档介绍了用于解决零售销售问题的通用数据科学家工作流程。 总结如下：

- 加载工作流所需的库。
- 加载库后，您可以使用统计摘要、可视化图表和图形开始查看数据。
- 接下来，将使用功能工程功能对零售数据集进行修改。
- 最后，创建数据模型并选择哪种模型在预测未来销售方面表现最佳。

准备就绪后，请首先阅读[JupyterLab用户指南](./jupyterlab/overview.md)，以快速了解Adobe Experience Platform Data Science Workspace中的笔记本。 此外，如果您有兴趣了解模型和方法，请首先阅读[零售销售架构和数据集](./models-recipes/create-retails-sales-dataset.md)教程。
