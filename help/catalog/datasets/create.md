---
keywords: Experience Platform；主页；热门主题；数据集；数据集；创建数据集；创建数据集
solution: Experience Platform
title: 使用API创建数据集
topic-legacy: datasets
description: 本文档提供了使用Adobe Experience Platform API创建数据集以及使用文件填充数据集的一般步骤。
exl-id: 3a5f48cf-ad05-4b9e-be1d-ff213a26a477
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 1%

---

# 使用API创建数据集

本文档提供了使用Adobe Experience Platform API创建数据集以及使用文件填充数据集的一般步骤。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [批量摄取](../../ingestion/batch-ingestion/overview.md): [!DNL Experience Platform] 允许您将数据作为批处理文件进行摄取。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功调用所需了解的其他信息 [!DNL Platform] API。

### 读取示例API调用

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定操作将在其中执行的沙盒的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关 [!DNL Platform]，请参阅 [沙盒概述文档](../../sandboxes/home.md).

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的标头：

* Content-Type:application/json

## 教程

要创建数据集，必须首先定义架构。 架构是一组用于帮助表示数据的规则。 除了描述数据结构之外，架构还提供了约束和期望，当数据在系统之间移动时，这些约束和期望可应用并用于验证数据。

这些标准定义允许对数据进行一致的解释（无论其来源如何），并且无需跨应用程序进行翻译。 有关合成架构的更多信息，请参阅 [架构组合基础知识](../../xdm/schema/composition.md)

## 查找数据集架构

本教程将从 [模式注册表API教程](../../xdm/tutorials/create-schema-api.md) 结束，以利用在本教程中创建的会员架构。

如果您尚未完成 [!DNL Schema Registry] 教程中，请从此处开始，并仅在您撰写了必需的架构后，才继续使用此数据集教程。

以下调用可用于查看您在 [!DNL Schema Registry] API教程：

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

响应对象的格式取决于请求中发送的Accept标头。 此响应中的各个属性已在空间上最小化。

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

现在，通过建立忠诚会员架构，您可以创建引用该架构的数据集。

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
| `schemaRef.contentType` | 指示架构的格式和版本。 请参阅 [模式版本控制](../../xdm/api/getting-started.md#versioning) ，以了解更多信息。 |

>[!NOTE]
>
>本教程使用 [Apache Parquet](https://parquet.apache.org/docs/) 文件格式。 在 [批量获取开发人员指南](../../ingestion/batch-ingestion/api-overview.md)

**响应**

成功的响应会返回HTTP状态201（已创建）和一个响应对象，该对象包含一个数组，其中包含以格式新创建数据集的ID `"@/datasets/{DATASET_ID}"`. 数据集ID是由系统生成的只读字符串，用于在API调用中引用数据集。

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## 创建批处理

在将数据添加到数据集之前，必须先创建一个链接到该数据集的批次。 然后，将使用批次进行上传。

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

成功的响应会返回HTTP状态201（已创建）以及包含新创建批处理详细信息(包括其 `id`，系统生成的只读字符串。

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

现在，在成功创建了要上传的新批处理之后，您可以将文件上传到特定数据集。 请务必记住，在定义数据集时，您将文件格式指定为Parquet。 因此，您上传的文件必须采用该格式。

>[!NOTE]
>
>支持的最大数据上载文件为512 MB。 如果您的数据文件大于此大小，则需要将其划分为不大于512 MB的块，然后一次上传一个。 您可以使用相同的批处理ID，对每个文件重复此步骤，以同一批次上载每个文件。 如果文件可以作为批处理的一部分上传，则数字没有限制。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{BATCH_ID}` | 的 `id` 上传到的批次。 |
| `{DATASET_ID}` | 的 `id` 在数据集中，将保留该批次。 |
| `{FILE_NAME}` | 您上传的文件的名称。 |

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

成功上传的文件会返回空白响应正文和HTTP状态200（确定）。

## 信号批处理完成

将所有数据文件上传到批后，您可以发出该批完成的信号。 信令完成导致服务创建 [!DNL Catalog] `DataSetFile` 上传文件的条目，并将它们与之前生成的批处理相关联。 的 [!DNL Catalog] 批次标记为成功，这会触发任何可随后处理当前可用数据的下游流。

**API格式**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 参数 | 描述 |
| --- | --- |
| `{BATCH_ID}` | 的 `id` 标记为完成的批次。 |

**请求**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**响应**

成功完成的批处理返回空白响应正文和HTTP状态200（确定）。

## 监控摄取

批次的摄取时间会因数据的大小而异。 您可以通过附加 `batch` 包含批次ID的请求参数 `GET /batches` 请求。 API会从摄取开始对数据集轮询批处理状态，直到 `status` 响应中指示完成（“success”或“failure”）。

**API格式**

```HTTP
GET /batches?batch={BATCH_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{BATCH_ID}` | 的 `id` 要监视的批次的数量。 |

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

正向响应会返回带有其 `status` 包含值的属性 `success`:

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

负响应返回值为 `"failed"` 在 `"status"` ，并包含任何相关错误消息：

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

## 从数据集读取数据

使用批处理ID，您可以使用数据访问API来读回并验证上传到该批处理的所有文件。 响应会返回一个包含文件ID列表的数组，每个ID都引用批处理中的文件。

您还可以使用数据访问API返回名称、大小（以字节为单位）以及用于下载文件或文件夹的链接。

有关使用数据访问API的详细步骤，请参阅 [Data Access开发人员指南](../../data-access/home.md).

## 更新数据集架构

您可以添加字段并将其他数据摄取到已创建的数据集。 为此，您首先需要通过添加定义新数据的其他属性来更新架构。 可以使用PATCH和/或PUT操作来更新现有架构，以完成此操作。

有关更新架构的更多信息，请参阅 [架构注册API开发人员指南](../../xdm/api/getting-started.md).

更新架构后，您可以重新按照本教程中的步骤操作，以摄取符合修订的架构的新数据。

请务必记住，架构演变纯粹是可添加的，这意味着一旦架构保存到注册表并用于数据摄取，就无法对其进行突破性更改。 要了解有关构建架构以与Adobe Experience Platform一起使用的最佳实践的更多信息，请参阅 [架构组合基础知识](../../xdm/schema/composition.md).
