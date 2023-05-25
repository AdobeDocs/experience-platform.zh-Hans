---
keywords: Experience Platform；JupyterLab；笔记本；Data Science Workspace；热门主题；分析数据笔记本
solution: Experience Platform
title: 使用笔记本分析数据
type: Tutorial
description: 本教程重点介绍如何使用Jupyter Notebooks（构建于Data Science Workspace内）访问、探索和可视化您的数据。
exl-id: 3b0148d1-9c08-458b-9601-979cb6c7a0fb
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1724'
ht-degree: 0%

---

# 使用笔记本分析数据

本教程重点介绍如何使用Jupyter Notebooks（构建于Data Science Workspace内）访问、探索和可视化您的数据。 在本教程结束时，您应该了解Jupyter Notebooks提供的一些功能，以便更好地了解您的数据。

介绍了以下概念：

- **[!DNL JupyterLab]：** [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) 是Project Jupyter的下一代基于Web的界面，与紧密集成 [!DNL Adobe Experience Platform].
- **批次：** 数据集由批量组成。 批次是指一段时间内收集并作为一个单元一起处理的一组数据。 向数据集中添加数据时会创建新批次。
- **数据访问SDK（已弃用）：** Data Access SDK现已弃用。 请使用 [[!DNL Platform SDK]](../authoring/platform-sdk.md) 指南。

## 探索Data Science Workspace中的笔记本

在本节中，将探究之前摄取到零售模式的数据。

数据科学工作区允许用户创建 [!DNL Jupyter Notebooks] 通过 [!DNL JupyterLab] 他们可以在其中创建和编辑机器学习工作流的平台。 [!DNL JupyterLab] 是一种服务器 — 客户端协作工具，允许用户通过Web浏览器编辑笔记本文档。 这些笔记本可以包含可执行代码和富文本元素。 出于我们的目的，我们将使用Markdown提供分析描述和可执行文件 [!DNL Python] 执行数据探索和分析的代码。

### 选择您的工作区

启动时 [!DNL JupyterLab]，我们为Jupyter Notebooks提供了一个基于Web的界面。 根据选择的笔记本类型，将启动相应的内核。

