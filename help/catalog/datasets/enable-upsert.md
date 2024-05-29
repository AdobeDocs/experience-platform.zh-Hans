---
keywords: Experience Platform；配置文件；实时客户配置文件；故障排除；API；启用数据集
title: 使用API为配置文件更新启用数据集
type: Tutorial
description: 本教程向您展示如何使用Adobe Experience Platform API启用具有“更新插入”功能的数据集，以更新实时客户个人资料数据。
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 6%

---

# 使用API为配置文件更新启用数据集

本教程介绍了如何启用具有“更新插入”功能的数据集以更新实时客户档案数据。 这包括创建新数据集和配置现有数据集的步骤。

>[!NOTE]
>
>本教程中描述的工作流仅适用于批量摄取。 有关流式摄取更新插件的信息，请参阅上的指南 [使用数据准备将部分行更新发送到实时客户个人资料](../../data-prep/upserts.md).

## 快速入门

本教程需要对管理启用了配置文件的数据集所涉及的几项Adobe Experience Platform服务有一定的了解。 在开始本教程之前，请查看相关文档 [!DNL Platform] 服务：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
- [[!DNL Catalog Service]](../../catalog/home.md)：一个RESTful API，允许您为创建数据集并配置它们 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Platform] 组织客户体验数据。
- [批量摄取](../../ingestion/batch-ingestion/overview.md)：批量摄取API允许您将数据作为批处理文件摄取到Experience Platform中。

以下部分提供了成功调用Platform API所需了解的其他信息。

### 正在读取示例 API 调用

本教程提供了示例API调用来演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关文档中用于示例API调用的惯例的信息，请参阅 [如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标头的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

所有包含有效负载(POST、PUT、PATCH)的请求都需要一个额外的 `Content-Type` 标题。 必要时，此标头的正确值会显示在示例请求中。

中的所有资源 [!DNL Experience Platform] 被隔离到特定的虚拟沙盒中。 所有请求 [!DNL Platform] API需要 `x-sandbox-name` 用于指定在其中执行操作的沙盒的名称的标头。 有关中沙箱的详细信息 [!DNL Platform]，请参见 [沙盒概述文档](../../sandboxes/home.md).

## 创建为配置文件更新启用的数据集

创建新数据集时，可以为用户档案启用该数据集，并在创建时启用更新功能。

>[!NOTE]
>
>要创建新的启用配置文件的数据集，您必须知道为配置文件启用的现有XDM架构的ID。 有关如何查找或创建启用配置文件的架构的信息，请参阅关于的教程 [使用架构注册表API创建架构](../../xdm/tutorials/create-schema-api.md).

要创建为配置文件和更新启用的数据集，请使用POST请求 `/dataSets` 端点。

**API格式**

```http
POST /dataSets
```

**请求**

通过同时包含 `unifiedIdentity` 和 `unifiedProfile` 下 `tags` 在请求正文中，将启用数据集 [!DNL Profile] 创建时。 在 `unifiedProfile` 数组，添加 `isUpsert:true` 将添加数据集支持更新的功能。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Sample dataset",
        "description: "A sample dataset with a sample description.",
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
| `schemaRef.id` | 的ID [!DNL Profile]启用数据集的架构。 |
| `{TENANT_ID}` | 中的命名空间 [!DNL Schema Registry] ，其中包含属于您组织的资源。 请参阅 [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) 的部分 [!DNL Schema Registry] 开发人员指南，以了解更多信息。 |

**响应**

成功的响应会显示一个数组，其中包含以形式新建的数据集的ID `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 配置现有数据集 {#configure-an-existing-dataset}

以下步骤介绍了如何为更新(upsert)功能配置现有的启用用户档案的数据集。

>[!NOTE]
>
>要为更新插入配置现有的启用配置文件的数据集，您必须先为配置文件禁用该数据集，然后随着 `isUpsert` 标记之前。 如果没有为配置文件启用现有数据集，您可以直接执行的步骤 [为配置文件和更新插入启用数据集](#enable-the-dataset). 如果不确定，以下步骤会显示如何检查是否已启用数据集。

### 检查是否已为配置文件启用数据集

使用 [!DNL Catalog] API时，您可以检查现有数据集以确定是否在中启用它 [!DNL Real-Time Customer Profile]. 以下调用将按ID检索数据集的详细信息。

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
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "{VIEW_ID}",
        "files": "@/dataSetFiles?dataSetId=5b020a27e7040801dedbf46e",
        "schema": "{SCHEMA}",
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

在 `tags` 属性，您可以看到 `unifiedProfile` 与值同时存在 `enabled:true`. 因此， [!DNL Real-Time Customer Profile] 已为此数据集启用。

### 为配置文件禁用数据集

为了配置支持配置文件的数据集以进行更新，您必须首先禁用 `unifiedProfile` 和 `unifiedIdentity` 标记，然后在页面的 `isUpsert` 标记之前。 可使用两个PATCH请求完成此操作，一个用于禁用，另一个用于重新启用。

>[!WARNING]
>
>在禁用数据时摄取到数据集中的数据将不会摄取到配置文件存储中。 在为配置文件重新启用数据之前，您应该避免将数据摄取到数据集中。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASET_ID}` | 要更新的数据集的ID。 |

**请求**

第一PATCH请求正文包括 `path` 到 `unifiedProfile` 和 `path` 到 `unifiedIdentity`，设置 `value` 到 `enabled:false` 以禁用标记。

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

成功的PATCH请求会返回HTTP状态200 （正常）以及包含已更新数据集的ID的数组。 此ID应该与PATCH请求中发送的ID匹配。 此 `unifiedProfile` 和 `unifiedIdentity` 现已禁用标记。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### 为配置文件启用数据集并更新插入 {#enable-the-dataset}

可以使用单个PATCH请求为现有数据集启用配置文件和属性更新。

>[!IMPORTANT]
>
>为配置文件启用数据集时，请确保与该数据集关联的架构是 **另外** 启用配置文件。 如果架构未启用配置文件，则数据集将 **非** 在Platform UI中显示为启用配置文件。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASET_ID}` | 要更新的数据集的ID。 |

**请求**

请求正文包括 `path` 到 `unifiedProfile` 设置 `value` 以包含 `enabled` 和 `isUpsert` 标记，均设置为 `true`，和 `path` 到 `unifiedIdentity` 设置 `value` 以包含 `enabled` 标记设置为 `true`.

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

成功的PATCH请求会返回HTTP状态200 （正常）以及包含已更新数据集的ID的数组。 此ID应该与PATCH请求中发送的ID匹配。 此 `unifiedProfile` 标记和 `unifiedIdentity` 标记现在已启用并配置为属性更新。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 后续步骤

批量摄取工作流现在可以使用您的用户档案和启用了更新插入的数据集来更新用户档案数据。 要了解有关将数据摄取到Adobe Experience Platform的更多信息，请先阅读 [数据摄取概述](../../ingestion/home.md).
