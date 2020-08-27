---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics;models;sensei machine learning api
solution: Experience Platform
title: 模型
topic: Developer guide
description: 模型是机器学习配方的实例，该配方使用历史数据和配置进行培训，以便为业务用例进行解决。
translation-type: tm+mt
source-git-commit: 194a29124949571638315efe00ff0b04bff19303
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 4%

---


# 模型

模型是机器学习配方的实例，该配方使用历史数据和配置进行培训，以便为业务用例进行解决。

## 检索一列表模型

通过对/models执行单个GET请求，可以检索属于所有模型的模型详细信息列表。 默认情况下，此列表将自行从最早创建的模型排序，并将结果限制为25。 您可以通过指定一些查询参数来筛选结果。 有关可用查询的列表，请参阅附录部分中有关资产检 [索查询参数的部分](./appendix.md#query)。

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

成功的响应会返回一个有效负荷，其中包含包括每个模型唯一标识符()的模型的详细`id`信息。

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
| `id` | 与“模型”(Model)对应的ID。 |
| `modelArtifactUri` | 一个URI，指示模型的存储位置。 URI以模型 `name` 的值结束。 |
| `experimentId` | 有效的实验ID。 |
| `experimentRunId` | 有效的实验运行ID。 |

## 检索特定模型

通过执行单个GET请求并在请求路径中提供有效的模型ID，可以检索属于特定模型的模型详细信息列表。 要帮助筛选结果，您可以在请求路径中指定查询参数。 有关可用查询的列表，请参阅附录部分中有关资产检 [索查询参数的部分](./appendix.md#query)。

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

以下请求包含一个查询，并检索共享相同empericRunID({EXPERICE_RUN_ID})的受训模型的列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/?property=experimentRunId==33408593-2871-4198-a812-6d1b7d939cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回一个有效负荷，其中包含包括模型唯一标识符()在内的模型的详细`id`信息。

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
| `id` | 与“模型”(Model)对应的ID。 |
| `modelArtifactUri` | 一个URI，指示模型的存储位置。 URI以模型 `name` 的值结束。 |
| `experimentId` | 有效的实验ID。 |
| `experimentRunId` | 有效的实验运行ID。 |

## 注册预生成的模型 {#register-a-model}

可以通过向端点发出POST请求来注册预生成的 `/models` 模型。 要注册模型，需 `modelArtifact` 要将 `model` 文件和属性值包含在请求正文中。

**API格式**

```http
POST /models
```

**请求**

以下POST包 `modelArtifact` 含所需 `model` 的文件和属性值。 有关这些值的详细信息，请参阅下表。

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的响应会返回一个有效负荷，其中包含包括模型唯一标识符()在内的模型的详细`id`信息。

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
| `id` | 与“模型”(Model)对应的ID。 |
| `modelArtifactUri` | 一个URI，指示模型的存储位置。 URI以模型 `id` 的值结束。 |

## 按ID更新模型

您可以通过以下方式更新现有模型：通过在请求路径中包含PUT模型ID的目标请求覆盖其属性，并提供包含已更新属性的JSON有效负荷。

>[!TIP]
>
>为确保此PUT请求成功，建议您首先执行GET请求以按ID检索模型。 然后，修改并更新返回的JSON对象，并应用已修改的JSON对象的整个作为PUT请求的有效负荷。

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
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的响应会返回包含实验的更新详细信息的有效负荷。

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

您可以通过执行DELETE请求来删除单个模型，该请求在请求路径中包含目标模型的ID。

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
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回包含200状态的有效负荷，确认删除模型。

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Model deletion was successful"
}
```

## 为模型创建新的转码 {#create-transcoded-model}

转码是指将一种编码直接数字到另一种编码的转换。 通过提供和希望新输出包含在中， `{MODEL_ID}` 为模 `targetFormat` 型创建新的转码。

**API格式**

```http
POST /models/{MODEL_ID}/transcodings
```

| 参数 | 描述 |
| --- | --- |
| `{MODEL_ID}` | 已培训或已发布模型的标识符。 |

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: text/plain' \
    -D '{
 "id": "491a3be5-1d32-4541-94d5-cd1cd07affb5",
 "modelId" : "15c53796-bd6b-4e09-b51d-7296aa20af71",
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

成功的响应会返回包含JSON对象的有效负荷，其中包含转码信息。 这包括检索特定转码模型时`id`使用的转 [码唯一标识符()](#retrieve-transcoded-model)。

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

## 检索模型的转换列表 {#retrieve-transcoded-model-list}

您可以通过执行列表请求来检索已对模型执行的转换GET, `{MODEL_ID}`

**API格式**

```http
GET /models/{MODEL_ID}/transcodings
```

| 参数 | 描述 |
| --- | --- |
| `{MODEL_ID}` | 已培训或已发布模型的标识符。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回一个包含json对象的有效负荷，其列表为在模型上执行的每个转码。 每个转码模型接收唯一标识符(`id`)。

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

## 检索特定转码模型 {#retrieve-transcoded-model}

通过使用转码模型的id和您的GET请求，可 `{MODEL_ID}` 以检索特定的转码模型。

**API格式**

```http
GET /models/{MODEL_ID}/transcodings/{TRANSCODING_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{MODEL_ID}` | 已培训或已发布模型的唯一标识符。 |
| `{TRANSCODING_ID}` | 转码模型的唯一标识符。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/models/15c53796-bd6b-4e09-b51d-7296aa20af71/transcodings/460aa5a1-e972-455d-b8dc-4bc6cd91edb6 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回包含JSON对象的有效负荷，该JSON对象包含转码模型的数据。

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


