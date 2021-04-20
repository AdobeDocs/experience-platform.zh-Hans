---
keywords: Experience Platform;JupyterLab；笔记本；数据科学工作区；热门主题；分析数据笔记
solution: Experience Platform
title: 使用笔记本分析数据
topic: tutorial
type: Tutorial
description: 本教程重点介绍如何使用在数据科学工作区中构建的Jupyter Notebooks来访问、探索和可视化您的数据。
translation-type: tm+mt
source-git-commit: 6908c582cb7e0d60b82112dbc0854411d76b4fd4
workflow-type: tm+mt
source-wordcount: '1733'
ht-degree: 0%

---


# 使用笔记本分析数据

本教程重点介绍如何使用在数据科学工作区中构建的Jupyter Notebooks来访问、探索和可视化您的数据。 在本教程的结尾，您应该了解Jupyter Notebooks优惠的一些功能，以便更好地了解您的数据。

以下概念介绍：

- **[!DNL JupyterLab]:** [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) 是Project Jupyter的下一代基于Web的界面，并紧密集成到其中 [!DNL Adobe Experience Platform]。
- **Batches:** 数据集由批组成。批是在一段时间内收集的一组数据，并作为单个单元一起处理。 将数据添加到数据集时会创建新批。
- **Data Access SDK（已弃用）：** Data Access SDK现在已弃用。请使用[[!DNL Platform SDK]](../authoring/platform-sdk.md)指南。

## 在数据科学工作区中探索笔记本

在本节中，将探索之前引入零售销售模式的数据。

Data Science Workspace允许用户通过[!DNL JupyterLab]平台创建[!DNL Jupyter Notebooks]，在该平台中，他们可以创建和编辑机器学习工作流。 [!DNL JupyterLab] 是一种服务器 — 客户端协作工具，允许用户通过Web浏览器编辑笔记本文档。这些笔记本电脑可同时包含可执行代码和富文本元素。 出于我们的目的，我们将使用Markdown进行分析描述和可执行[!DNL Python]代码，以执行数据探索和分析。

### 选择工作区

启动[!DNL JupyterLab]时，将为Jupyter Notebooks提供一个基于Web的界面。 根据我们选择的笔记本类型，将启动相应的内核。

