---
keywords: Experience Platform;walkthrough;Data Science Workspace;popular topics
solution: Experience Platform
title: 数据科学工作区演练
topic: Walkthrough
description: 此文档为Adobe Experience Platform数据科学工作区提供了演练。 具体来说，数据科学家将通过的一般工作流程来解决使用机器学习的问题。
translation-type: tm+mt
source-git-commit: 194a29124949571638315efe00ff0b04bff19303
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 0%

---


# [!DNL Data Science Workspace] 漫游

本文档为Adobe Experience Platform提供了一个演练 [!DNL Data Science Workspace]。 具体来说，我们将讲述一个数据科学家将经历的一般工作流程，用机器学习来解决一个问题。

## 先决条件

- 注册的Adobe ID帐户
   - Adobe ID帐户必须已添加到一个可访问Adobe Experience Platform和 [!DNL Data Science Workspace]

## 数据科学家的动机

在当前市场中，零售商要保持竞争力，面临着许多挑战。 该零售商的主要关注点之一是决定其产品的最优定价，并预测销售趋势。 通过准确的预测模型，零售商将能够找到需求与定价策略之间的关系并做出优化的定价决策，以最大化销售和收入。

## 数据科学家的解决方案

数据科学家的解决方案是利用零售商可以访问的丰富历史数据，预测未来趋势并优化定价决策。 我们将利用过去的销售数据来培训我们的机器学习模型，并使用该模型来预测未来的销售趋势。 通过这种方式，零售商将能够获得洞察，在更改定价时帮助他们。

在此概述中，我们将介绍数据科学家通过的步骤来获取数据集并创建一个模型来预测每周的销售。 我们将浏览Adobe Experience Platform零售销售示例笔记本的以下部分 [!DNL Data Science Workspace]:

