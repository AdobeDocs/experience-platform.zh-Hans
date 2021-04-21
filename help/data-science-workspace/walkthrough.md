---
keywords: Experience Platform；演练；数据科学工作区；热门主题
solution: Experience Platform
title: 数据科学工作区演练
topic-legacy: Walkthrough
description: 本文档为Adobe Experience Platform Data Science Workspace提供了一个演练。 具体而言，数据科学家将通过的通用工作流来使用机器学习解决问题。
exl-id: d814846e-52a9-46c6-831a-3399241959f2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1709'
ht-degree: 0%

---

# [!DNL Data Science Workspace] 演练

此文档为Adobe Experience Platform [!DNL Data Science Workspace]提供了一个演练。 本教程概述了通用数据科学家工作流程，以及他们如何使用机器学习解决问题。

## 先决条件

- 已注册的Adobe ID帐户
   - Adobe ID帐户必须已添加到可访问Adobe Experience Platform和[!DNL Data Science Workspace]的组织。

## 零售用例

在当前市场中保持竞争力，零售商面临着许多挑战。 零售商的主要担忧之一是决定产品的最优定价，并预测销售趋势。 通过准确的预测模型，零售商将能够找到需求与定价策略之间的关系并做出优化的定价决策，以最大化销售和收入。

## 数据科学家的解决方案

数据科学家的解决方案是利用零售商提供的丰富历史信息，预测未来趋势并优化定价决策。 本演练使用过去的销售数据来训练一个机器学习模型，并使用该模型来预测未来的销售趋势。 利用此功能，您可以生成洞察以帮助实现最佳定价更改。

此概述反映了数据科学家为获取数据集和创建模型以预测每周销售额而将采取的措施。 本教程介绍Adobe Experience Platform [!DNL Data Science Workspace]上的Sample Retail Sales Notebook中的以下部分：

