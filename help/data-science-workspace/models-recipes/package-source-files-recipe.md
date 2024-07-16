---
keywords: Experience Platform；包源文件；数据科学Workspace；热门主题；Docker；Docker图像
solution: Experience Platform
title: 将Source文件打包到方法中
type: Tutorial
description: 本教程介绍了如何将提供的零售业示例源文件打包到存档文件中，该文件可用于在Adobe Experience Platform数据科学Workspace中通过在UI中或使用API遵循方法导入工作流创建方法。
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 0%

---

# 将源文件打包到方法中

本教程介绍如何将提供的零售业示例源文件打包到存档文件中，该文件可用于通过在UI中或使用API中遵循方法导入工作流在Adobe Experience Platform [!DNL Data Science Workspace]中创建方法。

要了解的概念：

- **方法**：方法是Adobe对模型规范的术语，是一个顶级容器，表示构建和执行经过训练的模型并因此帮助解决特定业务问题所需的特定机器学习、人工智能算法或算法组合、处理逻辑和配置。
- **Source文件**：项目中包含方法逻辑的单个文件。

## 先决条件

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## 方法创建

方法创建从打包源文件开始，以构建存档文件。 Source文件定义了用于解决手头特定问题的机器学习逻辑和算法，并以[!DNL Python]、R、PySpark或Scala编写。 构建存档文件采用Docker映像的形式。 构建后，将打包的存档文件导入[!DNL Data Science Workspace]以在UI](./import-packaged-recipe-ui.md)中或使用API](./import-packaged-recipe-api.md)在[中创建方法[。

### 基于Docker的模型创作 {#docker-based-model-authoring}

利用Docker映像，开发人员可以将应用程序打包到其所需的所有部分（如库和其他依赖项），并将其作为一个包发出。

使用在方法创建工作流期间提供给您的凭据，将生成的Docker图像推送到Azure容器注册表。

若要获取Azure Container Registry凭据，请登录[Adobe Experience Platform](https://platform.adobe.com)。 在左侧导航列中，导航到&#x200B;**[!UICONTROL 工作流]**。 选择&#x200B;**[!UICONTROL 导入方法]**，然后选择&#x200B;**[!UICONTROL 启动项]**。 请参阅下面的屏幕快照以供参考。

![](../images/models-recipes/package-source-files/import.png)

将打开&#x200B;**[!UICONTROL 配置]**&#x200B;页面。 提供适当的&#x200B;**[!UICONTROL 方法名称]**，例如“零售方法”，并可以选择提供描述或文档URL。 完成后，单击&#x200B;**[!UICONTROL 下一步]**。

![](../images/models-recipes/package-source-files/configure.png)

选择适当的&#x200B;*运行时*，然后为&#x200B;*类型*&#x200B;选择&#x200B;**[!UICONTROL 分类]**。 完成后，将生成Azure容器注册表凭据。

>[!NOTE]
>
>*类型*&#x200B;是设计方法的机器学习问题类，训练后用于帮助定制评估训练运行。

>[!TIP]
>
>- 对于[!DNL Python]脚本，请选择&#x200B;**[!UICONTROL Python]**&#x200B;运行时。
>- 对于R脚本，请选择&#x200B;**[!UICONTROL R]**&#x200B;运行时。
>- 对于PySpark脚本，请选择&#x200B;**[!UICONTROL PySpark]**&#x200B;运行时。 工件类型会自动填充。
>- 对于Scala配方，请选择&#x200B;**[!UICONTROL Spark]**&#x200B;运行时。 工件类型会自动填充。

![](../images/models-recipes/package-source-files/docker-creds.png)

记下Docker主机、用户名和密码的值。 这些功能用于在下面概述的工作流中生成和推送您的[!DNL Docker]图像。

>[!NOTE]
>
>在完成下面列出的步骤后，将提供Source URL。 在[后续步骤](#next-steps)中提供的后续教程中说明了配置文件。

### 打包源文件

首先，获取在<a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform数据科学Workspace引用</a>存储库中找到的示例代码库。

- [构建Python Docker图像](#python-docker)
- [构建或Docker图像](#r-docker)
- [构建PySpark Docker图像](#pyspark-docker)
- [构建Scala (Spark) Docker图像](#scala-docker)

### 生成[!DNL Python] Docker图像 {#python-docker}

如果尚未这样做，请使用以下命令将[!DNL GitHub]存储库克隆到本地系统：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

导航到目录`experience-platform-dsw-reference/recipes/python/retail`。 在这里，您将找到用于登录到Docker并构建[!DNL Python Docker]映像的脚本`login.sh`和`build.sh`。 如果您已准备好[Docker凭据](#docker-based-model-authoring)，请依次输入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

请注意，执行登录脚本时，您需要提供Docker主机、用户名和密码。 构建时，您需要提供Docker主机和构建版本标记。

构建脚本完成后，控制台输出中会为您提供Docker源文件URL。 对于此特定示例，它类似于：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

复制此URL并转到[后续步骤](#next-steps)。

### 生成R [!DNL Docker]图像 {#r-docker}

如果尚未这样做，请使用以下命令将[!DNL GitHub]存储库克隆到本地系统：

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

导航到克隆的存储库中的目录`experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting`。 在这里，您将找到用于登录Docker和构建R Docker映像的文件`login.sh`和`build.sh`。 如果您已准备好[Docker凭据](#docker-based-model-authoring)，请依次输入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

请注意，执行登录脚本时，您需要提供Docker主机、用户名和密码。 构建时，您需要提供Docker主机和构建版本标记。

构建脚本完成后，控制台输出中会为您提供Docker源文件URL。 对于此特定示例，它类似于：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

复制此URL并转到[后续步骤](#next-steps)。

### 构建PySpark Docker图像 {#pyspark-docker}

首先，使用以下命令将[!DNL GitHub]存储库克隆到本地系统：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

导航到目录`experience-platform-dsw-reference/recipes/pyspark/retail`。 脚本`login.sh`和`build.sh`位于此处，用于登录Docker和构建Docker映像。 如果您已准备好[Docker凭据](#docker-based-model-authoring)，请依次输入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

请注意，执行登录脚本时，您需要提供Docker主机、用户名和密码。 构建时，您需要提供Docker主机和构建版本标记。

构建脚本完成后，控制台输出中会为您提供Docker源文件URL。 对于此特定示例，它类似于：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

复制此URL并转到[后续步骤](#next-steps)。

### 构建Scala Docker映像 {#scala-docker}

首先，在“终端”中使用以下命令将[!DNL GitHub]存储库克隆到本地系统：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

接下来，导航到目录`experience-platform-dsw-reference/recipes/scala`，您可以在其中找到脚本`login.sh`和`build.sh`。 这些脚本用于登录到Docker并构建Docker映像。 如果您已准备好[Docker凭据](#docker-based-model-authoring)，请依次向终端输入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>如果您在尝试使用`login.sh`脚本登录Docker时遇到权限错误，请尝试使用命令`bash login.sh`。

执行登录脚本时，您需要提供Docker主机、用户名和密码。 构建时，您需要提供Docker主机和构建版本标记。

构建脚本完成后，控制台输出中会为您提供Docker源文件URL。 对于此特定示例，它类似于：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

复制此URL并转到[后续步骤](#next-steps)。

## 后续步骤 {#next-steps}

本教程将源文件打包到方法中，这是将方法导入[!DNL Data Science Workspace]的先决步骤。 现在，您应在Azure容器注册表中具有Docker图像以及相应的图像URL。 您现在可以开始教程，介绍如何将打包的方法导入[!DNL Data Science Workspace]。 选择以下教程链接之一开始：

- [在UI中导入打包的方法](./import-packaged-recipe-ui.md)
- [使用API导入打包的方法](./import-packaged-recipe-api.md)
