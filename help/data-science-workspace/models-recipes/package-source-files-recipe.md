---
keywords: Experience Platform;package source files;Data Science Workspace;popular topics
solution: Experience Platform
title: 将源文件打包到菜谱中
topic: Tutorial
translation-type: tm+mt
source-git-commit: 91c7b7e285a4745da20ea146f2334510ca11b994

---


# 将源文件打包到菜谱中

本教程提供了有关如何将提供的零售销售示例源文件打包到存档文件中的说明，该存档文件可用于通过在UI中或使用API遵循菜谱导入工作流在Adobe Experience Platform Data Science Workspace中创建菜谱。

要了解的概念：

- **菜谱**:菜谱是Adobe的“模型”规范术语，是表示构建和执行经过培训的模型所需的特定机器学习、人工智能算法或算法集合、处理逻辑和配置的顶级容器，因此有助于解决特定的业务问题。
- **源文件**:项目中包含菜谱逻辑的单个文件。

## 先决条件

- <a href="https://docs.docker.com/install/#supported-platforms" target="_blank">Docker</a>
- <a href="https://docs.conda.io/en/latest/miniconda.html" target="_blank">Python 3和pip</a>
- <a href="https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883" target="_blank">斯卡拉</a>
- <a href="https://maven.apache.org/install.html" target="_blank">马文</a>

## 菜谱创建

菜谱创建开始与打包源文件以构建存档文件。 源文件定义了用于解决现有特定问题的机器学习逻辑和算法，并以Python、R、PySpark或Scala Spark编写。 根据源文件的编写语言，构建的存档文件将是Docker图像或二进制文件。 构建完毕后，打包的存档文件将导入Data Science Workspace中，以在UI中或 [使用API](./import-packaged-recipe-ui.md)[创建菜谱](./import-packaged-recipe-api.md)。

### 基于Docker的模型创作

Docker图像允许开发人员将应用程序与其所需的所有部件（如库和其他依赖项）打包，并将其作为一个包发布。

构建的Docker图像将使用在菜谱创建工作流程中提供给您的凭据推送到Azure容器注册表。

>[!NOTE] 只有以 **Python**、 **R**&#x200B;和Tensorflow编写的源文件需 **** 要Azure容器注册表凭据。

要获取您的Azure容器注册表凭据，请登 <a href="https://platform.adobe.com" target="_blank">录Adobe Experience Platform</a>。 在左侧导航列上，导航到 **工作流**。 选择 **“从源文件导入菜谱**”，然 **后启动** 新的导入过程。 请参阅下面的屏幕截图以作参考。

![](../images/models-recipes/package-source-files/workflow_ss.png)

提供相应的 **处方名称**（例如“零售销售处方”），并（可选）提供说明或文档URL。 完成后，单击“下 **一步**”。

![](../images/models-recipes/package-source-files/recipe_info.png)

选择相应的 **Runtime**，然后选择“类 **型** ” **分类**。 将生成Azure容器注册表凭据。

![](../images/models-recipes/package-source-files/recipe_workflow_recipe_source.png)

请注意Docker主 **机、用户名****和密**&#x200B;码值 ****。 稍后将使用这些组件构建和推送Docker图像。

推送后，您和其他用户可以通过URL访问图像。 “ **源文件** ”字段将要求此URL作为输入。

### 基于二进制的模型创作

对于使用Scala或PySpark编写的源文件，将生成一个二进制文件。 构建二进制文件与运行提供的构建脚本一样简单。
>[!NOTE] 只有使用ScalaSpark或PySpark编写的源文件在运行构建脚本时才会生成二进制文件。

### 打包源文件

开始，即可获取 <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform Data Science Workspace参考存储库中的示例代码库</a> 。 根据编写示例源文件所用的编程语言，构建它们各自的归档文件的过程有所不同。

- [构建Python Docker图像](#build-python-docker-image)
- [构建R Docker图像](#build-r-docker-image)
- [构建PySpark二进制文件](#build-pyspark-binaries)
- [构建Scala二进制文件](#build-scala-binaries)

#### 构建Python Docker图像

如果尚未这样做，请使用以下命令将github存储库克隆到本地系统上：

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigate to the directory `experience-platform-dsw-reference/recipes/python/retail`. 在此，您将找到脚 `login.sh` 本以 `build.sh` 及用于登录Docker和构建python Docker图像的脚本。 如果您的 [Docker凭据已准备好](#docker-based-model-authoring) ，请按顺序输入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

请注意，执行登录脚本时，您需要提供Docker主机、用户名和密码。 在构建时，您需要为构建提供Docker主机和版本标签。

构建脚本完成后，控制台输出中会为您提供一个Docker源文件URL。 对于此特定示例，其外观将类似于：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

复制此URL并转到下 [一步](#next-steps)。

#### 构建R Docker图像

如果尚未这样做，请使用以下命令将github存储库克隆到本地系统上：

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

导航到克隆存储库 `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` 中的目录。 在此，您将找到用 `login.sh` 于登 `build.sh` 录Docker和构建R Docker映像的文件。 如果您的 [Docker凭据已准备好](#docker-based-model-authoring) ，请按顺序输入以下命令：

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

请注意，执行登录脚本时，您需要提供Docker主机、用户名和密码。 在构建时，您需要为构建提供Docker主机和版本标签。

构建脚本完成后，控制台输出中会为您提供一个Docker源文件URL。 对于此特定示例，其外观将类似于：

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

复制此URL并转到下 [一步](#next-steps)。

#### 构建PySpark二进制文件

如果尚未这样做，请使用以下命令将github存储库克隆到本地系统上：

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

导览至本地系统上的克隆存储库并运行以下命令，以构建导入PySpark菜谱 `.egg` 所需的文件：

```BASH
cd recipes/pyspark
./build.sh
```

文件 `.egg` 会在文件夹中生 `dist` 成。

您现在可以继续执行下 [一步](#next-steps)。

#### 构建Scala二进制文件

如果尚未执行此操作，请运行以下命令将Github存储库克隆到本地系统：

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

要构建用于 `.jar` 导入Scala菜谱的对象，请导航到克隆的存储库，然后按照以下步骤操作：

```BASH
cd recipes/scala/
./build.sh
```

目录中 `.jar` 可找到生成的具有依赖关系的 `/target` 对象。

您现在可以继续执行下 [一步](#next-steps)。

## 后续步骤

本教程详细介绍了将源文件打包到菜谱中，这是将菜谱导入数据科学工作区的先决条件。 您现在应该在Azure容器注册表中有一个Docker图像，以及相应的图像URL或二进制文件存储在文件系统中的本地。 您现在可以开始教程“将打包的菜谱 **导入数据科学工作区”**。 选择以下教程链接之一以开始。

- [在UI中导入打包的菜谱](./import-packaged-recipe-ui.md)
- [使用API导入打包的菜谱](./import-packaged-recipe-api.md)