---
keywords: Experience Platform；开发人员指南；端点；Data Science Workspace；热门主题；实例；sensei机器学习api
solution: Experience Platform
title: MLInstances API终结点
description: MLInstance是现有引擎与定义任何培训参数、评分参数或硬件资源配置的适当配置集的配对。
role: Developer
exl-id: e78cda69-1ff9-47ce-b25d-915de4633e11
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 3%

---

# MLInstances终结点

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档适用于先前有权使用Data Science Workspace的现有客户。

MLInstance是现有[引擎](./engines.md)与定义任何培训参数、评分参数或硬件资源配置的适当配置集的配对。

## 创建MLInstance {#create-an-mlinstance}

通过在提供包含有效引擎ID (`{ENGINE_ID}`)和一组适当的默认配置的请求负载时执行POST请求，可以创建MLInstance。

如果引擎ID引用PySpark或Spark引擎，则您能够配置计算资源的数量，例如核心数量或内存量。 如果引用了Python引擎，则可以在使用CPU或GPU之间进行选择，以进行培训和评分。 请参阅附录中有关[PySpark和Spark资源配置](./appendix.md#resource-config)以及[Python CPU和GPU配置](./appendix.md#cpu-gpu-config)的部分以了解更多信息。

**API格式**

```http
POST /mlInstances
```

**请求**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -d '{
        "name": "A name for this MLInstance",
        "description": "A description for this MLInstance",
        "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
        "tasks": [
            {
                "name": "train",
                "parameters": [
                    {
                        "key": "training parameter",
                        "value": "parameter value"
                    }
                ]
            },
            {
                "name": "score",
                "parameters": [
                    {
                        "key": "scoring parameter",
                        "value": "parameter value"
                    }
                ]
            },
            {
                "name": "fp",
                "parameters": [
                    {
                        "key": "feature pipeline parameter",
                        "value": "parameter value"
                    }
                ]
            }
        ],
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | MLInstance所需的名称。 与此MLInstance对应的模型将继承此值，以作为模型的名称显示在UI中。 |
| `description` | MLInstance的可选描述。 与此MLInstance对应的模型将继承此值，以作为模型的描述显示在UI中。 此属性是必需的。 如果您不想提供描述，请将其值设置为空字符串。 |
| `engineId` | 现有引擎的ID。 |
| `tasks` | 用于训练、评分或功能管道的一组配置。 |

**响应**

成功响应将返回一个负载，其中包含新创建的MLInstance的详细信息，包括其唯一标识符(`id`)。

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "training parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoring parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "fp",
            "parameters": [
                {
                    "key": "feature pipeline parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## 检索MLInstances列表

可以通过执行单个GET请求来检索MLInstances的列表。 为帮助筛选结果，您可以在请求路径中指定查询参数。 有关可用查询的列表，请参阅[用于资源检索的查询参数](./appendix.md#query)的附录部分。

**API格式**

```http
GET /mlInstances
GET /mlInstances?{QUERY_PARAMETER}={VALUE}
GET /mlInstances?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 参数 | 描述 |
| --- | --- |
| `{QUERY_PARAMETER}` | 用于筛选结果的[可用查询参数](./appendix.md#query)之一。 |
| `{VALUE}` | 前面的查询参数的值。 |

**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回MLInstances列表及其详细信息。

```json
{
    "children": [
        {
            "id": "46986c8f-7739-4376-8509-0178bdf32cda",
            "name": "A name for this MLInstance",
            "description": "A description for this MLInstance",
            "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "56986c8f-7739-4376-8509-0178bdf32cda",
            "name": "Retail Sales Model",
            "description": "A Model created with the Retail Sales Recipe",
            "engineId": "32f4166f-85ba-4130-a995-a2b8e1edde32",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "deleted==false",
        "totalCount": 2,
        "count": 2
    }
}
```

## 检索特定MLInstance {#retrieve-specific}

通过执行GET请求，您可以检索特定MLInstance的详细信息，该请求路径中包含所需MLInstance的ID。

**API格式**

```http
GET /mlInstances/{MLINSTANCE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{MLINSTANCE_ID}` | 所需MLInstance的ID。 |

**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回MLInstance的详细信息。

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "training parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoring parameter",
                    "value": "parameter value"
                }
            ]
        },
        {
            "name": "featurePipeline",
            "parameters": [
                {
                    "key": "feature pipeline parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## 更新MLInstance

您可以更新现有MLInstance，方法是通过PUT请求覆盖其属性，该请求在请求路径中包含目标MLInstance的ID，并提供包含更新属性的JSON负载。

>[!TIP]
>
>为了确保此PUT请求成功，建议您首先执行[按ID](#retrieve-specific)检索MLInstance的GET请求。 然后，修改并更新返回的JSON对象，并将修改后的JSON对象的整个内容应用为PUT请求的有效负载。

以下示例API调用将在最初具有这些属性时更新MLInstance的训练和评分参数：

```json
{
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "00000000-0000-0000-0000-000000000000",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "learning_rate",
                    "value": "0.3"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "output_dataset_id",
                    "value": "output-dataset-000"
                }
            ]
        }
    ]
}
```

**API格式**

```http
PUT /mlInstances/{MLINSTANCE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{MLINSTANCE_ID}` | 有效的MLInstance ID。 |

**请求**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -d '{
        "name": "A name for this MLInstance",
        "description": "A description for this MLInstance",
        "engineId": "00000000-0000-0000-0000-000000000000",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "displayName": "Jane Doe",
            "userId": "Jane_Doe@AdobeID"
        },
        "tasks": [
            {
                "name": "train",
                "parameters": [
                    {
                        "key": "learning_rate",
                        "value": "0.5"
                    }
                ]
            },
            {
                "name": "score",
                "parameters": [
                    {
                        "key": "output_dataset_id",
                        "value": "output-dataset-001"
                    }
                ]
            }
        ]
    }'
```

**响应**

成功的响应将返回包含MLInstance更新详细信息的有效负载。

```json
{
    "id": "46986c8f-7739-4376-8509-0178bdf32cda",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "00000000-0000-0000-0000-000000000000",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "learning_rate",
                    "value": "0.5"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "output_dataset_id",
                    "value": "output-data-set-001"
                }
            ]
        }
    ]
}
```

## 按引擎ID删除MLInstances

通过执行包含引擎ID作为查询参数的DELETE请求，可以删除共享同一引擎的所有MLInstances。

**API格式**

```http
DELETE /mlInstances?engineId={ENGINE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{ENGINE_ID}` | 有效的引擎ID。 |

**请求**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances?engineId=22f4166f-85ba-4130-a995-a2b8e1edde32 \
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
    "detail": "MLInstances successfully deleted"
}
```

## 删除MLInstance

通过执行请求DELETE（该请求路径中包含目标MLInstance的ID），可以删除单个MLInstance。

**API格式**

```http
DELETE /mlInstances/{MLINSTANCE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{MLINSTANCE_ID}` | 有效的MLInstance ID。 |

**请求**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlInstances/46986c8f-7739-4376-8509-0178bdf32cda \
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
    "detail": "MLInstance deletion was successful"
}
```
