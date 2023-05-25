---
keywords: Experience Platform；导入打包的脚本；Data Science Workspace；热门主题；脚本；API；Sensei机器学习；创建引擎
solution: Experience Platform
title: 使用Sensei机器学习API导入打包的方法
type: Tutorial
description: 本教程使用Sensei机器学习API创建引擎，在用户界面中也称为“方法”。
exl-id: c8dde30b-5234-448d-a597-f1c8d32f23d4
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 2%

---

# 使用Sensei机器学习API导入包装好的方法

本教程使用 [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) 创建 [引擎](../api/engines.md)，在用户界面中又称为“方法” 。

在开始之前，请务必注意Adobe Experience Platform [!DNL Data Science Workspace] 使用不同的术语来引用API和UI中的类似元素。 在本教程中使用API术语，下表概述了相关术语：

| UI术语 | API术语 |
| ---- | ---- |
| 方法 | [引擎](../api/engines.md) |
| 模型 | [MLInstance](../api/mlinstances.md) |
| 培训和评价 | [试验](../api/experiments.md) |
| 服务 | [MLService](../api/mlservices.md) |

引擎包含用于解决特定问题的机器学习算法和逻辑。 下图提供了一个可视化图表，其中显示了 [!DNL Data Science Workspace]. 本教程侧重于创建引擎，即机器学习模型的大脑。

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## 快速入门

本教程需要一个格式为Docker URL的打包“方法”文件。 请遵循 [将源文件打包到方法中](./package-source-files-recipe.md) 本教程介绍如何创建打包的“方法”文件或提供您自己的文件。

- `{DOCKER_URL}`：智能服务的Docker图像的URL地址。

本教程要求您已完成 [Adobe Experience Platform身份验证教程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功调用 [!DNL Platform] API。 完成身份验证教程将提供所有中所有所需标头的值 [!DNL Experience Platform] API调用，如下所示：

- `{ACCESS_TOKEN}`：在身份验证后提供的特定持有者令牌值。
- `{ORG_ID}`：在独特的Adobe Experience Platform集成中找到您的组织凭据。
- `{API_KEY}`：在独特的Adobe Experience Platform集成中找到的特定API密钥值。

## 创建引擎

可以通过向/engines端点发出POST请求来创建引擎。 已创建的引擎是根据必须作为API请求的一部分包含的已打包方法文件的形式配置的。

### 创建具有Docker URL的引擎 {#create-an-engine-with-a-docker-url}

要使用存储在Docker容器中的打包的配方文件创建引擎，您必须为打包的配方文件提供Docker URL。

>[!CAUTION]
>
> 如果您使用 [!DNL Python] 或R使用下面的请求。 如果您使用的是PySpark或Scala，请使用位于Python/R示例下方的PySpark/Scala请求示例。

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `engine.name` | 所需的引擎名称。 与此引擎对应的方法将继承此值，以显示在中 [!DNL Data Science Workspace] 用户界面作为方法的名称。 |
| `engine.description` | 引擎的可选描述。 与此引擎对应的方法将继承此值，以显示在中 [!DNL Data Science Workspace] 用户界面作为方法的描述。 不要删除此属性，如果您选择不提供描述，请将此值设置为空字符串。 |
| `engine.type` | 引擎的执行类型。 该值对应于在其中开发Docker图像的语言。 当提供Docker URL以创建引擎时， `type` 是 `Python`， `R`， `PySpark`， `Spark` (Scala)，或 `Tensorflow`. |
| `artifacts.default.image.location` | 您的 `{DOCKER_URL}` 此处显示。 完整的Docker URL具有以下结构： `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Docker图像文件的附加名称。 不要删除此属性，如果您选择不提供其他Docker图像文件名，请将此值设置为空字符串。 |
| `artifacts.default.image.executionType` | 此引擎的执行类型。 该值对应于在其中开发Docker图像的语言。 当提供Docker URL以创建引擎时， `executionType` 是 `Python`， `R`， `PySpark`， `Spark` (Scala)，或 `Tensorflow`. |

**请求PySpark**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | 所需的引擎名称。 与此引擎对应的方法将继承此值，该值将作为方法的名称显示在UI中。 |
| `description` | 引擎的可选描述。 与此引擎对应的方法将继承此值，以作为方法的描述显示在UI中。 此属性是必需的。如果不希望提供描述，请将其值设置为空字符串。 |
| `type` | 引擎的执行类型。 此值对应于在“PySpark”上构建Docker图像的语言。 |
| `mlLibrary` | 为PySpark和Scala配方创建引擎时所需的字段。 |
| `artifacts.default.image.location` | 通过Docker URL链接到的Docker图像的位置。 |
| `artifacts.default.image.executionType` | 引擎的执行类型。 此值对应于在“Spark”上构建Docker图像的语言。 |

**请求Scale**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | 所需的引擎名称。 与此引擎对应的方法将继承此值，该值将作为方法的名称显示在UI中。 |
| `description` | 引擎的可选描述。 与此引擎对应的方法将继承此值，以作为方法的描述显示在UI中。 此属性是必需的。如果不希望提供描述，请将其值设置为空字符串。 |
| `type` | 引擎的执行类型。 此值对应于在“Spark”上构建Docker图像的语言。 |
| `mlLibrary` | 为PySpark和Scala配方创建引擎时所需的字段。 |
| `artifacts.default.image.location` | 通过Docker URL链接到的Docker图像的位置。 |
| `artifacts.default.image.executionType` | 引擎的执行类型。 此值对应于在“Spark”上构建Docker图像的语言。 |

**响应**

成功响应将返回包含新创建引擎的详细信息的有效负载，包括其唯一标识符(`id`)。 以下示例响应适用于 [!DNL Python] 引擎。 此 `executionType` 和 `type` 键会根据提供的POST而更改。

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

成功的响应会显示包含有关新创建引擎的信息的JSON有效负载。 此 `id` key表示唯一引擎标识符，在下一个教程中需要它来创建MLInstance。 在继续后续步骤之前，请确保已保存引擎标识符。

## 后续步骤 {#next-steps}

您已使用API创建了一个引擎，并且获取了唯一的引擎标识符作为响应正文的一部分。 了解如何使用此引擎标识符后，您可以在下一个教程中使用它 [使用API创建、训练和评估模型](./train-evaluate-model-api.md).
