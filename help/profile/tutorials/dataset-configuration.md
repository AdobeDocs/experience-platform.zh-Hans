---
keywords: Experience Platform;用户档案；实时客户用户档案；疑难解答；API；启用数据集
title: 使用API为用户档案和身份服务配置数据集
topic: tutorial
type: Tutorial
description: 本教程向您展示如何使用Adobe Experience PlatformAPI启用数据集以与实时客户用户档案和身份服务一起使用。
translation-type: tm+mt
source-git-commit: f34983dc13a900e7c8fe2e2cef454400c1b6a726
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 1%

---


# 使用API为[!DNL Profile]和[!DNL Identity Service]配置数据集

本教程介绍如何启用数据集以用于[!DNL Real-time Customer Profile]和[!DNL Identity Service]，具体分为以下步骤：

1. 使用以下两个选项之一启用数据集以在[!DNL Real-time Customer Profile]中使用：
   - [创建新数据集](#create-a-dataset-enabled-for-profile-and-identity)
   - [配置现有数据集](#configure-an-existing-dataset)
1. [将数据摄取到数据集中](#ingest-data-into-the-dataset)
1. [确认实时客户用户档案收集数据](#confirm-data-ingest-by-real-time-customer-profile)
1. [确认由Identity Service收录数据](#confirm-data-ingest-by-identity-service)

## 入门指南

本教程需要对管理[!DNL Profile]启用数据集时涉及的各种Adobe Experience Platform服务进行有效的了解。 在开始本教程之前，请查阅以下相关[!DNL Platform]服务的文档：

- [[!DNL Real-time Customer Profile]](../home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
- [[!DNL Identity Service]](../../identity-service/home.md):通过将 [!DNL Real-time Customer Profile] 来自被引入的不同数据源的身份连接到其中，实现 [!DNL Platform]了。
- [[!DNL Catalog Service]](../../catalog/home.md):一个REST风格的API，它允许您创建数据集并为其配 [!DNL Real-time Customer Profile] 置和 [!DNL Identity Service]。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。

以下各节提供了成功调用平台API所需了解的其他信息。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参见[!DNL Experience Platform]疑难解答指南中关于如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的一节。[

### 收集所需标题的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

- 授权：载体`{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要附加标头：

- 内容类型：application/json

[!DNL Experience Platform]中的所有资源都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个标头，它指定操作将在其中进行的沙箱的名称。 有关[!DNL Platform]中沙箱的详细信息，请参阅[沙箱概述文档](../../sandboxes/home.md)。

- x-sandbox-name:`{SANDBOX_NAME}`

## 创建为[!DNL Profile]和[!DNL Identity] {#create-a-dataset-enabled-for-profile-and-identity}启用的数据集

您可以在创建后立即或在创建数据集后的任意点为[!DNL Real-time Customer Profile]和[!DNL Identity Service]启用数据集。 如果要启用已创建的数据集，请按照[配置此文档后找到的现有数据集](#configure-an-existing-dataset)的步骤操作。 要创建新数据集，您必须知道已启用实时模式的现有XDM用户档案的ID。 有关如何查找或创建启用用户档案的模式的信息，请参阅教程中的[使用模式注册表API](../../xdm/tutorials/create-schema-api.md)创建模式。 以下对[!DNL Catalog] API的调用为[!DNL Profile]和[!DNL Identity Service]启用数据集。

**API格式**

```http
POST /dataSets
```

**请求**

通过在请求主体中的`tags`下包含`unifiedProfile`和`unifiedIdentity`，将立即为[!DNL Profile]和[!DNL Identity Service]启用数据集。 这些标记的值必须是包含字符串`"enabled:true"`的数组。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fileDescription" : {
    "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    },
    "fields":[],
    "schemaRef" : {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
    },
    "tags" : {
       "unifiedProfile": ["enabled:true"],
       "unifiedIdentity": ["enabled:true"]
    }
  }'
```

| 属性 | 描述 |
|---|---|
| `schemaRef.id` | 启用[!DNL Profile]的模式的ID，数据集将基于该ID。 |
| `{TENANT_ID}` | [!DNL Schema Registry]中的命名空间，它包含属于您的IMS组织的资源。 有关详细信息，请参阅[!DNL Schema Registry]开发人员指南的[TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id)部分。 |

**响应**

成功的响应会显示一个数组，其中包含以`"@/dataSets/{DATASET_ID}"`形式新创建的数据集的ID。 成功创建并启用数据集后，请继续执行[上传数据](#upload-data-to-the-dataset)的步骤。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 配置现有数据集{#configure-an-existing-dataset}

以下步骤介绍如何为[!DNL Real-time Customer Profile]和[!DNL Identity Service]启用先前创建的数据集。 如果已创建启用用户档案的数据集，请继续执行[获取数据](#ingest-data-into-the-dataset)的步骤。

### 检查数据集是否已启用{#check-if-the-dataset-is-enabled}

使用[!DNL Catalog] API，您可以检查现有数据集以确定它是否允许在[!DNL Real-time Customer Profile]和[!DNL Identity Service]中使用。 以下调用按ID检索数据集的详细信息。

**API格式**

```http
GET /dataSets/{DATASET_ID}
```

| 参数 | 描述 |
|---|---|
| `{DATASET_ID}` | 要检查的数据集的ID。 |

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "Commission Program Events DataSet",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedProfile": [
                "enabled:true"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ]
        },
        "lastBatchId": "6dcd9128a1c84e6aa5177641165e18e4",
        "lastBatchStatus": "success",
        "dule": {},
        "statsCache": {
            "startDate": null,
            "endDate": null
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "5b020a27e7040801dedbf46f",
        "status": "enabled",
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "@/xdms/context/experienceevent",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": [],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

在`tags`属性下，您可以看到`unifiedProfile`和`unifiedIdentity`都存在值`enabled:true`。 因此，分别为此数据集启用[!DNL Real-time Customer Profile]和[!DNL Identity Service]。

### 启用数据集{#enable-the-dataset}

如果[!DNL Profile]或[!DNL Identity Service]尚未启用现有数据集，则可以通过使用数据集ID发出PATCH请求来启用它。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 参数 | 描述 |
|---|---|
| `{DATASET_ID}` | 要更新的数据集的ID。 |

**请求**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags" : {
        "unifiedProfile": ["enabled:true"],
        "unifiedIdentity": ["enabled:true"]
    }
  }'
```

请求主体包括`tags`属性，该属性包含两个子属性：`"unifiedProfile"`和`"unifiedIdentity"`。 这些子属性的值是包含字符串`"enabled:true"`的数组。

**响**
应成功的PATCH请求返回HTTP状态200(OK)和包含更新数据集ID的数组。此ID应与在PATCH请求中发送的ID匹配。 `"unifiedProfile"`和`"unifiedIdentity"`标记现已添加，且用户档案和标识服务启用了数据集。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 将数据摄取到数据集{#ingest-data-into-the-dataset}

[!DNL Real-time Customer Profile]和[!DNL Identity Service]在将XDM数据引入数据集时都会使用它。 有关如何将数据上传到数据集的说明，请参阅教程中的[使用API](../../catalog/datasets/create.md)创建数据集。 在规划要发送到支持[!DNL Profile]的数据集的数据时，请考虑以下最佳实践：

- 包括要用作受众段条件的任何数据。
- 根据您的用户档案数据包含尽可能多的标识符，以最大化您的标识图。 这样，[!DNL Identity Service]可以更高效地跨数据集拼接身份。

## 确认由[!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}收录数据

首次将数据上传到新数据集时，或者作为涉及新ETL或数据源的流程的一部分，建议仔细检查数据，确保数据已按预期上传。 使用[!DNL Real-time Customer Profile] Access API，可以在批处理数据加载到数据集时检索它。 如果无法检索任何期望的实体，则可能未为[!DNL Real-time Customer Profile]启用数据集。 确认已启用数据集后，请确保源数据格式和标识符支持您的预期。 有关如何使用[!DNL Real-time Customer Profile] API访问[!DNL Profile]数据的详细说明，请按照[entities端点指南](../api/entities.md)操作，也称为“[!DNL Profile Access] API”。

## 确认由Identity Service {#confirm-data-ingest-by-identity-service}收录数据

摄取的包含多个标识的每个数据片段会在您的专用标识图中创建一个链接。 有关标识图和访问标识数据的详细信息，请首先阅读[标识服务概述](../../identity-service/home.md)。