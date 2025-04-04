---
keywords: Experience Platform；主页；热门主题；数据集；数据集；创建数据集；创建数据集
solution: Experience Platform
title: 使用API创建数据集
description: 本文档提供了使用Adobe Experience Platform API创建数据集以及使用文件填充数据集的一般步骤。
exl-id: 3a5f48cf-ad05-4b9e-be1d-ff213a26a477
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1302'
ht-degree: 6%

---

# 使用API创建数据集

本文档提供了使用Adobe Experience Platform API创建数据集以及使用文件填充数据集的一般步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [批量摄取](../../ingestion/batch-ingestion/overview.md)： [!DNL Experience Platform]允许您将数据作为批处理文件摄取。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
* [[!DNL Sandboxes]](../../sandboxes/home.md)： [!DNL Experience Platform]提供了将单个[!DNL Experience Platform]实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

以下部分提供了成功调用[!DNL Experience Platform] API所需了解的其他信息。

### 正在读取示例 API 调用

本教程提供了示例API调用来演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中有关[如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。

### 收集所需标头的值

要调用[!DNL Experience Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

[!DNL Experience Platform]中的所有资源都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Experience Platform]中沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

包含有效负载(POST、PUT、PATCH)的所有请求都需要额外的`Content-Type: application/json`标头。 对于JSON+PATCH请求，`Content-Type`应为`application/json-patch+json`。

## 教程

要创建数据集，必须首先定义架构。 架构是一组用于帮助表示数据的规则。 除了描述数据结构之外，模式还提供了约束和期望，可以应用这些约束和期望来验证系统之间的数据移动。

这些标准定义允许以一致的方式解释数据，而不管数据来自何处，并且消除跨应用程序翻译的需要。 有关组合架构的更多信息，请参阅架构组合基础[指南](../../xdm/schema/composition.md)

## 查找数据集架构

本教程从[架构注册API教程](../../xdm/tutorials/create-schema-api.md)结束处开始，并利用在该教程中创建的忠诚度会员架构。

如果您尚未完成[!DNL Schema Registry]教程，请从此处开始，然后仅在编写完必要的架构后继续此数据集教程。

以下调用可用于查看您在[!DNL Schema Registry] API教程中创建的忠诚度成员架构：

**API格式**

```HTTP
GET /tenant/schemas/{schema meta:altId or URL encoded $id URI}
```

**请求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应对象的格式取决于请求中发送的“接受”标头。 此响应中的各个属性已最小化以节省空间。

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "properties": {
        "repositoryCreatedBy": {},
        "repositoryLastModifiedBy": {},
        "createdByBatchID": {},
        "modifiedByBatchID": {},
        "_repo": {},
        "identityMap": {},
        "_id": {},
        "timeSeriesEvents": {},
        "person": {},
        "homeAddress": {},
        "personalEmail": {},
        "homePhone": {},
        "mobilePhone": {},
        "faxPhone": {},
        "_{TENANT_ID}": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "loyalty": {
                    "title": "Loyalty",
                    "description": "Loyalty Info",
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "loyaltyPoints": {
                            "title": "Loyalty Points",
                            "type": "integer",
                            "description": "Loyalty points total.",
                            "meta:xdmType": "int"
                        },
                        "memberSince": {
                            "title": "Member Since",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined the Loyalty Program.",
                            "meta:xdmType": "date-time"
                        }
                    }
                }
            }
        }
    },
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.4",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551843052271,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## 创建数据集

在忠诚度成员架构就绪后，您现在可以创建引用该架构的数据集。

**API格式**

```HTTP
POST /dataSets
```

**请求**

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| 属性 | 描述 |
| --- | --- |
| `schemaRef.id` | 数据集将基于的XDM架构的URI `$id`值。 |
| `schemaRef.contentType` | 指示架构的格式和版本。 有关详细信息，请参阅XDM API指南中有关[架构版本控制](../../xdm/api/getting-started.md#versioning)的部分。 |

>[!NOTE]
>
>本教程的所有示例都使用[Apache Parquet](https://parquet.apache.org/docs/)文件格式。 可以在[批量摄取开发人员指南](../../ingestion/batch-ingestion/api-overview.md)中找到使用JSON文件格式的示例

**响应**

成功的响应返回HTTP状态201 （已创建）和一个响应对象，该响应对象由包含新创建的数据集的ID的数组组成，格式为`"@/datasets/{DATASET_ID}"`。 数据集ID是系统生成的只读字符串，用于在API调用中引用数据集。

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## 创建批次

将数据添加到数据集之前，必须创建链接到数据集的批次。 然后，该批次将用于上传。

**API格式**

```HTTP
POST /batches
```

**请求**

请求正文包含“datasetId”字段，其值是上一步中生成的`{DATASET_ID}`。

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

**响应**

成功的响应返回HTTP状态201（已创建）和响应对象。 响应对象由一个数组组成，该数组包含新创建的批次ID，格式为`"@/batches/{BATCH_ID}"`。 批次ID是系统生成的只读字符串，用于在API调用中引用批次。

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{ORG_ID}",
    "updated": 1552694873602,
    "status": "loading",
    "created": 1552694873602,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "5c8c3c555033b814b69f947f"
        }
    ],
    "version": "1.0.0",
    "tags": {
        "acp_producer": [
            "{CREATED_CLIENT}"
        ],
        "acp_stagePath": [
            "{CREATED_CLIENT}/stage/5d01230fc78a4e4f8c0c6b387b4b8d1c"
        ],
        "use_plan_b_batch_status": [
            "false"
        ]
    },
    "createdUser": "{CREATED_BY}",
    "updatedUser": "{CREATED_BY}",
    "externalId": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "createdClient": "{CREATED_CLIENT}",
    "inputFormat": {
        "format": "parquet"
    }
}
```

## 将文件上载到批处理

成功创建新的上传批次后，您现在可以将文件上传到特定数据集。 请务必记住，在定义数据集时，将文件格式指定为Parquet。 因此，您上传的文件必须采用该格式。

>[!NOTE]
>
>支持的最大数据上传文件为512 MB。 如果您的数据文件大于此值，则需要将其划分为不超过512 MB的块，以便一次上传一个。 您可以对每个文件重复此步骤，使用相同的批次ID在同一批次中上载每个文件。 如果文件可作为批次的一部分上传，则数量没有限制。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{BATCH_ID}` | 您正在上载的批次的`id`。 |
| `{DATASET_ID}` | 批次将保留在的数据集的`id`。 |
| `{FILE_NAME}` | 您正在上载的文件的名称。 |

