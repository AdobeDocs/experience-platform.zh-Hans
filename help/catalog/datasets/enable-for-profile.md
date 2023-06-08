---
keywords: Experience Platform；配置文件；实时客户配置文件；故障排除；API；启用数据集
title: 使用API为配置文件和身份服务启用数据集
type: Tutorial
description: 本教程向您展示了如何使用Adobe Experience Platform API启用数据集以用于Real-time Customer Profile和Identity Service。
exl-id: a115e126-6775-466d-ad7e-ee36b0b8b49c
source-git-commit: 2226b1878ef3398554b6cf96ff400cc1767a9e4c
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 1%

---

# 为以下项启用数据集 [!DNL Profile] 和 [!DNL Identity Service] 使用API

本教程介绍了启用数据集以供在中使用的过程 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service]，可细分为以下步骤：

1. 启用数据集以用于中 [!DNL Real-Time Customer Profile]，使用以下两个选项之一：
   - [创建新数据集](#create-a-dataset-enabled-for-profile-and-identity)
   - [配置现有数据集](#configure-an-existing-dataset)
1. [将数据摄取到数据集](#ingest-data-into-the-dataset)
1. [确认通过实时客户资料摄取数据](#confirm-data-ingest-by-real-time-customer-profile)
1. [确认由Identity Service引入的数据](#confirm-data-ingest-by-identity-service)

## 快速入门

要阅读本教程，您需要深入了解管理启用了配置文件的数据集所包含的多项Adobe Experience Platform服务。 在开始本教程之前，请查看相关文档 [!DNL Platform] 服务：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
- [[!DNL Identity Service]](../../identity-service/home.md)：启用 [!DNL Real-Time Customer Profile] 通过桥接来自被摄取到的不同数据源的身份 [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md)：一个RESTful API，允许您为创建数据集并配置数据集 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Platform] 组织客户体验数据。

以下部分提供了成功调用Platform API时需要了解的其他信息。

### 正在读取示例API调用

本教程提供了示例API调用来演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将提供所有中所有所需标头的值 [!DNL Experience Platform] API调用，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

包含有效负载(POST、PUT、PATCH)的所有请求都需要一个额外的 `Content-Type` 标头。 必要时，此标头的正确值会显示在示例请求中。

中的所有资源 [!DNL Experience Platform] 与特定的虚拟沙盒隔离。 的所有请求 [!DNL Platform] API需要 `x-sandbox-name` 头，指定将在其中执行操作的沙盒的名称。 有关中沙箱的详细信息 [!DNL Platform]，请参见 [沙盒概述文档](../../sandboxes/home.md).

## 创建启用配置文件和标识的数据集 {#create-a-dataset-enabled-for-profile-and-identity}

您可以在创建数据集后立即或创建数据集后的任何时候为Real-time Customer Profile和Identity Service启用数据集。 如果要启用已创建的数据集，请按照 [配置现有数据集](#configure-an-existing-dataset) 可在本文档的后文中找到。

>[!NOTE]
>
>要创建新的启用配置文件的数据集，您必须知道为配置文件启用的现有XDM架构的ID。 有关如何查找或创建启用配置文件的架构的信息，请参阅以下教程： [使用架构注册表API创建架构](../../xdm/tutorials/create-schema-api.md).

要创建为配置文件启用的数据集，您可以使用POST请求 `/dataSets` 端点。

**API格式**

```http
POST /dataSets
```

**请求**

通过包含 `unifiedProfile` 和 `unifiedIdentity` 下 `tags` 在请求正文中，数据集将立即启用 [!DNL Profile] 和 [!DNL Identity Service]，则不会显示任何内容。 这些标记的值必须是包含字符串的数组 `"enabled:true"`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
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
| `schemaRef.id` | 的ID [!DNL Profile]启用数据集所基于的架构。 |
| `{TENANT_ID}` | 中的命名空间 [!DNL Schema Registry] ，其中包含属于您组织的资源。 请参阅 [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) 部分 [!DNL Schema Registry] 开发人员指南，以了解更多信息。 |

**响应**

成功的响应会显示一个数组，其中包含新创建的数据集的ID，其形式为 `"@/dataSets/{DATASET_ID}"`. 成功创建并启用数据集后，请继续执行以下操作的步骤 [上传数据](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 配置现有数据集 {#configure-an-existing-dataset}

以下步骤介绍了如何为启用之前创建的数据集 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service]. 如果您已创建启用了配置文件的数据集，请继续执行以下操作的步骤： [正在引入数据](#ingest-data-into-the-dataset).

### 检查数据集是否已启用 {#check-if-the-dataset-is-enabled}

使用 [!DNL Catalog] API时，您可以检查现有数据集以确定是否已启用它以便在中使用 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service]. 以下调用按ID检索数据集的详细信息。

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
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "5b020a27e7040801dedbf46f",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "@/xdms/context/experienceevent",
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

在 `tags` 属性，您可以看到 `unifiedProfile` 和 `unifiedIdentity` 同时存在值 `enabled:true`. 因此， [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service] 分别为此数据集启用。

### 启用数据集 {#enable-the-dataset}

如果尚未为以下项启用现有数据集 [!DNL Profile] 或 [!DNL Identity Service]，则可以使用数据集ID发出PATCH请求来启用它。

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

请求正文包括 `path` 两种类型的标记， `unifiedProfile` 和 `unifiedIdentity`. 此 `value` 个是包含字符串的数组 `enabled:true`.

**响应**

成功的PATCH请求会返回HTTP状态200 （正常）和一个包含已更新数据集ID的数组。 此ID应与PATCH请求中发送的ID匹配。 此 `unifiedProfile` 和 `unifiedIdentity` 现在添加了标记，并启用数据集以供Profile和Identity服务使用。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 将数据摄取到数据集 {#ingest-data-into-the-dataset}

两者 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service] 在将XDM数据摄取到数据集中时使用。 有关如何将数据上传到数据集的说明，请参阅关于的教程 [使用API创建数据集](../../catalog/datasets/create.md). 在计划向贵机构发送哪些数据时 [!DNL Profile]启用数据集时，请考虑以下最佳实践：

- 包含要用作分段标准的任何数据。
- 包括可从配置文件数据中确定的任意数量的标识符，以最大化您的身份图。 这允许 [!DNL Identity Service] 更有效地拼合数据集之间的身份。

## 确认数据摄取方式 [!DNL Real-Time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

首次将数据上载到新数据集时，或作为涉及新ETL或数据源的流程的一部分，建议仔细检查数据，以确保已按预期上载数据。 使用 [!DNL Real-Time Customer Profile] 访问API，您可以在批量数据加载到数据集时检索该数据。 如果您无法检索任何预期的实体，则您的数据集可能未启用 [!DNL Real-Time Customer Profile]. 确认已启用数据集后，请确保源数据格式和标识符支持您的预期。 有关如何使用 [!DNL Real-Time Customer Profile] 用于访问的API [!DNL Profile] 有关数据，请参阅 [实体端点指南](../../profile/api/entities.md)，也称为“[!DNL Profile Access]&quot; API.

## 确认由Identity Service引入的数据 {#confirm-data-ingest-by-identity-service}

摄取的每个包含多个身份的数据片段都会在专用身份图中创建链接。 有关身份图形和访问身份数据的更多信息，请首先阅读 [Identity服务概述](../../identity-service/home.md).
