---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;enable dataset
title: 使用API为用户档案和身份服务配置数据集
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 1%

---


# 为配置数据集并 [!DNL Profile] 使用 [!DNL Identity Service] API

本教程介绍如何启用数据集以在和中 [!DNL Real-time Customer Profile] 使 [!DNL Identity Service]用，具体分为以下步骤：

1. 使用以下两个选项之 [!DNL Real-time Customer Profile]一启用数据集以供使用：
   - [创建新数据集](#create-a-dataset-enabled-for-profile-and-identity)
   - [配置现有数据集](#configure-an-existing-dataset)
1. [将数据摄取到数据集中](#ingest-data-into-the-dataset)
1. [确认实时客户用户档案收集数据](#confirm-data-ingest-by-real-time-customer-profile)
1. [确认由Identity Service收录数据](#confirm-data-ingest-by-identity-service)

## 入门指南

本教程需要对管理启用数据集时涉及的各种Adobe Experience Platform服 [!DNL Profile]务进行有效了解。 在开始本教程之前，请查阅以下相关服务的 [!DNL Platform] 文档：

- [[!DNL实时客户用户档案]](../home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
- [[!DNL标识服务]](../../identity-service/home.md):通过将 [!DNL Real-time Customer Profile] 来自被引入的不同数据源的身份连接到其中，实现 [!DNL Platform]了。
- [[!DNL目录服务]](../../catalog/home.md):一个REST风格的API，它允许您创建数据集并为和配 [!DNL Real-time Customer Profile] 置它 [!DNL Identity Service]们。
- [[!DNL体验数据模型(XDM)]](../../xdm/home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。

以下各节提供了成功调用平台API所需了解的其他信息。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

- 授权：承载者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要附加标头：

- 内容类型：application/json

中的所有资源 [!DNL Experience Platform] 都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作所在沙箱的名称。 有关中沙箱的详细信 [!DNL Platform]息，请参阅 [沙箱概述文档](../../sandboxes/home.md)。

- x-sandbox-name: `{SANDBOX_NAME}`

## 创建启用和 [!DNL Profile] [!DNL Identity] {#create-a-dataset-enabled-for-profile-and-identity}

您可以在创建时或 [!DNL Real-time Customer Profile] 创 [!DNL Identity Service] 建数据集后的任何时刻为启用数据集。 如果要启用已创建的数据集，请按照以下步骤配置此文档 [后找到的现](#configure-an-existing-dataset) 有数据集。 要创建新数据集，您必须知道已启用实时模式的现有XDM用户档案的ID。 有关如何查找或创建启用用户档案的模式的信息，请参阅有关使用 [模式注册表API创建模式的教程](../../xdm/tutorials/create-schema-api.md)。 以下对API的调 [!DNL Catalog] 用为和启用 [!DNL Profile] 数据集 [!DNL Identity Service]。

**API格式**

```http
POST /dataSets
```

**请求**

通过在 `unifiedProfile` 请求 `unifiedIdentity` 体 `tags` 中包括和在请求体下，将立即启用 [!DNL Profile] 数据集 [!DNL Identity Service]和。 这些标记的值必须是包含字符串的数组 `"enabled:true"`。

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
| `schemaRef.id` | 数据集将 [!DNL Profile]基于的已启用模式的ID。 |
| `{TENANT_ID}` | 包含属于您 [!DNL Schema Registry] 的IMS组织的资源的命名空间。 有关详 [细信息](../../xdm/api/getting-started.md#know-your-tenant-id) ，请参 [!DNL Schema Registry] 阅开发人员指南的TENANT_ID部分。 |

**响应**

成功的响应以以下形式显示包含新创建数据集ID的数组 `"@/dataSets/{DATASET_ID}"`。 成功创建并启用数据集后，请继续执行上传数据 [的步骤](#upload-data-to-the-dataset)。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 配置现有数据集 {#configure-an-existing-dataset}

以下步骤介绍了如何为和启用以前创建的 [!DNL Real-time Customer Profile] 数据集 [!DNL Identity Service]。 如果已创建启用用户档案的数据集，请继续执行数据 [获取步骤](#ingest-data-into-the-dataset)。

### 检查数据集是否已启用 {#check-if-the-dataset-is-enabled}

使用 [!DNL Catalog] API，您可以检查现有数据集以确定它是否允许在和中使用 [!DNL Real-time Customer Profile][!DNL Identity Service]。 以下调用按ID检索数据集的详细信息。

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

在属 `tags` 性下，您可以看到 `unifiedProfile` 和 `unifiedIdentity` 都存在该值 `enabled:true`。 因此， [!DNL Real-time Customer Profile] 并 [!DNL Identity Service] 分别启用此数据集。

### 启用数据集 {#enable-the-dataset}

如果尚未为或启用现有数 [!DNL Profile] 据集 [!DNL Identity Service]，则可以通过使用数据集ID发出PATCH请求来启用它。

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

**响应**&#x200B;成功的PATCH请求返回HTTP状态200(OK)和包含更新数据集ID的数组。 此ID应与在PATCH请求中发送的ID匹配。 现在 `"unifiedProfile"` 已添 `"unifiedIdentity"` 加和标记，并且用户档案和标识服务启用了数据集。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 将数据摄取到数据集中 {#ingest-data-into-the-dataset}

XDM [!DNL Real-time Customer Profile] 数据 [!DNL Identity Service] 在被摄取到数据集中时，会同时消耗和消耗数据。 有关如何将数据上传到数据集的说明，请参阅教程 [中的“使用API创建数据集](../../catalog/datasets/create.md)”。 在规划要发送到启用数据集 [!DNL Profile]的数据时，请考虑以下最佳实践：

- 包括要用作受众段条件的任何数据。
- 根据您的用户档案数据包含尽可能多的标识符，以最大化您的标识图。 这可以更 [!DNL Identity Service] 有效地在数据集之间拼接身份。

## 确认数据摄取方式 [!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

首次将数据上传到新数据集时，或者作为涉及新ETL或数据源的流程的一部分，建议仔细检查数据，确保数据已按预期上传。 使用 [!DNL Real-time Customer Profile] Access API，您可以在批处理数据加载到数据集时检索它。 如果无法检索任何您期望的实体，则可能未启用您的数据集 [!DNL Real-time Customer Profile]。 确认已启用数据集后，请确保源数据格式和标识符支持您的预期。 有关如何使用API访问数 [!DNL Real-time Customer Profile] 据的详细说 [!DNL Profile] 明，请遵循实 [体端点指南](../api/entities.md)(也称为“[!DNL Profile Access] API”)。

## 确认由Identity Service收录数据 {#confirm-data-ingest-by-identity-service}

摄取的包含多个标识的每个数据片段会在您的专用标识图中创建一个链接。 有关标识图和访问标识数据的详细信息，请首先阅读Identity [Service概述](../../identity-service/home.md)。