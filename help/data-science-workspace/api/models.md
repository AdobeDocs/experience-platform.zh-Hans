---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: 模型
topic: Developer guide
translation-type: tm+mt
source-git-commit: 01cfbc86516a05df36714b8c91666983f7a1b0e8

---


# 模型

模型是机器学习菜谱的实例，该菜谱使用历史数据和配置来训练以解决业务用例。

## 检索一列表模型

通过对/models执行单个GET请求，可以检索属于所有模型的模型详细信息列表。 默认情况下，此列表将自行从最早创建的模型排序，并将结果限制为25。 您可以选择通过指定一些查询参数来过滤结果。 有关可用查询的列表，请参阅有关资产检索的查询参 [数的附录部分](./appendix.md#query)。

**API格式**

```http
GET /models
```

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/ \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回一个有效负荷，其中包含包括每个模型唯一标识符(`id`)的模型详细信息。

```json
{
    "children": [
        {
            "id": "{MODEL_ID}",
            "name": "A name for this Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "{MODEL_ID}",
            "name": "Model 2",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "A description for Model2",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "{MODEL_ID}",
            "name": "Model 3",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "A description for Model3",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
    ],
    "_page": {
        "property": "deleted==false",
        "count": 3
    }
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 与“模型”(Model)对应的ID。 |
| `modelArtifactUri` | 一个URI，指示模型的存储位置。 URI以模型的 `name` 值结束。 |
| `experimentId` | 有效的实验ID。 |
| `experimentRunId` | 有效的实验运行ID。 |

## 检索特定模型

您可以通过执行单个GET请求并在请求路径中提供有效的模型ID来检索属于特定模型的模型详细信息列表。 要帮助筛选结果，您可以在请求路径中指定查询参数。 有关可用查询的列表，请参阅有关资产检索的查询参 [数的附录部分](./appendix.md#query)。

**API格式**

```http
GET /models/{MODEL_ID}
GET /models/?property=experimentRunID=={EXPERIMENT_RUN_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{MODEL_ID}` | 已培训或已发布模型的标识符。 |
| `{EXPERIMENT_RUN_ID}` | 实验运行的标识符。 |

**请求**

以下请求包含一个查询，并检索共享相同emperityRunID({EXPERICE_RUN_ID})的受训模型的列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回一个有效负荷，其中包含包括模型唯一标识符(`id`)在内的模型的详细信息。

```json
{
    "children": [
        {
            "id": "{MODEL_ID}",
            "name": "A name for this Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       }
    ],
    "_page": {
        "property": "experimentRunId=={EXPERIMENT_RUN_ID},deleted==false",
        "count": 1
    }
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 与“模型”(Model)对应的ID。 |
| `modelArtifactUri` | 一个URI，指示模型的存储位置。 URI以模型的 `name` 值结束。 |
| `experimentId` | 有效的实验ID。 |
| `experimentRunId` | 有效的实验运行ID。 |

## 按ID更新模型

您可以通过PUT请求覆盖现有模型的属性，该请求在请求路径中包含目标模型的ID，并提供包含已更新属性的JSON有效负荷，从而更新现有模型。

>[!TIP] 为了确保此PUT请求成功，建议首先执行GET请求以按ID检索模型。 然后，修改并更新返回的JSON对象，并应用修改后的JSON对象的整个作为PUT请求的有效负荷。

**API格式**

```http
PUT /models/{MODEL_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{MODEL_ID}` | 已培训或已发布模型的标识符。 |

**请求**

```shell
curl -X PUT \
  https://platform.adobe.io/data/sensei/models/{MODEL_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -d '{
        "id": "{MODEL_ID}",
        "name": "A name for this Model",
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "description": "An updated description for this Model",
        "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "updated": "2019-01-02T00:00:00.000Z"
    }'
```

**响应**

成功的响应会返回包含实验的更新详细信息的有效负荷。

```json
{
        "id": "{MODEL_ID}",
        "name": "A name for this Model",
        "experimentId": "{EXPERIMENT_ID}",
        "experimentRunId": "{EXPERIMENT_RUN_ID}",
        "description": "An updated description for this Model",
        "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "updated": "2019-01-02T00:00:00.000Z"
    }
```

## 按ID删除模型

可以通过执行DELETE请求来删除单个模型，该请求在请求路径中包含目标模型的ID。

**API格式**

```http
DELETE /models/{MODEL_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{MODEL_ID}` | 已培训或已发布模型的标识符。 |

**请求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/sensei/models/{MODEL_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回一个包含200状态的有效负荷，该状态确认删除模型。

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Model deletion was successful"
}
```