在比较要使用的环境时，我们必须考虑每项服务的限制。 例如，如果我们将[pactis](https://pandas.pydata.org/)库与[!DNL Python]一起使用，则作为普通用户，RAM限制为2 GB。 即使是高级用户，我们也将仅限20 GB的RAM。 如果处理较大的计算，则使用与所有笔记本实例共享的[!DNL Spark]优惠1.5 TB是有意义的。

默认情况下，Tensorflow菜谱在GPU群集中工作，Python在CPU群集中运行。

### 创建新笔记本

在[!DNL Adobe Experience Platform] UI中，单击顶部菜单中的“数据科学”选项卡，将您带到数据科学工作区。 在此页中，单击将打开[!DNL JupyterLab]启动程序的[!DNL JupyterLab]选项卡。 您应该会看到一个类似于此的页面。

![](../images/jupyterlab/analyze-data/jupyterlab-launcher.png)

在我们的教程中，我们将使用Jupyter笔记本中的[!DNL Python] 3来显示如何访问和浏览数据。 在“启动器”页面中，提供了示例笔记本。 我们将使用[!DNL Python] 3的零售销售菜谱。

![](../images/jupyterlab/analyze-data/retail_sales.png)

零售销售菜谱是一个独立示例，它使用相同的零售销售数据集来显示如何在Jupyter Notebook中探索和可视化数据。 此外，笔记本还通过培训和验证进一步深入。 有关此特定笔记本的详细信息，请参阅此[演练](../walkthrough.md)。

### 访问数据

>[!NOTE]
>
>`data_access_sdk_python`已弃用，不再建议。 要转换代码，请参阅[将数据访问SDK转换为平台SDK](../authoring/platform-sdk.md)教程。 以下相同步骤仍适用于本教程。

我们将从[!DNL Adobe Experience Platform]内部访问数据，从外部访问数据。 我们将使用`data_access_sdk_python`库访问内部数据，如数据集和XDM模式。 对于外部数据，我们将使用[!DNL Python]库。

#### 外部数据

打开零售销售笔记本后，找到“加载数据”标题。 下面的[!DNL Python]代码使用pantics&#39; `DataFrame`数据结构和[read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv)函数将[!DNL Github]上托管的CSV读入DataFrame:

![](../images/jupyterlab/analyze-data/read_csv.png)

熊猫的DataFrame数据结构是一种二维标记数据结构。 要快速查看数据的维度，我们可以使用`df.shape`。 这返回表示DataFrame的维度的元组：

![](../images/jupyterlab/analyze-data/df_shape.png)

最后，我们可以一瞥数据的外观。 我们可以使用`df.head(n)`视图DataFrame的前一行`n`:

![](../images/jupyterlab/analyze-data/df_head.png)

#### [!DNL Experience Platform] 数据

现在，我们将重点介绍访问[!DNL Experience Platform]数据。

##### 按数据集ID

对于此部分，我们使用零售销售数据集，该数据集与零售销售示例笔记本中使用的数据集相同。

在Jupyter Notebook中，您可以从左侧的&#x200B;**数据**&#x200B;选项卡![数据选项卡](../images/jupyterlab/analyze-data/dataset-tab.png)访问数据。 选择该选项卡后，将提供两个文件夹。 选择&#x200B;**[!UICONTROL Datasets]**&#x200B;文件夹。

![](../images/jupyterlab/analyze-data/dataset_tab.png)

现在，在“数据集”目录中，您可以看到所有收录的数据集。 请注意，如果目录中有大量数据集，则加载所有条目可能需要一分钟。

由于数据集是相同的，因此我们希望替换使用外部数据的上一部分中的加载数据。 在&#x200B;**加载数据**&#x200B;下选择代码块，并在键盘上按两次&#x200B;**&#39;d&#39;**&#x200B;键。 确保焦点在块上，而不在文本中。 在按两次&#x200B;**&#39;d&#39;**&#x200B;之前，可以按&#x200B;**&#39;esc&#39;**&#x200B;以转义文本焦点。

现在，我们可以右键单击`Retail-Training-<your-alias>`数据集并在下拉列表中选择“浏览笔记本中的数据”选项。 笔记本中将显示一个可执行代码项。

>[!TIP]
>
>请参阅[[!DNL Platform SDK]](../authoring/platform-sdk.md)指南以转换代码。

```PYTHON
from data_access_sdk_python.reader import DataSetReader
from datetime import date
reader = DataSetReader()
df = reader.load(data_set_id="xxxxxxxx", ims_org="xxxxxxxx@AdobeOrg")
df.head()
```

如果您正在使用除[!DNL Python]之外的其他内核，请参阅[此页](https://github.com/adobe/acp-data-services-dsw-reference/wiki/Accessing-Data-on-the-Platform)以访问[!DNL Adobe Experience Platform]上的数据。

选择可执行文件单元格，然后在工具栏中按播放按钮将运行可执行文件代码。 `head()`的输出将是一个表，数据集的键为列，数据集中的前n行为。 `head()` 接受整数参数以指定要输出的行数。默认情况下，此值为5。

![](../images/jupyterlab/analyze-data/datasetreader_head.png)

如果重新启动内核并再次运行所有单元格，应获得与以前相同的输出。

![](../images/jupyterlab/analyze-data/restart_kernel_run.png)


### 浏览数据

现在，我们可以访问您的数据，让我们通过统计和可视化来关注数据本身。 我们使用的数据集是零售数据集，它提供了有关给定日期45个不同商店的杂项信息。 给定`date`和`store`的某些特性包括：
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

我们可以利用[!DNL Python's]的pantics库来获取每个属性的数据类型。 以下调用的输出将提供有关每个列的条目数和数据类型的信息：

```PYTHON
df.info()
```

![](../images/jupyterlab/analyze-data/df_info.png)

此信息非常有用，因为了解每列的数据类型将使我们能够了解如何处理数据。

现在，让我们看一下统计摘要。 只显示数字数据类型，因此不输出`date`、`storeType`和`isHoliday`:

```PYTHON
df.describe()
```

![](../images/jupyterlab/analyze-data/df_describe.png)

通过这个，我们可以看到每个特征有6435个实例。 同时，给出了平均、标准偏差(std)、最小、最大和中间等统计信息。 这给了我们有关数据偏差的信息。 在下一节中，我们将重点介绍可视化功能，这些功能与这些信息一起使用，以便我们更好地了解我们的数据。

查看`store`的最小值和最大值，我们可以看到有45个数据表示的唯一存储。 还有`storeTypes`可区分存储区。 通过执行以下操作，可以看到`storeTypes`的分布：

![](../images/jupyterlab/analyze-data/df_groupby.png)

这意味着22个存储区`storeType` `A`,17个存储区`storeType` `B`,6个存储区`storeType` `C`。

#### 数据可视化

既然我们了解了数据框架值，我们想用可视化来补充，让事情变得更清晰、更容易地识别模式。 在将结果传送到受众时，图形也很有用。 对可视化有用的[!DNL Python]库包括：
- [马普洛特利布](https://matplotlib.org/)
- [熊猫](https://pandas.pydata.org/)
- [西伯恩](https://seaborn.pydata.org/)
- [g](https://ggplot2.tidyverse.org/)

在本节中，我们将快速介绍使用每个库的一些优势。

[Matplotlibis是](https://matplotlib.org/) 最古老的 [!DNL Python] 可视化包。他们的目标是让“简单易事和困难事情成为可能”。 这往往是事实，因为这个包非常强大，但也带有复杂性。 在不花费大量时间和精力的情况下，获得合理的外观图并不总是件容易的事。

[Pandasis](https://pandas.pydata.org/) 主要用于其DataFrame对象，该对象允许使用集成索引进行数据操作。不过，熊猫还包括一个基于matplotlib的内置绘图功能。

[西](https://seaborn.pydata.org/) 博尼斯在matplotlib上构建一个包。其主要目标是使默认图形在视觉上更具吸引力，并简化复杂图形的创建。

[ggplotis](https://ggplot2.tidyverse.org/) 也构建在matplotlib上的包。但主要区别在于该工具是ggplot2的端口。与西博恩类似，其目标是改进matplotlib。 熟悉ggplot2 for R的用户应考虑此库。


##### 单变量图

单变量图是单个变量的图。 通常的单变量图用于直观地显示您的数据是框图和晶须图。

利用我们以前的零售数据集，我们可以为45家商店及其每周销售量中的每家生成包装盒和晶须图。 图是使用`seaborn.boxplot`函数生成的。

![](../images/jupyterlab/analyze-data/box_whisker.png)

用方框图和晶须图显示数据的分布。 图的外线显示上和下四分位，而框跨越四分位范围。 框中的线标记中间值。 超过上或下四分之一的1.5倍的数据点将标记为圆。 这些点被视为异常值。

##### 多变量图

多变量图用于查看变量之间的交互。 通过可视化，数据科学家可以发现变量之间是否存在关联或模式。 常用的多变量图是相关矩阵。 利用相关矩阵，利用相关系数量化多变量之间的相关性。

使用相同的零售数据集，可以生成相关矩阵。

![](../images/jupyterlab/analyze-data/correlation_1.png)

注意中心下方1的对角线。 这表明，在比较变量本身时，它具有完全正相关性。 强正相关度将接近1，弱关联度将接近0。 负相关与负系数呈反趋势。


## 后续步骤

本教程详细介绍了如何在数据科学工作区中创建新的Jupyter笔记本，以及如何从外部以及从[!DNL Adobe Experience Platform]访问数据。 具体而言，我们完成了以下步骤：
- 创建新的Jupyter笔记本
- 访问数据集和模式
- 浏览数据集

现在，您可以继续访问[下一节](../models-recipes/package-source-files-recipe.md)来打包菜谱并导入到数据科学工作区。