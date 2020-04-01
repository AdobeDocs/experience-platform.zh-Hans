---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: 引擎
topic: Developer guide
translation-type: tm+mt
source-git-commit: 01cfbc86516a05df36714b8c91666983f7a1b0e8

---


# 引擎

引擎是数据科学工作区中机器学习模型的基础。 它们包含机器学习算法，这些算法可解决特定问题、通过特征管道执行特征工程或同时执行两者。

## 查找Docker注册表

要上传打包的Recipe文件（包括Docker主机URL、用户名和密码），需要您的Docker注册表凭据。 您可以通过执行以下GET请求来查找此信息：

**API格式**

```http
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

成功的响应会返回一个有效负荷，其中包含Docker注册表的详细信息，包括Docker URL(`host`)、用户名(`username`)和密码(`password`)。

>[!NOTE] 更新后，Docker密码会 `{ACCESS_TOKEN}` 更改。

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## 使用Docker URL创建引擎

您可以通过执行POST请求来创建引擎，同时提供其元数据和引用多部分表单中Docker图像的Docker URL。

**API格式**

```http
POST /engines
```

**请求**

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
                    "location": "{DOCKER_URL}",
                    "name": "An additional name for the Docker image",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| 属性 | 描述 |
| --- | --- |
| `name` | 引擎的所需名称。 与此引擎对应的菜谱将继承此值，该值将作为菜谱的名称显示在UI中。 |
| `description` | 引擎的可选说明。 与此引擎对应的菜谱将继承此值，该值将作为菜谱的说明显示在UI中。 此属性是必需的。如果不想提供说明，请将其值设置为空字符串。 |
| `type` | 引擎的执行类型。 此值与Docker图像所基于的语言相对应，可以是“Python”、“R”或“Tensorflow”。 |
| `algorithm` | 指定机器学习算法类型的字符串。 支持的算法类型包括“分类”、“回归”或“自定义”。 |
| `artifacts.default.image.location` | 由Docker URL链接到的Docker图像的位置。 |
| `artifacts.default.image.executionType` | 引擎的执行类型。 此值与Docker图像所基于的语言相对应，可以是“Python”、“R”或“Tensorflow”。 |


**响应**

成功的响应返回包含新创建引擎的详细信息(包括其唯一标识符(`id`))的有效负荷。

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

## 使用二进制伪像创建引擎

您可以通过执行POST请求来创建使用本 `.jar``.egg` 地或二进制伪像的引擎，同时以多部分形式提供其元数据和伪像的路径。

**API格式**

```http
POST /engines
```

**请求**

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
        "algorithm": "Classification",
        "type": "PySpark",
    }' \
    -F 'defaultArtifact=@path/to/binary/artifact/file.egg'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 引擎的所需名称。 与此引擎对应的菜谱将继承此值，该值将作为菜谱的名称显示在UI中。 |
| `description` | 引擎的可选说明。 与此引擎对应的菜谱将继承此值，该值将作为菜谱的说明显示在UI中。 此属性是必需的。如果不想提供说明，请将其值设置为空字符串。 |
| `algorithm` | 指定机器学习算法类型的字符串。 支持的算法类型包括“分类”、“回归”或“自定义”。 |
| `type` | 引擎的执行类型。 此值对应于构建二进制伪像的语言，可以是“PySpark”或“Spark”。 |


**响应**

成功的响应返回包含新创建引擎的详细信息(包括其唯一标识符(`id`))的有效负荷。

```json
{
    "id": "{ENGINE_ID}",
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
                "location": "wasbs://artifact-location.blob.core.windows.net/Engine_ID/default.egg",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

## 使用二进制伪像创建功能管道引擎

您可以通过执行POST请求来使用本地或二进制 `.jar``.egg` 伪像创建功能管道引擎，同时以多部分形式提供其元数据和伪像的路径。 PySpark或Spark Engine能够指定计算资源，如内核数或内存量。 有关详细信息，请参阅 [PySpark和Spark资源配置的附录部分](./appendix.md#resource-config) 。

**API格式**

```http
POST /engines
```

**请求**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
        "name": "Feature Pipeline Engine",
        "description": "A feature pipeline Engine",
        "algorithm":"fp",
        "type": "PySpark"
    }' \
    -F 'featurePipelineOverrideArtifact=@path/to/binary/artifact/feature_pipeline.egg' \
    -F 'defaultArtifact=@path/to/binary/artifact/feature_pipeline.egg'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 引擎的所需名称。 与此引擎对应的菜谱将继承此值，该值将作为菜谱的名称显示在UI中。 |
| `description` | 引擎的可选说明。 与此引擎对应的菜谱将继承此值，该值将作为菜谱的说明显示在UI中。 此属性是必需的。如果不想提供说明，请将其值设置为空字符串。 |
| `algorithm` | 指定机器学习算法类型的字符串。 将此值设置为“fp”，以将此创建指定为“特征管道引擎”。 |
| `type` | 引擎的执行类型。 此值对应于构建二进制伪像的语言，可以是“PySpark”或“Spark”。 |

**响应**

成功的响应返回包含新创建引擎的详细信息(包括其唯一标识符(`id`))的有效负荷。

```json
{
    "id": "{ENGINE_ID}",
    "name": "Feature Pipeline Engine",
    "description": "A feature pipeline Engine",
    "type": "PySpark",
    "algorithm": "fp",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "wasbs://artifact-location.blob.core.windows.net/Engine_ID/default.egg",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

## 检索引擎列表

您可以通过执行单个GET请求来检索引擎列表。 要帮助筛选结果，您可以在请求路径中指定查询参数。 有关可用查询的列表，请参阅有关资产检索的查询参 [数的附录部分](./appendix.md#query)。

**API格式**

```http
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

成功的响应会返回引擎及其详细信息的列表。

```json
{
    "children": [
        {
            "id": "{ENGINE_ID}",
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
            "id": "{ENGINE_ID}",
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
            "id": "{ENGINE_ID}",
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

```http
GET /engines/{ENGINE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{ENGINE_ID}` | 现有引擎的ID。 |

**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回包含所需引擎详细信息的有效负荷。

```json
{
    "id": "{ENGINE_ID}",
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
                "location": "wasbs://artifact-location.blob.core.windows.net/{ENGINE_ID}/default.egg",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

## 更新引擎

您可以通过以下方式修改和更新现有引擎：通过PUT请求覆盖其属性，该请求在请求路径中包含目标引擎的ID，并提供包含已更新属性的JSON有效负荷。

>[!NOTE] 为确保此PUT请求成功，建议首先执行GET请求以按ID [检索引擎](#retrieve-specific)。 然后，修改并更新返回的JSON对象，并应用修改后的JSON对象的整个作为PUT请求的有效负荷。

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

```http
PUT /engines/{ENGINE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{ENGINE_ID}` | 现有引擎的ID。 |

**请求**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
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
    "id": "{ENGINE_ID}",
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

您可以通过执行DELETE请求来删除引擎，同时在请求路径中指定目标引擎的ID。 删除引擎将级联删除引用该引擎的所有MLI实例，包括属于这些MLI实例的任何“实验”和“实验”运行。

**API格式**

```http
DELETE /engines/{ENGINE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{ENGINE_ID}` | 现有引擎的ID。 |

**请求**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
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
