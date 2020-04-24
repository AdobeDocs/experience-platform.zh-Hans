---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: MLInstances
topic: Developer guide
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# MLInstances

MLI实例是现有引擎与一组相应配置的配对，这些配置定义了任何培训参数、评分参数或硬件资源配置。 [](./engines.md)

## 创建MLInstance {#create-an-mlinstance}

您可以通过执行POST请求来创建MLI实例，同时提供由有效的引擎ID(`{ENGINE_ID}`)和一组适当的默认配置组成的请求有效负荷。

如果引擎ID引用PySpark或Spark引擎，则您可以配置计算资源量，如内核数或内存量。 如果引用了Python引擎，则您可以选择使用CPU或GPU进行培训和评分。 有关详细信息，请参 [阅PySpark和Spark资源配置](./appendix.md#resource-config)[以及Python CPU和GPU配置的附录部分](./appendix.md#cpu-gpu-config) 。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -d '{
        "name": "A name for this MLInstance",
        "description": "A description for this MLInstance",
        "engineId": "{ENGINE_ID}",
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
| `name` | MLInstance的所需名称。 与此MLI实例对应的模型将继承此值，该值将作为模型的名称显示在UI中。 |
| `description` | MLInstance的可选描述。 与此MLI实例对应的模型将继承此值，并作为模型的描述显示在UI中。 此属性是必需的。如果不想提供说明，请将其值设置为空字符串。 |
| `engineId` | 现有引擎的ID。 |
| `tasks` | 用于培训、评分或功能管道的一组配置。 |

**响应**

成功的响应返回包含新创建的MLI实例(包括其唯一标识符(`id`))的详细信息的有效负荷。

```json
{
    "id": "{MLINSTANCE_ID}",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "{ENGINE_ID}",
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

## 检索MLInstance的列表

您可以通过执行单个GET请求来检索MLInstances的列表。 要帮助筛选结果，您可以在请求路径中指定查询参数。 有关可用查询的列表，请参阅有关资产检索的查询参 [数的附录部分](./appendix.md#query)。

**API格式**

```http
GET /mlInstances
GET /mlInstances?{QUERY_PARAMETER}={VALUE}
GET /mlInstances?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 参数 | 描述 |
| --- | --- |
| `{QUERY_PARAMETER}` | 用于筛选 [结果的可用查询](./appendix.md#query) 参数之一。 |
| `{VALUE}` | 前面查询参数的值。 |

**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回一列表MLInstances及其详细信息。

```json
{
    "children": [
        {
            "id": "{MLINSTANCE_ID}",
            "name": "A name for this MLInstance",
            "description": "A description for this MLInstance",
            "engineId": "{ENGINE_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "{MLINSTANCE_ID}",
            "name": "Retail Sales Model",
            "description": "A Model created with the Retail Sales Recipe",
            "engineId": "{ENGINE_ID}",
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

您可以通过执行GET请求来检索特定MLI实例的详细信息，该请求在请求路径中包含所需MLI实例的ID。

**API格式**

```http
GET /mlInstances/{MLINSTANCE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{MLINSTANCE_ID}` | 所需MLI实例的ID。 |

**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlInstances/{MLINSTANCE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回MLInstance的详细信息。

```json
{
    "id": "{MLINSTANCE_ID}",
    "name": "A name for this MLInstance",
    "description": "A description for this MLInstance",
    "engineId": "{ENGINE_ID}",
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

## 更新MLInstance

您可以通过PUT请求覆盖现有MLI实例的属性，该请求在请求路径中包括目标MLInstance的ID并提供包含已更新属性的JSON有效负荷，从而更新现有MLI实例。

>[!TIP] 为了确保此PUT请求成功，建议首先执行GET请求以按ID [检索MLI实例](#retrieve-specific)。 然后，修改并更新返回的JSON对象，并应用修改后的JSON对象的整个作为PUT请求的有效负荷。

以下示例API调用将在最初具有这些属性时更新MLInstance的培训和评分参数：

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
    https://platform.adobe.io/data/sensei/mlInstances/{MLINSTANCE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的响应会返回包含MLInstance的更新详细信息的有效负荷。

```json
{
    "id": "{MLINSTANCE_ID}",
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

您可以通过执行DELETE请求来删除共享同一引擎的所有MLI实例，该请求将引擎ID作为查询参数。

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
    https://platform.adobe.io/data/sensei/mlInstances?engineId={ENGINE_ID} \
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
    "detail": "MLInstances successfully deleted"
}
```

## 删除MLInstance

您可以通过执行DELETE请求来删除单个MLI实例，该请求在请求路径中包含目标MLInstance的ID。

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
    https://platform.adobe.io/data/sensei/mlInstances/{MLINSTANCE_ID} \
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
    "detail": "MLInstance deletion was successful"
}
```
