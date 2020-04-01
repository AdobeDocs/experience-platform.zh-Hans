---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: 导入打包的菜谱(API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 92dad525123d321e987de527ae6c7aab40b22bc4

---


# 导入打包的菜谱(API)

本教程使用 [Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) ，创建 [Engine](../api/engines.md)，也称为用户界面中的Recipe。

在入门之前，请务必注意，Adobe Experience Platform Data Science Workspace使用不同的术语来引用API和UI中的类似元素。 本教程中使用API术语，下表概述了相关术语：

| UI期限 | API期限 |
| ---- | ---- |
| 菜谱 | [引擎](../api/engines.md) |
| 模型 | [MLInstance](../api/mlinstances.md) |
| 培训和评估 | [实验](../api/experiments.md) |
| 服务 | [MLService](../api/mlservices.md) |

引擎包含机器学习算法和用于解决特定问题的逻辑。 下图提供了一个可视化，显示了Data Science Workspace中的API工作流程。 本教程侧重于创建引擎，即机器学习模型的大脑。

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## 入门指南

本教程需要以二进制对象或Docker URL形式打包的Recipe文件。 按照“ [将源文件打包到菜谱”教程](./package-source-files-recipe.md) ，创建打包的菜谱文件或提供您自己的菜谱文件。

- 二进制伪像：二进制伪像(例如 JAR, EGG)，用于创建引擎。
- `{DOCKER_URL}` :智能服务的Docker图像的URL地址。

本教程要求您完成Adobe [Experience Platform身份验证教程](../../tutorials/authentication.md) ，以便成功调用平台API。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

- `{ACCESS_TOKEN}`:身份验证后提供的特定承载令牌值。
- `{IMS_ORG}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。
- `{API_KEY}`:您在独特的Adobe Experience Platform集成中可找到特定API密钥价值。

## 创建引擎

根据打包的菜谱文件的形式（将作为API请求的一部分），通过以下两种方法之一创建引擎：
- [创建具有二进制伪像的引擎](#create-an-engine-with-a-binary-artifact)
- [使用Docker URL创建引擎](#create-an-engine-with-a-docker-url)

### 创建具有二进制伪像的引擎

要使用本地打包或二进制对象创建引擎， `.jar` 您必须提供 `.egg` 本地文件系统中二进制对象文件的绝对路径。 请考虑导航到在终端环境中包含二进制对象的目录，然后对绝对路径执行 `pwd` Unix命令。

以下调用使用二进制对象创建引擎：

#### API格式

```http
POST /engines
```

#### 请求

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -F 'engine={
        "name": "Retail Sales Engine PySpark",
        "description": "A description for Retail Sales Engine, this Engines execution type is PySpark",
        "type": "PySpark"
    }' \
    -F 'defaultArtifact=@path/to/binary/artifact/file/pysparkretailapp-0.1.0-py3.7.egg'
```

- `engine > name` :引擎的所需名称。 与此引擎对应的菜谱将继承此值，该值将作为菜谱的名称显示在Data Science Workspace用户界面中。
- `engine > description` :引擎的可选说明。 与此引擎对应的菜谱将继承此值，该值将作为菜谱的说明显示在Data Science Workspace用户界面中。 请勿删除此属性，如果您选择不提供说明，则让此值为空字符串。
- `engine > type`:引擎的执行类型。 此值与在其中开发二进制伪像的语言相对应。

   >[!NOTE] 上传二进制对象以创建引擎时， `type` 为 `Spark` 或 `PySpark`。

- `defaultArtifact` :用于创建引擎的二进制对象文件的绝对路径。

   >[!NOTE] 确保在文 `@` 件路径之前包含。

#### 响应

```JSON
{
    "id": "00000000-1111-2222-3333-abcdefghijkl",
    "name": "Retail Sales Engine PySpark",
    "description": "A description for Retail Sales Engine, this Engines execution type is PySpark",
    "type": "PySpark",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "your_user_id@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "wasbs://some-storage-location.net/some-path/your-uploaded-binary-artifact.egg",
                "name": "pysparkretailapp-0.1.0-py3.7.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

成功的响应会显示包含有关新创建引擎的信息的JSON有效负荷。 该 `id` 键表示唯一的引擎标识符，在下一个教程中需要该键来创建MLI实例。 确保在继续执行后续步骤之前保存引擎 [标识符](#next-steps)。

### 使用Docker URL创建引擎

要创建具有存储在Docker容器中的打包的Recipe文件的引擎，您必须为打包的Recipe文件提供Docker URL。

以下调用创建具有Docker URL的引擎：

#### API格式

```http
POST /engines
```

#### 请求

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

- `engine > name` :引擎的所需名称。 与此引擎对应的菜谱将继承此值，该值将作为菜谱的名称显示在Data Science Workspace用户界面中。
- `engine > description` :引擎的可选说明。 与此引擎对应的菜谱将继承此值，该值将作为菜谱的说明显示在Data Science Workspace用户界面中。 请勿删除此属性，如果您选择不提供说明，则让此值为空字符串。
- `engine > type`:引擎的执行类型。 此值与开发Docker图像所用的语言相对应。

   >[!NOTE] 提供Docker URL以创建引擎时， `type` 为 `Python`、 `R`或 `Tensorflow`。

- `artifacts > default > image > location` :你 `{DOCKER_URL}` 来这。 完整的Docker URL具有以下结构：

   ```
   your_docker_host.azurecr.io/docker_image_file:version
   ```

- `artifacts > default > image > name` :Docker图像文件的其他名称。 请勿删除此属性，如果您选择不提供其他Docker图像文件名，则让此值为空字符串。
- `artifacts > default > image > executionType` :此引擎的执行类型。 此值与开发Docker图像所用的语言相对应。

   >[!NOTE] 提供Docker URL以创建引擎时， `executionType` 为 `Python`、 `R`或 `Tensorflow`。

#### 响应

```JSON
{
    "id": "00000000-1111-2222-3333-abcdefghijkl",
    "name": "Retail Sales Engine Python",
    "description": "A description for Retail Sales Engine, this Engines execution type is Python",
    "type": "Python",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "your_user_id@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "{DOCKER_URL}",
                "name": "retail_sales_python",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

成功的响应会显示包含有关新创建引擎的信息的JSON有效负荷。 该 `id` 键表示唯一的引擎标识符，在下一个教程中需要该键来创建MLI实例。 确保在继续执行后续步骤之前保存引擎标识符。

## 后续步骤

您已使用API创建了引擎，并且作为响应体的一部分获得了唯一的引擎标识符。 在下一个教程中，您可以使用此引擎标识符，因为您将学习如 [何使用API创建、培训和评估模型](./train-evaluate-model-api.md)。