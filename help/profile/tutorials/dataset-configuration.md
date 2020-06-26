---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 使用API为用户档案和身份服务配置数据集
topic: tutorial
translation-type: tm+mt
source-git-commit: 93aae0e394e1ea9b6089d01c585a94871863818e
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 1%

---


# 使用API为用户档案和身份服务配置数据集

本教程介绍如何启用数据集以用于实时客户用户档案和身份服务，具体分为以下步骤：

1. 使用以下两种选项之一启用数据集以在实时客户用户档案中使用：
   - [创建新数据集](#create-a-dataset-enabled-for-profile-and-identity)
   - [配置现有数据集](#configure-an-existing-dataset)
1. [将数据摄取到数据集中](#ingest-data-into-the-dataset)
1. [确认实时客户用户档案收集数据](#confirm-data-ingest-by-real-time-customer-profile)
1. [确认由Identity Service收录数据](#confirm-data-ingest-by-identity-service)

## 入门指南

本教程需要对管理支持Adobe Experience Platform的数据集时涉及的各种用户档案服务进行有效的了解。 在开始本教程之前，请查阅以下相关平台服务的文档：

- [实时客户用户档案](../home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
- [身份服务](../../identity-service/home.md): 通过将来自不同数据源的身份融入平台，实现实时客户用户档案。
- [目录服务](../../catalog/home.md): 一个RESTful API，它允许您创建数据集并为实时客户用户档案和身份服务进行配置。
- [体验数据模型(XDM)](../../xdm/home.md): 平台组织客户体验数据的标准化框架。

以下各节提供了成功调用平台API所需了解的其他信息。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用的章节。

### 收集所需标题的值

要调用平台API，您必须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

- 授权： 承载者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

- 内容类型： application/json

Experience Platform中的所有资源都隔离到特定虚拟沙箱。 对平台API的所有请求都需要一个标头，它指定操作将在其中进行的沙箱的名称。 有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

- x-sandbox-name: `{SANDBOX_NAME}`

## 创建启用用户档案和标识的数据集 {#create-a-dataset-enabled-for-profile-and-identity}

您可以在创建时或数据集创建后的任何时刻立即为实时客户用户档案和身份服务启用数据集。 如果要启用已创建的数据集，请按照以下步骤配置此文档 [后找到的现](#configure-an-existing-dataset) 有数据集。 要创建新数据集，您必须知道已启用实时模式的现有XDM用户档案的ID。 有关如何查找或创建启用用户档案的模式的信息，请参阅有关使用 [模式注册表API创建模式的教程](../../xdm/tutorials/create-schema-api.md)。 以下对Catalog API的调用为用户档案和标识服务启用数据集。

**API格式**

```http
POST /dataSets
```

**请求**

通过在 `unifiedProfile` 请 `unifiedIdentity` 求 `tags` 主体中加入和下，将立即启用用户档案和身份服务。 这些标记的值必须是包含字符串的数组 `"enabled:true"`。

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
| `schemaRef.id` | 启用用户档案的模式的ID，数据集将基于该ID。 |
| `{TENANT_ID}` | 命名空间注册表中包含属于您的IMS组织的资源的模式。 有关详 [细信息，请参阅模式](../../xdm/api/getting-started.md#know-your-tenant-id) “注册表开发人员指南”的TENANT_ID部分。 |

**响应**

成功的响应以以下形式显示包含新创建数据集ID的数组 `"@/dataSets/{DATASET_ID}"`。 成功创建并启用数据集后，请继续执行上传数据 [的步骤](#upload-data-to-the-dataset)。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 配置现有数据集 {#configure-an-existing-dataset}

以下步骤涵盖如何为实时客户用户档案和身份服务启用先前创建的数据集。 如果已创建启用用户档案的数据集，请继续执行数据 [获取步骤](#ingest-data-into-the-dataset)。

### 检查数据集是否已启用 {#check-if-the-dataset-is-enabled}

使用Catalog API，您可以检查现有数据集以确定它是否允许在实时客户用户档案和标识服务中使用。 以下调用按ID检索数据集的详细信息。

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

在属 `tags` 性下，您可以看到 `unifiedProfile` 和 `unifiedIdentity` 都存在该值 `enabled:true`。 因此，分别为该数据集启用实时客户用户档案和身份服务。

### 启用数据集 {#enable-the-dataset}

如果尚未为用户档案或标识服务启用现有数据集，则可以使用数据集ID发出PATCH请求来启用它。

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

请求主体包括一 `tags` 个属性，它包含两个子属性： `"unifiedProfile"` 和 `"unifiedIdentity"`。 这些子属性的值是包含字符串的数组 `"enabled:true"`。

**响应** PATCH请求成功返回HTTP状态200(OK)和包含更新数据集ID的数组。 此ID应与在PATCH请求中发送的ID匹配。 现在 `"unifiedProfile"` 已添 `"unifiedIdentity"` 加和标记，并且用户档案和标识服务启用了数据集。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 将数据摄取到数据集中 {#ingest-data-into-the-dataset}

实时客户用户档案和身份服务在将XDM数据引入数据集时都会消耗它。 有关如何将数据上传到数据集的说明，请参阅教程 [中的“使用API创建数据集](../../catalog/datasets/create.md)”。 在规划要发送哪些用户档案到启用数据集时，请考虑以下最佳实践：

- 包括要用作受众段条件的任何数据。
- 根据您的用户档案数据包含尽可能多的标识符，以最大化您的标识图。 这使Identity Service能够更高效地跨数据集拼接身份。

## 确认实时客户用户档案收集数据 {#confirm-data-ingest-by-real-time-customer-profile}

首次将数据上传到新数据集时，或者作为涉及新ETL或数据源的流程的一部分，建议仔细检查数据，确保数据已按预期上传。 使用实时客户用户档案访问API，您可以在批数据加载到数据集中时检索批数据。 如果无法检索任何您期望的实体，则可能未为实时客户用户档案启用数据集。 确认已启用数据集后，请确保源数据格式和标识符支持您的预期。 有关如何使用实时客户用户档案API访问用户档案数据的详细说明，请按照实 [体端点指南](../api/entities.md)(也称为“用户档案访问API”)进行操作。

## 确认由Identity Service收录数据 {#confirm-data-ingest-by-identity-service}

摄取的包含多个标识的每个数据片段会在您的专用标识图中创建一个链接。 有关标识图和访问标识数据的详细信息，请首先阅读Identity [Service概述](../../identity-service/home.md)。