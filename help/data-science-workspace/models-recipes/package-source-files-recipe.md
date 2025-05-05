---
keywords: Experience Platform；包源文件；Data Science Workspace；热门主题；Docker；Docker图像
solution: Experience Platform
title: 将源文件打包到配方中
type: Tutorial
description: 本教程提供了有关如何将提供的Retail Sales示例源文件打包为存档文件的说明，您可以使用存档文件，在UI中或通过使用API遵循处方导入工作流程，在Adobe Experience Platform Data Science Workspace中创建处方。
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 0%

---

# 将源文件打包到方法中

>[!NOTE]
>
>Data Science Workspace不再可购买。
>
>本文档适用于先前有权使用Data Science Workspace的现有客户。

本教程提供了有关如何将提供的Retail Sales示例源文件打包为存档文件的说明，该存档文件可用于在Adobe Experience Platform [!DNL Data Science Workspace]中创建处方，方法是在UI中遵循处方导入工作流程或使用API。

要了解的概念：

- **食谱**：食谱是模型规范的Adobe术语，是一个顶级容器，表示构建和执行训练模型从而帮助解决特定业务问题所需的特定机器学习、人工智能算法或算法、处理逻辑和配置组合。
- **源文件**：您的项目中包含配方逻辑的单个文件。

## 先决条件

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## 配方创建

