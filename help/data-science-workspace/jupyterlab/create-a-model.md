---
keywords: Experience Platform；JupyterLab；方法；笔记本；Data Science Workspace；热门主题；创建方法
solution: Experience Platform
title: 使用JupyterLab Notebooks创建模型
type: Tutorial
description: 本教程将指导您完成使用JupyterLab Notebooks方法生成器模板创建方法所需的步骤。
exl-id: d3f300ce-c9e8-4500-81d2-ea338454bfde
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '2119'
ht-degree: 0%

---

# 使用JupyterLab Notebooks创建模型

本教程将指导您完成使用JupyterLab笔记本方法生成器模板创建模型的所需步骤。

## 引入的概念：

- **配方：** 配方是模型规范的Adobe术语，是表示特定机器学习、AI算法或算法组合、处理逻辑和构建和执行训练模型所需的配置的顶级容器。
- **型号：** 模型是机器学习方法的一个实例，它使用历史数据和配置进行培训以针对业务用例进行解析。
- **培训：** 训练是从标记数据中学习模式和见解的过程。
- **评分：** 评分是使用经过训练的模型从数据生成洞察的过程。

## 下载所需的资产 {#assets}

在继续本教程之前，您必须创建所需的架构和数据集。 访问教程，了解 [创建Luma倾向模型架构和数据集](../models-recipes/create-luma-data.md) 下载所需的资源和设置先决条件。

## 开始使用 [!DNL JupyterLab] 笔记本环境

