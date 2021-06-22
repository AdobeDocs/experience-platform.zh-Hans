---
keywords: Experience Platform；主页；热门主题；数据集；数据集；创建数据集；创建数据集
solution: Experience Platform
title: 使用API创建数据集
topic-legacy: datasets
description: 本文档提供了使用Adobe Experience Platform API创建数据集以及使用文件填充数据集的一般步骤。
exl-id: 3a5f48cf-ad05-4b9e-be1d-ff213a26a477
source-git-commit: e4bf5bb77ac4186b24580329699d74d653310d93
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 1%

---

# 使用API创建数据集

本文档提供了使用Adobe Experience Platform API创建数据集以及使用文件填充数据集的一般步骤。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [批量摄取](../../ingestion/batch-ingestion/overview.md): [!DNL Experience Platform] 允许您将数据作为批处理文件进行摄取。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):用于组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了成功调用[!DNL Platform] API所需了解的其他信息。

### 读取示例API调用

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅[!DNL Experience Platform]疑难解答指南中[如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一节。

### 收集所需标题的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程可为所有[!DNL Experience Platform] API调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源均与特定虚拟沙箱隔离。 对[!DNL Platform] API的所有请求都需要一个标头来指定操作将在其中进行的沙盒的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Platform]中沙箱的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的标头：

* Content-Type:application/json

## 教程

要创建数据集，必须首先定义架构。 架构是一组用于帮助表示数据的规则。 除了描述数据结构之外，架构还提供了约束和期望，当数据在系统之间移动时，这些约束和期望可应用并用于验证数据。

这些标准定义允许对数据进行一致的解释（无论其来源如何），并且无需跨应用程序进行翻译。 有关合成架构的更多信息，请参阅[架构合成基础知识](../../xdm/schema/composition.md)指南

## 查找数据集架构

本教程从[架构注册表API教程](../../xdm/tutorials/create-schema-api.md)结束的位置开始，该教程将利用在本教程中创建的会员架构。

如果您尚未完成[!DNL Schema Registry]教程，请从此处开始，并仅在您撰写了必需的架构后继续使用此数据集教程。

以下调用可用于查看您在[!DNL Schema Registry] API教程中创建的会员架构：

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrg": "{IMS_ORG}",
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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `schemaRef.contentType` | 指示架构的格式和版本。 有关更多信息，请参阅XDM API指南中关于[模式版本控制](../../xdm/api/getting-started.md#versioning)的部分。 |

>[!NOTE]
>
>本教程对其所有示例都使用[Apache Parquet](https://parquet.apache.org/documentation/latest/)文件格式。 [批量摄取开发人员指南](../../ingestion/batch-ingestion/api-overview.md)中提供了使用JSON文件格式的示例

**响应**

成功的响应会返回HTTP状态201（已创建）和一个响应对象，该对象由一个数组组成，该数组包含格式为`"@/datasets/{DATASET_ID}"`的新创建数据集的ID。 数据集ID是由系统生成的只读字符串，用于在API调用中引用数据集。

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

请求正文包含一个“datasetId”字段，其值是在上一步中生成的`{DATASET_ID}`。

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

**响应**

成功的响应会返回HTTP状态201（已创建）和一个包含新创建批处理详细信息（包括其`id`，只读的系统生成字符串）的响应对象。

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{IMS_ORG}",
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
| `{BATCH_ID}` | 您要上传到的批次的`id`。 |
| `{DATASET_ID}` | 将保留该批处理的数据集的`id`。 |
| `{FILE_NAME}` | 您上传的文件的名称。 |

**请求**

```SHELL
curl -X PUT 'https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c/datasets/5c8c3c555033b814b69f947f/files/loyaltyData.parquet' \
  -H 'content-type: application/octet-stream' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  --data-binary '@{FILE_PATH_AND_NAME}.parquet'
```

**响应**

成功上传的文件会返回空白响应正文和HTTP状态200（确定）。

## 信号批处理完成

将所有数据文件上传到批后，您可以发出该批完成的信号。 信令完成导致服务为上传的文件创建[!DNL Catalog] `DataSetFile`条目，并将这些条目与之前生成的批处理相关联。 [!DNL Catalog]批次标记为成功，这会触发任何下游流，这些流随后可以处理当前可用的数据。

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
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**响应**

成功完成的批处理返回空白响应正文和HTTP状态200（确定）。

## 监控摄取

批次的摄取时间会因数据的大小而异。 您可以通过将包含批处理ID的`batch`请求参数附加到`GET /batches`请求来监视批处理的状态。 API会从摄取开始轮询数据集的批处理状态，直到响应中的`status`指示完成（“success”或“failure”）。

**API格式**

```HTTP
GET /batches?batch={BATCH_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{BATCH_ID}` | 要监视的批处理的`id`。 |

**请求**

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?batch=5d01230fc78a4e4f8c0c6b387b4b8d1c' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**响应**

正向响应会返回一个对象，其`status`属性包含`success`的值：

```JSON
{
    "5b7129a879323401ef2a6486": {
        "imsOrg": "{IMS_ORG}",
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
        "imsOrg": "{IMS_ORG}",
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

有关使用数据访问API的详细步骤，请参阅[Data Access开发人员指南](../../data-access/home.md)。

## 更新数据集架构

您可以添加字段并将其他数据摄取到已创建的数据集。 为此，您首先需要通过添加定义新数据的其他属性来更新架构。 可以使用PATCH和/或PUT操作来更新现有架构，以完成此操作。

有关更新架构的更多信息，请参阅[架构注册API开发人员指南](../../xdm/api/getting-started.md)。

更新架构后，您可以重新按照本教程中的步骤操作，以摄取符合修订的架构的新数据。

请务必记住，架构演变纯粹是可添加的，这意味着一旦架构保存到注册表并用于数据摄取，就无法对其进行突破性更改。 要了解有关合成架构以与Adobe Experience Platform一起使用的最佳实践的更多信息，请参阅[架构合成基础知识](../../xdm/schema/composition.md)指南。