**请求**

```SHELL
curl -X PUT 'https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c/datasets/5c8c3c555033b814b69f947f/files/loyaltyData.parquet' \
  -H 'content-type: application/octet-stream' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  --data-binary '@{FILE_PATH_AND_NAME}.parquet'
```

**响应**

成功上传的文件返回空白响应正文和HTTP状态200（确定）。

## 信号批次完成

将所有数据文件上载到批次后，可以发出完成批次的信号。 信号指示完成会导致服务为上载的文件创建[!DNL Catalog] `DataSetFile`条目，并将它们与先前生成的批处理相关联。 [!DNL Catalog]批次标记为成功，这将触发任何下游流，这些流随后可以使用现在可用的数据。

**API格式**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 参数 | 描述 |
| --- | --- |
| `{BATCH_ID}` | 您标记为完成的批次的`id`。 |

**请求**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**响应**

成功完成的批处理将返回空白的响应正文和HTTP状态200（确定）。

## 监测引入

根据数据的大小，批次摄取的时间长短各不相同。 通过将批次的ID附加到`GET /batches`请求，您可以监视批次的状态。

**API格式**

```HTTP
GET /batches/{BATCH_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{BATCH_ID}` | 要监视的批次的`id`。 |

**请求**

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?batch=5d01230fc78a4e4f8c0c6b387b4b8d1c' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**响应**

正响应返回一个对象，该对象的`status`属性包含`success`的值：

```JSON
{
    "5b7129a879323401ef2a6486": {
        "imsOrg": "{ORG_ID}",
        "created": 1534142888068,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1534142955152,
        "replay": {},
        "status": "success",
        "errors": [],
        "version": "1.0.3",
        "availableDates": {},
        "relatedObjects": [
            {
                "type": "batch",
                "id": "29285e08378f4a41827e7e70fb7cb8f0"
            }
        ],
        "metrics": {
            "startTime": 1534142943819,
            "endTime": 1534142951760,
            "recordsRead": 108,
            "recordsWritten": 108
        }
    }
}
```

负响应返回其`"status"`属性中值为`"failed"`的对象，并包含任何相关的错误消息：

```JSON
{
    "5b96ce65badcf701e51f075d": {
        "imsOrg": "{ORG_ID}",
        "status": "failed",
        "relatedObjects": [
            {
                "type": "batch",
                "id": "29285e08378f4a41827e7e70fb7cb8f0"
            }
        ],
        "replay": {},
        "availableDates": {},
        "metrics": {
            "startTime": 1536610322329,
            "endTime": 1536610438083,
            "recordsRead": 4004,
            "recordsWritten": 4004,
            "failureReason": "Job aborted due to stage failure: Task 0 in stage 1.0 failed 4 times,:"
        },
        "errors": [
            {
                "code": "0070000017",
                "description": "Unknown error occurred."
            },
            {
                "code": "unknown",
                "description": "Job aborted."
            }
        ],
        "created": 1536609893629,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1536610442814,
        "version": "1.0.5"
    }
}
```

>[!NOTE]
>
>建议的轮询间隔为两分钟。

## 从数据集中读取数据

通过批处理ID，您可以使用数据访问API进行回读并验证上载到批处理的所有文件。 响应将返回一个包含文件ID列表的数组，每个文件ID均引用批次中的文件。

您还可以使用数据访问API返回名称、大小（以字节为单位）以及用于下载文件或文件夹的链接。

有关使用数据访问API的详细步骤，请参阅[数据访问开发人员指南](../../data-access/home.md)。

## 更新数据集架构

您可以添加字段并将其他数据摄取到已创建的数据集中。 为此，您首先需要通过添加定义新数据的其他属性来更新架构。 可使用PATCH和/或PUT操作更新现有架构来完成此操作。

有关更新架构的详细信息，请参阅[架构注册表API开发人员指南](../../xdm/api/getting-started.md)。

更新架构后，您可以重新执行本教程中的步骤以摄取符合修订后的架构的新数据。

请务必记住，架构演化是完全可加的，这意味着一旦架构被保存到注册表并用于数据摄取，就无法将重大更改引入架构。 要了解有关组合架构以用于Adobe Experience Platform的最佳实践的更多信息，请参阅架构组合基础[指南](../../xdm/schema/composition.md)。