- [设置](#setup)
- [浏览数据](#exploring-data)
- [功能工程](#feature-engineering)
- [培训和验证](#training-and-verification)

### [!DNL Data Science Workspace]中的笔记本

在Adobe Experience Platform UI中，从&#x200B;**[!UICONTROL Data Science]**&#x200B;选项卡中选择&#x200B;**[!UICONTROL Notebooks]**，以转到[!UICONTROL Notebooks]概述页面。 在此页中，选择[!DNL JupyterLab]选项卡以启动[!DNL JupyterLab]环境。 [!DNL JupyterLab]的默认登陆页是&#x200B;**[!UICONTROL Launcher]**。

![](./images/walkthrough/notebooks.png)

![](./images/walkthrough/jupyterlab_launcher.png)

本教程使用[!DNL JupyterLab Notebooks]中的[!DNL Python] 3来显示如何访问和浏览数据。 在“启动器”页面中，提供了示例笔记本。 **[!UICONTROL Retail Sales]**&#x200B;示例笔记本在以下示例中使用。

### 设置 {#setup}

打开零售销售笔记本后，您应首先加载工作流程所需的库。 以下列表对后续步骤中示例中使用的每个库进行了简短描述。

- **跳跃**:添加对大型、多维阵列和矩阵的支持的科学计算库
- **熊猫**:优惠用于数据处理和分析的数据结构和操作的库
- **matplotlib.pyplot**:绘图时提供类似MATLAB的体验的绘图库
- **西博恩** :基于matplotlib的高层界面数据可视化库
- **sklearn**:具有分类、回归、支持向量和群集算法的机器学习库
- **警告**:控制警告消息的库

### 浏览数据{#exploring-data}

#### 加载数据

加载库后，您可以开始查看数据。 下面的[!DNL Python]代码使用pantics&#39; `DataFrame`数据结构和[read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv)函数将[!DNL Github]上托管的CSV读入pantics DataFrame中：

![](./images/walkthrough/read_csv.png)

熊猫的DataFrame数据结构是二维标记的数据结构。 要快速查看数据的尺寸，可使用`df.shape`。 这返回表示DataFrame的维度的元组：

![](./images/walkthrough/df_shape.png)

最后，您可以预览数据的外观。 可以使用`df.head(n)`视图DataFrame的前一行`n`:

![](./images/walkthrough/df_head.png)

#### 统计摘要

我们可以利用[!DNL Python's]的pantics库来获取每个属性的数据类型。 以下调用的输出将提供有关每个列的条目数和数据类型的信息：

```PYTHON
df.info()
```

![](./images/walkthrough/df_info.png)

此信息非常有用，因为了解每列的数据类型将使我们能够了解如何处理数据。

现在，让我们看一下统计摘要。 只显示数字数据类型，因此不输出`date`、`storeType`和`isHoliday`:

```PYTHON
df.describe()
```

![](./images/walkthrough/df_describe.png)

通过这个，您可以看到每个特征有6435个实例。 此外，还给出了平均、标准偏差(std)、最小、最大和四分位数等统计信息。 这给了我们有关数据偏差的信息。 在下一节中，您将浏览可视化功能，这些功能与这些信息配合使用，让我们能够完全了解您的数据。

查看`store`的最小值和最大值，您可以看到有45个数据表示的唯一存储。 还有`storeTypes`可区分存储区。 通过执行以下操作，可以看到`storeTypes`的分布：

![](./images/walkthrough/df_groupby.png)

这意味着22个存储区`storeType A`,17个为`storeType B`,6个为`storeType C`。

#### 可视化数据

既然您了解了数据框架值，您希望用可视化来补充这一点，使事情更清晰、更容易识别模式。 在将结果传送到受众时，这些图形也很有用。

#### 单变量图

单变量图是单个变量的图。 用于可视化数据的常见单变量图是方框图和晶须图。

使用之前的零售数据集，您可以为45家商店及其每周销售量中的每家生成包装盒和晶须图。 图是使用`seaborn.boxplot`函数生成的。

![](./images/walkthrough/box_whisker.png)

用方框图和晶须图显示数据的分布。 图的外线显示上和下四分点，而框跨越四分点范围。 框中的线标记中间值。 超过上或下四分之一的1.5倍的数据点将标记为圆。 这些点被视为异常值。

接下来，您可以按时绘制每周销售情况。 您将仅显示第一个存储的输出。 笔记本中的代码会生成6个图块，对应于我们数据集中45个商店中的6个。

![](./images/walkthrough/weekly_sales.png)

通过此图，您可以比较2年期间的每周销售额。 随着时间的推移，很容易看到销售高峰和低谷模式。

#### 多变量图

多变量图用于查看变量之间的交互。 通过可视化，数据科学家可以发现变量之间是否存在关联或模式。 常用的多变量图是相关矩阵。 利用相关矩阵，利用相关系数量化多变量之间的相关性。

使用相同的零售数据集，您可以生成关联矩阵。

![](./images/walkthrough/correlation_1.png)

注意中间对角线。 这表明，在比较变量本身时，它具有完全正相关性。 强正相关度将接近1，弱关联度将接近0。 负相关与负系数呈反趋势。

### 特征工程{#feature-engineering}

在本节中，功能设计用于通过执行以下操作来修改您的零售数据集：

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

接下来，您要将storeType列转换为表示每个`storeType`的列。 有3种存储类型(`A`、`B`、`C`)，您要从中创建3个新列。 在每个列中设置的值是一个布尔值，其中根据`storeType`是什么设置“1”，而其他2列的`0`设置“1”。

![](./images/walkthrough/storeType.png)

当前`storeType`列被删除。

#### 将isHoliday转换为数字类型

下一步修改是将`isHoliday`布尔值更改为数值表示形式。

![](./images/walkthrough/isHoliday.png)

#### 预测每周下周的销售

现在，您希望将之前和未来的每周销售额添加到每个数据集。 可以通过偏移`weeklySales`执行此操作。 此外，还计算`weeklySales`差值。 这是通过用前一周的`weeklySales`减去`weeklySales`来实现的。

![](./images/walkthrough/weekly_past_future.png)

由于您正在向前偏移`weeklySales`数据45个数据集，向后偏移45个数据集以创建新列，因此前45个和后45个数据点都有NaN值。 您可以使用`df.dropna()`函数从数据集中删除这些点，该函数会删除所有具有NaN值的行。

![](./images/walkthrough/dropna.png)

以下是修改后数据集的摘要：

![](./images/walkthrough/df_info_new.png)

### 培训和验证{#training-and-verification}

现在，是时候创建一些数据模型并选择哪个模型在预测未来销售方面表现最佳。 您将评估以下5种算法：

- 线性回归
- 决策树
- 随机森林
- 渐变提升
- K邻居

#### 将数据集拆分为培训和测试子集

您需要一种方法来了解模型能够预测值的准确程度。 此评估可通过分配部分数据集以用作验证，而其余部分用作培训数据来完成。 由于`weeklySalesAhead`是`weeklySales`的实际未来值，因此您可以使用它来评估模型在预测值时的准确性。 拆分操作如下：

![](./images/walkthrough/split_data.png)

您现在有`X_train`和`y_train`来准备模型，并有`X_test`和`y_test`供以后评估。

#### 专题检查算法

在本节中，您将所有算法声明到名为`model`的数组中。 接下来，您对此数组进行迭代，对于每个算法，使用`model.fit()`输入培训数据，该数据创建一个模型`mdl`。 使用此模型，您可以使用`X_test`数据预测`weeklySalesAhead`。

![](./images/walkthrough/training_scoring.png)

对于评分，您使用预测`weeklySalesAhead`与`y_test`数据中实际值之间的平均百分比差。 由于您希望将预测与实际结果之间的差异降至最低，因此，“渐变提升回归”是效果最佳的模型。

#### 可视化预测

最后，使用实际的每周销售值可视化您的预测模型。 蓝线表示实际数字，绿线表示使用渐变提升的预测。 以下代码生成6个图，表示数据集中45个存储中的6个。 此处仅显示`Store 1`:

![](./images/walkthrough/visualize_prediction.png)

## 后续步骤

此文档涵盖了用于解决零售销售问题的通用数据科学家工作流程。 总结：

- 加载工作流所需的库。
- 加载库后，您可以使用统计摘要、可视化和图形开始查看数据。
- 接下来，使用功能工程对您的零售数据集进行修改。
- 最后，创建数据模型，选择预测未来销售效果最佳的模型。

准备就绪后，请阅读[JupyterLab用户指南](./jupyterlab/overview.md)开始Adobe Experience Platform Data Science Workspace中的笔记本。 此外，如果您有兴趣了解模型和方法，请阅读[零售销售模式和数据集](./models-recipes/create-retails-sales-dataset.md)教程进行开始。 本教程为您准备后续的数据科学工作区教程，这些教程可在数据科学工作区[教程页](../tutorials/data-science-workspace.md)中查看。
