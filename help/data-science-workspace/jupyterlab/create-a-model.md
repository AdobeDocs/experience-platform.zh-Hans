---
keywords: Experience Platform;JupyterLab；方法；笔记本；Data Science Workspace；热门主题；创建方法
solution: Experience Platform
title: 使用JupyterLab Notebooks创建模型
topic-legacy: tutorial
type: Tutorial
description: 本教程将指导您完成使用JupyterLab笔记本电脑方法生成器模板创建方法所需的步骤。
exl-id: d3f300ce-c9e8-4500-81d2-ea338454bfde
source-git-commit: b4dabd36f54cc571b78a6c6c9535f9f08c403b64
workflow-type: tm+mt
source-wordcount: '2119'
ht-degree: 0%

---

# 使用JupyterLab Notebooks创建模型

本教程将指导您完成使用JupyterLab笔记本电脑方法生成器模板创建模型所需的步骤。

## 引入的概念：

- **方法：** 方法是Adobe对模型规范的术语，是表示构建和执行训练模型所需的特定机器学习、AI算法或算法组合、处理逻辑和配置的顶级容器。
- **模型：** 模型是机器学习方法的一个实例，该方法使用历史数据和配置进行培训，以针对业务用例进行求解。
- **培训：** 培训是从标记数据中学习模式和洞察信息的过程。
- **评分：** 评分是使用经过训练的模型从数据生成洞察的过程。

## 下载所需的资产 {#assets}

在继续本教程之前，您必须创建所需的架构和数据集。 请访问 [创建Luma倾向模型模式和数据集](../models-recipes/create-luma-data.md) 以下载所需的资产并设置先决条件。

## 开始使用 [!DNL JupyterLab] 笔记本环境