配方创建从打包源文件开始，以构建存档文件。 源文件定义了用于解决手头特定问题的机器学习逻辑和算法，并用 R、PySpark 或 Scala 编写 [!DNL Python]。 构建的存档文件采用 Docker 映像的形式。 生成后，将打包的存档文件导入到[!DNL Data Science Workspace]中，以使用API[&#128279;](./import-packaged-recipe-api.md)在UI[&#128279;](./import-packaged-recipe-ui.md)或中创建方法。

### 基于Docker的模型创作 {#docker-based-model-authoring}

使用Docker映像，开发人员可以将应用程序打包为它需要的所有组件（如库和其他依赖项），然后将其作为一个包发送。

在创建处方工作流程期间，使用为您提供的凭据将构建的Docker图像推送到Azure容器注册表。

要获取Azure Container Registry凭据，请登录[Adobe Experience Platform](https://platform.adobe.com)。 在左侧导航列中，导航到&#x200B;**[!UICONTROL 工作流]**。 选择&#x200B;**[!UICONTROL 导入配方]**，然后选择&#x200B;**[!UICONTROL 启动]**。 请参阅以下屏幕截图以供参考。

![](../images/models-recipes/package-source-files/import.png)

此时会打开“ **[!UICONTROL 配置]** ”页面。 提供适当的 **[!UICONTROL 配方名称]**，例如“零售销售配方”，并选择性地提供描述或文档 URL。 完成后，单击“下一步&#x200B;**”。**

![](../images/models-recipes/package-source-files/configure.png)

选择适当的&#x200B;*运行时*，然后为&#x200B;*类型*&#x200B;选择&#x200B;**[!UICONTROL 分类]**。 您的Azure Container Registry凭据将在完成后生成。

>[!NOTE]
>
>*类型*&#x200B;是配方设计的机器学习问题类，在培训后用于帮助定制评估培训运行。

>[!TIP]
>
>- 对于[!DNL Python]处方，请选择&#x200B;**[!UICONTROL Python]**&#x200B;运行时。
>- 对于R处方，请选择&#x200B;**[!UICONTROL R]**&#x200B;运行时。
>- 对于PySpark配方，请选择&#x200B;**[!UICONTROL PySpark]**&#x200B;运行时。 项目类型自动填充。
>- 对于Scala配方，请选择&#x200B;**[!UICONTROL Spark]**&#x200B;运行时。 项目类型自动填充。

![](../images/models-recipes/package-source-files/docker-creds.png)

请记下Docker主机、用户名和密码的值。 这些用于在下面概述的工作流程中构建和推送[!DNL Docker]图像。

>[!NOTE]
>
>完成下述步骤后会提供源URL。 在[后续步骤](#next-steps)中找到的后续教程中说明了该配置文件。

### 打包源文件

首先获取<a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience PlatformData Science Workspace Reference</a>存储库中找到的示例代码库。

- [构建Python Docker映像](#python-docker)
- [Build R Docker映像](#r-docker)
- [构建PySpark Docker图像](#pyspark-docker)
- [构建Scala (Spark) Docker图像](#scala-docker)

### 构建 [!DNL Python] Docker 映像 {#python-docker}

如果尚未执行此操作，请使用以下命令将存储库克隆 [!DNL GitHub] 到本地系统上：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

导航到目录 `experience-platform-dsw-reference/recipes/python/retail`。 在这里，您将找到用于登录到 Docker 和构建[!DNL Python Docker]映像的脚本。`login.sh` `build.sh`如果您已 [准备好 Docker 凭据](#docker-based-model-authoring) ，请按顺序输入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

请注意，在执行登录脚本时，您需要提供Docker主机、用户名和密码。 在生成时，您需要提供Docker主机和生成的版本标记。

生成脚本完成后，将在控制台输出中为您提供一个Docker源文件URL。 对于此特定示例，其内容将类似于：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

复制此URL并继续执行[后续步骤](#next-steps)。

### 生成[!DNL Docker]映像 {#r-docker}

如果尚未这样做，请使用以下命令将[!DNL GitHub]存储库克隆到您的本地系统：

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

导航到克隆的存储库内的目录 `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` 。 在这里，你将找到这些文件，`build.sh`你将使用这些文件`login.sh`登录到 Docker 并生成 R Docker 映像。如果您已 [准备好 Docker 凭据](#docker-based-model-authoring) ，请按顺序输入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

请注意，执行登录脚本时，您需要提供 Docker 主机、用户名和密码。 在生成时，您需要提供Docker主机和生成的版本标记。

生成脚本完成后，将在控制台输出中为您提供一个Docker源文件URL。 对于此特定示例，其内容将类似于：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

复制此URL并继续执行[后续步骤](#next-steps)。

### 构建PySpark Docker图像 {#pyspark-docker}

首先使用 [!DNL GitHub] 以下命令将存储库克隆到本地系统上：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

导航到目录 `experience-platform-dsw-reference/recipes/pyspark/retail`。 脚本 `login.sh` 和 `build.sh` 位于此处，用于登录到 Docker 和构建 Docker 映像。 如果您已 [准备好 Docker 凭据](#docker-based-model-authoring) ，请按顺序输入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

请注意，执行登录脚本时，您需要提供 Docker 主机、用户名和密码。 在生成时，您需要提供Docker主机和生成的版本标记。

生成脚本完成后，将在控制台输出中为您提供一个Docker源文件URL。 对于此特定示例，其内容将类似于：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

复制此URL并继续执行[后续步骤](#next-steps)。

### 构建Scala Docker映像 {#scala-docker}

首先在终端中使用以下命令将[!DNL GitHub]存储库克隆到本地系统：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

接下来，导航到目录`experience-platform-dsw-reference/recipes/scala`，您可以在其中找到脚本`login.sh`和`build.sh`。 这些脚本用于登录Docker并构建Docker映像。 如果您已准备好[Docker凭据](#docker-based-model-authoring)，请依次向终端输入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>如果在尝试使用`login.sh`脚本登录Docker时收到权限错误，请尝试使用命令`bash login.sh`。

执行登录脚本时，您需要提供Docker主机、用户名和密码。 在生成时，您需要提供Docker主机和生成的版本标记。

生成脚本完成后，将在控制台输出中为您提供一个Docker源文件URL。 对于此特定示例，其内容将类似于：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

复制此 URL 并继续执行 [后续步骤](#next-steps)。

## 后续步骤 {#next-steps}

本教程介绍了如何将源文件打包到配方中，这是将配方导入 的 [!DNL Data Science Workspace]先决条件步骤。 现在，Azure容器注册表中应该有一个Docker图像以及相应的图像URL。 您现在已准备好开始有关将打包配方导入[!DNL Data Science Workspace]的教程。 选择以下教程链接之一以开始：

- [在UI中导入包装后的处方](./import-packaged-recipe-ui.md)
- [使用API导入包装的处方](./import-packaged-recipe-api.md)
