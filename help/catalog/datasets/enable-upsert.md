---
keywords: Experience Platform；配置文件；实时客户配置文件；故障诊断；API；启用数据集
title: 使用API为配置文件更新启用数据集
type: Tutorial
description: 本教程将向您演示如何使用Adobe Experience Platform API启用具有“插入”功能的数据集，以便更新实时客户资料数据。
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: 5bd3e43e6b307cc1527e8734936c051fb4fc89c4
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 1%

---

# 使用API为配置文件更新启用数据集

本教程介绍如何启用具有“更新”功能的数据集，以便更新实时客户资料数据。 这包括创建新数据集和配置现有数据集的步骤。

>[!NOTE]
>
>新插入工作流仅适用于批量摄取。 流式摄取是 **not** 受支持。

## 快速入门

本教程需要对管理启用了用户档案的数据集时涉及的多项Adobe Experience Platform服务有一定的了解。 在开始本教程之前，请查阅这些相关文档 [!DNL Platform] 服务：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
- [[!DNL Catalog Service]](../../catalog/home.md):一个RESTful API，允许您创建数据集并为 [!DNL Real-time Customer Profile] 和 [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):标准化框架， [!DNL Platform] 组织客户体验数据。
- [批量摄取](../../ingestion/batch-ingestion/overview.md):批量摄取API允许您将数据作为批处理文件导入到Experience Platform中。

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

## 创建为配置文件更新启用的数据集

创建新数据集时，您可以为配置文件启用该数据集，并在创建时启用更新功能。

>[!NOTE]
>
>要创建新的启用了“配置文件”的数据集，您必须知道已为“配置文件”启用的现有XDM架构的ID。 有关如何查找或创建启用了用户档案的架构的信息，请参阅 [使用模式注册表API创建模式](../../xdm/tutorials/create-schema-api.md).

要创建为配置文件和更新启用的POST集，请使用 `/dataSets` 端点。

**API格式**

```http
POST /dataSets
```

**请求**

通过将 `unifiedIdentity` 和 `unifiedProfile` 在 `tags` 在请求正文中，将为 [!DNL Profile] 创建时。 在 `unifiedProfile` 数组，添加 `isUpsert:true` 将添加数据集支持更新的功能。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "fields": [],
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags": {
            "unifiedIdentity": [
                "enabled: true"
            ],
            "unifiedProfile": [
                "enabled: true",
                "isUpsert: true"
            ]
        }
      }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `schemaRef.id` | 的ID [!DNL Profile]启用了数据集所基于的架构。 |
| `{TENANT_ID}` | 中的命名空间 [!DNL Schema Registry] 其中包含属于贵组织的资源。 请参阅 [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) 部分 [!DNL Schema Registry] 开发人员指南以了解更多信息。 |

**响应**

成功响应会显示一个数组，其中包含以下形式新创建数据集的ID: `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 配置现有数据集 {#configure-an-existing-dataset}

以下步骤介绍如何配置现有启用了“配置文件”的数据集，以便进行更新（插入）功能。

>[!NOTE]
>
>要配置现有启用了“配置文件”的数据集以进行重新插入，您必须先禁用“配置文件”的数据集，然后在 `isUpsert` 标记。 如果未为“配置文件”启用现有数据集，则可以直接继续执行 [启用“配置文件”数据集并重新插入](#enable-the-dataset). 如果不确定，以下步骤将向您显示如何检查数据集是否已启用。

### 检查数据集是否已为“配置文件”启用

使用 [!DNL Catalog] API中，您可以检查现有数据集以确定它是否已启用以供在中使用 [!DNL Real-time Customer Profile]. 以下调用按ID检索数据集的详细信息。

**API格式**

```http
GET /dataSets/{DATASET_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASET_ID}` | 要检查的数据集的ID。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "{DATASET_NAME}",
        "imsOrg": "{ORG_ID}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ],
            "unifiedProfile": [
                "enabled:true"
            ]
        },
        "lastBatchId": "{BATCH_ID}",
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
        "viewId": "{VIEW_ID}",
        "status": "enabled",
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "{SCHEMA}",
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

在 `tags` 属性，您可以看到 `unifiedProfile` 值存在 `enabled:true`. 因此， [!DNL Real-time Customer Profile] 已为此数据集启用。

### 禁用配置文件的数据集

要配置启用了“配置文件”的数据集进行更新，您必须首先禁用 `unifiedProfile` 和 `unifiedIdentity` 标记，然后在 `isUpsert` 标记。 可使用两个PATCH请求完成此操作，一个用于禁用，另一个用于重新启用。

>[!WARNING]
>
>禁用时摄取到数据集的数据将不会摄取到配置文件存储中。 在为“配置文件”重新启用数据之前，应避免将数据摄取到数据集中。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASET_ID}` | 要更新的数据集的ID。 |

**请求**

第一PATCH请求正文包括 `path` to `unifiedProfile` 和 `path` to `unifiedIdentity`，设置 `value` to `enabled:false` ，以便禁用标记。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { 
            "op": "replace", 
            "path": "/tags/unifiedProfile", 
            "value": ["enabled:false"] 
        },
        {
            "op": "replace",
            "path": "/tags/unifiedIdentity",
            "value": ["enabled:false"]
        }
      ]'
```

**响应**

成功的PATCH请求会返回HTTP状态200（确定）和一个包含已更新数据集ID的数组。 此ID应与在PATCH请求中发送的ID匹配。 的 `unifiedProfile` 和 `unifiedIdentity` 标记现已禁用。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### 为配置文件启用数据集并重新插入 {#enable-the-dataset}

可以使用单个数据集请求为配置文件和属性更新启用现有PATCH。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASET_ID}` | 要更新的数据集的ID。 |

**请求**

请求正文包括 `path` to `unifiedProfile` 设置 `value` 包含 `enabled` 和 `isUpsert` 标记，均设置为 `true`和 `path` to `unifiedIdentity` 设置 `value` 包含 `enabled` 标记设置为 `true`.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { 
            "op": "add", 
            "path": "/tags/unifiedProfile", 
            "value": [
                "enabled:true",
                "isUpsert:true"
            ] 
        },
        {
            "op": "add",
            "path": "/tags/unifiedIdentity",
            "value": [
                "enabled:true"
            ]
        }
      ]'
```

**响应**

成功的PATCH请求会返回HTTP状态200（确定）和一个包含已更新数据集ID的数组。 此ID应与在PATCH请求中发送的ID匹配。 的 `unifiedProfile` 标记和 `unifiedIdentity` 标记现已启用并配置，用于属性更新。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 后续步骤

现在，批量摄取工作流可以使用您的配置文件和启用了更新的数据集来更新配置文件数据。 要了解有关将数据摄取到Adobe Experience Platform的更多信息，请首先阅读 [数据摄取概述](../../ingestion/home.md).
