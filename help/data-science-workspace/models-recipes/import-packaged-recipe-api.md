---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: 导入打包的菜谱(API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 2%

---


# 导入打包的菜谱(API)

本教程使 [用[!DNL Sensei机器学](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) 习API] [创建引](../api/engines.md)擎，在用户界面中也称为菜谱。

在入门之前，请务必注意，Adobe Experience Platform [!DNL Data Science Workspace] 使用不同的术语来指代API和UI中的类似元素。 本教程中使用API术语，下表概述了相关术语：

| UI术语 | API术语 |
| ---- | ---- |
| 菜谱 | [引擎](../api/engines.md) |
| 模型 | [MLInstance](../api/mlinstances.md) |
| 培训和评估 | [实验](../api/experiments.md) |
| 服务 | [MLService](../api/mlservices.md) |

引擎包含机器学习算法和逻辑来解决特定问题。 下图提供了一个可视化，显示中的API工作流程 [!DNL Data Science Workspace]。 本教程重点介绍如何创建引擎，即机器学习模型的大脑。

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## 入门指南

本教程需要以Docker URL形式打包的Recipe文件。 按照“ [将源文件打包到菜谱”教程](./package-source-files-recipe.md) ，创建打包的菜谱文件或提供您自己的菜谱文件。

- `{DOCKER_URL}`:智能服务的Docker映像的URL地址。

本教程要求您完成对Adobe Experience Platform [的身份验证教程](../../tutorials/authentication.md) ，以便成功调用 [!DNL Platform] API。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

- `{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。
- `{IMS_ORG}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。
- `{API_KEY}`:您在独特的Adobe Experience Platform集成中找到的特定API密钥值。

## 创建引擎

可以通过向/engine端点发出POST请求来创建引擎。 创建的引擎基于打包的处方文件的形式进行配置，该文件必须作为API请求的一部分提供。

### 使用Docker URL创建引擎 {#create-an-engine-with-a-docker-url}

要创建包含存储在Docker容器中的打包Recipe文件的引擎，您必须为打包Recipe文件提供Docker URL。

>[!CAUTION]
>
> 如果您使用或 [!DNL Python] 者R使用以下请求。 如果您使用PySpark或Scala，请使用位于Python/R示例下的PySpark/Scala请求示例。

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
| `engine.name` | 引擎的所需名称。 与此引擎对应的处方将继承此值，该值将作为处方 [!DNL Data Science Workspace] 的名称显示在用户界面中。 |
| `engine.description` | 引擎的可选说明。 与此引擎对应的处方将继承此值，该值将作为处方 [!DNL Data Science Workspace] 的说明显示在用户界面中。 请勿删除此属性，如果您选择不提供说明，则让此值为空字符串。 |
| `engine.type` | 引擎的执行类型。 此值与开发Docker图像所用的语言相对应。 当提供Docker URL以创建引擎时， `type` 该URL `Python`为、 `R`、 `PySpark`( `Spark` Scala)或 `Tensorflow`。 |
| `artifacts.default.image.location` | 你 `{DOCKER_URL}` 来这。 完整的Docker URL具有以下结构： `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Docker图像文件的附加名称。 请勿删除此属性，如果您选择不提供其他Docker图像文件名，则让此值为空字符串。 |
| `artifacts.default.image.executionType` | 此引擎的执行类型。 此值与开发Docker图像所用的语言相对应。 当提供Docker URL以创建引擎时， `executionType` 该URL `Python`为、 `R`、 `PySpark`( `Spark` Scala)或 `Tensorflow`。 |

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

成功的响应返回包含新创建引擎的详细信息(包括其唯一标识符(`id`))的有效负荷。 以下示例响应针对引 [!DNL Python] 擎。 根 `executionType` 据提 `type` 供的POST更改和键。

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

成功的响应会显示包含有关新创建引擎的信息的JSON有效负荷。 该 `id` 键表示唯一的引擎标识符，在下一个教程中需要该标识符才能创建MLInstance。 确保在继续执行后续步骤之前保存引擎标识符。

## 后续步骤 {#next-steps}

您已使用API创建了引擎，并且作为响应主体的一部分获得了唯一的引擎标识符。 在您学习如何使用API创建、培训和评估 [模型时，您可以在下一个教程中使用此引擎标识符](./train-evaluate-model-api.md)。