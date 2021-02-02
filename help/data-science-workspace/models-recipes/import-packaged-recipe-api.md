---
keywords: Experience Platform；导入打包菜谱；数据科学工作区；热门主题；菜谱；api;sensei机器学习；创建引擎
solution: Experience Platform
title: 导入打包的菜谱(API)
topic: tutorial
type: Tutorial
description: '本教程使用Sensei Machine Learning API创建引擎，在用户界面中也称为“菜谱”。 '
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 2%

---


# 导入打包的菜谱(API)

本教程使用[[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)创建[Engine](../api/engines.md)，在用户界面中也称为“菜谱”。

在开始之前，请务必注意，Adobe Experience Platform[!DNL Data Science Workspace]使用不同术语来引用API和UI中的类似元素。 本教程中使用API术语，下表概述了相关术语：

| UI术语 | API术语 |
| ---- | ---- |
| 菜谱 | [引擎](../api/engines.md) |
| 模型 | [MLInstance](../api/mlinstances.md) |
| 培训和评估 | [实验](../api/experiments.md) |
| 服务 | [MLService](../api/mlservices.md) |

引擎包含机器学习算法和逻辑来解决特定问题。 下图提供了显示[!DNL Data Science Workspace]中的API工作流的可视化。 本教程重点介绍如何创建引擎，即机器学习模型的大脑。

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## 入门指南

本教程需要以Docker URL形式打包的Recipe文件。 按照[将源文件打包到Recipe](./package-source-files-recipe.md)教程，创建打包的Recipe文件或提供您自己的文件。

- `{DOCKER_URL}`:智能服务的Docker映像的URL地址。

本教程要求您完成对Adobe Experience Platform的[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)，以成功调用[!DNL Platform] API。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

- `{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。
- `{IMS_ORG}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。
- `{API_KEY}`:您在独特的Adobe Experience Platform集成中找到的特定API密钥值。

## 创建引擎

可以通过向/engine端点发出POST请求来创建引擎。 创建的引擎基于打包的处方文件的形式进行配置，该文件必须作为API请求的一部分提供。

### 创建具有Docker URL {#create-an-engine-with-a-docker-url}的引擎

要创建包含存储在Docker容器中的打包Recipe文件的引擎，您必须为打包Recipe文件提供Docker URL。

>[!CAUTION]
>
> 如果您使用[!DNL Python]或R，请使用下面的请求。 如果您使用PySpark或Scala，请使用位于Python/R示例下的PySpark/Scala请求示例。

**API格式**

```http
POST /engines
```

**请求Python/R**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H `x-sandbox-name: {SANDBOX_NAME}` \
    -F 'engine={
        "name": "Retail Sales Engine Python",
        "description": "A description for Retail Sales Engine, this Engines execution type is Python",
        "type": "Python"
        "artifacts": {
            "default": {
                "image": {
                    "location": "{DOCKER_URL}",
                    "name": "retail_sales_python",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| 属性 | 描述 |
| -------  | ----------- |
| `engine.name` | 引擎的所需名称。 与此引擎对应的处方将继承此值，该值将作为处方的名称显示在[!DNL Data Science Workspace]用户界面中。 |
| `engine.description` | 引擎的可选说明。 此引擎对应的处方将继承此值，该值将作为处方的说明显示在[!DNL Data Science Workspace]用户界面中。 请勿删除此属性，如果您选择不提供说明，则让此值为空字符串。 |
| `engine.type` | 引擎的执行类型。 此值与开发Docker图像所用的语言相对应。 当提供Docker URL以创建引擎时，`type`是`Python`、`R`、`PySpark`、`Spark`(Scala)或`Tensorflow`。 |
| `artifacts.default.image.location` | 您的`{DOCKER_URL}`将转到此处。 完整的Docker URL具有以下结构：`your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Docker图像文件的附加名称。 请勿删除此属性，如果您选择不提供其他Docker图像文件名，则让此值为空字符串。 |
| `artifacts.default.image.executionType` | 此引擎的执行类型。 此值与开发Docker图像所用的语言相对应。 当提供Docker URL以创建引擎时，`executionType`是`Python`、`R`、`PySpark`、`Spark`(Scala)或`Tensorflow`。 |

**请求PySpark**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
    "name": "PySpark retail sales recipe",
    "description": "A description for this Engine",
    "type": "PySpark",
    "mlLibrary":"databricks-spark",
    "artifacts": {
        "default": {
            "image": {
                "name": "modelspark",
                "executionType": "PySpark",
                "packagingType": "docker",
                "location": "v1d2cs4mimnlttw.azurecr.io/sarunbatchtest:0.0.1"
            }
        }
    }
}'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 引擎的所需名称。 与此引擎对应的处方将继承此值，该值将作为处方的名称显示在UI中。 |
| `description` | 引擎的可选说明。 与此引擎对应的处方将继承此值，该值将在UI中作为处方的说明显示。 此属性是必需的。如果不想提供说明，请将其值设置为空字符串。 |
| `type` | 引擎的执行类型。 此值与在“PySpark”上构建Docker图像的语言相对应。 |
| `mlLibrary` | 为PySpark和Scala菜谱创建引擎时需要的字段。 |
| `artifacts.default.image.location` | 由Docker URL链接到的Docker图像的位置。 |
| `artifacts.default.image.executionType` | 引擎的执行类型。 此值与在“Spark”上构建Docker图像的语言相对应。 |

**请求Scala**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
    "name": "Spark retail sales recipe",
    "description": "A description for this Engine",
    "type": "Spark",
    "mlLibrary":"databricks-spark",
    "artifacts": {
        "default": {
            "image": {
                "name": "modelspark",
                "executionType": "Spark",
                "packagingType": "docker",
                "location": "v1d2cs4mimnlttw.azurecr.io/sarunbatchtest:0.0.1"
            }
        }
    }
}'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 引擎的所需名称。 与此引擎对应的处方将继承此值，该值将作为处方的名称显示在UI中。 |
| `description` | 引擎的可选说明。 与此引擎对应的处方将继承此值，该值将在UI中作为处方的说明显示。 此属性是必需的。如果不想提供说明，请将其值设置为空字符串。 |
| `type` | 引擎的执行类型。 此值与在“Spark”上构建Docker图像的语言相对应。 |
| `mlLibrary` | 为PySpark和Scala菜谱创建引擎时需要的字段。 |
| `artifacts.default.image.location` | 由Docker URL链接到的Docker图像的位置。 |
| `artifacts.default.image.executionType` | 引擎的执行类型。 此值与在“Spark”上构建Docker图像的语言相对应。 |

**响应**

成功的响应返回包含新创建引擎的详细信息(包括其唯一标识符(`id`))的有效负荷。 以下示例响应针对[!DNL Python]引擎。 `executionType`和`type`键根据提供的POST而改变。

```json
{
    "id": "{ENGINE_ID}",
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "Python",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "{DOCKER_URL}",
                "name": "An additional name for the Docker image",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

成功的响应会显示包含有关新创建引擎的信息的JSON有效负荷。 `id`键表示唯一的引擎标识符，在下一个教程中需要它来创建MLInstance。 确保在继续执行后续步骤之前保存引擎标识符。

## 后续步骤 {#next-steps}

您已使用API创建了引擎，并且作为响应主体的一部分获得了唯一的引擎标识符。 在下一个教程中，当您学习如何使用API](./train-evaluate-model-api.md)创建、培训和评估模型时，您可以使用此引擎标识符。[