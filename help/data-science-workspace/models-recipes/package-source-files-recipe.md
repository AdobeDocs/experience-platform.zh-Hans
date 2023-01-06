---
keywords: Experience Platform；包源文件；Data Science Workspace；热门主题；Docker;Docker图像
solution: Experience Platform
title: 将源文件打包到方法中
type: Tutorial
description: 本教程提供了有关如何将提供的零售销售示例源文件打包到存档文件中的说明，该存档文件可用于通过在UI中或使用API按照方法导入工作流在Adobe Experience Platform Data Science Workspace中创建方法。
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 0%

---

# 将源文件打包到方法中

本教程提供了有关如何将提供的零售销售示例源文件打包到存档文件中的说明，该存档文件可用于在Adobe Experience Platform中创建方法 [!DNL Data Science Workspace] 通过在UI中或使用API遵循方法导入工作流。

要了解的概念：

- **方法**:方法是Adobe对模型规范的术语，是顶级容器，代表构建和执行训练模型所需的特定机器学习、人工智能算法或算法组合、处理逻辑和配置，从而帮助解决特定业务问题。
- **源文件**:项目中包含方法逻辑的单个文件。

## 先决条件

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## 方法创建

方法创建从打包源文件开始，以构建存档文件。 源文件定义用于解决手头特定问题的机器学习逻辑和算法，并以任一方式写入 [!DNL Python]、R、PySpark或Scala。 构建的存档文件采用Docker映像的形式。 生成后，打包的存档文件将导入到 [!DNL Data Science Workspace] 创建方法 [在UI中](./import-packaged-recipe-ui.md) 或 [使用API](./import-packaged-recipe-api.md).

### 基于Docker的模型创作 {#docker-based-model-authoring}

Docker图像允许开发人员将应用程序与其所需的所有部件（如库和其他依赖项）打包，然后作为一个包发送。

使用在方法创建工作流中为您提供的凭据，将构建的Docker图像推送到Azure容器注册表。

