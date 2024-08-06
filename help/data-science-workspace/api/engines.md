---
keywords: Experience Platform；开发人员指南；端点；Data Science Workspace；热门主题；引擎；sensei机器学习api
solution: Experience Platform
title: 引擎API终结点
description: 引擎是数据科学工作区中机器学习模型的基础。 它们包含可解决特定问题的机器学习算法、用于执行特征工程的特征管道，或两者兼有。
role: Developer
exl-id: 7c670abd-636c-47d8-bd8c-5ce0965ce82f
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 2%

---

# 引擎终结点

>[!NOTE]
>
>Data Science Workspace不再可购买。
>
>本文档适用于先前有权使用Data Science Workspace的现有客户。

引擎是数据科学工作区中机器学习模型的基础。 它们包含可解决特定问题的机器学习算法、用于执行特征工程的特征管道，或两者兼有。

## 查找Docker注册表

>[!TIP]
>
>如果您没有Docker URL，请访问[将源文件打包成配方](../models-recipes/package-source-files-recipe.md)教程，以了解创建Docker主机URL的分步演练。

需要提供Docker注册表凭据才能上传打包的配方文件，包括Docker主机URL、用户名和密码。 您可以通过执行以下GET请求来查找此信息：

**API格式**

```https
GET /engines/dockerRegistry
```

**请求**