从头开始创建方法可以在中完成 [!DNL Data Science Workspace]. 要开始，请导航到 [Adobe Experience Platform](https://platform.adobe.com) 并选择 **[!UICONTROL Notebooks]** 选项卡。 要创建新笔记本，请从中选择方法生成器模板 [!DNL JupyterLab Launcher].

此 [!UICONTROL 方法生成器] 笔记本允许您在笔记本内运行训练和评分运行。 这让您能够灵活地更改其 `train()` 和 `score()` 方法实验之间对训练数据和评分数据进行实验。 如果您对训练和评分的输出感到满意，则可以创建一个方法，然后使用该方法为功能建模并将其作为模型发布。

>[!NOTE]
>
>此 [!UICONTROL 方法生成器] notebook支持使用所有文件格式，但目前仅支持创建方法功能 [!DNL Python].

![](../images/jupyterlab/create-recipe/recipe_builder-new.png)

当您选择 [!UICONTROL 方法生成器] 从启动器中打开笔记本，笔记本将在新选项卡中打开。

在顶部的新笔记本选项卡中，将加载一个包含三个附加操作的工具栏 —  **[!UICONTROL 训练]**， **[!UICONTROL 分数]**、和 **[!UICONTROL 创建方法]**. 这些图标仅显示在 [!UICONTROL 方法生成器] 笔记本。 提供了有关这些操作的更多信息 [在训练和评分部分中](#training-and-scoring) 在笔记本中构建您的方法后。

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## 开始使用 [!UICONTROL 方法生成器] 笔记本

在提供的assets文件夹中，为Luma倾向模型 `propensity_model.ipynb`. 使用JupyterLab中的“上载笔记本”选项，上载提供的型号并打开笔记本。

![上传笔记本](../images/jupyterlab/create-recipe/upload_notebook.png)

本教程的其余部分介绍了在倾向性模型笔记本中预定义的以下文件：

- [要求文件](#requirements-file)
- [配置文件](#configuration-files)
- [训练数据加载器](#training-data-loader)
- [评分数据加载器](#scoring-data-loader)
- [管道文件](#pipeline-file)
- [计算器文件](#evaluator-file)
- [数据保存程序文件](#data-saver-file)

以下视频教程介绍Luma倾向模型笔记本：

>[!VIDEO](https://video.tv.adobe.com/v/333570)

### 要求文件 {#requirements-file}

要求文件用于声明您希望在模型中使用的其他库。 如果存在依赖关系，则可以指定版本号。 要查找其他库，请访问 [anaconda.org](https://anaconda.org). 要了解如何格式化要求文件，请访问 [Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-file-manually). 已在使用中的主库列表包括：

```JSON
python=3.6.7
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>您添加的库或特定版本可能与上述库不兼容。 此外，如果您选择手动创建环境文件， `name` 字段不能被覆盖。

对于Luma倾向模型笔记本，无需更新要求。

### 配置文件 {#configuration-files}

配置文件， `training.conf` 和 `scoring.conf`，用于指定您希望用于训练和评分以及添加超参数的数据集。 有单独的训练和评分配置。

为了使模型运行训练，您必须提供 `trainingDataSetId`， `ACP_DSW_TRAINING_XDM_SCHEMA`、和 `tenantId`. 此外，对于评分，您必须提供 `scoringDataSetId`， `tenantId`、和 `scoringResultsDataSetId `.

要查找数据集和架构ID，请转到“数据”选项卡 ![“数据”选项卡](../images/jupyterlab/create-recipe/dataset-tab.png) （在文件夹图标下）左侧导航栏中的notebooks。 需要提供三个不同的数据集ID。 此 `scoringResultsDataSetId` 用于存储模型评分结果，并且应当为空数据集。 这些数据集以前是在 [所需资产](#assets) 步骤。

![](../images/jupyterlab/create-recipe/dataset_tab.png)

相同的信息可在上找到 [Adobe Experience Platform](https://platform.adobe.com/) 在 **[架构](https://platform.adobe.com/schema)** 和 **[数据集](https://platform.adobe.com/dataset/overview)** 选项卡。

竞争后，您的训练和评分配置应类似于以下屏幕快照：

![配置](../images/jupyterlab/create-recipe/config.png)

默认情况下，在训练数据和为数据评分时，会为您设置以下配置参数：

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## 了解培训数据加载器 {#training-data-loader}

训练数据加载器的目的是实例化用于创建机器学习模型的数据。 通常，培训数据加载器会完成以下两个任务：

- 正在加载数据 [!DNL Platform]
- 数据准备和功能设计

以下两个部分将重新加载数据和准备数据。

### 正在加载数据 {#loading-data}

此步骤使用 [熊猫数据流](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html). 数据可以从中的文件加载 [!DNL Adobe Experience Platform] 使用 [!DNL Platform] SDK (`platform_sdk`)，或从外部来源使用大熊猫 `read_csv()` 或 `read_json()` 函数。

- [[!DNL Platform SDK]](#platform-sdk)
- [外部源](#external-sources)

>[!NOTE]
>
>在配方生成器笔记本中，数据通过 `platform_sdk` 数据加载器。

### [!DNL Platform] SDK {#platform-sdk}

有关使用的深入教程 `platform_sdk` 数据加载器，请访问 [Platform SDK指南](../authoring/platform-sdk.md). 本教程提供有关构建身份验证、数据基本读取和数据基本写入的信息。

### 外部源 {#external-sources}

本节介绍如何将JSON或CSV文件导入Pandas对象。 大熊猫图书馆的官方文件可在以下网址找到：
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

首先，是导入CSV文件的示例。 此 `data` 参数是CSV文件的路径。 此变量导入自 `configProperties` 在 [上一节](#configuration-files).

```PYTHON
df = pd.read_csv(data)
```

您还可以从JSON文件导入。 此 `data` 参数是CSV文件的路径。 此变量导入自 `configProperties` 在 [上一节](#configuration-files).

```PYTHON
df = pd.read_json(data)
```

现在，您的数据位于数据流对象中，并且可以在中分析和处理 [下一节](#data-preparation-and-feature-engineering).

## 培训数据加载器文件

在此示例中，数据是使用Platform SDK加载的。 可通过在页面顶部包含以下行来导入库：

`from platform_sdk.dataset_reader import DatasetReader`

然后，您可以使用 `load()` 从中获取训练数据集的方法 `trainingDataSetId` 在配置中设置(`recipe.conf`)文件。

```PYTHON
def load(config_properties):
    print("Training Data Load Start")

    #########################################
    # Load Data
    #########################################    
    client_context = get_client_context(config_properties)
    dataset_reader = DatasetReader(client_context, dataset_id=config_properties['trainingDataSetId'])
```

>[!NOTE]
>
>如 [“配置文件”部分](#configuration-files)，在使用从Experience Platform访问数据时为您设置了以下配置参数 `client_context = get_client_context(config_properties)`：
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


现在您已经拥有了数据，接下来可以从数据准备和功能工程开始。

### 数据准备和功能设计 {#data-preparation-and-feature-engineering}

加载数据后，需要清理数据并进行数据准备。 在此示例中，模型的目标是预测客户是否会订购产品。 由于模型未查看特定产品，因此您不需要 `productListItems` 因此会丢弃该列。 接下来，将删除只在一列中包含单个值或两个值的其他列。 在训练模型时，请务必仅保留有助于预测目标的有用数据。

![数据准备示例](../images/jupyterlab/create-recipe/data_prep.png)

一旦删除了任何不必要的数据，即可开始特征工程。 用于此示例的演示数据不包含任何会话信息。 通常，您需要特定客户的当前会话和过去会话的数据。 由于缺少会话信息，此示例改为通过历程划分来模拟当前和过去的会话。

![历程分界](../images/jupyterlab/create-recipe/journey_demarcation.png)

完成分界后，数据将进行标记，并创建一个历程。

![标记数据](../images/jupyterlab/create-recipe/label_data.png)

接下来，创建特征并将其分为过去和现在。 然后，任何不必要的列都会被丢弃，从而为您留下Luma客户的过去和当前历程。 这些历程包含诸如客户是否购买了一个项目以及购买之前所经历的历程等信息。

![最终当前培训](../images/jupyterlab/create-recipe/final_journey.png)

## 评分数据加载器 {#scoring-data-loader}

加载用于评分的数据的过程与加载训练数据类似。 仔细查看代码，您可以看到除了 `scoringDataSetId` 在 `dataset_reader`. 这是因为训练和评分使用的是相同的Luma数据源。

如果您希望使用不同的数据文件来进行训练和评分，训练和评分数据加载器是分开的。 这样，您就可以执行其他预处理，如在必要时将培训数据映射到评分数据。

## 管道文件 {#pipeline-file}

此 `pipeline.py` 文件包含训练和评分的逻辑。

培训的目的在于使用培训数据集中的功能和标签创建模型。 选择训练模型后，必须将x和y训练数据集适合模型，并且函数会返回经过训练的模型。

>[!NOTE]
> 
>特征是指机器学习模型用来预测标签的输入变量。

![def火车](../images/jupyterlab/create-recipe/def_train.png)

此 `score()` 函数应包含评分算法并返回一个衡量标准以指示模型执行的有效性。 此 `score()` 函数使用评分数据集标签和训练好的模型生成一组预测特征。 然后，将这些预测值与评分数据集中的实际特征进行比较。 在此示例中， `score()` 函数使用训练好的模型，使用评分数据集中的标签来预测特征。 返回预测的特征。

![def分数](../images/jupyterlab/create-recipe/def_score.png)

## 计算器文件 {#evaluator-file}

此 `evaluator.py` 文件包含有关如何评估训练的方法以及如何拆分训练数据的逻辑。

### 拆分数据集 {#split-the-dataset}

训练的数据准备阶段需要拆分数据集以用于训练和测试。 此 `val` 模型训练后，隐式使用数据对模型进行评估。 此过程与评分不同。

此部分显示 `split()` 函数将数据加载到笔记本中，然后通过删除数据集中不相关的列来清理数据。 从那里，可以执行特征工程，即从数据中的现有原始特征创建其它相关特征的过程。

![Split函数](../images/jupyterlab/create-recipe/split.png)

### 评估经过训练的模型 {#evaluate-the-trained-model}

此 `evaluate()` 函数在模型训练后执行，并返回一个量度以指示模型的执行效果。 此 `evaluate()` 函数使用测试数据集标签和训练好的模型来预测一组特征。 然后，将这些预测值与测试数据集中的实际特征进行比较。 在此示例中，使用的量度包括 `precision`， `recall`， `f1`、和 `accuracy`. 请注意，该函数返回 `metric` 包含评估指标数组的对象。 这些量度用于评估经过训练的模型的性能。

![评估](../images/jupyterlab/create-recipe/evaluate.png)

添加 `print(metric)` 用于查看量度结果。

![量度结果](../images/jupyterlab/create-recipe/evaluate_metric.png)

## 数据保存程序文件 {#data-saver-file}

此 `datasaver.py` 文件包含 `save()` 函数，用于在测试评分时保存您的预测。 此 `save()` 函数进行预测和使用 [!DNL Experience Platform Catalog] API，将数据写入 `scoringResultsDataSetId` 您指定的 `scoring.conf` 文件。 您可以

![数据保存程序](../images/jupyterlab/create-recipe/data_saver.png)

## 培训和评分 {#training-and-scoring}

当您对笔记本进行更改并想要训练您的方法时，您可以选择栏顶部的相关按钮，以在单元格中创建训练运行。 选择该按钮后，训练脚本的命令和输出日志将显示在笔记本中(在 `evaluator.py` 单元格)。 Conda首先安装所有的依赖项，然后开始训练。

请注意，在运行评分之前，您必须至少运行一次培训。 选择 **[!UICONTROL 运行评分]** 按钮将在训练期间生成的经过训练的模型上得分。 评分脚本将显示在 `datasaver.py`.

出于调试目的，如果您希望查看隐藏的输出，请添加 `debug` 到输出单元的末尾，然后重新运行它。

![训练与得分](../images/jupyterlab/create-recipe/toolbar_actions.png)

## 创建方法 {#create-recipe}

编辑完方法并对训练/评分输出感到满意后，您可以通过选择从笔记本中创建方法 **[!UICONTROL 创建方法]** 右上角。

![](../images/jupyterlab/create-recipe/create-recipe.png)

选择后 **[!UICONTROL 创建方法]**，系统会提示您输入方法名称。 此名称表示创建的实际方法 [!DNL Platform].

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

一旦您选择 **[!UICONTROL 确定]**，方法创建过程随即开始。 这可能需要一些时间，并且会显示一个进度条来代替“创建方法”按钮。 完成后，您可以选择 **[!UICONTROL 查看配方]** 按钮将您转到 **[!UICONTROL 配方]** 选项卡位于 **[!UICONTROL ML模型]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

>[!CAUTION]
>
> - 不删除任何文件单元格
> - 不要编辑 `%%writefile` 文件单元格顶部的行
> - 不要同时在不同笔记本中创建配方


## 后续步骤 {#next-steps}

通过完成本教程，您已了解如何在中创建机器学习模型 [!UICONTROL 方法生成器] 笔记本。 您还了解了如何练习将笔记本用于配方工作流。

继续学习如何使用中的资源 [!DNL Data Science Workspace]，请访问 [!DNL Data Science Workspace] 配方和模型下拉列表。