要获取Azure容器注册表凭据，请登录 [Adobe Experience Platform](https://platform.adobe.com). 在左侧导航列中，导航到 **[!UICONTROL 工作流]**. 选择 **[!UICONTROL 导入方法]** 后接选择 **[!UICONTROL Launch]**. 请参阅下面的屏幕截图以作参考。

![](../images/models-recipes/package-source-files/import.png)

的 **[!UICONTROL 配置]** 页面。 提供适当的 **[!UICONTROL 方法名称]**，例如“零售销售方法”，并（可选）提供描述或文档URL。 完成后，单击 **[!UICONTROL 下一个]**.

![](../images/models-recipes/package-source-files/configure.png)

选择相应的 *运行时*，然后选择 **[!UICONTROL 分类]** 表示 *类型*. 完成后，将生成Azure容器注册表凭据。

>[!NOTE]
>
>*类型* 是机器学习类问题，该方法是为设计的，经过培训后用于帮助定制评估培训运行。

>[!TIP]
>
>- 对于 [!DNL Python] 方法选择 **[!UICONTROL Python]** 运行时。
>- 对于R种方法，请选择 **[!UICONTROL R]** 运行时。
>- 对于PySpark配方，请选择 **[!UICONTROL PySpark]** 运行时。 自动填充对象类型。
>- 对于Scala方法，选择 **[!UICONTROL 火花]** 运行时。 自动填充对象类型。


![](../images/models-recipes/package-source-files/docker-creds.png)

请注意Docker主机、用户名和密码的值。 这些组件用于构建和推送您的 [!DNL Docker] 图像。

>[!NOTE]
>
>完成下面列出的步骤后，会提供源URL。 有关配置文件的说明，请参阅 [后续步骤](#next-steps).

### 打包源文件

首先，获取在 <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform数据科学工作区参考</a> 存储库。

- [构建Python Docker图像](#python-docker)
- [生成R Docker映像](#r-docker)
- [构建PySpark Docker图像](#pyspark-docker)
- [构建Scala(Spark)Docker图像](#scala-docker)

### 生成 [!DNL Python] Docker图像 {#python-docker}

如果尚未复制，请克隆 [!DNL GitHub] 使用以下命令将存储库放到本地系统上：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

导航到目录 `experience-platform-dsw-reference/recipes/python/retail`. 在此，您将找到脚本 `login.sh` 和 `build.sh` 用于登录到Docker并构建 [!DNL Python Docker] 图像。 如果您 [Docker凭据](#docker-based-model-authoring) 就绪，按顺序输入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

请注意，在执行登录脚本时，您需要提供Docker主机、用户名和密码。 构建时，需要提供Docker主机和内部版本的版本标记。

生成脚本完成后，控制台输出中会为您提供一个Docker源文件URL。 对于此特定示例，它将类似于：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

复制此URL并转到 [后续步骤](#next-steps).

### 内部版本R [!DNL Docker] 图像 {#r-docker}

如果尚未复制，请克隆 [!DNL GitHub] 使用以下命令将存储库放到本地系统上：

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

导航到目录 `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` 在克隆的存储库中。 在这里，你会找到文件 `login.sh` 和 `build.sh` 用于登录Docker和构建R Docker图像。 如果您 [Docker凭据](#docker-based-model-authoring) 就绪，按顺序输入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

请注意，在执行登录脚本时，您需要提供Docker主机、用户名和密码。 构建时，需要提供Docker主机和内部版本的版本标记。

生成脚本完成后，控制台输出中会为您提供一个Docker源文件URL。 对于此特定示例，它将类似于：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

复制此URL并转到 [后续步骤](#next-steps).

### 构建PySpark Docker图像 {#pyspark-docker}

首先，克隆 [!DNL GitHub] 使用以下命令将存储库放到本地系统上：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

导航到目录 `experience-platform-dsw-reference/recipes/pyspark/retail`. 脚本 `login.sh` 和 `build.sh` 位于此处，用于登录Docker和构建Docker图像。 如果您 [Docker凭据](#docker-based-model-authoring) 就绪，按顺序输入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

请注意，在执行登录脚本时，您需要提供Docker主机、用户名和密码。 构建时，需要提供Docker主机和内部版本的版本标记。

生成脚本完成后，控制台输出中会为您提供一个Docker源文件URL。 对于此特定示例，它将类似于：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

复制此URL并转到 [后续步骤](#next-steps).

### 生成Scala Docker图像 {#scala-docker}

首先，克隆 [!DNL GitHub] 在终端中使用以下命令将存储库存储到本地系统上：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

接下来，导航到目录 `experience-platform-dsw-reference/recipes/scala` 您可以在其中找到脚本 `login.sh` 和 `build.sh`. 这些脚本用于登录到Docker并构建Docker图像。 如果您 [Docker凭据](#docker-based-model-authoring) 就绪，按顺序向终端输入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>如果您在尝试使用 `login.sh` 脚本，尝试使用命令 `bash login.sh`.

执行登录脚本时，您需要提供Docker主机、用户名和密码。 构建时，需要提供Docker主机和内部版本的版本标记。

生成脚本完成后，控制台输出中会为您提供一个Docker源文件URL。 对于此特定示例，它将类似于：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

复制此URL并转到 [后续步骤](#next-steps).

## 后续步骤 {#next-steps}

本教程介绍了如何将源文件打包到方法中，这是将方法导入的先决条件步骤 [!DNL Data Science Workspace]. 现在，您应该在Azure容器注册表中拥有Docker图像以及相应的图像URL。 现在，您可以开始将打包的方法导入的教程 [!DNL Data Science Workspace]. 请选择以下教程链接之一以开始操作：

- [在UI中导入打包的方法](./import-packaged-recipe-ui.md)
- [使用API导入打包的方法](./import-packaged-recipe-api.md)
