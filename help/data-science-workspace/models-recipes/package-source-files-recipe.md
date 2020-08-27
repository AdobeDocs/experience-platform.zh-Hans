---
keywords: Experience Platform;package source files;Data Science Workspace;popular topics
solution: Experience Platform
title: 将源文件打包到菜谱中
topic: Tutorial
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 0%

---


# 将源文件打包到菜谱中

本教程提供了有关如何将提供的零售销售示例源文件打包到存档文件中的说明，该存档文件可用于在Adobe Experience Platform通过在UI中或使用API遵循菜谱导 [!DNL Data Science Workspace] 入工作流程来创建菜谱。

要了解的概念：

- **菜谱**:配方是“模型”规范的Adobe术语，是代表特定机器学习、人工智能算法或算法集合、处理逻辑和配置的顶级容器，构建和执行经过培训的模型，从而帮助解决特定的业务问题。
- **源文件**:项目中包含菜谱逻辑的各个文件。

## 先决条件

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3和pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## 菜谱创建

菜谱创建开始与打包源文件一起构建存档文件。 源文件定义用于解决现有特定问题的机器学习逻辑和算法，并以R、PySpark或 [!DNL Python]Scala格式编写。 构建的存档文件采用Docker图像的形式。 构建后，打包的存档文件将导入 [!DNL Data Science Workspace] 其中，以在 [UI中或](./import-packaged-recipe-ui.md)[使用API创建菜谱](./import-packaged-recipe-api.md)。

### 基于Docker的模型创作 {#docker-based-model-authoring}

Docker图像允许开发人员将应用程序与其所需的所有部件（如库和其他依赖项）打包，并将其作为一个包发布。

内置的Docker图像将使用在菜谱创建工作流程中提供给您的凭据推送到Azure容器注册表。

要获取您的Azure容器注册表凭据，请登录 [Adobe Experience Platform](https://platform.adobe.com)。 在左侧导航列中，导航到 **[!UICONTROL 工作流]**。 选择 **[!UICONTROL 导入菜谱]** ，然后选择 **[!UICONTROL 启动]**。 请参阅下面的屏幕快照。

![](../images/models-recipes/package-source-files/import.png)

此时将 *打开* “配置”页。 提供适当 *的处方名*（例如“零售销售处方”），并（可选）提供说明或文档URL。 完成后，单击“下 **[!UICONTROL 一步]**”。

![](../images/models-recipes/package-source-files/configure.png)

选择适当的 *运行时*，然后选择类 **[!UICONTROL 型的]** “分 *类”*。 完成后，将生成您的Azure容器注册表凭据。

>[!NOTE]
>
>*类型* ，是机器学习问题的类，它是为菜谱设计的，经过培训后，用来帮助定制对培训运行的评估。

>[!TIP]
>
>- 对于 [!DNL Python] 菜谱，请选 **[!UICONTROL 择Python]** runtime。
>- 对于R菜谱，请选 **[!UICONTROL 择]** R运行时。
>- 对于PySpark菜谱，请选 **[!UICONTROL 择PySpark]** 运行时。 自动填充对象类型。
>- 对于Scala菜谱，请选择 **[!UICONTROL Spark]** runtime。 自动填充对象类型。


![](../images/models-recipes/package-source-files/docker-creds.png)

请注意Docker主 *机、**用户名*&#x200B;和密 *码值*。 它们用于在下面概述的工作流 [!DNL Docker] 中构建和推送您的图像。

>[!NOTE]
>
>完成以下步骤后，将提供源URL。 配置文件将在后续步骤中的后续教程中 [进行说明](#next-steps)。

### 打包源文件

开始，方法是获取Experience Platform科学工作区参 <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">考存储库中的示例代码</a> 。

- [构建Python Docker图像](#python-docker)
- [构建R Docker图像](#r-docker)
- [构建PySpark Docker图像](#pyspark-docker)
- [构建Scala(Spark)Docker图像](#scala-docker)

### 构建 [!DNL Python] Docker图像 {#python-docker}

如果尚未这样做，请使用以下命 [!DNL GitHub] 令将存储库克隆到本地系统上：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigate to the directory `experience-platform-dsw-reference/recipes/python/retail`. 在此，您将找到用于 `login.sh` 登 `build.sh` 录Docker和构建图像的脚本 [!DNL Python Docker] 。 如果您的Docker凭 [据已准备](#docker-based-model-authoring) ，请按顺序输入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

请注意，执行登录脚本时，您需要提供Docker主机、用户名和密码。 在构建时，您需要提供Docker主机和版本标记。

构建脚本完成后，控制台输出中将为您提供一个Docker源文件URL。 对于此特定示例，其外观类似于：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

复制此URL并转到下 [一步](#next-steps)。

### 构建R图 [!DNL Docker] 像 {#r-docker}

如果尚未这样做，请使用以下命 [!DNL GitHub] 令将存储库克隆到本地系统上：

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

导览至克隆存储 `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` 库中的目录。 在此，您将找到用 `login.sh` 于 `build.sh` 登录Docker和构建R Docker图像的文件。 如果您的Docker凭 [据已准备](#docker-based-model-authoring) ，请按顺序输入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

请注意，执行登录脚本时，您需要提供Docker主机、用户名和密码。 在构建时，您需要提供Docker主机和版本标记。

构建脚本完成后，控制台输出中将为您提供一个Docker源文件URL。 对于此特定示例，其外观类似于：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

复制此URL并转到下 [一步](#next-steps)。

### 构建PySpark Docker图像 {#pyspark-docker}

开始，方法是 [!DNL GitHub] 使用以下命令将存储库克隆到本地系统上：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigate to the directory `experience-platform-dsw-reference/recipes/pyspark/retail`. 脚本 `login.sh` 和位 `build.sh` 于此处，用于登录Docker和构建Docker图像。 如果您的Docker凭 [据已准备](#docker-based-model-authoring) ，请按顺序输入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

请注意，执行登录脚本时，您需要提供Docker主机、用户名和密码。 在构建时，您需要提供Docker主机和版本标记。

构建脚本完成后，控制台输出中将为您提供一个Docker源文件URL。 对于此特定示例，其外观类似于：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

复制此URL并转到下 [一步](#next-steps)。

### 构建Scala Docker图像 {#scala-docker}

开始，在终端 [!DNL GitHub] 中使用以下命令将存储库克隆到本地系统上：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

接下来，导航到可 `experience-platform-dsw-reference/recipes/scala` 以找到脚本和的目 `login.sh` 录 `build.sh`。 这些脚本用于登录Docker并构建Docker图像。 如果您的Docker凭 [据已准备](#docker-based-model-authoring) ，请按顺序将以下命令输入终端：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>如果您在尝试使用脚本登录Docker时收到权限错 `login.sh` 误，请尝试使用命令 `bash login.sh`。

执行登录脚本时，您需要提供Docker主机、用户名和密码。 在构建时，您需要提供Docker主机和版本标记。

构建脚本完成后，控制台输出中将为您提供一个Docker源文件URL。 对于此特定示例，其外观类似于：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

复制此URL并转到下 [一步](#next-steps)。

## 后续步骤 {#next-steps}

本教程重点介绍将源文件打包到菜谱中，这是将菜谱导入的先决条件步骤 [!DNL Data Science Workspace]。 您现在应在Azure容器注册表中拥有Docker图像以及相应的图像URL。 现在，您可以开始将打包的菜谱导入的教程了 [!DNL Data Science Workspace]。 选择以下教程链接之一以开始：

- [在UI中导入打包的菜谱](./import-packaged-recipe-ui.md)
- [使用API导入打包的菜谱](./import-packaged-recipe-api.md)