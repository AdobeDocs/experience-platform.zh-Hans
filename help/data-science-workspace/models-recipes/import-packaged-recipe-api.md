---
keywords: Experience Platform；导入打包的方法；Data Science Workspace；热门主题；方法；API；感生机器学习；创建引擎
solution: Experience Platform
title: 使用Sensei机器学习API导入打包的方法
type: Tutorial
description: 本教程使用Sensei机器学习API创建引擎，也称为用户界面中的方法。
exl-id: c8dde30b-5234-448d-a597-f1c8d32f23d4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 2%

---

# 使用Sensei机器学习API导入打包的方法

本教程使用 [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) 创建 [引擎](../api/engines.md)，在用户界面中也称为方法。

在开始之前，请务必注意，Adobe Experience Platform [!DNL Data Science Workspace] 使用不同的术语来指代API和UI中的类似元素。 本教程中将使用API术语，下表概述了相关术语：

| UI术语 | API术语 |
| ---- | ---- |
| 方法 | [引擎](../api/engines.md) |
| 模型 | [MLInstance](../api/mlinstances.md) |
| 培训和评价 | [试验](../api/experiments.md) |
| 服务 | [MLService](../api/mlservices.md) |

引擎包含机器学习算法和逻辑以解决特定问题。 下图提供了一个可视化图表，其中显示了 [!DNL Data Science Workspace]. 本教程重点介绍如何创建引擎，即机器学习模型的大脑。

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## 快速入门

本教程需要以Docker URL形式打包的方法文件。 关注 [将源文件打包到方法中](./package-source-files-recipe.md) 教程创建打包的方法文件或提供您自己的方法文件。

- `{DOCKER_URL}`:智能服务的Docker图像的URL地址。

本教程要求您完成 [Adobe Experience Platform身份验证教程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功调用 [!DNL Platform] API。 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

- `{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。
- `{ORG_ID}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。
- `{API_KEY}`:您在独特的Adobe Experience Platform集成中找到的特定API密钥值。

## 创建引擎

可通过向/engines端点发出POST请求来创建引擎。 创建的引擎基于打包的处方文件的形式进行配置，该文件必须作为API请求的一部分包含在内。

### 使用Docker URL创建引擎 {#create-an-engine-with-a-docker-url}

要创建引擎，并将打包的处方文件存储在Docker容器中，您必须向打包的处方文件提供Docker URL。

>[!CAUTION]
>
> 如果您使用 [!DNL Python] 或者使用下面的请求。 如果您使用PySpark或Scala，请使用位于Python/R示例下方的PySpark/Scala请求示例。

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
| `engine.name` | 引擎的所需名称。 与此引擎对应的处方将继承此值，该值将显示在 [!DNL Data Science Workspace] 用户界面作为方法的名称。 |
| `engine.description` | 引擎的可选描述。 与此引擎对应的处方将继承此值，该值将显示在 [!DNL Data Science Workspace] 用户界面。 请勿删除此属性，如果您选择不提供描述，则允许此值为空字符串。 |
| `engine.type` | 引擎的执行类型。 此值对应于在中开发Docker图像的语言。 提供Docker URL以创建引擎时， `type` 是 `Python`, `R`, `PySpark`, `Spark` (Scala)或 `Tensorflow`. |
| `artifacts.default.image.location` | 您的 `{DOCKER_URL}` 到这里。 完整的Docker URL具有以下结构： `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Docker图像文件的附加名称。 请勿删除此属性，如果您选择不提供附加的Docker图像文件名，则允许此值为空字符串。 |
| `artifacts.default.image.executionType` | 此引擎的执行类型。 此值对应于在中开发Docker图像的语言。 提供Docker URL以创建引擎时， `executionType` 是 `Python`, `R`, `PySpark`, `Spark` (Scala)或 `Tensorflow`. |

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
| `name` | 引擎的所需名称。 与此引擎对应的处方将继承此值，该值将作为处方的名称显示在UI中。 |
| `description` | 引擎的可选描述。 与此引擎对应的处方将继承此值，该值将作为处方的说明显示在UI中。 此属性是必需的。如果不想提供描述，请将其值设置为空字符串。 |
| `type` | 引擎的执行类型。 此值对应于在“PySpark”上构建Docker图像的语言。 |
| `mlLibrary` | 为PySpark和Scala配方创建引擎时所需的字段。 |
| `artifacts.default.image.location` | 由Docker URL链接到的Docker图像的位置。 |
| `artifacts.default.image.executionType` | 引擎的执行类型。 此值对应于在“Spark”上构建Docker图像的语言。 |

**请求Scala**

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
| `name` | 引擎的所需名称。 与此引擎对应的处方将继承此值，该值将作为处方的名称显示在UI中。 |
| `description` | 引擎的可选描述。 与此引擎对应的处方将继承此值，该值将作为处方的说明显示在UI中。 此属性是必需的。如果不想提供描述，请将其值设置为空字符串。 |
| `type` | 引擎的执行类型。 此值对应于在“Spark”上构建Docker图像的语言。 |
| `mlLibrary` | 为PySpark和Scala配方创建引擎时所需的字段。 |
| `artifacts.default.image.location` | 由Docker URL链接到的Docker图像的位置。 |
| `artifacts.default.image.executionType` | 引擎的执行类型。 此值对应于在“Spark”上构建Docker图像的语言。 |

**响应**

成功响应会返回一个有效负载，其中包含新创建引擎的详细信息，包括其唯一标识符(`id`)。 以下示例响应针对 [!DNL Python] 引擎。 的 `executionType` 和 `type` 键值会根据提供的POST而发生更改。

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

成功响应会显示包含有关新创建引擎的信息的JSON有效负载。 的 `id` 键表示唯一的引擎标识符，在下一个教程中需要此键才能创建MLInstance。 在继续执行后续步骤之前，请确保已保存引擎标识符。

## 后续步骤 {#next-steps}

您已使用API创建引擎，并且获取了作为响应主体一部分的唯一引擎标识符。 在下一个教程中，您可以在了解如何使用此引擎标识符 [使用API创建、训练和评估模型](./train-evaluate-model-api.md).
