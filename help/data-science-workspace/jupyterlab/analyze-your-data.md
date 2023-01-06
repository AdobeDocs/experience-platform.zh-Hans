---
keywords: Experience Platform;JupyterLab；笔记本；Data Science Workspace；热门主题；分析数据笔记本
solution: Experience Platform
title: 使用笔记本分析数据
type: Tutorial
description: 本教程重点介绍如何使用在Data Science Workspace中构建的Jupyter Notebooks来访问、探索和可视化您的数据。
exl-id: 3b0148d1-9c08-458b-9601-979cb6c7a0fb
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1724'
ht-degree: 0%

---

# 使用笔记本分析数据

本教程重点介绍如何使用在Data Science Workspace中构建的Jupyter Notebooks来访问、探索和可视化您的数据。 在本教程结束时，您应该了解Jupyter Notebooks提供的一些功能，以便更好地了解您的数据。

将介绍以下概念：

- **[!DNL JupyterLab]:** [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) 是Project Jupyter的新一代基于Web的界面，并紧密集成到 [!DNL Adobe Experience Platform].
- **批次：** 数据集由批量组成。 批处理是在一段时间内收集并作为单个单位一起处理的一组数据。 将数据添加到数据集时会创建新批量。
- **Data Access SDK（已弃用）：** Data Access SDK现已弃用。 请使用 [[!DNL Platform SDK]](../authoring/platform-sdk.md) 的双曲余切值。

## 在Data Science Workspace中浏览笔记本

在此部分中，将探索之前引入零售销售架构的数据。

数据科学工作区允许用户创建 [!DNL Jupyter Notebooks] 到 [!DNL JupyterLab] 平台，用户可以在该平台中创建和编辑机器学习工作流。 [!DNL JupyterLab] 是一种服务器客户端协作工具，允许用户通过web浏览器编辑笔记本文档。 这些笔记本可以同时包含可执行代码和富文本元素。 出于我们的目的，我们将使用Markdown进行分析描述和可执行文件 [!DNL Python] 用于执行数据探索和分析的代码。

### 选择工作区

启动时 [!DNL JupyterLab]，我们为Jupyter Notebooks提供基于Web的界面。 根据我们选择的笔记本类型，将启动相应的内核。