```shell
curl -X GET https://platform.adobe.io/data/sensei/engines/dockerRegistry \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回包含Docker注册表详细信息(包括Docker URL (`host`)、用户名(`username`)和密码(`password`))的有效负载。

>[!NOTE]
>
>更新您的`{ACCESS_TOKEN}`后，您的Docker密码即会更改。

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## 使用Docker URL创建引擎 {#docker-image}

通过在提供引擎元数据和以多部分形式引用Docker图像的Docker URL时执行POST请求，可以创建引擎。

**API格式**

```https
POST /engines
```

**请求Python/R**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
        "name": "A name for this Engine",
        "description": "A description for this Engine",
        "type": "Python",
        "algorithm": "Classification",
        "artifacts": {
            "default": {
                "image": {
                    "location": "v1rsvj32smc4wbs.azurecr.io/ml-featurepipeline-pyspark:1.0",
                    "name": "An additional name for the Docker image",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| 属性 | 描述 |
| --- | --- |
| `name` | 引擎所需的名称。 与此引擎对应的方法将继承此值，以方法名称的形式显示在UI中。 |
| `description` | 引擎的可选描述。 与此引擎对应的方法将继承此值，以作为方法的描述显示在UI中。 此属性是必需的。 如果您不想提供描述，请将其值设置为空字符串。 |
| `type` | 引擎的执行类型。 此值对应于构建Docker图像时所用的语言，可以是“Python”、“R”或“Tensorflow”。 |
| `algorithm` | 一个字符串，它指定机器学习算法的类型。 支持的算法类型包括“分类”、“回归”或“自定义”。 |
| `artifacts.default.image.location` | Docker URL链接到的Docker图像的位置。 |
| `artifacts.default.image.executionType` | 引擎的执行类型。 此值对应于构建Docker图像时所用的语言，可以是“Python”、“R”或“Tensorflow”。 |

**请求PySpark/Scala**

在请求PySpark配方时，`executionType`和`type`是“PySpark”。 在请求Scala配方时，`executionType`和`type`是“Spark”。 以下Scala配方示例使用Spark：

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
| `name` | 引擎所需的名称。 与此引擎对应的处方将继承此值，以作为处方名称显示在UI中。 |
| `description` | 引擎的可选说明。 与此引擎对应的处方将继承此值，以作为处方说明显示在UI中。 此属性为必填。 如果您不想提供描述，请将其值设置为空字符串。 |
| `type` | 引擎的执行类型。 此值对应于构建Docker图像所使用的语言。 值可以设置为Spark或PySpark。 |
| `mlLibrary` | 为PySpark和Scala配方创建引擎时所需的字段。 此字段必须设置为`databricks-spark`。 |
| `artifacts.default.image.location` | Docker图像的位置。 仅支持Azure ACR或Public （未经过身份验证的） Dockerhub。 |
| `artifacts.default.image.executionType` | 引擎的执行类型。 此值对应于构建Docker图像所使用的语言。 这可以是“Spark”或“PySpark”。 |

**响应**

成功的响应将返回一个负载，其中包含新创建的引擎的详细信息，包括其唯一标识符(`id`)。 以下示例响应适用于Python引擎。 所有引擎响应均遵循以下格式：

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
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
                "location": "v1rsvj32smc4wbs.azurecr.io/ml-featurepipeline-pyspark:1.0",
                "name": "An additional name for the Docker image",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## 使用Docker URL创建功能管道引擎 {#feature-pipeline-docker}

通过在提供功能管道引擎的元数据和引用Docker图像的Docker URL时执行POST请求，可以创建功能管道引擎。

**API格式**

```https
POST /engines
```

**请求**

```shell
curl -X POST \
 https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer ' \
    -H 'x-gw-ims-org-id: 20655D0F5B9875B20A495E23@AdobeOrg' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=engine.v1.json' \
    -H 'x-api-key: acp_foundation_machineLearning' \
    -H 'Content-Type: text/plain' \
    -F '{
    "type": "PySpark",
    "algorithm":"fp",
    "name": "Feature_Pipeline_Engine",
    "description": "Feature_Pipeline_Engine",
    "mlLibrary": "databricks-spark",
    "artifacts": {
       "default": {
           "image": {
                "location": "v7d1cs2mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "datatransformation",
                "executionType": "PySpark",
                "packagingType": "docker"
            },
           "defaultMLInstanceConfigs": [ ...
           ]
       }
   }
}'
```

| 属性 | 描述 |
| --- | --- |
| `type` | 引擎的执行类型。 此值对应于构建Docker图像所使用的语言。 值可以设置为Spark或PySpark。 |
| `algorithm` | 正在使用的算法，将此值设置为`fp`（功能管道）。 |
| `name` | 特征管线引擎所需的名称。 与此引擎对应的处方将继承此值，以作为处方名称显示在UI中。 |
| `description` | 引擎的可选说明。 与此引擎对应的处方将继承此值，以作为处方说明显示在UI中。 此属性为必填。 如果您不想提供描述，请将其值设置为空字符串。 |
| `mlLibrary` | 为PySpark和Scala配方创建引擎时所需的字段。 此字段必须设置为`databricks-spark`。 |
| `artifacts.default.image.location` | Docker图像的位置。 仅支持Azure ACR或Public （未经过身份验证的） Dockerhub。 |
| `artifacts.default.image.executionType` | 引擎的执行类型。 此值对应于构建Docker图像所使用的语言。 这可以是“Spark”或“PySpark”。 |
| `artifacts.default.image.packagingType` | 引擎的包装类型。 此值应设置为`docker`。 |
| `artifacts.default.defaultMLInstanceConfigs` | 您的`pipeline.json`配置文件参数。 |

**响应**

成功的响应将返回一个有效负载，其中包含新创建的功能管道引擎的详细信息，包括其唯一标识符(`id`)。 以下示例响应适用于PySpark功能管道引擎。

```json
{
    "id": "88236891-4309-4fd9-acd0-3de7827cecd1",
    "name": "Feature_Pipeline_Engine",
    "description": "Feature_Pipeline_Engine",
    "type": "PySpark",
    "algorithm": "fp",
    "mlLibrary": "databricks-spark",
    "created": "2020-04-24T20:46:58.382Z",
    "updated": "2020-04-24T20:46:58.382Z",
    "deprecated": false,
    "artifacts": {
        "default": {
            "image": {
                "location": "v7d1cs3mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "datatransformation",
                "executionType": "PySpark",
                "packagingType": "docker"
            },
        "defaultMLInstanceConfigs": [ ... ]
        }
    }
}
```

## 检索引擎列表

您可以通过执行单个GET请求来检索引擎列表。 要帮助筛选结果，您可以在请求路径中指定查询参数。 有关可用查询的列表，请参阅[用于资源检索的查询参数](./appendix.md#query)的附录部分。

**API格式**

```https
GET /engines
GET /engines?parameter_1=value_1
GET /engines?parameter_1=value_1&parameter_2=value_2
```

**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回引擎及其详细信息的列表。

```json
{
    "children": [
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde31",
            "name": "A name for this Engine",
            "description": "A description for this Engine",
            "type": "PySpark",
            "algorithm": "Classification",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
            "name": "A name for this Engine",
            "description": "A description for this Engine",
            "type": "Python",
            "algorithm": "Classification",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde33",
            "name": "Feature Pipeline Engine",
            "description": "A feature pipeline Engine",
            "type": "PySpark",
            "algorithm":"fp",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "deleted==false",
        "totalCount": 100,
        "count": 3
    }
}
```

### 检索特定引擎 {#retrieve-specific}

您可以通过执行请求（请求路径中包含所需引擎的ID）来检索特定GET的详细信息。

**API格式**

```https
GET /engines/{ENGINE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{ENGINE_ID}` | 现有引擎的ID。 |

**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回包含所需引擎详细信息的有效负载。

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "PySpark",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "v7d1cs2mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "docker"
            }
        }
    }
}
```

## 更新引擎

您可以修改和更新现有引擎，方法是通过PUT请求（请求路径中包含目标引擎的ID）覆盖其属性，并提供包含已更新属性的JSON有效负载。

>[!NOTE]
>
>为确保此PUT请求成功，建议您首先执行GET请求，以[按ID](#retrieve-specific)检索引擎。 然后，修改并更新返回的JSON对象，并将修改后的JSON对象的整个内容应用为PUT请求的有效负载。

以下示例API调用将在最初具有这些属性时更新引擎的名称和说明：

```json
{
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "Python",
    "algorithm": "Classification",
    "artifacts": {
        "default": {
            "image": {
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

**API格式**

```https
PUT /engines/{ENGINE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{ENGINE_ID}` | 现有引擎的ID。 |

**请求**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=engine.v1.json' \
    -d '{
        "name": "An updated name for this Engine",
        "description": "An updated description",
        "type": "Python",
        "algorithm": "Classification",
        "artifacts": {
            "default": {
                "image": {
                    "executionType": "Python",
                    "packagingType": "docker"
                }
            }
        }
    }'
```

**响应**

成功的响应将返回包含引擎已更新详细信息的有效负载。

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "An updated name for this Engine",
    "description": "An updated description",
    "type": "Python",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## 删除引擎

通过在请求路径中指定DELETE引擎的ID时执行目标请求，可以删除引擎。 删除引擎将级联删除引用该引擎的所有MLInstances，包括属于这些MLInstances的所有试验和试验运行。

**API格式**

```https
DELETE /engines/{ENGINE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{ENGINE_ID}` | 现有引擎的ID。 |

**请求**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Engine deletion was successful"
}
```