在比较要使用的环境时，我们必须考虑每个服务的限制。 例如，如果我们使用 [熊猫](https://pandas.pydata.org/) 库 [!DNL Python]，作为常规用户，RAM限制为2 GB。 作为高级用户，我们最多只能使用20 GB的RAM。 如果处理较大的计算，则使用 [!DNL Spark] 它提供1.5 TB的容量，可与所有笔记本实例共享。

默认情况下，Tensorflow方法在GPU群集中工作，Python在CPU群集中运行。

### 创建新笔记本

在 [!DNL Adobe Experience Platform] UI，选择 [!UICONTROL 数据科学] ，以转到数据科学工作区。 在此页面中，选择 [!DNL JupyterLab] 以打开 [!DNL JupyterLab] 发射器。 您应会看到一个类似于此内容的页面。

![](../images/jupyterlab/analyze-data/jupyterlab-launcher-new.png)

在我们的教程中，我们将使用 [!DNL Python] 3 ，以展示如何访问和浏览数据。 在“启动器”页面中，提供了示例笔记本。 我们将使用“零售”方法来 [!DNL Python] 3.

![](../images/jupyterlab/analyze-data/retail_sales.png)

零售方式是一个独立的示例，它使用相同的零售数据集来显示如何在Jupyter Notebook中探索和可视化数据。 此外，该笔记本在培训和验证方面也更加深入。 有关此特定笔记本的更多信息，请参阅此处 [演练](../walkthrough.md).

### 访问数据

>[!NOTE]
>
>此 `data_access_sdk_python` 已弃用，不再推荐。 请参阅 [将数据访问SDK转换为Platform SDK](../authoring/platform-sdk.md) 教程以转换代码。 以下相同步骤仍适用于本教程。

我们将从内部访问数据 [!DNL Adobe Experience Platform] 以及外部数据。 我们将使用 `data_access_sdk_python` 库，用于访问数据集和XDM架构等内部数据。 对于外部数据，我们将使用大熊猫 [!DNL Python] 库。

#### 外部数据

打开零售笔记本后，找到“加载数据”标头。 以下各项 [!DNL Python] 代码使用熊猫 `DataFrame` 数据结构和 [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) 用于读取托管的CSV的函数 [!DNL Github] 到DataFrame：

![](../images/jupyterlab/analyze-data/read_csv.png)

大熊猫的DataFrame数据结构是一种二维标记数据结构。 要快速查看数据的维度，我们可以使用 `df.shape`. 这将返回一个表示DataFrame维度的元组：

![](../images/jupyterlab/analyze-data/df_shape.png)

最后，我们可以看看我们的数据是什么样的。 我们可以使用 `df.head(n)` 查看第一个 `n` DataFrame的行：

![](../images/jupyterlab/analyze-data/df_head.png)

#### [!DNL Experience Platform] 数据

现在，我们将转到访问 [!DNL Experience Platform] 数据。

##### 按数据集ID

对于此部分，我们使用零售业数据集，该数据集与零售业示例笔记本中使用的数据集相同。

在Jupyter Notebook中，您可以从 **数据** 选项卡 ![“数据”选项卡](../images/jupyterlab/analyze-data/dataset-tab.png) 左边。 选择选项卡后，提供了两个文件夹。 选择 **[!UICONTROL 数据集]** 文件夹。

![](../images/jupyterlab/analyze-data/dataset_tab.png)

现在，在“数据集”目录中，您可以看到所有摄取的数据集。 请注意，如果您的目录中填充了大量数据集，则加载所有条目可能需要一分钟。

由于数据集相同，因此我们希望替换使用外部数据的上一节中的加载数据。 选择下的代码块 **加载数据** 然后按下 **&#39;d&#39;** 两次键盘按键。 确保焦点在块上而不是文本中。 您可以按下 **&#39;esc&#39;** 在按之前对文本焦点进行转义 **&#39;d&#39;** 两次。

现在，我们可以右键单击 `Retail-Training-<your-alias>` 数据集，然后在下拉列表中选择“在笔记本中浏览数据”选项。 您的笔记本中将显示一个可执行代码条目。

>[!TIP]
>
>请参阅 [[!DNL Platform SDK]](../authoring/platform-sdk.md) 代码转换指南。

```PYTHON
from data_access_sdk_python.reader import DataSetReader
from datetime import date
reader = DataSetReader()
df = reader.load(data_set_id="xxxxxxxx", ims_org="xxxxxxxx@AdobeOrg")
df.head()
```

如果您使用的是 [!DNL Python]，请参阅 [此页面](https://github.com/adobe/acp-data-services-dsw-reference/wiki/Accessing-Data-on-the-Platform) 以访问 [!DNL Adobe Experience Platform].

选择可执行单元格，然后按工具栏中的播放按钮将运行可执行代码。 输出 `head()` 将是一个表，其中数据集的键为列，而数据集的前n行为列。 `head()` 接受一个整数参数以指定要输出的行数。 默认情况下，此值为5。

![](../images/jupyterlab/analyze-data/datasetreader_head.png)

如果重新启动内核并再次运行所有单元格，则应当获得与之前相同的输出。

![](../images/jupyterlab/analyze-data/restart_kernel_run.png)


### 探索您的数据

现在，我们可以访问您的数据，让我们通过使用统计和可视化来关注数据本身。 我们使用的数据集是一个零售数据集，它提供给定一天45个不同商店的各种信息。 给定的一些特性 `date` 和 `store` 包括以下内容：
- `storeType`
- `weeklySales`
- `storeSize`
- `temperature`
- `regionalFuelPrice`
- `markDown`
- `cpi`
- `unemployment`
- `isHoliday`

#### 统计摘要

我们可以利用 [!DNL Python's] 熊猫库获取每个属性的数据类型。 以下调用的输出将为我们提供有关每个列的条目数和数据类型的信息：

```PYTHON
df.info()
```

![](../images/jupyterlab/analyze-data/df_info.png)

此信息非常有用，因为知道每列的数据类型将使我们能够知道如何处理数据。

现在我们来看看统计摘要。 将仅显示数值数据类型，因此 `date`， `storeType`、和 `isHoliday` 将不会输出：

```PYTHON
df.describe()
```

![](../images/jupyterlab/analyze-data/df_describe.png)

这样，我们可以看到每个特征有6435个实例。 此外，还给出了平均值、标准偏差(std)、最小值、最大值和四分位数等统计信息。 这为我们提供了有关数据偏差的信息。 在下一部分中，我们将介绍可视化图表，它可与此信息配合使用，以使我们对数据有很好的理解。

查看最小值和最大值 `store`，我们可以看到数据表示有45个唯一存储。 还有 `storeTypes` 区分商店的含义。 我们可以看到 `storeTypes` ，方法是：

![](../images/jupyterlab/analyze-data/df_groupby.png)

这意味着22家商店属于 `storeType` `A`，17个 `storeType` `B`和6是 `storeType` `C`.

#### 数据可视化

现在我们知道了数据帧值，我们想通过可视化图表来补充这一点，以使事情更清晰、更易于识别模式。 在向受众传达结果时，图形也很有用。 部分 [!DNL Python] 对可视化图表有用的库包括：
- [Matplotlib](https://matplotlib.org/)
- [熊猫](https://pandas.pydata.org/)
- [海港](https://seaborn.pydata.org/)
- [控制图](https://ggplot2.tidyverse.org/)

在本节中，我们将快速介绍使用每个库的一些优势。

[Matplotlib](https://matplotlib.org/) 是最早的 [!DNL Python] 可视化图表包。 他们的目标是让“简单的事情变得容易，困难的事情变得可能”。 这往往是正确的，因为程序包功能非常强大，但也伴随着复杂性。 要获得一张看起来合理的图表，并不总是需要花费大量时间和精力。

[熊猫](https://pandas.pydata.org/) 主要用于其DataFrame对象，允许使用集成索引进行数据操作。 不过，熊猫还包括基于matplotlib的内置绘图功能。

[海港](https://seaborn.pydata.org/) 是在matplotlib之上的包构建。 它的主要目标是使默认图形更具吸引力，并简化复杂图形的创建。

[控制图](https://ggplot2.tidyverse.org/) 是一个同样基于matplotlib构建的包。 但主要区别在于，该工具是R的ggplot2端口。与seaborn类似，其目的是改进matplotlib。 熟悉R的ggplot2的用户应考虑此库。


##### 单变量图

单变量图是指单个变量的图形。 盒形图和胡须图是用来可视化数据的常用单变量图。

使用我们之前提供的零售数据集，我们可以为45家商店中的每家及其每周销售额生成盒子和胡须图。 使用下列方式生成绘图 `seaborn.boxplot` 函数。

![](../images/jupyterlab/analyze-data/box_whisker.png)

盒子和晶须图用于显示数据的分布。 图的外线显示上四分位数和下四分位数，而框跨越四分位数之间的范围。 方框中的线条标记中间值。 任何超过四分位数上方或下方1.5倍的数据点均标记为圆形。 这些点被视为离群值。

##### 多变量图

多变量图用于查看变量之间的交互。 通过可视化，数据科学家可以看到变量之间是否存在任何关联或模式。 常用的多变量图是关联矩阵。 利用相关矩阵，用相关系数量化多个变量之间的相关性。

使用相同的零售数据集，我们可以生成关联矩阵。

![](../images/jupyterlab/analyze-data/correlation_1.png)

注意中心对角线1的向下。 这表明在比较变量和变量本身时，变量具有完全正相关性。 强正关联强度更接近1，弱关联强度更接近0。 负相关系数呈反趋势，负相关系数呈反趋势。


## 后续步骤

本教程介绍了如何在数据科学工作区中创建新的Jupyter Notebook，以及如何从外部访问数据 [!DNL Adobe Experience Platform]. 具体来说，我们执行了以下步骤：
- 创建新的Jupyter Notebook
- 访问数据集和架构
- 浏览数据集

现在您已准备好继续使用 [下一节](../models-recipes/package-source-files-recipe.md) 打包方法并导入到数据科学工作区中。