- [设置](#setup)
- [浏览数据](#exploring-data)
- [功能工程](#feature-engineering)
- [培训和验证](#training-and-verification)

### 笔记本 [!DNL Data Science Workspace]

首先，我们要创建一个笔记本 [!DNL JupyterLab] ，以打开“零售销售”范例笔记本。 按照笔记本中数据科学家所完成的步骤操作，我们将能够了解典型的工作流程。

在Adobe Experience PlatformUI中，单击顶部菜单中的“数据科学”选项卡，将您带到 [!DNL Data Science Workspace]。 在此页中，单击将打 [!DNL JupyterLab] 开启动器的选 [!DNL JupyterLab] 项卡。 您应当看到一个类似于此的页面。

![](./images/walkthrough/jupyterlab_launcher.png)

在我们的教程中，我们将 [!DNL Python] 使用中的 [!DNL Jupyter Notebook] 3来展示如何访问和浏览数据。 在“启动器”页面中提供了示例笔记本。 我们将使用“零售销售”范例(3 [!DNL Python] )。

![](./images/walkthrough/retail_sales.png)

### 设置 {#setup}

打开零售销售笔记本后，我们要做的第一件事就是加载工作流程所需的库。 以下列表将简短描述每种应用程序的用途：
- **numpy** —— 可添加对大型、多维数组和矩阵支持的科学计算库
- **熊猫** -优惠数据结构和操作用于数据操作和分析的图书馆
- **matplotlib.pyplot** —— 绘图库，在绘制时提供类似MATLAB的体验
- **seaborn** -基于matplotlib的高层界面数据可视化库
- **sklearn** —— 具备分类、回归、支持向量和群集算法的机器学习库
- **警告** -控制警告消息的库

### 浏览数据 {#exploring-data}

#### 加载数据

载入库后，我们可以开始查看数据。 以下代 [!DNL Python] 码使用 `DataFrame` 熊猫的数据 [结构和read_csv()函数将熊猫数据框中托](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) 管的CSV读 [!DNL Github] 入熊猫数据框：

![](./images/walkthrough/read_csv.png)

熊猫的DataFrame数据结构是一种二维标记数据结构。 为了快速查看数据的维度，我们可以使用 `df.shape`。 这会返回表示DataFrame的维度的元组：

![](./images/walkthrough/df_shape.png)

最后，我们可以一睹数据的真实效果。 我们可 `df.head(n)` 以使用视图 `n` DataFrame的前几行：

![](./images/walkthrough/df_head.png)

#### 统计摘要

我们可以利 [!DNL Python's] 用熊猫库来获取每个属性的数据类型。 以下调用的输出将提供有关每个列的条目数和数据类型的信息：

```PYTHON
df.info()
```

![](./images/walkthrough/df_info.png)

此信息非常有用，因为了解每列的数据类型将使我们能够了解如何处理数据。

现在我们来看统计摘要。 将只显示数字数据类 `date`型 `storeType`，并 `isHoliday` 且不输出：

```PYTHON
df.describe()
```

![](./images/walkthrough/df_describe.png)

通过这个，我们可以看到每个特征有6435个实例。 此外，还给出了平均、标准偏差(std)、最小、最大和间隔等统计信息。 这给出了有关数据偏差的信息。 在下一节中，我们将重点介绍可视化功能，这些功能与这些信息一起使用，以便我们能够完全了解我们的数据。

从最小值和最大值看 `store`，我们可以看到有45个数据表示的唯一存储。 店也 `storeTypes` 有差别。 通过执行以下操作， `storeTypes` 我们可以查看分发内容：

![](./images/walkthrough/df_groupby.png)

这意味着22家商店 `storeType A` 是，17 `storeType B`家是，6家 `storeType C`。

#### 可视化数据

既然我们了解了数据帧值，我们想用可视化来补充这一点，使事情更清晰、更容易地识别模式。 这些图在将结果传送到受众时也很有用。

#### 单变量图

单变量图是单个变量的图。 用于可视化数据的通用单变量图是方框图和晶须图。

利用我们以前的零售数据，我们可以为45家商店及其每周销售量中的每家生成包装盒和须条图。 该图是使用该函数生 `seaborn.boxplot` 成的。

![](./images/walkthrough/box_whisker.png)

用方框和晶须图显示数据的分布。 出图的外线显示上和下四分位图，而框跨越四分位图范围。 框中的线标记中间值。 高于上四分之一或下四分之一的任何数据点都标记为圆。 这些点被视为异常值。

接下来，我们可以按时计算每周的销售情况。 我们只显示第一家商店的输出。 笔记本中的代码生成6个图，对应于我们数据集中45个商店中的6个。

![](./images/walkthrough/weekly_sales.png)

通过此图表，我们可以比较2年内的每周销售额。 随着时间推移，销售高峰和低谷很容易出现。

#### 多变量图

多变量图用于查看变量之间的交互。 通过可视化，数据科学家可以发现变量之间是否存在关联或模式。 常用的多变量图是相关矩阵。 利用相关矩阵，用相关系数量化多变量之间的依赖关系。

利用同一个零售数据集，可以生成相关矩阵。

![](./images/walkthrough/correlation_1.png)

注意中间对角线。 这表明，在比较变量本身时，它具有完全正相关性。 强正相关度将接近1，弱正相关度将接近0。 负相关性与负系数呈逆趋势显示。

### 特征工程 {#feature-engineering}

在本节中，我们将修改我们的零售数据集。 我们将执行以下操作：

- 添加周和年列
- 将storeType转换为指示符变量
- 将isHoliday转换为数字变量
- 预测每周下周的销售

#### 添加周和年列

日期()的当前格`2010-02-05`式很难区分数据是每周使用的。 因此，我们将日期转换为周和年。

![](./images/walkthrough/date_to_week_year.png)

现在，周和日期如下：

![](./images/walkthrough/date_week_year.png)

#### 将storeType转换为指示符变量

接下来，我们要将storeType列转换为代表每个列的列 `storeType`。 我们有3种存储类`A`型 `B`( `C`、、)，从中创建新列。 在每个列中设置的值将是布尔值，其中将根据其它2列的原 `storeType` 样 `0` 设置“1”。

![](./images/walkthrough/storeType.png)

将删 `storeType` 除当前列。

#### 将isHoliday转换为数字类型

下一步修改是将布尔值 `isHoliday` 更改为数值表示。

![](./images/walkthrough/isHoliday.png)


#### 预测每周下周的销售

现在，我们希望将之前和未来每周的销售添加到每个数据集。 我们这样做是为了抵消我们的 `weeklySales`。 此外，我们还计算了差 `weeklySales` 异。 这是用上周 `weeklySales` 的减法完成的 `weeklySales`。

![](./images/walkthrough/weekly_past_future.png)

由于我们正在向前偏移45 `weeklySales` 个数据集，向后偏移45个数据集以创建新列，因此前45个数据点和后45个数据点将具有NaN值。 我们可以使用函数从数据集中删除这些点，该函 `df.dropna()` 数删除所有具有NaN值的行。

![](./images/walkthrough/dropna.png)

修改后的数据集摘要如下：

![](./images/walkthrough/df_info_new.png)

### 培训和验证 {#training-and-verification}

现在，是时候创建一些数据模型，选择哪个模型在预测未来销售方面表现最佳。 我们将对以下5种算法进行评估：

- 线性回归
- 决策树
- 随机森林
- 渐变提升
- K邻居

#### 将数据集拆分为培训和测试子集

我们需要一种方法来了解我们的模型能够预测值的准确程度。 此评估可通过分配部分数据集以用作验证，而其余数据集则用作培训数据来完成。 由 `weeklySalesAhead` 于是实际的未来值， `weeklySales`因此我们可以用它来评估模型在预测值时的准确性。 拆分操作如下所示：

![](./images/walkthrough/split_data.png)

我们现在有 `X_train` 准备 `y_train` 这些模型，以 `X_test` 及以 `y_test` 后进行评估。

#### 专题检查算法

在本节中，我们将将所有算法声明到一个名为的数组中 `model`。 接下来，我们对这个数组进行迭代，并针对每个算法输入我们的训练数据， `model.fit()` 用它创建一个模型 `mdl`。 利用这个模型，我们将用我们 `weeklySalesAhead` 的数据来 `X_test` 预测。

![](./images/walkthrough/training_scoring.png)

对于评分，我们采用预测值与数据实际值之 `weeklySalesAhead` 间的平均百分比差 `y_test` 异。 由于我们希望将预测与实际结果的差异降至最低，因此梯度提升回归模型是性能最好的模型。

#### 可视化预测

最后，我们用实际的每周销售值来可视化我们的预测模型。 蓝线表示实际数字，绿色表示使用渐变提升的预测。 以下代码生成6个图，代表我们数据集中45个商店中的6个。 仅 `Store 1` 在此处显示：

![](./images/walkthrough/visualize_prediction.png)

<!--TODO UI Flow> -->

## 结论

通过这个概述，我们回顾了数据科学家将通过的工作流来解决零售销售问题。 具体而言，我们通过以下步骤获得一个可预测未来每周销售额的解决方案。

- [设置](#setup)
- [浏览数据](#exploring-data)
- [功能工程](#feature-engineering)
- [培训和验证](#training-and-verification)