在比较要使用的环境时，我们必须考虑每项服务的限制。 例如，如果我们使用 [熊猫](https://pandas.pydata.org/) 库 [!DNL Python]，作为普通用户， RAM限制为2 GB。 即使是电源用户，我们的RAM也将限制为20 GB。 如果处理较大的计算，则使用 [!DNL Spark] 提供与所有笔记本实例共享的1.5 TB。

默认情况下，Tensorflow方法在GPU群集中工作，Python在CPU群集中运行。

### 创建新笔记本

在 [!DNL Adobe Experience Platform] UI，选择 [!UICONTROL 数据科学] ，以转到数据科学工作区。 在此页面中，选择 [!DNL JupyterLab] 打开 [!DNL JupyterLab] 启动器。 您应会看到与此类似的页面。

![](../images/jupyterlab/analyze-data/jupyterlab-launcher-new.png)

在本教程中，我们将使用 [!DNL Python] 3，以显示如何访问和探索数据。 在“启动器”页面中，提供了示例笔记本。 我们将使用零售销售方法 [!DNL Python] 3.

![](../images/jupyterlab/analyze-data/retail_sales.png)

零售销售方法是一个独立的示例，它使用相同的零售销售数据集来显示如何在Jupyter Notebook中探索和显示数据。 此外，笔记本还进一步深入培训和验证。 有关此特定笔记本的详细信息，请参阅 [演练](../walkthrough.md).

### 访问数据

>[!NOTE]
>
>的 `data_access_sdk_python` 已弃用，不再推荐。 请参阅 [将数据访问SDK转换为Platform SDK](../authoring/platform-sdk.md) 代码转换教程。 以下相同步骤仍适用于本教程。

我们将从内部访问数据 [!DNL Adobe Experience Platform] 和外部数据。 我们将使用 `data_access_sdk_python` 库以访问内部数据，例如数据集和XDM架构。 对于外部数据，我们会用熊猫 [!DNL Python] 库。

#### 外部数据

打开零售销售笔记本后，找到“Load Data”标题。 以下 [!DNL Python] 代码使用熊猫 `DataFrame` 数据结构和 [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) 函数来读取托管在 [!DNL Github] 到DataFrame中：

![](../images/jupyterlab/analyze-data/read_csv.png)

熊猫的DataFrame数据结构是一种二维标记数据结构。 为了快速查看数据的维度，我们可以使用 `df.shape`. 这会返回一个表示DataFrame维度的元组：

![](../images/jupyterlab/analyze-data/df_shape.png)

最后，我们可以一睹数据的样子。 我们可以 `df.head(n)` 查看 `n` DataFrame的行：

![](../images/jupyterlab/analyze-data/df_head.png)

#### [!DNL Experience Platform] 数据

现在，我们将重新访问 [!DNL Experience Platform] 数据。

##### 按数据集ID

对于此部分，我们使用的是零售销售数据集，该数据集与零售销售示例笔记本中使用的数据集相同。

在Jupyter Notebook中，您可以从 **数据** 选项卡 ![“数据”选项卡](../images/jupyterlab/analyze-data/dataset-tab.png) 左边。 选择选项卡后，将提供两个文件夹。 选择 **[!UICONTROL 数据集]** 文件夹。

![](../images/jupyterlab/analyze-data/dataset_tab.png)

现在，在Datasets目录中，您可以看到所有摄取的数据集。 请注意，如果目录中填充了大量数据集，则可能需要一分钟才能加载所有条目。

由于数据集相同，因此我们希望替换使用外部数据的上一部分中的加载数据。 在下选择代码块 **加载数据** 然后按 **&#39;d&#39;** 键盘上键两次。 确保焦点在块上，而不是文本中。 你可以按 **&#39;esc&#39;** 以在按前避开文本焦点 **&#39;d&#39;** 两次。

现在，我们可以右键单击 `Retail-Training-<your-alias>` 数据集，然后在下拉菜单中选择“在笔记本中浏览数据”选项。 可执行代码条目将显示在笔记本中。

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

如果您正在处理除 [!DNL Python]，请参阅 [本页](https://github.com/adobe/acp-data-services-dsw-reference/wiki/Accessing-Data-on-the-Platform) 访问 [!DNL Adobe Experience Platform].

选择可执行单元格，然后按工具栏中的播放按钮将运行可执行代码。 的输出 `head()` 将是一个表，其中包含数据集的键值作为列，且数据集中的前n行为。 `head()` 接受整数参数以指定要输出的行数。 默认情况下，此值为5。

![](../images/jupyterlab/analyze-data/datasetreader_head.png)

如果重新启动内核并再次运行所有单元格，则应获得与之前相同的输出。

![](../images/jupyterlab/analyze-data/restart_kernel_run.png)


### 探索数据

现在，我们可以访问您的数据，接下来让我们使用统计数据和可视化图表来重点关注数据本身。 我们使用的数据集是一个零售数据集，该数据集提供了有关给定日期45个不同商店的其他信息。 给定的一些特征 `date` 和 `store` 包括以下内容：
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

我们可以利用 [!DNL Python's] 熊猫库获取每个属性的数据类型。 以下调用的输出将提供有关每个列的条目数和数据类型的信息：

```PYTHON
df.info()
```

![](../images/jupyterlab/analyze-data/df_info.png)

此信息非常有用，因为了解每列的数据类型将使我们能够了解如何处理数据。

现在，我们来看一下统计摘要。 将只显示数字数据类型，因此 `date`, `storeType`和 `isHoliday` 将不输出：

```PYTHON
df.describe()
```

![](../images/jupyterlab/analyze-data/df_describe.png)

通过这个，我们可以看到每个特征有6435个实例。 给出了平均值、标准差(std)、最小值、最大值和四分位数等统计信息。 这会提供有关数据偏差的信息。 在下一部分中，我们将介绍可视化图表，这些可视化图表与这些信息一起使用，以便我们更好地了解我们的数据。

查看 `store`，则我们可以看到有45个唯一的存储区来代表数据。 还有 `storeTypes` 能区分店面。 我们可以看到 `storeTypes` 通过执行以下操作：

![](../images/jupyterlab/analyze-data/df_groupby.png)

这意味着22家店的 `storeType` `A`, 17个 `storeType` `B`和6 `storeType` `C`.

#### 数据可视化

既然我们知道数据框架的值，我们希望通过可视化图表来补充这些值，以使事物变得更清晰、更便于识别模式。 在将结果传递给受众时，图形也非常有用。 部分 [!DNL Python] 可用于可视化的库包括：
- [马特普洛特利布](https://matplotlib.org/)
- [熊猫](https://pandas.pydata.org/)
- [西伯恩](https://seaborn.pydata.org/)
- [图](https://ggplot2.tidyverse.org/)

在本节中，我们将快速介绍使用每个库的一些优势。

[马特普洛特利布](https://matplotlib.org/) 是最古老的 [!DNL Python] 可视化图表包。 他们的目标是“让事情变得容易，而且有困难”。 这往往是事实，因为这一方案极其强大，但也伴随着复杂性。 在不花费大量时间和精力的情况下，获得合理的外观图并不总是件容易的事。

[熊猫](https://pandas.pydata.org/) 主要用于其DataFrame对象，该对象允许通过集成索引进行数据操作。 但是，熊猫还包括一个内置的绘图功能，该功能基于matplotlib。

[西伯恩](https://seaborn.pydata.org/) 是一个基于matplotlib的包内部版本。 其主要目标是使默认图表更直观，并简化创建复杂图表的过程。

[图](https://ggplot2.tidyverse.org/) 是一个也基于matplotlib构建的包。 但主要区别在于该工具是ggplot2的端口，用于R。与西博恩类似，目标是改进matplotlib。 熟悉gplot2 for R的用户应考虑使用此库。


##### 单变量图

单变量图是单个变量的图。 通常使用单变量图来直观地显示数据，即框图和晶须图。

使用我们以前的零售数据集，我们可以为45家商店及其每周销售量中的每家，生成盒子和晶须图。 绘图是使用 `seaborn.boxplot` 函数。

![](../images/jupyterlab/analyze-data/box_whisker.png)

用盒状和晶须状图显示数据的分布。 出图的外线显示上四分位点和下四分位点，而框跨越四分位点范围。 框中的线条表示中间值。 超过上四分位数或下四分位数1.5倍的任何数据点都标记为圆。 这些点被视为异常值。

##### 多变量图表

多变量图用于查看变量之间的交互。 通过可视化，数据科学家可以查看变量之间是否存在任何关联或模式。 使用的常见多变量图表是关联矩阵。 利用相关矩阵，利用相关系数量化多个变量之间的依赖关系。

使用相同的零售数据集，我们可以生成关联矩阵。

![](../images/jupyterlab/analyze-data/correlation_1.png)

请注意中心下方1的对角线。 这表明，在比较变量本身时，它具有完全正相关。 强正相关度将接近1，而弱关联度将接近0。 负相关显示，负系数显示逆趋势。


## 后续步骤

本教程介绍了如何在数据科学工作区中创建新的Jupyter Notebook，以及如何从外部和从 [!DNL Adobe Experience Platform]. 具体来说，我们完成了以下步骤：
- 创建新的Jupyter笔记本
- 访问数据集和架构
- 浏览数据集

现在，您可以继续 [下一部分](../models-recipes/package-source-files-recipe.md) 来打包方法并导入数据科学工作区。