您可以在中从头开始创建方法 [!DNL Data Science Workspace]. 要开始，请导航到 [Adobe Experience Platform](https://platform.adobe.com) ，然后选择 **[!UICONTROL 笔记本]** 选项卡。 要创建新笔记本，请从 [!DNL JupyterLab Launcher].

的 [!UICONTROL 方法生成器] 笔记本允许您在笔记本内运行培训和评分。 这样，您就可以灵活地更改 `train()` 和 `score()` 在对训练数据和评分数据运行实验之间进行方法。 在您对培训和评分的结果感到满意后，您就可以创建一个方法，然后使用该方法将其作为模型发布，以对功能进行建模。

>[!NOTE]
>
>的 [!UICONTROL 方法生成器] 笔记本支持使用所有文件格式，但当前创建方法功能仅支持 [!DNL Python].

![](../images/jupyterlab/create-recipe/recipe_builder-new.png)

当您选择 [!UICONTROL 方法生成器] 在启动器中，笔记本在新选项卡中打开。

在顶部的“新笔记本”(new notebook)选项卡中，工具栏会加载，其中包含三个其他操作 —  **[!UICONTROL 火车]**, **[!UICONTROL 得分]**&#x200B;和 **[!UICONTROL 创建方法]**. 这些图标仅显示在 [!UICONTROL 方法生成器] 笔记本。 提供了有关这些操作的更多信息 [培训和评分部分](#training-and-scoring) 在笔记本中构建食谱之后。

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## 开始使用 [!UICONTROL 方法生成器] 笔记本

在提供的assets文件夹中，是一个Luma倾向模型 `propensity_model.ipynb`. 使用JupyterLab中的“上传笔记本”选项，上传提供的型号并打开笔记本。

![上载笔记本](../images/jupyterlab/create-recipe/upload_notebook.png)

本教程的其余部分涵盖在倾向模型笔记本中预定义的以下文件：

- [要求文件](#requirements-file)
- [配置文件](#configuration-files)
- [培训数据加载器](#training-data-loader)
- [评分数据加载器](#scoring-data-loader)
- [管道文件](#pipeline-file)
- [计算器文件](#evaluator-file)
- [数据保护程序文件](#data-saver-file)

以下视频教程介绍Luma倾向模型笔记本：

>[!VIDEO](https://video.tv.adobe.com/v/333570)

### 要求文件 {#requirements-file}

要求文件用于声明您希望在模型中使用的其他库。 如果存在依赖关系，则可以指定版本号。 要查找其他库，请访问 [anaconda.org](https://anaconda.org). 要了解如何设置要求文件的格式，请访问 [孔达](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-file-manually). 已在使用的主库列表包括：

```JSON
python=3.6.7
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>您添加的库或特定版本可能与上述库不兼容。 此外，如果您选择手动创建环境文件，则 `name` 不允许覆盖字段。

对于Luma倾向模型笔记本，无需更新要求。

### 配置文件 {#configuration-files}

配置文件， `training.conf` 和 `scoring.conf`，用于指定您希望用于培训和评分以及添加超参数的数据集。 培训和评分有单独的配置。

要使模型运行培训，您必须提供 `trainingDataSetId`, `ACP_DSW_TRAINING_XDM_SCHEMA`和 `tenantId`. 此外，对于评分，您必须提供 `scoringDataSetId`, `tenantId`和 `scoringResultsDataSetId `.

要查找数据集和架构ID，请转到数据选项卡 ![“数据”选项卡](../images/jupyterlab/create-recipe/dataset-tab.png) 在笔记本中（在文件夹图标下）。 需要提供三个不同的数据集ID。 的 `scoringResultsDataSetId` 用于存储模型评分结果，且应为空数据集。 这些数据集以前是在 [必需资产](#assets) 中。

![](../images/jupyterlab/create-recipe/dataset_tab.png)

可在 [Adobe Experience Platform](https://platform.adobe.com/) 下 **[架构](https://platform.adobe.com/schema)** 和 **[数据集](https://platform.adobe.com/dataset/overview)** 选项卡。

竞争后，您的培训和评分配置应类似于以下屏幕截图：

![配置](../images/jupyterlab/create-recipe/config.png)

默认情况下，在培训和分数数据时，会为您设置以下配置参数：

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## 了解培训数据加载器 {#training-data-loader}

培训数据加载器的目的是实例化用于创建机器学习模型的数据。 通常，培训数据加载器可完成以下两项任务：

- 从加载数据 [!DNL Platform]
- 数据准备和特征工程

以下两节将介绍如何加载数据和准备数据。

### 加载数据 {#loading-data}

此步骤使用 [熊猫数据帧](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html). 数据可从 [!DNL Adobe Experience Platform] 使用 [!DNL Platform] SDK(`platform_sdk`)，或从外部来源使用熊猫 `read_csv()` 或 `read_json()` 函数。

- [[!DNL Platform SDK]](#platform-sdk)
- [外部源](#external-sources)

>[!NOTE]
>
>在方法生成器笔记本中，数据通过 `platform_sdk` 数据加载器。

### [!DNL Platform] SDK {#platform-sdk}

有关使用 `platform_sdk` 数据加载器，请访问 [Platform SDK指南](../authoring/platform-sdk.md). 本教程提供有关构建身份验证、基本数据读取和基本数据写入的信息。

### 外部源 {#external-sources}

此部分将向您展示如何将JSON或CSV文件导入Pantics对象。 熊猫图书馆的官方文件可在此处找到：
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

首先，以下是导入CSV文件的示例。 的 `data` 参数是CSV文件的路径。 此变量是从 `configProperties` 在 [上一部分](#configuration-files).

```PYTHON
df = pd.read_csv(data)
```

您还可以从JSON文件导入。 的 `data` 参数是CSV文件的路径。 此变量是从 `configProperties` 在 [上一部分](#configuration-files).

```PYTHON
df = pd.read_json(data)
```

现在，您的数据位于Dataframe对象中，可以在 [下一部分](#data-preparation-and-feature-engineering).

## 培训数据加载器文件

在此示例中，数据使用Platform SDK加载。 可通过包含以下行，在页面顶部导入库：

`from platform_sdk.dataset_reader import DatasetReader`

然后，您可以使用 `load()` 从获取培训数据集的方法 `trainingDataSetId` 在配置中设置(`recipe.conf`)文件。

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
>如 [配置文件部分](#configuration-files)，在使用从Experience Platform访问数据时，将为您设置以下配置参数 `client_context = get_client_context(config_properties)`:
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


现在，您已掌握数据，接下来可以开始进行数据准备和功能工程。

### 数据准备和特征工程 {#data-preparation-and-feature-engineering}

加载数据后，需要清理数据并进行数据准备。 在此示例中，模型的目标是预测客户是否要订购产品。 由于模型不查看特定产品，因此您不需要 `productListItems` 因此，该列会被删除。 接下来，将删除仅包含单个值或单个列中两个值的其他列。 在培训模型时，必须仅保留有助于预测目标的有用数据。

![数据准备示例](../images/jupyterlab/create-recipe/data_prep.png)

删除任何不必要的数据后，即可开始功能工程。 本示例使用的演示数据不包含任何会话信息。 通常，您会希望拥有特定客户的当前会话和过去会话的数据。 由于缺少会话信息，此示例而是通过历程标定来模拟当前和过去的会话。

![历程标界](../images/jupyterlab/create-recipe/journey_demarcation.png)

标界完成后，将标记数据并创建旅程。

![为数据设置标签](../images/jupyterlab/create-recipe/label_data.png)

接下来，创建这些功能，并将其分为过去和现在。 然后，将删除任何不必要的列，从而为Luma客户保留过去和当前的历程。 这些历程包含诸如客户是否购买了产品以及购买前所花费的历程等信息。

![最近培训](../images/jupyterlab/create-recipe/final_journey.png)

## 评分数据加载器 {#scoring-data-loader}

加载用于评分的数据的过程与加载培训数据类似。 仔细查看代码，您可以看到除 `scoringDataSetId` 在 `dataset_reader`. 这是因为同一Luma数据源用于培训和评分。

如果您希望使用不同的数据文件进行培训和评分，则培训和评分数据加载器是分开的。 这允许您执行其他预处理，例如根据需要将培训数据映射到您的评分数据。

## 管道文件 {#pipeline-file}

的 `pipeline.py` 文件包含用于培训和评分的逻辑。

培训的目的是使用培训数据集中的功能和标签创建模型。 选择培训模型后，必须将x和y培训数据集与该模型相匹配，并且该函数会返回培训的模型。

>[!NOTE]
> 
>功能是指机器学习模型用于预测标签的输入变量。

![def列车](../images/jupyterlab/create-recipe/def_train.png)

的 `score()` 函数应包含评分算法并返回一个测量，以指示模型执行的成功程度。 的 `score()` 函数使用评分数据集标签和训练的模型来生成一组预测特征。 然后，将这些预测值与评分数据集中的实际特征进行比较。 在本例中， `score()` 函数使用经过训练的模型来使用评分数据集中的标签来预测特征。 返回预测的特征。

![def分数](../images/jupyterlab/create-recipe/def_score.png)

## 计算器文件 {#evaluator-file}

的 `evaluator.py` 文件包含有关如何评估培训方法以及如何拆分培训数据的逻辑。

### 拆分数据集 {#split-the-dataset}

培训的数据准备阶段需要拆分要用于培训和测试的数据集。 此 `val` 数据在训练后被隐式用于评估模型。 此过程与评分分开。

此部分显示 `split()` 函数将数据加载到笔记本中，然后通过删除数据集中不相关的列来清理数据。 从此处，您可以执行特征工程，即根据数据中的现有原始特征创建其他相关特征的过程。

![拆分函数](../images/jupyterlab/create-recipe/split.png)

### 评估训练后的模型 {#evaluate-the-trained-model}

的 `evaluate()` 函数在模型训练后执行，并返回一个量度以指示模型执行的成功程度。 的 `evaluate()` 函数使用测试数据集标签和经过训练的模型来预测一组功能。 然后，将这些预测值与测试数据集中的实际特征进行比较。 在本例中，使用的量度包括 `precision`, `recall`, `f1`和 `accuracy`. 请注意，该函数返回 `metric` 包含评估量度数组的对象。 这些量度用于评估受训模型的效果。

![评估](../images/jupyterlab/create-recipe/evaluate.png)

添加 `print(metric)` 用于查看量度结果。

![量度结果](../images/jupyterlab/create-recipe/evaluate_metric.png)

## 数据保护程序文件 {#data-saver-file}

的 `datasaver.py` 文件包含 `save()` 函数，用于在测试评分时保存您的预测。 的 `save()` 函数进行预测和使用 [!DNL Experience Platform Catalog] API，会将数据写入 `scoringResultsDataSetId` 在 `scoring.conf` 文件。 您可以

![数据保护程序](../images/jupyterlab/create-recipe/data_saver.png)

## 培训和评分 {#training-and-scoring}

当您对笔记本进行了更改并想要培训方法时，可以选择栏顶部的关联按钮，以在单元格中创建培训运行。 选择按钮后，培训脚本的命令和输出日志将显示在笔记本(位于 `evaluator.py` 单元格)。 Conda首先安装所有依赖项，然后启动培训。

请注意，在运行评分之前，您必须至少运行一次培训。 选择 **[!UICONTROL 运行评分]** 按钮将根据培训期间生成的培训模型进行分数。 评分脚本显示在 `datasaver.py`.

出于调试目的，如果要查看隐藏的输出，请添加 `debug` 到输出单元格的末尾，并重新运行它。

![训练和评分](../images/jupyterlab/create-recipe/toolbar_actions.png)

## 创建方法 {#create-recipe}

编辑完处方并对培训/评分输出满意后，您可以通过选择 **[!UICONTROL 创建方法]** 在右上方。

![](../images/jupyterlab/create-recipe/create-recipe.png)

选择后 **[!UICONTROL 创建方法]**，系统会提示您输入方法名称。 此名称表示在上创建的实际方法 [!DNL Platform].

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

选择 **[!UICONTROL 确定]**，则处方创建过程将开始。 这可能需要一些时间，并且会显示进度条来代替创建方法按钮。 完成后，您可以选择 **[!UICONTROL 查看方法]** 按钮 **[!UICONTROL 方法]** 选项卡 **[!UICONTROL ML模型]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

>[!CAUTION]
>
> - 请勿删除任何文件单元格
> - 请勿编辑 `%%writefile` 行（位于文件单元格顶部）
> - 不要同时在不同的笔记本中创建菜谱


## 后续步骤 {#next-steps}

完成本教程后，您便学会了如何在 [!UICONTROL 方法生成器] 笔记本。 您还学习了如何练习笔记本，以制作方法工作流。

继续了解如何在 [!DNL Data Science Workspace]，请访问 [!DNL Data Science Workspace] 方法和模型下拉列表。