---
keywords: Experience Platform；配置文件；实时客户配置文件；故障排除；API；启用数据集
title: 使用API为配置文件更新启用数据集
type: Tutorial
description: 本教程向您展示如何使用Adobe Experience Platform API启用具有“更新插入”功能的数据集，以更新实时客户个人资料数据。
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 6%

---

# 使用API为配置文件更新启用数据集

本教程介绍了如何启用具有“更新插入”功能的数据集以更新实时客户档案数据。 这包括创建新数据集和配置现有数据集的步骤。

>[!NOTE]
>
>本教程中描述的工作流仅适用于批量摄取。 有关流式摄取更新插入的信息，请参阅有关使用数据准备[&#128279;](../../data-prep/upserts.md)将部分行更新发送到实时客户个人资料的指南。

## 快速入门

本教程需要对管理启用了配置文件的数据集所涉及的几项Adobe Experience Platform服务有一定的了解。 在开始本教程之前，请查看以下相关[!DNL Experience Platform]服务的文档：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。
- [[!DNL Catalog Service]](../../catalog/home.md)： RESTful API，允许您为[!DNL Real-Time Customer Profile]和[!DNL Identity Service]创建数据集并配置它们。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
- [批量摄取](../../ingestion/batch-ingestion/overview.md)：批量摄取API允许您将数据作为批处理文件摄取到Experience Platform中。

以下部分提供了成功调用Experience Platform API所需了解的其他信息。

### 正在读取示例 API 调用

本教程提供了示例API调用来演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中有关[如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。

### 收集所需标头的值

要调用[!DNL Experience Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

包含有效负载(POST、PUT、PATCH)的所有请求都需要额外的`Content-Type`标头。 必要时，此标头的正确值会显示在示例请求中。

[!DNL Experience Platform]中的所有资源都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的所有请求都需要`x-sandbox-name`标头，用于指定将在其中执行操作的沙盒的名称。 有关[!DNL Experience Platform]中沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

## 创建为配置文件更新启用的数据集

创建新数据集时，可以为用户档案启用该数据集，并在创建时启用更新功能。

>[!NOTE]
>
>要创建新的启用配置文件的数据集，您必须知道为配置文件启用的现有XDM架构的ID。 有关如何查找或创建启用配置文件的架构的信息，请参阅关于使用架构注册表API [创建架构的教程](../../xdm/tutorials/create-schema-api.md)。

要创建为配置文件和更新启用的数据集，请使用对`/dataSets`端点的POST请求。

**API格式**

```http
POST /dataSets
```

**请求**

通过在请求正文中的`tags`下同时包含`unifiedIdentity`和`unifiedProfile`，将在创建时为[!DNL Profile]启用数据集。 在`unifiedProfile`数组中，添加`isUpsert:true`将使数据集能够支持更新。

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
| `schemaRef.id` | 数据集将基于启用了[!DNL Profile]的架构的ID。 |
| `{TENANT_ID}` | [!DNL Schema Registry]中包含属于您组织的资源的命名空间。 有关详细信息，请参阅[!DNL Schema Registry]开发人员指南的[TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id)部分。 |

**响应**

成功的响应显示了一个数组，该数组包含`"@/dataSets/{DATASET_ID}"`形式的新创建数据集的ID。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 配置现有数据集 {#configure-an-existing-dataset}

以下步骤介绍了如何为更新(upsert)功能配置现有的启用用户档案的数据集。

>[!NOTE]
>
>要为更新插入配置现有的启用配置文件的数据集，您必须先为配置文件禁用该数据集，然后随着`isUpsert`标记重新启用它。 如果没有为配置文件启用现有数据集，您可以直接进入[为配置文件启用数据集并更新插入](#enable-the-dataset)的步骤。 如果不确定，以下步骤会显示如何检查是否已启用数据集。

### 检查是否已为配置文件启用数据集

使用[!DNL Catalog] API，您可以检查现有数据集以确定是否已启用它以便在[!DNL Real-Time Customer Profile]中使用。 以下调用将按ID检索数据集的详细信息。

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

在`tags`属性下，您可以看到存在`unifiedProfile`，其值为`enabled:true`。 因此，已为此数据集启用[!DNL Real-Time Customer Profile]。

### 为配置文件禁用数据集

为了配置启用配置文件的数据集以进行更新，您必须首先禁用`unifiedProfile`和`unifiedIdentity`标记，然后随着`isUpsert`标记重新启用它们。 可使用两个PATCH请求来完成，一个用于禁用，另一个用于重新启用。

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

第一个PATCH请求正文包括`path`到`unifiedProfile`和`path`到`unifiedIdentity`，为这两个路径将`value`设置为`enabled:false`以禁用标记。

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

成功的PATCH请求会返回HTTP状态200 （正常）以及包含已更新数据集的ID的数组。 此ID应该与PATCH请求中发送的ID匹配。 `unifiedProfile`和`unifiedIdentity`标记现已禁用。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### 为配置文件启用数据集并更新插入 {#enable-the-dataset}

可以使用单个PATCH请求为现有数据集启用配置文件和属性更新。

>[!IMPORTANT]
>
>为配置文件启用数据集时，请确保数据集关联的架构也&#x200B;**启用了**&#x200B;配置文件。 如果架构未启用配置文件，则数据集&#x200B;**不会**&#x200B;在Experience Platform UI中显示为启用配置文件。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASET_ID}` | 要更新的数据集的ID。 |

**请求**

请求正文包括`path`到`unifiedProfile`设置`value`以包含`enabled`和`isUpsert`标记（两者均设置为`true`），以及`path`到`unifiedIdentity`设置`value`以包含`enabled`标记设置为`true`。

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

成功的PATCH请求会返回HTTP状态200 （正常）以及包含已更新数据集的ID的数组。 此ID应该与PATCH请求中发送的ID匹配。 `unifiedProfile`标记和`unifiedIdentity`标记现已启用并为属性更新进行了配置。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 后续步骤

批量摄取工作流现在可以使用您的用户档案和启用了更新插入的数据集来更新用户档案数据。 要了解有关将数据摄取到Adobe Experience Platform的更多信息，请从阅读[数据摄取概述](../../ingestion/home.md)开始。
