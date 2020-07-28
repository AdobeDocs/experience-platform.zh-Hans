---
keywords: Experience Platform;JupyterLab;recipe;notebooks;Data Science Workspace;popular topics
solution: Experience Platform
title: 使用Jupyter笔记本创建菜谱
topic: Tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '2292'
ht-degree: 0%

---


# 使用Jupyter笔记本创建菜谱

本教程将分两个主要部分。 首先，您将使用中的模板创建机器学习模型 [!DNL JupyterLab Notebook]。 接下来，您将练习笔记本到菜谱工作流程， [!DNL JupyterLab] 在中创建菜谱 [!DNL Data Science Workspace]。

## 引入的概念：

- **菜谱：** 处方是模型规范的Adobe术语，是代表特定机器学习、AI算法或算法集合、处理逻辑和配置的顶级容器，用于构建和执行经过培训的模型，从而帮助解决特定的业务问题。
- **模型：** 模型是机器学习配方的实例，该配方使用历史数据和配置进行培训，以便为业务用例进行解决。
- **培训：** 培训是从标记数据中学习模式和洞察的过程。
- **评分：** 评分是指使用经过培训的模型从数据生成洞察的过程。

## 开始使用笔记本 [!DNL JupyterLab] 环境

您可以在中从头开始创建菜谱 [!DNL Data Science Workspace]。 要进行开始，请导 [航到](https://platform.adobe.com) “Adobe Experience Platform”，然 **[!UICONTROL 后单击左]** 侧的“笔记本”选项卡。 从中选择Recipe Builder模板，创建新笔记本 [!DNL JupyterLab Launcher]。

Recipe Builder [!UICONTROL 笔记本] ，可在笔记本内运行培训和评分运行。 这使您能够灵活地在对培训和评分 `train()` 数据 `score()` 运行实验之间更改其和方法。 一旦您对培训和评分的输出感到满意，您就可以创建一个菜谱，用于使用笔记本 [!DNL Data Science Workspace] 将内置到Recipe Builder笔记本的菜谱功能。

>[!NOTE]
>
>
>Recipe Builder笔记本支持处理所有文件格式，但当前“创建菜谱”功能仅支持 [!DNL Python]。

![](../images/jupyterlab/create-recipe/recipe-builder.png)

当您从启动器单击Recipe Builder笔记本时，该笔记本将在选项卡中打开。 笔记本中使用的模板是Python Retail Sales Forecasting Recipe，您也可以在此公共存储库 [中找到它](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/python/retail/)

您会注意到，在工具栏中有三个附加操作，即 **[!UICONTROL 培训]**、 **[!UICONTROL 得分]** 和 **[!UICONTROL 创建菜谱]**。 这些图标将仅显示在 [!UICONTROL Recipe Builder笔记本] 中。 在笔记本中构建“菜谱”后，将在 [培训和评分部分讨论](#training-and-scoring) 有关这些操作的更多信息。

![](../images/jupyterlab/create-recipe/toolbar_actions.png)

## 编辑菜谱文件

要编辑菜谱文件，请导航到Jupyter中与文件路径对应的单元格。 例如，如果要更改，请 `evaluator.py`查找 `%%writefile demo-recipe/evaluator.py`。

开始对单元格进行必要的更改，完成后，只需运行单元格。 命 `%%writefile filename.py` 令将单元格的内容写入 `filename.py`。 您必须手动为每个文件运行更改的单元格。

>[!NOTE]
>
>如果适用，您应手动运行单元格。

## 开始使用Recipe Builder笔记本

现在您已了解笔记本环境的 [!DNL JupyterLab] 基础知识，可开始查看构成机器学习模型菜谱的文件。 我们将讨论的文件显示在此处：

- [要求文件](#requirements-file)
- [配置文件](#configuration-files)
- [培训数据加载器](#training-data-loader)
- [评分数据加载器](#scoring-data-loader)
- [管道文件](#pipeline-file)
- [求值器文件](#evaluator-file)
- [数据保护程序文件](#data-saver-file)

### 要求文件 {#requirements-file}

要求文件用于声明您希望在菜谱中使用的其他库。 如果存在依赖关系，则可以指定版本号。 要查找其他库，请访问https://anaconda.org。 正在使用的主要库的列表包括：

```JSON
python=3.5.2
scikit-learn
pandas
numpy
data_access_sdk_python
```

>[!NOTE]
>
>
>您添加的库或特定版本可能与上述库不兼容。

### 配置文件 {#configuration-files}

配置文件和 `training.conf` 用 `scoring.conf`于指定您希望用于培训和评分以及添加超参数的数据集。 培训和评分有单独的配置。

用户在运行培训和评分之前必须填写以下变量：
- `trainingDataSetId`
- `ACP_DSW_TRAINING_XDM_SCHEMA`
- `scoringDataSetId`
- `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA`
- `scoringResultsDataSetId`

要查找数据集和模式ID，请转到左侧导航栏（文件夹图标下）笔记本中的“数据选项卡”。

![](../images/jupyterlab/create-recipe/datasets.png)

在Adobe Experience Platform和模式集选项卡 [下](https://platform.adobe.com/) ，可 **[以找](https://platform.adobe.com/schema)**到相**[同](https://platform.adobe.com/dataset/overview)** 的信息。

默认情况下，在访问数据时会为您设置以下配置参数：

- `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
- `ML_FRAMEWORK_IMS_TOKEN`
- `ML_FRAMEWORK_IMS_ML_TOKEN`
- `ML_FRAMEWORK_IMS_TENANT_ID`

## 培训数据加载器 {#training-data-loader}

培训数据加载器的目的是实例化用于创建机器学习模型的数据。 通常，培训数据加载器将完成以下两个任务:
- 从 [!DNL Platform]
- 数据准备和功能工程

以下两个部分将重新加载数据和准备数据。

### 加载数据 {#loading-data}

这一步使用了 [熊猫数据框](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html)。 数据可以使用SDK() [!DNL Adobe Experience Platform] 从文件中加 [!DNL Platform] 载，也可`platform_sdk`以使用熊猫的功能从外部 `read_csv()` 源加载 `read_json()` 数据。

- [!DNL Platform SDK](#platform-sdk)
- [外部源](#external-sources)

>[!NOTE]
>
>
>在Recipe Builder笔记本中，数据通过数据加载 `platform_sdk` 器加载。

### [!DNL Platform] SDK {#platform-sdk}

有关使用数据加载器的详细 `platform_sdk` 教程，请访问 [Platform SDK指南](../authoring/platform-sdk.md)。 本教程提供有关构建身份验证、基本数据读取和基本数据写入的信息。

### 外部源 {#external-sources}

本节将向您介绍如何将JSON或CSV文件导入到Apnotics对象。 熊猫图书馆的官方文件可在以下网址找到：
- [read_csv](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html)
- [read_json](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_json.html)

首先，下面是导入CSV文件的示例。 参 `data` 数是CSV文件的路径。 此变量是从上一 `configProperties` 节中 [导入的](#configuration-files)。

```PYTHON
df = pd.read_csv(data)
```

您还可以从JSON文件导入。 参 `data` 数是CSV文件的路径。 此变量是从上一 `configProperties` 节中 [导入的](#configuration-files)。

```PYTHON
df = pd.read_json(data)
```

现在，您的数据位于数据帧对象中，可在下一节中进行分析 [和处理](#data-preparation-and-feature-engineering)。

### 从数据访问SDK（已弃用）

>[!CAUTION]
>
>
> `data_access_sdk_python` 不再推荐，请参阅将 [数据访问代码转换为平台SDK](../authoring/platform-sdk.md) ，以获取有关使用数据加载器 `platform_sdk` 的指南。

用户可以使用数据访问SDK加载数据。 通过包含以下行，可以在页面顶部导入库：

`from data_access_sdk_python.reader import DataSetReader`

然后，使用 `load()` 该方法从配置()文 `trainingDataSetId` 件中的集合中获取培训`recipe.conf`数据集。

```PYTHON
prodreader = DataSetReader(client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                           user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                           service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

df = prodreader.load(data_set_id=configProperties['trainingDataSetId'],
                     ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])
```

>[!NOTE]
>
>
>如配置文 [件部分所述](#configuration-files)，当您从中访问数据时，将为您设置以下配置参数 [!DNL Experience Platform]:
> - `ML_FRAMEWORK_IMS_USER_CLIENT_ID`
> - `ML_FRAMEWORK_IMS_TOKEN`
> - `ML_FRAMEWORK_IMS_ML_TOKEN`
> - `ML_FRAMEWORK_IMS_TENANT_ID`


现在您拥有了数据，您可以从数据准备和功能工程开始。

### 数据准备和功能工程 {#data-preparation-and-feature-engineering}

加载数据后，数据将进行准备，然后被拆分到数据集 `train` 和数 `val` 据集。 示例代码如下所示：

```PYTHON
#########################################
# Data Preparation/Feature Engineering
#########################################
dataframe.date = pd.to_datetime(dataframe.date)
dataframe['week'] = dataframe.date.dt.week
dataframe['year'] = dataframe.date.dt.year

dataframe = pd.concat([dataframe, pd.get_dummies(dataframe['storeType'])], axis=1)
dataframe.drop('storeType', axis=1, inplace=True)
dataframe['isHoliday'] = dataframe['isHoliday'].astype(int)

dataframe['weeklySalesAhead'] = dataframe.shift(-45)['weeklySales']
dataframe['weeklySalesLag'] = dataframe.shift(45)['weeklySales']
dataframe['weeklySalesDiff'] = (dataframe['weeklySales'] - dataframe['weeklySalesLag']) / dataframe['weeklySalesLag']
dataframe.dropna(0, inplace=True)

dataframe = dataframe.set_index(dataframe.date)
dataframe.drop('date', axis=1, inplace=True) 
```

在此示例中，对原始数据集有五项操作：
- 添加 `week` 和列 `year`
- 转换 `storeType` 为指示符变量
- 转 `isHoliday` 换为数字变量
- 抵 `weeklySales` 销以获得未来和过去销售价值
- 按日期拆分数据至 `train` 和数 `val` 据

首先， `week` 创建列 `year` ，并将原始列转 `date` 换为日期 [!DNL Python] 时 [间](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.to_datetime.html)。 周值和年值从日期时间对象中提取。

接下来 `storeType` ，将转换为表示三种不同存储类型(`A`、 `B`和)的三 `C`列。 每个值都将包含一个布尔值，它 `storeType` 为true。 将 `storeType` 删除该列。

同样， `weeklySales` 将布尔 `isHoliday` 值更改为数字表示，1或0。

此数据分为数据 `train` 集和 `val` 数据集。

函 `load()` 数应以和数 `train` 据集 `val` 为输出。

### 评分数据加载器 {#scoring-data-loader}

加载评分数据的过程与函数中加载培训数据的过程类 `split()` 似。 我们使用数据访问SDK从我们的文 `scoringDataSetId` 件中加载 `recipe.conf` 数据。

```PYTHON
def load(configProperties):

    print("Scoring Data Load Start")

    #########################################
    # Load Data
    #########################################
    prodreader = DataSetReader(client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                               user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                               service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

    df = prodreader.load(data_set_id=configProperties['scoringDataSetId'],
                         ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])
```

数据加载后，进行数据准备和特征工程。

```PYTHON
#########################################
# Data Preparation/Feature Engineering
#########################################
df.date = pd.to_datetime(df.date)
df['week'] = df.date.dt.week
df['year'] = df.date.dt.year

df = pd.concat([df, pd.get_dummies(df['storeType'])], axis=1)
df.drop('storeType', axis=1, inplace=True)
df['isHoliday'] = df['isHoliday'].astype(int)

df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
df.dropna(0, inplace=True)

df = df.set_index(df.date)
df.drop('date', axis=1, inplace=True)

print("Scoring Data Load Finish")

return df
```

由于我们模型的目的是预测未来每周的销售量，因此您需要创建一个评分数据集来评估模型的预测效果。

此Recipe Builder笔记本可通过向后抵销我们的每周销售额7天来实现。 请注意，每周有45个存储区的测量值，这样您就可以将45个 `weeklySales` 数据集向前移入一个名为的新列 `weeklySalesAhead`。

```PYTHON
df['weeklySalesAhead'] = df.shift(-45)['weeklySales']
```

同样，可以通过向后移 `weeklySalesLag` 45来创建列。 使用此选项，您还可以计算每周销售额的差额，并将其存储在列中 `weeklySalesDiff`。

```PYTHON
df['weeklySalesLag'] = df.shift(45)['weeklySales']
df['weeklySalesDiff'] = (df['weeklySales'] - df['weeklySalesLag']) / df['weeklySalesLag']
```

由于您正在向前偏移45 `weeklySales` 个数据集，向后偏移45个数据集以创建新列，因此前45个数据点和最后45个数据点将具有NaN值。 您可以使用删除所有具有NaN值的行的 `df.dropna()` 函数从数据集中删除这些点。

```PYTHON
df.dropna(0, inplace=True)
```

评分 `load()` 数据加载器中的函数应以评分数据集作为输出。

### 管道文件 {#pipeline-file}

该文 `pipeline.py` 件包括用于培训和评分的逻辑。

### 培训 {#training}

培训的目的是使用培训数据集中的功能和标签创建模型。

>[!NOTE]
>
> 
>_特征_ ，是指机器学习模型用来预测标签的输入变 _量_。

该 `train()` 功能应包括训练模型和返回训练模型。 不同型号的一些示例可在scikit-learn [用户指南文档中找到](https://scikit-learn.org/stable/user_guide.html)。

选择培训模型后，您将将x和y培训数据集拟合到该模型中，该函数将返回该培训模型。 一个显示此情况的示例如下：

```PYTHON
def train(configProperties, data):

    print("Train Start")

    #########################################
    # Extract fields from configProperties
    #########################################
    learning_rate = float(configProperties['learning_rate'])
    n_estimators = int(configProperties['n_estimators'])
    max_depth = int(configProperties['max_depth'])


    #########################################
    # Fit model
    #########################################
    X_train = data.drop('weeklySalesAhead', axis=1).values
    y_train = data['weeklySalesAhead'].values

    seed = 1234
    model = GradientBoostingRegressor(learning_rate=learning_rate,
                                      n_estimators=n_estimators,
                                      max_depth=max_depth,
                                      random_state=seed)

    model.fit(X_train, y_train)

    print("Train Complete")

    return model
```

请注意，根据您的应用程序，您的函数中将包含参 `GradientBoostingRegressor()` 数。 `xTrainingDataset` 应包含用于培训的功能，而 `yTrainingDataset` 应包含标签。

### 评分 {#scoring}

该函 `score()` 数应包含评分算法并返回一个度量，以指示模型执行的成功程度。 该函 `score()` 数使用评分数据集标签和训练模型来生成一组预测特征。 然后，将这些预测值与评分数据集中的实际特征进行比较。 在此示例中，函数 `score()` 使用经过训练的模型来使用评分数据集中的标签来预测特征。 返回预测特征。

```PYTHON
def score(configProperties, data, model):

    print("Score Start")

    X_test = data.drop('weeklySalesAhead', axis=1).values
    y_test = data['weeklySalesAhead'].values
    y_pred = model.predict(X_test)

    data['prediction'] = y_pred
    data = data[['store', 'prediction']].reset_index()
    data['date'] = data['date'].astype(str)

    print("Score Complete")

    return data
```

### 求值器文件 {#evaluator-file}

该 `evaluator.py` 文件包含如何评估您的培训菜谱以及如何拆分培训数据的逻辑。 在零售销售示例中，将包括加载和准备培训数据的逻辑。 我们将浏览以下两节。

### 拆分数据集 {#split-the-dataset}

培训的数据准备阶段需要拆分要用于培训和测试的数据集。 该 `val` 数据将在训练后隐式用于评估模型。 此过程与评分分开。

此部分将显示首 `split()` 先将数据加载到笔记本的函数，然后通过删除数据集中不相关的列来清除数据。 从那里，您将能够执行功能工程，即根据数据中的现有原始功能创建其他相关功能的过程。 下面显示了此过程的示例和说明。

函 `split()` 数如下所示。 参数中提供的数据帧将拆分为 `train` 和 `val` 要返回的变量。

```PYTHON
def split(self, configProperties={}, dataframe=None):
    train_start = '2010-02-12'
    train_end = '2012-01-27'
    val_start = '2012-02-03'
    train = dataframe[train_start:train_end]
    val = dataframe[val_start:]

    return train, val
```

### 评估训练的模型 {#evaluate-the-trained-model}

该函 `evaluate()` 数在模型训练后执行，并将返回一个度量来指示模型执行的成功程度。 该函 `evaluate()` 数使用测试数据集标签和Traended模型来预测一组特征。 然后，将这些预测值与测试数据集中的实际特征进行比较。 常见评分算法包括：
- [平均绝对百分比错误(MAPE)](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
- [平均绝对误差(MAE)](https://en.wikipedia.org/wiki/Mean_absolute_error)
- [均方根误差](https://en.wikipedia.org/wiki/Root-mean-square_deviation)


零 `evaluate()` 售销售示例中的函数如下所示：

```PYTHON
def evaluate(self, data=[], model={}, configProperties={}):
    print ("Evaluation evaluate triggered")
    val = data.drop('weeklySalesAhead', axis=1)
    y_pred = model.predict(val)
    y_actual = data['weeklySalesAhead'].values
    mape = np.mean(np.abs((y_actual - y_pred) / y_actual))
    mae = np.mean(np.abs(y_actual - y_pred))
    rmse = np.sqrt(np.mean((y_actual - y_pred) ** 2))

    metric = [{"name": "MAPE", "value": mape, "valueType": "double"},
                {"name": "MAE", "value": mae, "valueType": "double"},
                {"name": "RMSE", "value": rmse, "valueType": "double"}]

    return metric
```

请注意，该函数返回一 `metric` 个对象，其中包含一组评估度量。 这些指标将用于评估经过训练的模型的性能。

### 数据保护程序文件 {#data-saver-file}

该文 `datasaver.py` 件包含在测 `save()` 试评分时保存预测的函数。 该函 `save()` 数将执行您的预测， [!DNL Experience Platform Catalog] 并使用API将数据写入 `scoringResultsDataSetId` 您在文件中指定的 `scoring.conf` 值。

在零售销售示例菜谱中使用的示例在此处可见。 请注意使用 `DataSetWriter` 库将数据写入平台：

```PYTHON
from data_access_sdk_python.writer import DataSetWriter

def save(configProperties, prediction):
    print("Datasaver Start")
    print("Setting up Writer")

    catalog_url = "https://platform.adobe.io/data/foundation/catalog"
    ingestion_url = "https://platform.adobe.io/data/foundation/import"

    writer = DataSetWriter(catalog_url=catalog_url,
                           ingestion_url=ingestion_url,
                           client_id=configProperties['ML_FRAMEWORK_IMS_USER_CLIENT_ID'],
                           user_token=configProperties['ML_FRAMEWORK_IMS_TOKEN'],
                           service_token=configProperties['ML_FRAMEWORK_IMS_ML_TOKEN'])

    print("Writer Configured")

    writer.write(data_set_id=configProperties['scoringResultsDataSetId'],
                 dataframe=prediction,
                 ims_org=configProperties['ML_FRAMEWORK_IMS_TENANT_ID'])

    print("Write Done")
    print("Datasaver Finish")
    print(prediction)
```

## 培训和评分 {#training-and-scoring}

在对笔记本进行更改并要培训菜谱后，您可以单击栏顶部的关联按钮在单元格中创建培训运行。 单击该按钮后，培训脚本的命令和输出日志将显示在笔记本(单元格 `evaluator.py` 下)中。 首先安装所有依赖项，然后启动培训。

请注意，必须至少运行一次培训，然后才能运行评分。 单击“运 **[!UICONTROL 行评分]** ”按钮将对培训期间生成的培训模型进行得分。 评分脚本将显示在下方 `datasaver.py`。

出于调试目的，如果要查看隐藏的输出，请将 `debug` 其添加到输出单元格的末尾，然后重新运行它。

## 创建菜谱 {#create-recipe}

编辑完菜谱并对培训／评分输出感到满意后，您可以通过按右上方导航中的“创建菜谱” **[!UICONTROL 从笔记本]** 创建菜谱。

![](../images/jupyterlab/create-recipe/create-recipe.png)

按下按钮后，系统会提示您输入菜谱名称。 此名称表示在上创建的实际菜谱 [!DNL Platform]。

![](../images/jupyterlab/create-recipe/enter_recipe_name.png)

按“确 **[!UICONTROL 定]** ”后 [，您将能够导航到Adobe Experience Platform上的新菜](https://platform.adobe.com/)谱。 单击“视图菜 **[!UICONTROL 谱]** ”按钮可转到“ML模型 **[!UICONTROL ”下]** 的“菜 **[!UICONTROL 谱”选项卡]**

![](../images/jupyterlab/create-recipe/recipe_creation_started.png)

一旦流程完成，菜谱将显示如下内容：

![](../images/jupyterlab/create-recipe/recipe_details.png)

>[!CAUTION]
> - 请勿删除任何文件单元格
> - 不要编辑文 `%%writefile` 件单元格顶部的行
> - 不要同时在不同的笔记本中创建菜谱


## 后续步骤 {#next-steps}

完成本教程后，您学会了如何在Recipe Builder笔记本中创建机器学习模型。 您还学习了如何在笔记本中练习笔记本到菜谱工作流，以便在中创建菜谱 [!DNL Data Science Workspace]。

要继续了解如何在中使用资源， [!DNL Data Science Workspace]请访问菜谱 [!DNL Data Science Workspace] 和模型下拉列表。

## 其他资源 {#additional-resources}

以下视频旨在支持您对构建和部署模型的理解。

>[!VIDEO](https://video.tv.adobe.com/v/30575?quality=12&enable10seconds=on&speedcontrol=on)


