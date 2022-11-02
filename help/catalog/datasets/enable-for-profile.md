---
keywords: Experience Platform；配置文件；实时客户配置文件；故障诊断；API；启用数据集
title: 使用API为配置文件和Identity服务启用数据集
type: Tutorial
description: 本教程将向您展示如何使用Adobe Experience Platform API启用数据集，以便与实时客户资料和Identity Service结合使用。
exl-id: a115e126-6775-466d-ad7e-ee36b0b8b49c
source-git-commit: 132407af947b97a1925799a1fb5e12caa2b0410c
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 1%

---

# 为 [!DNL Profile] 和 [!DNL Identity Service] 使用API

本教程介绍如何启用数据集以供在中使用 [!DNL Real-time Customer Profile] 和 [!DNL Identity Service]，分为以下步骤：

1. 启用数据集以在中使用 [!DNL Real-time Customer Profile]，使用以下两个选项之一：
   - [创建新数据集](#create-a-dataset-enabled-for-profile-and-identity)
   - [配置现有数据集](#configure-an-existing-dataset)
1. [将数据摄取到数据集中](#ingest-data-into-the-dataset)
1. [通过实时客户资料确认数据摄取](#confirm-data-ingest-by-real-time-customer-profile)
1. [确认由Identity服务摄取数据](#confirm-data-ingest-by-identity-service)

## 快速入门

本教程需要对管理启用了用户档案的数据集时涉及的多项Adobe Experience Platform服务有一定的了解。 在开始本教程之前，请查阅这些相关文档 [!DNL Platform] 服务：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
- [[!DNL Identity Service]](../../identity-service/home.md):启用 [!DNL Real-time Customer Profile] 通过将来自不同数据源的身份桥接到 [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md):一个RESTful API，允许您创建数据集并为 [!DNL Real-time Customer Profile] 和 [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):标准化框架， [!DNL Platform] 组织客户体验数据。

以下部分提供了成功调用平台API所需了解的其他信息。

### 读取示例API调用

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

所有包含有效负载(POST、PUT、PATCH)的请求都需要附加 `Content-Type` 标题。 如有必要，此标头的正确值会显示在示例请求中。

中的所有资源 [!DNL Experience Platform] 与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要 `x-sandbox-name` 用于指定操作将在其中进行的沙盒名称的标头。 有关 [!DNL Platform]，请参阅 [沙盒概述文档](../../sandboxes/home.md).

## 创建为“配置文件和身份”启用的数据集 {#create-a-dataset-enabled-for-profile-and-identity}

您可以在创建时立即或在创建数据集后的任何时间点为实时客户配置文件和Identity服务启用数据集。 如果要启用已创建的数据集，请按照 [配置现有数据集](#configure-an-existing-dataset) 在本文档的后面部分找到。

>[!NOTE]
>
>要创建新的启用了“配置文件”的数据集，您必须知道已为“配置文件”启用的现有XDM架构的ID。 有关如何查找或创建启用了用户档案的架构的信息，请参阅 [使用模式注册表API创建模式](../../xdm/tutorials/create-schema-api.md).

要创建为“配置文件”启用的POST集，您可以使用 `/dataSets` 端点。

**API格式**

```http
POST /dataSets
```

**请求**

包括 `unifiedProfile` 和 `unifiedIdentity` 在 `tags` 在请求正文中，将立即为 [!DNL Profile] 和 [!DNL Identity Service]，分别为。 这些标记的值必须是包含字符串的数组 `"enabled:true"`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields":[],
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
    },
    "tags": {
       "unifiedProfile": ["enabled:true"],
       "unifiedIdentity": ["enabled:true"]
    }
  }'
```

| 属性 | 描述 |
|---|---|
| `schemaRef.id` | 的ID [!DNL Profile]启用了数据集所基于的架构。 |
| `{TENANT_ID}` | 中的命名空间 [!DNL Schema Registry] 其中包含属于您的IMS组织的资源。 请参阅 [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) 部分 [!DNL Schema Registry] 开发人员指南以了解更多信息。 |

**响应**

成功响应会显示一个数组，其中包含以下形式新创建数据集的ID: `"@/dataSets/{DATASET_ID}"`. 成功创建并启用数据集后，请继续执行 [上载数据](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 配置现有数据集 {#configure-an-existing-dataset}

以下步骤介绍如何为启用之前创建的数据集 [!DNL Real-time Customer Profile] 和 [!DNL Identity Service]. 如果已创建启用了用户档案的数据集，请继续执行 [摄取数据](#ingest-data-into-the-dataset).

### 检查数据集是否已启用 {#check-if-the-dataset-is-enabled}

使用 [!DNL Catalog] API中，您可以检查现有数据集以确定它是否已启用以供在中使用 [!DNL Real-time Customer Profile] 和 [!DNL Identity Service]. 以下调用按ID检索数据集的详细信息。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "Commission Program Events DataSet",
        "imsOrg": "{ORG_ID}",
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
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "@/xdms/context/experienceevent",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

在 `tags` 属性，您可以看到 `unifiedProfile` 和 `unifiedIdentity` 都与值一起存在 `enabled:true`. 因此， [!DNL Real-time Customer Profile] 和 [!DNL Identity Service] 已分别为此数据集启用。

### 启用数据集 {#enable-the-dataset}

如果未为 [!DNL Profile] 或 [!DNL Identity Service]，则可以通过使用数据集ID发出PATCH请求来启用它。

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
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true"] },
        { "op": "add", "path": "/tags/unifiedIdentity", "value": ["enabled:true"] } 
      ]'
```

请求正文包括 `path` 到两种类型的标记， `unifiedProfile` 和 `unifiedIdentity`. 的 `value` 每个都是包含字符串的数组 `enabled:true`.

**响应**
成功的PATCH请求会返回HTTP状态200（确定）和一个包含已更新数据集ID的数组。 此ID应与在PATCH请求中发送的ID匹配。 的 `unifiedProfile` 和 `unifiedIdentity` 标记现已添加，并且数据集已启用以供配置文件和Identity服务使用。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 将数据摄取到数据集中 {#ingest-data-into-the-dataset}

两者兼有 [!DNL Real-time Customer Profile] 和 [!DNL Identity Service] 在将XDM数据摄取到数据集时使用XDM数据。 有关如何将数据上载到数据集的说明，请参阅 [使用API创建数据集](../../catalog/datasets/create.md). 规划要发送给您的 [!DNL Profile]启用的数据集，请考虑以下最佳实践：

- 包括要用作分段标准的任何数据。
- 根据用户档案数据确定的尽可能多的标识符，以最大化身份图。 这允许 [!DNL Identity Service] 更有效地跨数据集拼合身份。

## 确认数据摄取方式 [!DNL Real-time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

首次将数据上传到新数据集时，或在涉及新ETL或数据源的流程中，建议仔细检查数据，以确保数据已按预期上传。 使用 [!DNL Real-time Customer Profile] 访问API时，您可以在批量数据加载到数据集中时对其进行检索。 如果无法检索您期望的任何实体，则可能未为 [!DNL Real-time Customer Profile]. 确认您的数据集已启用后，请确保源数据格式和标识符支持您的预期。 有关如何使用 [!DNL Real-time Customer Profile] 用于访问的API [!DNL Profile] 数据，请参阅 [entities endpoint指南](../../profile/api/entities.md)，也称为“[!DNL Profile Access]&quot; API.

## 确认由Identity服务摄取数据 {#confirm-data-ingest-by-identity-service}

摄取的每个包含多个身份的数据片段会在您的专用身份图中创建一个链接。 有关身份图和访问身份数据的更多信息，请首先阅读 [Identity Service概述](../../identity-service/home.md).
