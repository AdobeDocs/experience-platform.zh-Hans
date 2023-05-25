---
keywords: Experience Platform；主页；热门主题；数据集；数据集；创建数据集；创建数据集
solution: Experience Platform
title: 使用API创建数据集
description: 本文档提供了使用Adobe Experience Platform API创建数据集和使用文件填充数据集的常规步骤。
exl-id: 3a5f48cf-ad05-4b9e-be1d-ff213a26a477
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 1%

---

# 使用API创建数据集

本文档提供了使用Adobe Experience Platform API创建数据集和使用文件填充数据集的常规步骤。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [批量摄取](../../ingestion/batch-ingestion/overview.md)： [!DNL Experience Platform] 允许您将数据摄取为批处理文件。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
* [[!DNL Sandboxes]](../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功调用 [!DNL Platform] API。

### 正在读取示例API调用

本教程提供了示例API调用来演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将提供所有中所有所需标头的值 [!DNL Experience Platform] API调用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定的虚拟沙盒隔离。 的所有请求 [!DNL Platform] API需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信息 [!DNL Platform]，请参见 [沙盒概述文档](../../sandboxes/home.md).

包含有效负载(POST、PUT、PATCH)的所有请求都需要额外的标头：

* Content-Type： application/json

## 教程

要创建数据集，必须首先定义架构。 架构是一组规则，可帮助表示数据。 除了描述数据结构之外，架构还提供约束和期望，当数据在系统之间移动时，可以应用这些约束和期望来验证数据。

这些标准定义允许以一致的方式解释数据，而不管数据来自何处，并且无需跨应用程序进行翻译。 有关构成架构的更多信息，请参阅以下指南中的 [模式组合基础](../../xdm/schema/composition.md)

## 查找数据集架构

本教程将从以下位置开始： [架构注册表API教程](../../xdm/tutorials/create-schema-api.md) 最后，使用在该教程中创建的忠诚度会员模式。

如果您尚未完成 [!DNL Schema Registry] 教程，请从此处开始，仅在您编写了必要的架构后继续此数据集教程。

以下调用可用于查看您在 [!DNL Schema Registry] api教程：

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

响应对象的格式取决于请求中发送的“接受”标头。 此响应中的各个属性已最小化，留出空间。

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
| `schemaRef.id` | URI `$id` 数据集将基于的XDM架构的值。 |
| `schemaRef.contentType` | 指示架构的格式和版本。 请参阅以下部分： [架构版本控制](../../xdm/api/getting-started.md#versioning) 有关更多信息，请参阅XDM API指南。 |

>[!NOTE]
>
>本教程使用 [Apache Parquet](https://parquet.apache.org/docs/) 所有示例的文件格式。 有关使用JSON文件格式的示例，请参阅 [批量摄取开发人员指南](../../ingestion/batch-ingestion/api-overview.md)

**响应**

成功的响应会返回HTTP状态201（已创建）和一个响应对象，该响应对象由一个数组组成，数组包含采用格式的新创建数据集的ID `"@/datasets/{DATASET_ID}"`. 数据集ID是系统生成的只读字符串，用于在API调用中引用数据集。

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## 创建批次

在将数据添加到数据集之前，必须创建链接到数据集的批次。 然后，该批次将用于上传。

**API格式**

```HTTP
POST /batches
```

**请求**

请求正文包含一个“datasetId”字段，其值为 `{DATASET_ID}` 在上一步中生成。

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

成功的响应会返回HTTP状态201（已创建）和一个响应对象，其中包含新创建的批处理的详细信息，包括其 `id`，系统生成的只读字符串。

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

## 将文件上传到批处理

成功创建新批次以进行上传后，您现在可以将文件上传到特定数据集。 请务必记住，定义数据集时，将文件格式指定为Parquet。 因此，您上传的文件必须采用该格式。

>[!NOTE]
>
>支持的最大数据上传文件为512 MB。 如果您的数据文件大于此值，则需要将其划分为不超过512 MB的块，以便一次上传一个。 您可以对每个文件重复此步骤，使用相同的批次ID在同一批次中上载每个文件。 如果文件可以作为批次的一部分上传，则数量没有限制。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{BATCH_ID}` | 此 `id` 要上传到的批次的。 |
| `{DATASET_ID}` | 此 `id` 批次将保留在的数据集的。 |
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

成功上传的文件返回空白响应正文和HTTP状态200 （确定）。

## 信号批次完成

将所有数据文件上载到批次后，可以发出完成批次的信号。 发出完成信号会导致服务创建 [!DNL Catalog] `DataSetFile` 已上传文件的条目，并将其与之前生成的批次关联。 此 [!DNL Catalog] 批量标记为成功，这将触发任何下游流，这些流随后可以使用现在可用的数据。

**API格式**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 参数 | 描述 |
| --- | --- |
| `{BATCH_ID}` | 此 `id` 标记完成的批次。 |

**请求**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**响应**

成功完成的批处理返回空白响应正文和HTTP状态200 （确定）。

## 监测引入

根据数据的大小，批量摄取的时间长短各不相同。 您可以通过附加 `batch` 包含批次ID的请求参数 `GET /batches` 请求。 API会在数据集中轮询批次从摄取到 `status` 在响应中指示完成（“success”或“failure”）。

**API格式**

```HTTP
GET /batches?batch={BATCH_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{BATCH_ID}` | 此 `id` 要监视的批次。 |

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

正响应返回一个对象，其 `status` 包含值的属性 `success`：

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

负响应返回一个对象，其值为 `"failed"` 在其中 `"status"` 属性，并包括任何相关的错误消息：

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
>建议轮询间隔为两分钟。

## 从数据集中读取数据

通过批处理ID，您可以使用数据访问API回读并验证上载到批处理的所有文件。 响应将返回一个包含文件ID列表的数组，每个文件ID均引用批处理中的文件。

您还可以使用数据访问API返回名称、大小（以字节为单位）以及用于下载文件或文件夹的链接。

有关使用数据访问API的详细步骤，请参阅 [Data Access开发人员指南](../../data-access/home.md).

## 更新数据集架构

您可以添加字段并将其他数据摄取到已创建的数据集中。 为此，您首先需要通过添加定义新数据的其他属性来更新架构。 可以使用PATCH和/或PUT操作更新现有架构来完成此操作。

有关更新架构的更多信息，请参阅 [架构注册表API开发人员指南](../../xdm/api/getting-started.md).

更新架构后，您可以重新执行本教程中的步骤以摄取符合修订后的架构的新数据。

请务必记住，架构演化是纯粹的累加，这意味着一旦架构保存到注册表并用于数据摄取，您就不能对架构引入重大更改。 要了解有关撰写架构以用于Adobe Experience Platform的最佳实践的更多信息，请参阅有关以下内容的指南： [模式组合基础](../../xdm/schema/composition.md).
