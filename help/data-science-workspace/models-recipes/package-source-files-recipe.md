---
keywords: Experience Platform；打包源文件；数据科学工作区；热门主题；Docker;Docker图像
solution: Experience Platform
title: 将源文件打包到菜谱中
topic-legacy: tutorial
type: Tutorial
description: 本教程说明了如何将提供的零售销售示例源文件打包到存档文件中，该存档文件可用于通过在UI中或使用API遵循菜谱导入工作流在Adobe Experience Platform Data Science Workspace中创建菜谱。
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 0%

---

# 将源文件打包到菜谱中

本教程说明了如何将提供的零售销售示例源文件打包到存档文件中，该存档文件可用于通过在UI中或使用API遵循菜谱导入工作流在Adobe Experience Platform [!DNL Data Science Workspace]中创建菜谱。

要了解的概念：

- **菜谱**:菜谱是“模型”规范的Adobe术语，是表示特定机器学习、人工智能算法或集成算法、处理逻辑和配置的顶级容器，用于构建和执行经过培训的模型，从而帮助解决特定的业务问题。
- **源文件**:项目中包含菜谱逻辑的各个文件。

## 先决条件

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## 菜谱创建

菜谱创建开始与打包源文件以构建存档文件。 源文件定义用于解决手头特定问题的机器学习逻辑和算法，并以[!DNL Python]、R、PySpark或Scala编写。 构建的存档文件采用Docker图像的形式。 生成后，打包的归档文件将导入[!DNL Data Science Workspace]中，以使用API](./import-packaged-recipe-api.md)在UI](./import-packaged-recipe-ui.md)或[中创建菜谱[。

### 基于Docker的模型创作{#docker-based-model-authoring}

Docker图像允许开发者将应用程序与所需的所有部件（如库和其他依赖项）打包，并将其作为一个包发布。

生成的Docker映像将使用在菜谱创建工作流程期间提供给您的凭据推送到Azure容器注册表。

要获取您的Azure容器注册表凭据，请登录[Adobe Experience Platform](https://platform.adobe.com)。 在左侧导航列中，导航到&#x200B;**[!UICONTROL Workflows]**。 选择&#x200B;**[!UICONTROL Import Recipe]**，然后选择&#x200B;**[!UICONTROL Launch]**。 请参阅下面的屏幕截图。

![](../images/models-recipes/package-source-files/import.png)

将打开&#x200B;**[!UICONTROL Configure]**&#x200B;页。 提供相应的&#x200B;**[!UICONTROL Recipe Name]**（例如“零售销售菜谱”），并（可选）提供说明或文档URL。 完成后，单击&#x200B;**[!UICONTROL Next]**。

![](../images/models-recipes/package-source-files/configure.png)

选择适当的&#x200B;*Runtime*，然后为&#x200B;*类型*&#x200B;选择&#x200B;**[!UICONTROL Classification]**。 完成后，将生成您的Azure容器注册表凭据。

>[!NOTE]
>
>*Type是* 菜谱所针对的机器学习类问题，经过培训后可用于帮助定制评估培训运行。

>[!TIP]
>
>- 对于[!DNL Python]方法，请选择&#x200B;**[!UICONTROL Python]**&#x200B;运行时。
>- 对于R方法，请选择&#x200B;**[!UICONTROL R]**&#x200B;运行时。
>- 对于PySpark方法，请选择&#x200B;**[!UICONTROL PySpark]**&#x200B;运行时。 自动填充伪像类型。
>- 对于Scala方法，请选择&#x200B;**[!UICONTROL Spark]**&#x200B;运行时。 自动填充伪像类型。


![](../images/models-recipes/package-source-files/docker-creds.png)

请注意Docker主机、用户名和密码的值。 这些组件用于在下面概述的工作流中构建和推送您的[!DNL Docker]映像。

>[!NOTE]
>
>完成以下步骤后将提供源URL。 配置文件将在[后续步骤](#next-steps)中的后续教程中说明。

### 打包源文件

开始，方法是获取<a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform数据科学工作区参考</a>存储库中的示例代码库。

- [构建Python Docker图像](#python-docker)
- [构建R Docker图像](#r-docker)
- [构建PySpark Docker图像](#pyspark-docker)
- [构建Scala(Spark)Docker图像](#scala-docker)

### 生成[!DNL Python] Docker映像{#python-docker}

如果尚未这样做，请使用以下命令将[!DNL GitHub]存储库克隆到本地系统上：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

导航到目录`experience-platform-dsw-reference/recipes/python/retail`。 在此，您将找到用于登录Docker和构建[!DNL Python Docker]图像的脚本`login.sh`和`build.sh`。 如果您的[Docker凭据](#docker-based-model-authoring)已准备就绪，请按顺序输入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

请注意，在执行登录脚本时，您需要提供Docker主机、用户名和密码。 在构建时，您需要提供Docker主机和用于构建的版本标签。

构建脚本完成后，控制台输出中会为您提供一个Docker源文件URL。 对于此特定示例，它将类似于：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

复制此URL并转到[后续步骤](#next-steps)。

### 生成R [!DNL Docker]映像{#r-docker}

如果尚未这样做，请使用以下命令将[!DNL GitHub]存储库克隆到本地系统上：

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

导航到克隆存储库中的目录`experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting`。 在此，您将找到用于登录Docker和生成R Docker图像的文件`login.sh`和`build.sh`。 如果您的[Docker凭据](#docker-based-model-authoring)已准备就绪，请按顺序输入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

请注意，在执行登录脚本时，您需要提供Docker主机、用户名和密码。 在构建时，您需要提供Docker主机和用于构建的版本标签。

构建脚本完成后，控制台输出中会为您提供一个Docker源文件URL。 对于此特定示例，它将类似于：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

复制此URL并转到[后续步骤](#next-steps)。

### 构建PySpark Docker图像{#pyspark-docker}

开始：使用以下命令将[!DNL GitHub]存储库克隆到本地系统上：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

导航到目录`experience-platform-dsw-reference/recipes/pyspark/retail`。 脚本`login.sh`和`build.sh`位于此处，用于登录Docker和生成Docker图像。 如果您的[Docker凭据](#docker-based-model-authoring)已准备就绪，请按顺序输入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

请注意，在执行登录脚本时，您需要提供Docker主机、用户名和密码。 在构建时，您需要提供Docker主机和用于构建的版本标签。

构建脚本完成后，控制台输出中会为您提供一个Docker源文件URL。 对于此特定示例，它将类似于：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

复制此URL并转到[后续步骤](#next-steps)。

### 生成Scala Docker映像{#scala-docker}

开始：使用终端中的以下命令将[!DNL GitHub]存储库克隆到本地系统上：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

接下来，导览至目录`experience-platform-dsw-reference/recipes/scala`，您可以在其中找到脚本`login.sh`和`build.sh`。 这些脚本用于登录Docker并构建Docker图像。 如果您的[Docker凭据](#docker-based-model-authoring)已准备就绪，请按顺序向终端输入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>如果您在尝试使用`login.sh`脚本登录Docker时收到权限错误，请尝试使用命令`bash login.sh`。

执行登录脚本时，您需要提供Docker主机、用户名和密码。 在构建时，您需要提供Docker主机和用于构建的版本标签。

构建脚本完成后，控制台输出中会为您提供一个Docker源文件URL。 对于此特定示例，它将类似于：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

复制此URL并转到[后续步骤](#next-steps)。

## 后续步骤 {#next-steps}

本教程重点介绍将源文件打包到菜谱中，这是将菜谱导入[!DNL Data Science Workspace]的先决条件步骤。 您现在应在Azure容器注册表中拥有Docker图像以及相应的图像URL。 现在，您已准备好开始将打包菜谱导入[!DNL Data Science Workspace]的教程。 选择以下教程链接之一以开始使用：

- [在UI中导入打包菜谱](./import-packaged-recipe-ui.md)
- [使用API导入打包的菜谱](./import-packaged-recipe-api.md)
