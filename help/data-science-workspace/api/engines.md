---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics;engines;sensei machine learning api
solution: Experience Platform
title: 引擎
topic: Developer guide
description: 引擎是数据科学工作区中机器学习模型的基础。 它们包含机器学习算法，这些算法可解决特定问题、用于执行特征工程的特征管道，或同时解决这两个问题。
translation-type: tm+mt
source-git-commit: 6e4a3ebe84c82790f58f8ec54e6f72c2aca0b7da
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 3%

---


# 引擎

引擎是数据科学工作区中机器学习模型的基础。 它们包含机器学习算法，这些算法可解决特定问题、用于执行特征工程的特征管道，或同时解决这两个问题。

## 查找Docker注册表

>[!TIP]
>
>如果您没有Docker URL，请访 [问将源文件打包到菜谱教程](../models-recipes/package-source-files-recipe.md) ，以逐步演练创建Docker主机URL。

要上传打包的Recipe文件（包括您的Docker主机URL、用户名和密码），需要您的Docker注册表凭据。 您可以通过执行以下GET请求来查找此信息：

**API格式**

```https
GET /engines/dockerRegistry
```

**请求**

```shell
curl -X GET https://platform.adobe.io/data/sensei/engines/dockerRegistry \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回一个有效负荷，其中包含Docker注册表的详细信息，`host`包括Docker URL()、用`username`户名()和密码(`password`)。

>[!NOTE]
>
>每次更新Docker密码时， `{ACCESS_TOKEN}` 密码都会更改。

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## 使用Docker URL创建引擎 {#docker-image}

您可以通过执行POST请求来创建引擎，同时提供其元数据和在多部件表单中引用Docker图像的Docker URL。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | 引擎的所需名称。 与此引擎对应的处方将继承此值，该值将作为处方的名称显示在UI中。 |
| `description` | 引擎的可选说明。 与此引擎对应的处方将继承此值，该值将在UI中作为处方的说明显示。 此属性是必需的。如果不想提供说明，请将其值设置为空字符串。 |
| `type` | 引擎的执行类型。 此值与Docker图像所基于的语言相对应，可以是“Python”、“R”或“Tensorflow”。 |
| `algorithm` | 指定机器学习算法类型的字符串。 支持的算法类型包括“分类”、“回归”或“自定义”。 |
| `artifacts.default.image.location` | 由Docker URL链接到的Docker图像的位置。 |
| `artifacts.default.image.executionType` | 引擎的执行类型。 此值与Docker图像所基于的语言相对应，可以是“Python”、“R”或“Tensorflow”。 |

**请求PySpark/Scala**

请求PySpark菜谱时， `executionType` 和 `type` 为“PySpark”。 请求Scala菜谱时， `executionType` 和 `type` 是“Spark”。 以下Scala菜谱示例使用Spark:

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
| `type` | 引擎的执行类型。 此值与Docker图像所基于的语言相对应。 该值可设置为Spark或PySpark。 |
| `mlLibrary` | 为PySpark和Scala菜谱创建引擎时需要的字段。 此字段必须设置为 `databricks-spark`。 |
| `artifacts.default.image.location` | Docker图像的位置。 仅支持Azure ACR或Public（未验证）Dockerhub。 |
| `artifacts.default.image.executionType` | 引擎的执行类型。 此值与Docker图像所基于的语言相对应。 这可以是“Spark”或“PySpark”。 |

**响应**

成功的响应返回包含新创建引擎的详细信息(包括其唯一标识符(`id`))的有效负荷。 以下示例响应针对Python引擎。 所有引擎响应都采用以下格式：

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

您可以通过执行POST请求来创建功能管道引擎，同时提供其元数据和引用Docker图像的Docker URL。

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
| `type` | 引擎的执行类型。 此值与Docker图像所基于的语言相对应。 该值可设置为Spark或PySpark。 |
| `algorithm` | 使用的算法，将此值设置为( `fp` 特征管线)。 |
| `name` | 特征管道引擎的所需名称。 与此引擎对应的处方将继承此值，该值将作为处方的名称显示在UI中。 |
| `description` | 引擎的可选说明。 与此引擎对应的处方将继承此值，该值将在UI中作为处方的说明显示。 此属性是必需的。如果不想提供说明，请将其值设置为空字符串。 |
| `mlLibrary` | 为PySpark和Scala菜谱创建引擎时需要的字段。 此字段必须设置为 `databricks-spark`。 |
| `artifacts.default.image.location` | Docker图像的位置。 仅支持Azure ACR或Public（未验证）Dockerhub。 |
| `artifacts.default.image.executionType` | 引擎的执行类型。 此值与Docker图像所基于的语言相对应。 这可以是“Spark”或“PySpark”。 |
| `artifacts.default.image.packagingType` | 引擎的打包类型。 此值应设置为 `docker`。 |
| `artifacts.default.defaultMLInstanceConfigs` | 您的 `pipeline.json` 配置文件参数。 |

**响应**

成功的响应返回包含新创建的功能管道引擎的详细信息(包括其唯一标识符(`id`))的有效负荷。 以下示例响应针对PySpark功能管道引擎。

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

您可以通过执行单个列表请求来检索引擎GET。 要帮助筛选结果，您可以在请求路径中指定查询参数。 有关可用查询的列表，请参阅附录部分中有关资产检 [索查询参数的部分](./appendix.md#query)。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回引擎列表及其详细信息。

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

您可以通过执行GET请求来检索特定引擎的详细信息，该请求在请求路径中包含所需引擎的ID。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回包含所需引擎详细信息的有效负荷。

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

您可以通过以下方式修改和更新现有引擎：通过在请求路径中包含PUT引擎ID的目标请求覆盖其属性，并提供包含已更新属性的JSON有效负荷。

>[!NOTE]
>
>为确保此PUT请求成功，建议您首先执行GET请求，以 [按ID检索引擎](#retrieve-specific)。 然后，修改并更新返回的JSON对象，并应用已修改的JSON对象的整个作为PUT请求的有效负荷。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的响应会返回包含引擎更新的详细信息的有效负荷。

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

您可以通过执行DELETE请求来删除引擎，同时在请求路径中指定目标引擎的ID。 删除引擎将级联删除引用该引擎的所有MLI实例，包括属于这些MLI实例的任何实验和实验运行。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
