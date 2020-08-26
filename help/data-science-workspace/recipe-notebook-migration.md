---
keywords: Experience Platform;Data Science Workspace;popular topics
solution: Experience Platform
title: 菜谱和笔记本迁移指南
topic: Tutorial
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '3311'
ht-degree: 0%

---


# 菜谱和笔记本迁移指南

>[!NOTE]
>使用/R的笔记本 [!DNL Python]和菜谱不受影响。 迁移仅适用于PySpark/[!DNL Spark] (2.3)菜谱和笔记本电脑。

以下指南概述了迁移现有菜谱和笔记本所需的步骤和信息。

- [菜谱迁移指南](#recipe-migration)
- [笔记本迁移指南](#notebook-migration)

## 菜谱迁移指南 {#recipe-migration}

最近对要求 [!DNL Data Science Workspace] 更新现有和 [!DNL Spark] PySpark菜谱的更改。 使用以下工作流协助转换您的菜谱。

- [Spark迁移指南](#spark-migration-guide)
   - [修改数据集的读写方式](#read-write-recipe-spark)
   - [下载范例菜谱](#download-sample-spark)
   - [添加文档程序文件](#add-dockerfile-spark)
   - [检查相关性](#change-dependencies-spark)
   - [准备Docker脚本](#prepare-docker-spark)
   - [使用docker创建菜谱](#create-recipe-spark)
- [PySpark迁移指南](#pyspark-migration-guide)
   - [修改数据集的读写方式](#pyspark-read-write)
   - [下载范例菜谱](#pyspark-download-sample)
   - [添加文档程序文件](#pyspark-add-dockerfile)
   - [准备Docker脚本](#pyspark-prepare-docker)
   - [使用docker创建菜谱](#pyspark-create-recipe)

## [!DNL Spark] 迁移指南 {#spark-migration-guide}

生成步骤生成的菜谱项目现在是包含。jar二进制文件的Docker图像。 此外，用于使用SDK读取和写入数据集的语 [!DNL Platform] 法已发生更改，需要您修改处方代码。

以下视频旨在进一步帮助您了解菜谱所需的更 [!DNL Spark] 改：

>[!VIDEO](https://video.tv.adobe.com/v/33243)

### 读写数据集([!DNL Spark]) {#read-write-recipe-spark}

在构建Docker图像之前，请查看以下各节中提供的在SDK中读 [!DNL Platform] 写数据集的示例。 如果要转换现有菜谱， [!DNL Platform] 则需要更新SDK代码。

#### 阅读数据集

本节概述读取数据集时需要进行的更改，并使 [用Adobe提供](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/helper/Helper.scala) 的helper.scala示例。

**旧的阅读数据方式**

```scala
 var df = sparkSession.read.format("com.adobe.platform.dataset")
    .option(DataSetOptions.orgId, orgId)
    .option(DataSetOptions.serviceToken, serviceToken)
    .option(DataSetOptions.userToken, userToken)
    .option(DataSetOptions.serviceApiKey, apiKey)
    .load(dataSetId)
```

**阅读数据集的新方式**

对菜谱进行 [!DNL Spark] 更新后，需要添加和更改许多值。 首先， `DataSetOptions` 不再使用。 Replace `DataSetOptions` with `QSOption`. 此外，还 `option` 需要新参数。 我们 `QSOption.mode` 都 `QSOption.datasetId` 需要。 最后， `orgId` 需 `serviceApiKey` 要将其更改为 `imsOrg` 和 `apiKey`。 有关读取数据集的比较，请查看以下示例：

```scala
import com.adobe.platform.query.QSOption
var df = sparkSession.read.format("com.adobe.platform.query")
  .option(QSOption.userToken", {userToken})
  .option(QSOption.serviceToken, {serviceToken})
  .option(QSOption.imsOrg, {orgId})
  .option(QSOption.apiKey, {apiKey})
  .option(QSOption.mode, "interactive")
  .option(QSOption.datasetId, {dataSetId})
  .load()
```

>[!TIP]
> 如果查询运行时间超过10分钟，则交互模式超时。 如果要摄取超过几GB的数据，建议切换到“批处理”模式。 批处理模式需要较长的开始时间，但可以处理较大的数据集。

#### 写入数据集

本节概述使用Adobe提供的ScaringDataSaver.scala示 [例编写数据集所需](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/ScoringDataSaver.scala) 的更改。

**旧的写数据方式**

```scala
df.write.format("com.adobe.platform.dataset")
    .option(DataSetOptions.orgId, orgId)
    .option(DataSetOptions.serviceToken, serviceToken)
    .option(DataSetOptions.userToken, userToken)
    .option(DataSetOptions.serviceApiKey, apiKey)
    .save(scoringResultsDataSetId)
```

**编写数据集的新方法**

对菜谱进行 [!DNL Spark] 更新后，需要添加和更改许多值。 首先， `DataSetOptions` 不再使用。 Replace `DataSetOptions` with `QSOption`. 此外，还 `option` 需要新参数。 `QSOption.datasetId` is needed and replaces the need to load `{dataSetId}` the `.save()`in. 最后， `orgId` 需 `serviceApiKey` 要将其更改为 `imsOrg` 和 `apiKey`。 有关编写数据集的比较，请查看以下示例：

```scala
import com.adobe.platform.query.QSOption
df.write.format("com.adobe.platform.query")
  .option(QSOption.userToken", {userToken})
  .option(QSOption.serviceToken, {serviceToken})
  .option(QSOption.imsOrg, {orgId})
  .option(QSOption.apiKey, {apiKey})
  .option(QSOption.datasetId, {dataSetId})
  .save()
```

### 打包基于Docker的源文件([!DNL Spark]) {#package-docker-spark}

开始，方法是导航到菜谱所在的目录。

以下部分使用新的Scala零售销售菜谱，该菜谱可在Data Science Workspace公 [共Github存储库中找到](https://github.com/adobe/experience-platform-dsw-reference)。

### 下载范例菜谱([!DNL Spark]) {#download-sample-spark}

示例菜谱包含需要复制到现有菜谱的文件。 要克隆包含所有示例方法的公共Github，请在终端中输入以下内容：

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Scala菜谱位于以下目录中 `experience-platform-dsw-reference/recipes/scala/retail`。

### 添加Docker文件([!DNL Spark]) {#add-dockerfile-spark}

您的菜谱文件夹中需要一个新文件，才能使用基于文档的工作流。 从位于的菜谱文件夹复制并粘贴Docker文件 `experience-platform-dsw-reference/recipes/scala/Dockerfile`。 或者，您也可以将下面的代码复制并粘贴到名为的新文件中 `Dockerfile`。

>[!IMPORTANT]
> 下面显示的示例 `ml-retail-sample-spark-*-jar-with-dependencies.jar` jar文件应替换为菜谱的jar文件的名称。

```scala
FROM adobe/acp-dsw-ml-runtime-spark:0.0.1

COPY target/ml-retail-sample-spark-*-jar-with-dependencies.jar /application.jar
```

### 更改依赖关系([!DNL Spark]) {#change-dependencies-spark}

如果您使用现有菜谱，pom.xml文件中需要更改依赖关系。 将model-authoring-sdk依赖项版本更改为2.0.0。然后，将pom文件中的 [!DNL Spark] 版本更新为2.4.3，将Scala版本更改为2.11.12。

```json
<groupId>com.adobe.platform.ml</groupId>
<artifactId>authoring-sdk_2.11</artifactId>
<version>2.0.0</version>
<classifier>jar-with-dependencies</classifier>
```

### 准备Docker脚本([!DNL Spark]) {#prepare-docker-spark}

[!DNL Spark] 方法不再使用二进制伪像，而是需要构建Docker图像。 如果尚未安装，请 [下载并安装Docker](https://www.docker.com/products/docker-desktop)。

在提供的Scala范例菜谱中，您可以找到脚本 `login.sh` 并 `build.sh` 位于 `experience-platform-dsw-reference/recipes/scala/` 。 将这些文件复制并粘贴到现有菜谱中。

您的文件夹结构现在应类似于以下示例（突出显示新添加的文件）:

![文件夹结构](./images/migration/scala-folder.png)

下一步是将包源文 [件纳入菜谱教程](./models-recipes/package-source-files-recipe.md) 。 本教程的一节概述了如何为Scala(Spark)菜谱构建Docker图像。 完成后，Azure容器注册表中会为您提供Docker图像以及相应的图像URL。

### 创建菜谱([!DNL Spark]) {#create-recipe-spark}

要创建菜谱，您必须先完成包源 [文件教程](./models-recipes/package-source-files-recipe.md) ，并准备好您的文档者图像URL。 您可以使用UI或API创建菜谱。

要使用UI构建菜谱，请按照 [Scala的打包菜谱(UI)教](./models-recipes/import-packaged-recipe-ui.md) 程进行导入。

要使用API构建菜谱，请按照 [Scala的打包菜谱(API)教程](./models-recipes/import-packaged-recipe-api.md) 进行导入。

## PySpark迁移指南 {#pyspark-migration-guide}

构建步骤生成的菜谱项目现在是包含。egg二进制文件的Docker图像。 此外，用于使用SDK读取和写入数据集的语 [!DNL Platform] 法已发生更改，需要您修改处方代码。

以下视频旨在进一步帮助您了解PySpark菜谱所需的更改：

>[!VIDEO](https://video.tv.adobe.com/v/33048?learn=on&quality=12)

### 读写数据集(PySpark) {#pyspark-read-write}

在构建Docker图像之前，请查看以下各节中提供的在SDK中读 [!DNL Platform] 写数据集的示例。 如果要转换现有菜谱， [!DNL Platform] 则需要更新SDK代码。

#### 阅读数据集

本节概述使用Adobe提供的helper.py示例 [读取数据集](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/pyspark/pysparkretailapp/helper.py) 所需的更改。

**旧的阅读数据方式**

```python
dataset_options = get_dataset_options(spark.sparkContext)
pd = spark.read.format("com.adobe.platform.dataset") 
  .option(dataset_options.serviceToken(), service_token) 
  .option(dataset_options.userToken(), user_token) 
  .option(dataset_options.orgId(), org_id) 
  .option(dataset_options.serviceApiKey(), api_key)
  .load(dataset_id)
```

**阅读数据集的新方式**

对菜谱进行 [!DNL Spark] 更新后，需要添加和更改许多值。 首先， `DataSetOptions` 不再使用。 Replace `DataSetOptions` with `qs_option`. 此外，还 `option` 需要新参数。 我们 `qs_option.mode` 都 `qs_option.datasetId` 需要。 最后， `orgId` 需 `serviceApiKey` 要将其更改为 `imsOrg` 和 `apiKey`。 有关读取数据集的比较，请查看以下示例：

```python
qs_option = spark_context._jvm.com.adobe.platform.query.QSOption
pd = sparkSession.read.format("com.adobe.platform.query") 
  .option(qs_option.userToken, {userToken}) 
  .option(qs_option.serviceToken, {serviceToken}) 
  .option(qs_option.imsOrg, {orgId}) 
  .option(qs_option.apiKey, {apiKey}) 
  .option(qs_option.mode, "interactive") 
  .option(qs_option.datasetId, {dataSetId}) 
  .load()
```

>[!TIP]
> 如果查询运行时间超过10分钟，则交互模式超时。 如果要摄取超过几GB的数据，建议切换到“批处理”模式。 批处理模式需要较长的开始时间，但可以处理较大的数据集。

#### 写入数据集

本节概述使用Adobe提供的data_saver.py [示例编写数据集所需](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/pyspark/pysparkretailapp/data_saver.py) 的更改。

**旧的写数据方式**

```python
df.write.format("com.adobe.platform.dataset")
  .option(DataSetOptions.orgId, orgId)
  .option(DataSetOptions.serviceToken, serviceToken)
  .option(DataSetOptions.userToken, userToken)
  .option(DataSetOptions.serviceApiKey, apiKey)
  .save(scoringResultsDataSetId)
```

**编写数据集的新方法**

对PySpark菜谱进行更新后，需要添加和更改许多值。 首先， `DataSetOptions` 不再使用。 Replace `DataSetOptions` with `qs_option`. 此外，还 `option` 需要新参数。  `qs_option.datasetId` ，并替换加载中 `{dataSetId}` 的需 `.save()` 要 最后， `orgId` 需 `serviceApiKey` 要将其更改为 `imsOrg` 和 `apiKey`。 有关读取数据集的比较，请查看以下示例：

```python
qs_option = spark_context._jvm.com.adobe.platform.query.QSOption
scored_df.write.format("com.adobe.platform.query") 
  .option(qs_option.userToken, {userToken}) 
  .option(qs_option.serviceToken, {serviceToken}) 
  .option(qs_option.imsOrg, {orgId}) 
  .option(qs_option.apiKey, {apiKey}) 
  .option(qs_option.datasetId, {dataSetId}) 
  .save()
```

### 打包基于Docker的源文件(PySpark) {#pyspark-package-docker}

开始，方法是导航到菜谱所在的目录。

在此示例中，使用新的PySpark零售销售菜谱，可在Data Science Workspace公共Github [存储库中找到它](https://github.com/adobe/experience-platform-dsw-reference)。

### 下载范例菜谱(PySpark) {#pyspark-download-sample}

示例菜谱包含需要复制到现有菜谱的文件。 要克隆包含所 [!DNL Github] 有示例菜谱的公共菜谱，请在终端中输入以下内容。

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

PySpark菜谱位于以下目录中 `experience-platform-dsw-reference/recipes/pyspark`。

### 添加Docker文件(PySpark) {#pyspark-add-dockerfile}

您的菜谱文件夹中需要一个新文件，才能使用基于文档的工作流。 从位于的菜谱文件夹复制并粘贴Docker文件 `experience-platform-dsw-reference/recipes/pyspark/Dockerfile`。 或者，您也可以复制并粘贴下面的代码，并创建一个名为的新文件 `Dockerfile`。

>[!IMPORTANT]
> 下面显示的示例 `pysparkretailapp-*.egg` egg文件应替换为菜谱的egg文件名称。

```scala
FROM adobe/acp-dsw-ml-runtime-pyspark:0.0.1
RUN mkdir /recipe

COPY . /recipe

RUN cd /recipe && \
    ${PYTHON} setup.py clean install && \
    rm -rf /recipe

RUN cp /databricks/conda/envs/${DEFAULT_DATABRICKS_ROOT_CONDA_ENV}/lib/python3.6/site-packages/pysparkretailapp-*.egg /application.egg
```

### 准备Docker脚本(PySpark) {#pyspark-prepare-docker}

PySpark菜谱不再使用二进制伪像，而是需要构建Docker图像。 如果尚未执行此操作，请下载并安装 [Docker](https://www.docker.com/products/docker-desktop)。

在提供的PySpark范例菜谱中，您可以找到脚本 `login.sh` 并位 `build.sh` 于上 `experience-platform-dsw-reference/recipes/pyspark` 。 将这些文件复制并粘贴到现有菜谱中。

您的文件夹结构现在应类似于以下示例（突出显示新添加的文件）:

![文件夹结构](./images/migration/folder.png)

您的菜谱现已准备好使用Docker图像构建。 下一步是将包源文 [件纳入菜谱教程](./models-recipes/package-source-files-recipe.md) 。 本教程的一节概述了如何为PySpark(Spark 2.4)菜谱构建文档处理器图像。 完成后，Azure容器注册表中会为您提供Docker图像以及相应的图像URL。

### 创建菜谱(PySpark) {#pyspark-create-recipe}

要创建菜谱，您必须先完成包源 [文件教程](./models-recipes/package-source-files-recipe.md) ，并准备好您的文档者图像URL。 您可以使用UI或API创建菜谱。

要使用UI构建菜谱，请按照 [PySpark的打包菜谱(UI)教](./models-recipes/import-packaged-recipe-ui.md) 程进行导入。

要使用API构建菜谱，请按照 [PySpark的打包菜谱(API)教程](./models-recipes/import-packaged-recipe-api.md) 进行导入。

## 笔记本迁移指南 {#notebook-migration}

笔记本的最 [!DNL JupyterLab] 近更改要求您将现有PySpark和 [!DNL Spark] 2.3笔记本更新为2.4。通过此更改，已 [!DNL JupyterLab Launcher] 使用新的启动笔记本进行更新。 有关如何转换笔记本的分步指南，请选择以下指南之一：

- [PySpark 2.3到2.4迁移指南](#pyspark-notebook-migration)
- [Spark 2.3到Spark 2.4(Scala)迁移指南](#spark-notebook-migration)

以下视频旨在进一步帮助您了解更改所需的内容 [!DNL JupyterLab Notebooks]:

>[!VIDEO](https://video.tv.adobe.com/v/33444?quality=12&learn=on)

## PySpark 2.3到2.4笔记本电脑迁移指南 {#pyspark-notebook-migration}

随着PySpark 2.4的推出， [!DNL JupyterLab Notebooks]带 [!DNL Python] 有PySpark 2.4的新笔记本现在使用 [!DNL Python] 3内核而不是PySpark 3内核。 这意味着PySpark 2.3上运行的现有代码在PySpark 2.4中不受支持。

>[!IMPORTANT]
>
>PySpark 2.3已弃用，并且设置为在后续版本中删除。 所有现有示例均设置为替换为PySpark 2.4示例。

要将现有PySpark 3(2.[!DNL Spark] 3)笔记本转换为 [!DNL Spark] 2.4，请按照以下示例操作：

### 内核

PySpark 3([!DNL Spark] 2.4)笔记本使用Python 3 Kernel，而不是PySpark 3（Spark 2.3 —— 已弃用）笔记本中已弃用的PySpark内核。

要在UI中确认或更改内 [!DNL JupyterLab] 核，请选择笔记本右上方导航栏中的内核按钮。 如果您使用的是某个预定义的启动器笔记本，则会预先选择内核。 以下示例使用PySpark 3(2.[!DNL Spark] 4)Aggregation笔记 *本* 启动器。

![检查内核](./images/migration/pyspark-migration/check-kernel.png)

选择下拉菜单会打开可用内核的列表。

![选择内核](./images/migration/pyspark-migration/kernel-click.png)

![内核下拉列表](./images/migration/pyspark-migration/select-kernel.png)

对于PySpark 3([!DNL Spark] 2.4)笔记本，选择Python 3内核，然后单击“选择”按钮进 **行确** 认。

![确认内核](./images/migration/pyspark-migration/confirm-kernel.png)

## 初始化SparkSession

所有 [!DNL Spark] 2.4笔记本电脑都要求您使用新的样板代码初始化会话。

<table>
  <th>笔记本</th>
  <th>PySpark 3（[!DNL Spark] 2.3 —— 已弃用）</th>
  <th>PySpark 3([!DNL Spark] 2.4)</th>
  <tr>
  <th>内核</th>
  <td align="center">PySpark 3</td>
  <td align="center">Python 3</td>
  </tr>
  <tr>
  <th>代码</th>
  <td>
  <pre class="JSON language-JSON hljs">
  [!DNL spark]
</pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
从pyspark.sql导入SparkSessionspark = SparkSession.builder.getOrCreate()
</pre>
  </td>
  </tr>
</table>

以下图像突出了PySpark 2.3和PySpark 2.4的配置差异。此示例使用中提供的 *Aggregation* starter笔记本 [!DNL JupyterLab Launcher]。

**2.3的配置示例（已弃用）**

![config 1](./images/migration/pyspark-migration/2.3-config.png)![config 2](./images/migration/pyspark-migration/2.3-config-import.png)

**2.4的配置示例**

![config 3](./images/migration/pyspark-migration/2.4-config.png)

## 使用%dataset魔术 {#magic}

随着2.4 [!DNL Spark] 的推出， `%dataset` 自定义魔术功能将被提供用于新的PySpark 3(2.4)[!DNL Spark] 笔记本([!DNL Python] 3内核)。

**用法**

`%dataset {action} --datasetId {id} --dataFrame {df}`

**描述**

用于从 [!DNL Data Science Workspace] 笔记本（3内核）读取或写入数据集 [!DNL Python] 的自定[!DNL Python] 义魔术命令。

- **{action}**:要对数据集执行的操作类型。 两个操作可用于“读取”或“写入”。
- **—datasetId {id}**:用于提供要读或写的数据集的id。 这是必需参数。
- **—dataFrame {df}**:熊猫数据框。 这是必需参数。
   - 当操作为“read”时，{df}是数据集读取操作结果可用的变量。
   - 当操作为“write”时，此数据帧{df}将写入数据集。
- **—mode（可选）**:允许的参数为“batch”和“interactive”。 默认情况下，该模式设置为“交互”。 在读取大量数据时，建议使用“批处理”模式。

**示例**

- **阅读示例**: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
- **编写示例**: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

## 在LocalContext中加载到数据帧

随着2.4 [!DNL Spark] 的引入， [`%dataset`](#magic) 提供了自定义魔术。 以下示例重点介绍在PySpark(2.3)和PySpark([!DNL Spark] 2.4)笔记本中加载数据帧[!DNL Spark] 的主要区别：

**使用PySpark 3[!DNL Spark]（2.3 —— 已弃用）- PySpark 3内核**

```python
dataset_options = sc._jvm.com.adobe.platform.dataset.DataSetOptions
pd0 = spark.read.format("com.adobe.platform.dataset")
  .option(dataset_options.orgId(), "310C6D375BA5248F0A494212@AdobeOrg")
  .load("5e68141134492718af974844")
```

**使用PySpark 3[!DNL Spark](2.4)- Python 3内核**

```python
%dataset read --datasetId 5e68141134492718af974844 --dataFrame pd0
```

| 元素 | 描述 |
| ------- | ----------- |
| pd0 | 要使用或创建的熊猫数据框对象的名称。 |
| [%dataset](#magic) | 在3个内核中实现数据访 [!DNL Python] 问的自定义魔法。 |

以下图像突出了PySpark 2.3和PySpark 2.4加载数据时的主要差异。此示例使用中提供的 *Aggregation* 起动笔记本 [!DNL JupyterLab Launcher]。

**在PySpark 2.3（Luma数据集）中加载数据——已弃用**

![加载1](./images/migration/pyspark-migration/2.3-load.png)

**在PySpark 2.4中加载数据（Luma数据集）**

在加载中定义了PySpark 3 `sc = spark.sparkContext` (Spark 2.4)。

![加载1](./images/migration/pyspark-migration/2.4-load.png)

**在PySpark[!DNL Experience Cloud Platform]2.3中加载数据——已弃用**

![加载2](./images/migration/pyspark-migration/2.3-load-alt.png)

**在[!DNL Experience Cloud Platform]PySpark 2.4中加载数据**

使用PySpark 3[!DNL Spark] (2.4), `org_id` 并 `dataset_id` 且不再需要定义。 此外，已 `df = spark.read.format` 被自定义功能所取代， [`%dataset`](#magic) 使读取和写入数据集更简单。

![加载2](./images/migration/pyspark-migration/2.4-load-alt.png)

| 元素 | 描述 |
| ------- | ----------- |
| [%dataset](#magic) | 在3个内核中实现数据访 [!DNL Python] 问的自定义魔法。 |

>[!TIP]
>
>—mode可设置为 `interactive` 或 `batch`。 —mode的缺省值为 `interactive`。 建议在读取大 `batch` 量数据时使用模式。

## 创建本地数据帧

PySpark 3(2[!DNL Spark] .4)不再 `%%` 支持sparkmagic。 不能再使用以下操作：

- `%%help`
- `%%info`
- `%%cleanup`
- `%%delete`
- `%%configure`
- `%%local`

下表概述了转换幻灯片查询所需 `%%sql` 的更改：

<table>
  <th>笔记本</th>
  <th>PySpark 3（[!DNL Spark] 2.3 —— 已弃用）</th>
  <th>PySpark 3([!DNL Spark] 2.4)</th>
  <tr>
  <th>内核</th>
  <td align="center">PySpark 3</td>
  <td align="center">[!DNL Python] 3</td>
  </tr>
  <tr>
  <th>代码</th>
      <td>
         <pre class="JSON language-JSON hljs">%%sql -o dfselect *来自sparkdf
</pre>
         <pre class="JSON language-JSON hljs"> %%sql -o pdf -n限制选择*从sparkdf
</pre>
         <pre class="JSON language-JSON hljs">%%sql -o pdf -qselect *来自sparkdf
</pre>
         <pre class="JSON language-JSON hljs"> %%sql -o pdf -r分数选择*从sparkdf
</pre>
      </td>
      <td>
         <pre class="JSON language-JSON hljs">
df = spark.sql(" SELECT * FROM sparkdf")
</pre>
         <pre class="JSON language-JSON hljs">
df = spark.sql（" SELECT * FROM sparkdf限制"）
</pre>
         <pre class="JSON language-JSON hljs">
df = spark.sql（" SELECT * FROM sparkdf限制"）
</pre>
         <pre class="JSON language-JSON hljs">
sample_df = df.sample(fraction)
</pre>
      </td>
   </tr>
</table>

>[!TIP]
>
>您还可以指定可选种子样本，如布尔值withReplacement、多次分数或长种子。

以下图像突出了在PySpark 2.3和PySpark 2.4中创建本地数据帧的主要区别。此示例使用中提供的 *Aggregation* 起动笔记本 [!DNL JupyterLab Launcher]。

**创建本地数据帧PySpark 2.3 —— 已弃用**

![数据帧1](./images/migration/pyspark-migration/2.3-dataframe.png)

**创建本地数据帧PySpark 2.4**

PySpark 3([!DNL Spark] 2.4)不再支 `%%sql` 持Sparkmagic，已替换为以下内容：

![数据帧2](./images/migration/pyspark-migration/2.4-dataframe.png)

## 写入数据集

随着2.4的推出 [!DNL Spark] ，提供了自定 [`%dataset`](#magic) 义的功能，使编写数据集更简洁。 要写入数据集，请使用以 [!DNL Spark] 下2.4示例：

**使用PySpark 3[!DNL Spark]（2.3 —— 已弃用）- PySpark 3内核**

```python
userToken = spark.sparkContext.getConf().get("spark.yarn.appMasterEnv.USER_TOKEN")
serviceToken = spark.sparkContext.getConf().get("spark.yarn.appMasterEnv.SERVICE_TOKEN")
serviceApiKey = spark.sparkContext.getConf().get("spark.yarn.appMasterEnv.SERVICE_API_KEY")

dataset_options = sc._jvm.com.adobe.platform.dataset.DataSetOptions

pd0.write.format("com.adobe.platform.dataset")
  .option(dataset_options.orgId(), "310C6D375BA5248F0A494212@AdobeOrg")
  .option(dataset_options.userToken(), userToken)
  .option(dataset_options.serviceToken(), serviceToken)
  .option(dataset_options.serviceApiKey(), serviceApiKey)
  .save("5e68141134492718af974844")
```

**使用PySpark 3[!DNL Spark](2.4)-[!DNL Python]3内核**

```python
%dataset write --datasetId 5e68141134492718af974844 --dataFrame pd0
pd0.describe()
pd0.show(10, False)
```

| 元素 | 描述 |
| ------- | ----------- |
| pd0 | 要使用或创建的熊猫数据框对象的名称。 |
| [%dataset](#magic) | 在3个内核中实现数据访 [!DNL Python] 问的自定义魔法。 |

>[!TIP]
>
>—mode可设置为 `interactive` 或 `batch`。 —mode的缺省值为 `interactive`。 建议在读取大 `batch` 量数据时使用模式。

以下图像突出了在PySpark 2.3和PySpark 2.4中将数 [!DNL Platform] 据写回的主要区别。此示例使用中提 *供的* Aggregation起动笔记本 [!DNL JupyterLab Launcher]。

**将数据写回[!DNL Platform]PySpark 2.3 —— 已弃用**

![数据帧1](./images/migration/pyspark-migration/2.3-write.png)![dataframe 1](./images/migration/pyspark-migration/2.3-write-2.png)![dataframe 1](./images/migration/pyspark-migration/2.3-write-3.png)

**将数据写回[!DNL Platform]PySpark 2.4**

借助PySpark 3[!DNL Spark] (2.4)，自 `%dataset` 定义魔术无需定义 `userToken`、 `serviceToken``serviceApiKey`和等值 `.option`。 此外， `orgId` 不再需要定义。

![数据帧2](./images/migration/pyspark-migration/2.4-write.png)![dataframe 2](./images/migration/pyspark-migration/2.4-write-2.png)

## [!DNL Spark] 2.3到2. [!DNL Spark] 4(Scala)笔记本迁移指南 {#spark-notebook-migration}

随着2.4 [!DNL Spark] 的引入，现 [!DNL JupyterLab Notebooks]有 [!DNL Spark] (2.3)笔记本现在使用Scala内核，而不是[!DNL Spark][!DNL Spark] 内核。 这意味着在(2. [!DNL Spark] 3)[!DNL Spark] 上运行的现有代码在Scala([!DNL Spark] 2.4)中不受支持。 此外，所有新 [!DNL Spark] 笔记本都应在[!DNL Spark] 中使用Scala(2.4) [!DNL JupyterLab Launcher]。

>[!IMPORTANT]
>
>[!DNL Spark] ([!DNL Spark] 2.3)已弃用，并且设置为在后续版本中删除。 所有现有示例都设置为用Scala(2.[!DNL Spark] 4)示例替换。

要将现有( [!DNL Spark] 2.[!DNL Spark] 3)笔记本转换为Scala([!DNL Spark] 2.4)，请按照以下示例操作：

## 内核

Scala(Spark 2.4)笔记本使用Scala Kernel，而不是(2.3 —— 已弃 [!DNL Spark] 用)笔记本 [!DNL Spark] 中使用的[!DNL Spark] 已弃用内核。

要在UI中确认或更改内 [!DNL JupyterLab] 核，请选择笔记本右上方导航栏中的内核按钮。 出现 *“Select Kernel* （选择内核）”窗口。 如果您使用某个预定义的启动器笔记本，则会预先选择内核。 以下示例使用中的 *Scala* Clustering笔记本 [!DNL JupyterLab Launcher]。

![检查内核](./images/migration/spark-scala/scala-kernel.png)

选择下拉菜单会打开可用内核的列表。

![内核下拉列表](./images/migration/spark-scala/select-dropdown.png)

![选择内核](./images/migration/spark-scala/dropdown.png)

对于Scala(Spark 2.4)笔记本，选择Scala内核，然后单击“选择”按 **钮进** 行确认。

![确认内核](./images/migration/spark-scala/select.png)

## 初始化SparkSession {#initialize-sparksession-scala}

所有Scala([!DNL Spark] 2.4)笔记本电脑都要求使用以下样板代码初始化会话：

<table>
  <th>笔记本</th>
  <th>Spark（[!DNL Spark] 2.3 —— 已弃用）</th>
  <th>Scala([!DNL Spark] 2.4)</th>
  <tr>
  <th>内核</th>
  <td align="center">[!DNL Spark]</td>
  <td align="center">斯卡拉</td>
  </tr>
  <tr>
  <th>代码</th>
  <td align="center">
  无需代码
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
导入org.apache.spark.sql。{ SparkSession }val spark = SparkSession .builder()。主控("local")。getOrCreate()
</pre>
  </td>
  </tr>
</table>

下面的Scala[!DNL Spark] (2.4)图像突出显示了使用2.3内核和2.4 Scala内核初始化 [!DNL Spark] sparkSession [!DNL Spark] 时的 [!DNL Spark] 主要区别。 此示例使用中 *提供* 的集群启动笔记本 [!DNL JupyterLab Launcher]。

**[!DNL Spark]([!DNL Spark]2.3 —— 已弃用)**

[!DNL Spark] ([!DNL Spark] 2.3 —— 已弃用)使 [!DNL Spark] 用内核，因此您无需定义 [!DNL Spark]。

**Scala([!DNL Spark]2.4)**

将 [!DNL Spark] 2.4与Scala内核一起使用需要 `val spark` 定义 `SparkSesson` 和导入才能读或写：

![导入和定义spark](./images/migration/spark-scala/start-session.png)

## 查询数据

Scala(2.[!DNL Spark] 4)不再 `%%` 支持sparkmagic。 不能再使用以下操作：

- `%%help`
- `%%info`
- `%%cleanup`
- `%%delete`
- `%%configure`
- `%%local`

下表概述了转换幻灯片查询所需 `%%sql` 的更改：

<table>
  <th>笔记本</th>
  <th>[!DNL Spark]（[!DNL Spark] 2.3 —— 已弃用）</th>
  <th>Scala([!DNL Spark] 2.4)</th>
  <tr>
  <th>内核</th>
  <td align="center">[!DNL Spark]</td>
  <td align="center">斯卡拉</td>
  </tr>
  <tr>
  <th>代码</th>
    <td>
       <pre class="JSON language-JSON hljs">
%%sql -o dfselect *来自sparkdf
</pre>
         <pre class="JSON language-JSON hljs">
%%sql -o pdf -n限制选择*从sparkdf
</pre>
         <pre class="JSON language-JSON hljs">
%%sql -o pdf -qselect *来自sparkdf
</pre>
         <pre class="JSON language-JSON hljs">
%%sql -o pdf -r分数选择*从sparkdf
</pre>
      </td>
      <td>
         <pre class="JSON language-JSON hljs">
val df = spark.sql(" SELECT * FROM sparkdf")
</pre>
         <pre class="JSON language-JSON hljs">
val df = spark.sql（" SELECT * FROM sparkdf限制"）
</pre>
         <pre class="JSON language-JSON hljs">
val df = spark.sql（" SELECT * FROM sparkdf限制"）
</pre>
         <pre class="JSON language-JSON hljs">
val sample_df = df.sample(fraction) </pre>
      </td>
   </tr>
</table>

下面的Scala[!DNL Spark] (2.4)图像突出了在使用2.3内核和Spark 2.4 Scala内核 [!DNL Spark] 制作查询 [!DNL Spark] 时的关键区别。 此示例使用中 *提供* 的集群启动笔记本 [!DNL JupyterLab Launcher]。

**[!DNL Spark]([!DNL Spark]2.3 —— 已弃用)**

( [!DNL Spark] 2.[!DNL Spark] 3 —— 已弃用)笔记本使用内 [!DNL Spark] 核。 内核 [!DNL Spark] 支持并使用sparkmagic `%%sql` 。

![](./images/migration/spark-scala/sql-2.3.png)

**Scala([!DNL Spark]2.4)**

Scala内核不再支持sparkmagic `%%sql` 。 需要转换现有sparkmagic代码。

![导入和定义spark](./images/migration/spark-scala/sql-2.4.png)

## 阅读数据集 {#notebook-read-dataset-spark}

在 [!DNL Spark] 2.3中，您需要为用于读取 `option` 数据或在代码单元格中使用原始值的值定义变量。 在Scala中，您可 `sys.env("PYDASDK_IMS_USER_TOKEN")` 以使用声明和返回值，这就无需定义变量，如 `var userToken`。 在以下Scala(Spark 2.4)示例中， `sys.env` 使用定义并返回读取数据集所需的所有值。

**使[!DNL Spark]用[!DNL Spark]（2.3 —— 已弃用）-内[!DNL Spark]核**

```scala
import com.adobe.platform.dataset.DataSetOptions
var df1 = spark.read.format("com.adobe.platform.dataset")
  .option(DataSetOptions.orgId, "310C6D375BA5248F0A494212@AdobeOrg")
  .option(DataSetOptions.batchId, "dbe154d3-197a-4e6c-80f8-9b7025eea2b9")
  .load("5e68141134492718af974844")
```

**使用Scala([!DNL Spark]2.4)- Scala内核**

```scala
import org.apache.spark.sql.{Dataset, SparkSession}
val spark = SparkSession.builder().master("local").getOrCreate()
val df1 = spark.read.format("com.adobe.platform.query")
  .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
  .option("ims-org", sys.env("IMS_ORG_ID"))
  .option("api-key", sys.env("PYDASDK_IMS_CLIENT_ID"))
  .option("service-token", sys.env("PYDASDK_IMS_SERVICE_TOKEN"))
  .option("mode", "interactive")
  .option("dataset-id", "5e68141134492718af974844")
  .load()
```

| 元素 | 描述 |
| ------- | ----------- |
| df1 | 一个变量，它表示用于读取和写入数据的Pactys数据帧。 |
| 用户令牌 | 使用自动获取的用户令牌 `sys.env("PYDASDK_IMS_USER_TOKEN")`。 |
| 服务令牌 | 您使用自动获取的服务令牌 `sys.env("PYDASDK_IMS_SERVICE_TOKEN")`。 |
| ims-org | 使用自动获取的ims-org id `sys.env("IMS_ORG_ID")`。 |
| api-key | 使用自动获取的API密钥 `sys.env("PYDASDK_IMS_CLIENT_ID")`。 |

下面的图像突出了使用2.3和2.4加载 [!DNL Spark] 数据时的 [!DNL Spark] 主要差异。此示例使用中提供 *的Clustering* starter笔记本电 [!DNL JupyterLab Launcher]脑。

**[!DNL Spark]([!DNL Spark]2.3 —— 已弃用)**

( [!DNL Spark] 2.[!DNL Spark] 3 —— 已弃用)笔记本使用内 [!DNL Spark] 核。 以下两个单元格显示了一个在日期范围(2019-3-21, 2019-3-29)内使用指定数据集ID加载数据集的示例。

![加载spark 2.3](./images/migration/spark-scala/load-2.3.png)

**Scala([!DNL Spark]2.4)**

Scala(2.[!DNL Spark] 4)笔记本使用Scala内核，该内核在设置时需要更多值，如第一个代码单元格中突出显示的。 此外， `var mdata` 需要填 `option` 写更多值。 在此笔记本中，之前提到的用于初 [始化SparkSession的代](#initialize-sparksession-scala) 码 `var mdata` ，包含在代码单元格中。

![加载spark 2.4](./images/migration/spark-scala/load-2.4.png)

>[!TIP]
>
>在Scala中，您可 `sys.env()` 以使用从中声明和返回值 `option`。 这样，如果您知道变量将仅用于一次，就无需定义变量。 以下示例在上 `val userToken` 面的示例中进行演示，并在其中内行声明 `option`:
> `.option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))`

## 写入数据集

与读取 [数据集类似](#notebook-read-dataset-spark)，写入数据集需 `option` 要下面示例中概述的其他值。 在Scala中，您可 `sys.env("PYDASDK_IMS_USER_TOKEN")` 以使用声明和返回值，这就无需定义变量，如 `var userToken`。 在下面的Scala示例 `sys.env` 中，用于定义和返回写入数据集所需的所有值。

**使[!DNL Spark]用[!DNL Spark]（2.3 —— 已弃用）-内[!DNL Spark]核**

```scala
import com.adobe.platform.dataset.DataSetOptions

var userToken = spark.sparkContext.getConf.getOption("spark.yarn.appMasterEnv.USER_TOKEN").get
var serviceToken = spark.sparkContext.getConf.getOption("spark.yarn.appMasterEnv.SERVICE_TOKEN").get
var serviceApiKey = spark.sparkContext.getConf.getOption("spark.yarn.appMasterEnv.SERVICE_API_KEY").get

df1.write.format("com.adobe.platform.dataset")
  .option(DataSetOptions.orgId, "310C6D375BA5248F0A494212@AdobeOrg")
  .option(DataSetOptions.userToken, userToken)
  .option(DataSetOptions.serviceToken, serviceToken)
  .option(DataSetOptions.serviceApiKey, serviceApiKey)
  .save("5e68141134492718af974844")
```

**使用Scala([!DNL Spark]2.4)- Scala内核**

```scala
import org.apache.spark.sql.{Dataset, SparkSession}

val spark = SparkSession.builder().master("local").getOrCreate()

df1.write.format("com.adobe.platform.query")
  .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
  .option("service-token", sys.env("PYDASDK_IMS_SERVICE_TOKEN"))
  .option("ims-org", sys.env("IMS_ORG_ID"))
  .option("api-key", sys.env("PYDASDK_IMS_CLIENT_ID"))
  .option("mode", "interactive")
  .option("dataset-id", "5e68141134492718af974844")
  .save()
```

| 元素 | 描述 |
| ------- | ----------- |
| df1 | 一个变量，它表示用于读取和写入数据的Pactys数据帧。 |
| 用户令牌 | 使用自动获取的用户令牌 `sys.env("PYDASDK_IMS_USER_TOKEN")`。 |
| 服务令牌 | 您使用自动获取的服务令牌 `sys.env("PYDASDK_IMS_SERVICE_TOKEN")`。 |
| ims-org | 使用自动获取的ims-org id `sys.env("IMS_ORG_ID")`。 |
| api-key | 使用自动获取的API密钥 `sys.env("PYDASDK_IMS_CLIENT_ID")`。 |