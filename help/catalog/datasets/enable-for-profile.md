---
keywords: Experience Platform；配置文件；实时客户配置文件；故障排除；API；启用数据集
title: 使用API为配置文件和Identity服务启用数据集
type: Tutorial
description: 本教程将演示如何使用Adobe Experience Platform API启用数据集以用于Real-time Customer Profile和Identity Service。
exl-id: a115e126-6775-466d-ad7e-ee36b0b8b49c
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 5%

---

# 使用API为[!DNL Profile]和[!DNL Identity Service]启用数据集

本教程介绍了启用数据集以在[!DNL Real-Time Customer Profile]和[!DNL Identity Service]中使用的过程，分为以下步骤：

1. 使用以下两个选项之一启用要在[!DNL Real-Time Customer Profile]中使用的数据集：
   - [创建新数据集](#create-a-dataset-enabled-for-profile-and-identity)
   - [配置现有数据集](#configure-an-existing-dataset)
1. [将数据摄取到数据集](#ingest-data-into-the-dataset)
1. [确认通过实时客户资料摄取数据](#confirm-data-ingest-by-real-time-customer-profile)
1. [确认身份服务摄取的数据](#confirm-data-ingest-by-identity-service)

## 快速入门

本教程需要对管理启用了配置文件的数据集所涉及的几项Adobe Experience Platform服务有一定的了解。 在开始本教程之前，请查看以下相关[!DNL Experience Platform]服务的文档：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。
- [[!DNL Identity Service]](../../identity-service/home.md)：通过桥接从被摄取到[!DNL Experience Platform]中的不同数据源的标识来启用[!DNL Real-Time Customer Profile]。
- [[!DNL Catalog Service]](../../catalog/home.md)： RESTful API，允许您为[!DNL Real-Time Customer Profile]和[!DNL Identity Service]创建数据集并配置它们。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。

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

## 创建为配置文件和身份启用的数据集 {#create-a-dataset-enabled-for-profile-and-identity}

您可以在创建数据集后立即或创建数据集后的任何时间点为Real-time Customer Profile和Identity Service启用数据集。 如果要启用已创建的数据集，请按照[配置此文档中稍后找到的现有数据集](#configure-an-existing-dataset)的步骤操作。

>[!NOTE]
>
>要创建新的启用配置文件的数据集，您必须知道为配置文件启用的现有XDM架构的ID。 有关如何查找或创建启用配置文件的架构的信息，请参阅关于使用架构注册表API [创建架构的教程](../../xdm/tutorials/create-schema-api.md)。

要创建为配置文件启用的数据集，您可以使用POST请求到`/dataSets`端点。

**API格式**

```http
POST /dataSets
```

**请求**

通过在请求正文中的`tags`下包含`unifiedProfile`和`unifiedIdentity`，将分别立即为[!DNL Profile]和[!DNL Identity Service]启用数据集。 这些标记的值必须是包含字符串`"enabled:true"`的数组。

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
| `schemaRef.id` | 数据集将基于启用了[!DNL Profile]的架构的ID。 |
| `{TENANT_ID}` | [!DNL Schema Registry]中包含属于您组织的资源的命名空间。 有关详细信息，请参阅[!DNL Schema Registry]开发人员指南的[TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id)部分。 |

**响应**

成功的响应显示了一个数组，该数组包含`"@/dataSets/{DATASET_ID}"`形式的新创建数据集的ID。 成功创建并启用数据集后，请继续执行[上传数据](#upload-data-to-the-dataset)的步骤。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 配置现有数据集 {#configure-an-existing-dataset}

以下步骤介绍了如何为[!DNL Real-Time Customer Profile]和[!DNL Identity Service]启用之前创建的数据集。 如果您已经创建了启用配置文件的数据集，请继续执行[摄取数据](#ingest-data-into-the-dataset)的步骤。

### 检查数据集是否已启用 {#check-if-the-dataset-is-enabled}

使用[!DNL Catalog] API，您可以检查现有数据集以确定是否已启用它以便在[!DNL Real-Time Customer Profile]和[!DNL Identity Service]中使用。 以下调用将按ID检索数据集的详细信息。

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
        "files": "@/dataSetFiles?dataSetId=5b020a27e7040801dedbf46e",
        "schema": "@/xdms/context/experienceevent",
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

在`tags`属性下，您可以看到`unifiedProfile`和`unifiedIdentity`都存在，且值为`enabled:true`。 因此，已为此数据集分别启用[!DNL Real-Time Customer Profile]和[!DNL Identity Service]。

### 启用数据集 {#enable-the-dataset}

如果尚未为[!DNL Profile]或[!DNL Identity Service]启用现有数据集，则可以通过使用该数据集ID发出PATCH请求来启用它。

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

请求正文包含`path`到两种类型的标记： `unifiedProfile`和`unifiedIdentity`。 每个的`value`都是包含字符串`enabled:true`的数组。

**响应**

成功的PATCH请求会返回HTTP状态200 （正常）以及包含已更新数据集的ID的数组。 此ID应该与PATCH请求中发送的ID匹配。 `unifiedProfile`和`unifiedIdentity`标记现已添加，并且数据集已允许配置文件和身份服务使用。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 将数据摄取到数据集 {#ingest-data-into-the-dataset}

[!DNL Real-Time Customer Profile]和[!DNL Identity Service]都使用XDM数据，因为它正在被摄取到数据集中。 有关如何将数据上载到数据集的说明，请参阅有关[使用API创建数据集](../../catalog/datasets/create.md)的教程。 在计划向启用了[!DNL Profile]的数据集发送哪些数据时，请考虑以下最佳实践：

- 包括要用作分段标准的任何数据。
- 包括可从配置文件数据中确定的任意数量的标识符，以最大化您的身份图。 这允许[!DNL Identity Service]更有效地跨数据集拼合身份。

## 确认[!DNL Real-Time Customer Profile]摄取的数据 {#confirm-data-ingest-by-real-time-customer-profile}

首次将数据上载到新数据集时，或者作为涉及新ETL或数据源的流程的一部分，建议仔细检查数据，以确保数据已按预期上载。 使用[!DNL Real-Time Customer Profile]访问API，您可以在批次数据加载到数据集时检索批次数据。 如果无法检索任何预期的实体，则可能无法为[!DNL Real-Time Customer Profile]启用数据集。 确认已启用数据集后，请确保源数据格式和标识符支持您的期望。 有关如何使用[!DNL Real-Time Customer Profile] API访问[!DNL Profile]数据的详细说明，请参阅[实体端点指南](../../profile/api/entities.md)，也称为“[!DNL Profile Access]”API。

## 确认由Identity服务摄取数据 {#confirm-data-ingest-by-identity-service}

摄取的每个包含多个身份的数据片段都会在专用身份图中创建链接。 有关身份图形和访问身份数据的详细信息，请先阅读[身份服务概述](../../identity-service/home.md)。
