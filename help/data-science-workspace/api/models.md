---
keywords: Experience Platform；开发人员指南；端点；数据科学Workspace；热门主题；模型；sensei机器学习api
solution: Experience Platform
title: 模型API端点
description: 模型是机器学习方法的一个实例，它使用历史数据和配置进行培训以针对业务用例进行解析。
role: Developer
exl-id: e66119a9-9552-497c-9b3a-b64eb3b51fcf
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 4%

---

# 模型端点

模型是机器学习方法的一个实例，它使用历史数据和配置进行培训以针对业务用例进行解析。

## 检索模型列表

通过执行对/models的单个GET请求，可以检索属于所有“模型”的“模型”详细信息列表。 默认情况下，此列表将从最早创建的模型对其自身排序，并将结果限制为25。 您可以选择通过指定某些查询参数来筛选结果。 有关可用查询的列表，请参阅[用于资源检索的查询参数](./appendix.md#query)的附录部分。

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回包含模型详细信息的有效负载，其中包括每个模型的唯一标识符(`id`)。

```json
{
    "children": [
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "A name for this Model",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for this Model",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "27c53796-bd6b-4u59-b51d-7296aa20er23",
            "name": "Model 2",
            "experimentId": "3cb25a2d-2cbd-4d34-a619-8ddae5259a5t",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
            "description": "A description for Model2",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/model-name",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-02T00:00:00.000Z"
       },
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "Model 3",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
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
| `id` | 对应于模型的ID。 |
| `modelArtifactUri` | 指示存储模型位置的URI。 URI以模型的`name`值结尾。 |
| `experimentId` | 有效的试验ID。 |
| `experimentRunId` | 有效的试验运行ID。 |

## 检索特定模型

通过执行单个GET请求并在请求路径中提供有效的模型ID，可以检索属于特定模型的模型详细信息列表。 要帮助筛选结果，您可以在请求路径中指定查询参数。 有关可用查询的列表，请参阅[用于资源检索的查询参数](./appendix.md#query)的附录部分。

**API格式**

```http
GET /models/{MODEL_ID}
GET /models/?property=experimentRunID=={EXPERIMENT_RUN_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{MODEL_ID}` | 已训练或已发布模型的标识符。 |
| `{EXPERIMENT_RUN_ID}` | 试验运行的标识符。 |

**请求**

以下请求包含一个查询，并检索共享相同experimentRunID ({EXPERIMENT_RUN_ID})的已训练模型的列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId==33408593-2871-4198-a812-6d1b7d939cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回包含模型详细信息(包括模型唯一标识符(`id`))的有效负载。

```json
{
    "children": [
        {
            "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "name": "A name for this Model",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
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
        "property": "experimentRunId==33408593-2871-4198-a812-6d1b7d939cda,deleted==false",
        "count": 1
    }
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 对应于模型的ID。 |
| `modelArtifactUri` | 指示存储模型位置的URI。 URI以模型的`name`值结尾。 |
| `experimentId` | 有效的试验ID。 |
| `experimentRunId` | 有效的试验运行ID。 |

## 注册预生成的模型 {#register-a-model}

您可以通过向`/models`端点发出POST请求来注册预生成的模型。 为了注册您的模型，`modelArtifact`文件和`model`属性值需要包含在请求正文中。

**API格式**

```http
POST /models
```

**请求**

以下POST包含所需的`modelArtifact`文件和`model`属性值。 有关这些值的更多信息，请参阅下表。

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -F 'modelArtifact=@/Users/yourname/Desktop/model.onnx' \
    -F 'model={
            "name": "Your Model - 0615-1342-45",
            "originType": "offline"
    }'
```

| 参数 | 描述 |
| --- | --- |
| `modelArtifact` | 要包括的完整模型工件的位置。 |
| `model` | 需要创建的Model对象的表单数据。 |

**响应**

成功的响应将返回包含模型详细信息(包括模型唯一标识符(`id`))的有效负载。

```json
{
  "id": "a28f151a-597a-4a7e-87e9-1c1dbc9c2af7",
  "name": "Your Model - 0615-1342-45",
  "originType": "offline",
  "modelArtifactUri": "http://storageblobml.blob.core.windows.net/prod-models/a28f151a-597a-4a7e-87e9-1c1dbc9c2af7",
  "created": "2020-06-15T20:55:41.520Z",
  "updated": "2020-06-15T20:55:41.520Z",
  "deprecated": false
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 对应于模型的ID。 |
| `modelArtifactUri` | 指示存储模型位置的URI。 URI以模型的`id`值结尾。 |

## 按ID更新模型

您可以更新现有模型，方法是通过PUT请求（请求路径中包含目标模型的ID）覆盖其属性，并提供包含已更新属性的JSON有效负载。

>[!TIP]
>
>为了确保此PUT请求成功，建议您首先执行GET请求以按ID检索模型。 然后，修改并更新返回的JSON对象，并将修改后的整个JSON对象应用作PUT请求的有效负载。

**API格式**

```http
PUT /models/{MODEL_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{MODEL_ID}` | 已训练或已发布模型的标识符。 |

**请求**

```shell
curl -X PUT \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -d '{
        "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
        "name": "A name for this Model",
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
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

成功的响应将返回包含试验更新详细信息的有效负载。

```json
{
        "id": "15c53796-bd6b-4e09-b51d-7296aa20af71",
        "name": "A name for this Model",
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
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

您可以通过执行请求(DELETE路径中包含目标模型的ID)来删除单个模型。

**API格式**

```http
DELETE /models/{MODEL_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{MODEL_ID}` | 已训练或已发布模型的标识符。 |

**请求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回一个包含200状态的有效负载，以确认删除模型。

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Model deletion was successful"
}
```

## 为模型创建新的转码 {#create-transcoded-model}

转码是将一种编码直接转换为另一种编码的数字转换。 通过提供`{MODEL_ID}`和您希望新输出在其中的`targetFormat`，为模型创建新的转码。

**API格式**

```http
POST /models/{MODEL_ID}/transcodings
```

| 参数 | 描述 |
| --- | --- |
| `{MODEL_ID}` | 已训练或已发布模型的标识符。 |

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: text/plain' \
    -D '{
 "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
 "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
 "targetFormat": "CoreML",
 "created": "2019-12-16T19:59:08.360Z",
 "createdBy": {
    "userId": "FDD760CD5CD467380A495FE2@AdobeID"
 },
 "updated": "2019-12-19T18:37:43.696Z",
 "deleted": false,
}'
```

**响应**

成功的响应会返回一个有效负载，该有效负载包含带有转码信息的JSON对象。 这包括在[检索特定转码模型](#retrieve-transcoded-model)中使用的转码唯一标识符(`id`)。

```json
{
  "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
  "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
  "targetFormat": "CoreML",
  "created": "2020-06-12T22:01:55.886Z",
  "createdBy": {
    "userId": "FDD760CD5CD467380A495FE2@AdobeID"
  },
  "updated": "2020-06-12T22:01:55.886Z",
  "deleted": false
}
```

## 检索模型的转码列表 {#retrieve-transcoded-model-list}

通过使用`{MODEL_ID}`执行GET请求，您可以检索已在模型上执行的转码列表。

**API格式**

```http
GET /models/{MODEL_ID}/transcodings
```

| 参数 | 描述 |
| --- | --- |
| `{MODEL_ID}` | 已训练或已发布模型的标识符。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回一个有效负载，该有效负载包含一个json对象，以及在该模型上执行的每个转码列表。 每个转码模型接收唯一标识符(`id`)。

```json
{
    "children": [
        {
            "id": "460aa5a1-e972-455d-b8dc-4bc6cd91edb6",
            "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "created": "2019-12-20T01:07:50.978Z",
            "createdBy": {
                "userId": "FDD760CD5CD467380A495FE2@AdobeID"
            },
            "updated": "2019-12-20T01:07:50.978Z",
            "deprecated": false
        },
        {
            "id": "bdb3e4c2-4702-4045-86b4-17ee40df91cc",
            "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "created": "2019-12-20T17:48:26.473Z",
            "createdBy": {
                "userId": "FDD760CD5CD467380A495FE2@AdobeID"
            },
            "updated": "2019-12-20T17:48:26.473Z",
            "deprecated": false
        }
    ],
    "_page": {
        "property": "modelId==15c53796-bd6b-4e09-b51d-7296aa20af71,deleted==false,deprecated==false",
        "count": 2
    }
}
```

## 检索特定的转码模型 {#retrieve-transcoded-model}

您可以通过使用`{MODEL_ID}`和转码模型的ID执行GET请求来检索特定的转码模型。

**API格式**

```http
GET /models/{MODEL_ID}/transcodings/{TRANSCODING_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{MODEL_ID}` | 已训练或已发布模型的唯一标识符。 |
| `{TRANSCODING_ID}` | 转码模型的唯一标识符。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings/460aa5a1-e972-455d-b8dc-4bc6cd91edb6 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回一个有效负载，该有效负载包含带有转码模型数据的JSON对象。

```json
{
    "id": "460aa5a1-e972-455d-b8dc-4bc6cd91edb6",
    "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
    "created": "2019-12-20T01:07:50.978Z",
    "createdBy": {
        "userId": "FDD760CD5CD467380A495FE2@AdobeID"
    },
    "updated": "2019-12-20T01:07:50.978Z",
    "deprecated": false
}
```
