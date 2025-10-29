---
keywords: Experience Platform；主页；热门主题；数据源连接
solution: Experience Platform
title: 使用流服务API从第三方云存储系统摄取Parquet数据
type: Tutorial
description: 本教程使用流服务API来指导您完成从第三方云存储系统摄取Apache Parquet数据的步骤。
exl-id: fb1b19d6-16bb-4a5f-9e81-f537bac95041
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 13%

---

# 使用[!DNL Flow Service] API从第三方云存储系统摄取Parquet数据

[!DNL Flow Service]用于收集和集中Adobe Experience Platform中各种不同来源的客户数据。 该服务提供了一个用户界面和RESTful API，所有受支持的源均可从该API连接。

本教程使用[!DNL Flow Service] API引导您完成从第三方云存储系统中摄取Parquet数据的步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

- [源](../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
- [沙盒](../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了使用[!DNL Flow Service] API从第三方云存储中成功摄取Parquet数据所需了解的其他信息。

### 正在读取示例 API 调用

本教程提供了示例API调用来演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例 API 调用的文档中所用惯例的信息，请参阅故障排除指南中的[如何读取示例 API 调用](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) [!DNL Experience Platform]。

### 收集所需标头的值

为调用 [!DNL Experience Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负载(POST、PUT、PATCH)的请求都需要一个额外的媒体类型标头：

- `Content-Type: application/json`

## 创建连接

要使用[!DNL Experience Platform] API摄取Parquet数据，您必须对要访问的第三方云存储源具有有效连接。 如果您尚未与要使用的存储建立连接，则可通过以下教程创建一个连接：

- [Amazon S3](./create/cloud-storage/s3.md)
- [Azure Blob](./create/cloud-storage/blob.md)
- [Azure Data Lake Storage Gen2](./create/cloud-storage/adls-gen2.md)
- [Google云存储](./create/cloud-storage/google.md)
- [SFTP](./create/cloud-storage/sftp.md)

获取并存储连接的唯一标识符(`$id`)，然后继续本教程的下一步。

## 创建目标架构

为了在[!DNL Experience Platform]中使用源数据，还必须创建目标架构以根据您的需求构建源数据。 然后使用目标架构创建包含源数据的[!DNL Experience Platform]数据集。

如果您希望在[!DNL Experience Platform]中使用用户界面，[架构编辑器教程](../../../xdm/tutorials/create-schema-ui.md)提供了在架构编辑器中执行类似操作的分步说明。

**API格式**

```http
POST /schemaregistry/tenant/schemas
```

**请求**

以下示例请求创建扩展XDM [!DNL Individual Profile]类的XDM架构。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
    "type": "object",
    "title": "Sample Demo Profile XDM {{$guid}}",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-subscriptions"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        }
    ],
    "meta:containerId": "tenant",
    "meta:resourceType": "schemas",
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile"
}'
```

**响应**

成功的响应返回新创建架构的详细信息，包括其唯一标识符(`$id`)。 在下一步创建源连接时需要此ID。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
    "meta:altId": "_{TENANT_ID}.schemas.e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Sample Demo Profile XDM 8d96a964-aad8-43c5-a73a-c8b9b1ccbfb1",
    "type": "object",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-subscriptions",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-subscriptions",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-subscriptions",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1584673864341,
        "repo:lastModifiedDate": 1584673864341,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{MODIFIED_USER_ID}",
        "eTag": "fa704f80da907c8f0f66f453ffcac3e52958687edbf55d71231dc5e1522193c4"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 创建源连接 {#source}

在创建目标XDM架构后，现在可以使用对[!DNL Flow Service] API的POST请求创建源连接。 源连接包括API连接、源数据格式以及对上一步中检索到的目标XDM架构的引用。

**API格式**

```http
POST /sourceConnections
```

**请求**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Source Connection S3 {{$guid}}",
        "baseConnectionId": "5831c52c-c261-4945-b1c5-2cc261d945b2",
        "connectionSpec": {
            "id": "ecadc60c-7455-4d87-84dc-2a0e293d997b",
            "version": 1
        },
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
                "id": "",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "path": "partners-demo/samples",
            "recursive": "true"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `baseConnectionId` | 表示您的云存储的API的连接。 |
| `data.schema.id` | (`$id`)，如果目标xdm架构在上一步中检索。 |
| `params.path` | 源文件的路径。 |

**响应**

成功的响应返回新创建的源连接的唯一标识符(`id`)。 将此值存储为以后创建目标连接步骤中所需的值。

```json
{
    "id": "73bc8911-505a-4e46-bc89-11505a6e466f",
    "etag": "\"c4004435-0000-0200-0000-5e7437d90000\""
}
```

## 创建数据集基本连接

为了将外部数据摄取到[!DNL Experience Platform]，必须首先获取[!DNL Experience Platform]数据集基本连接。

<!--
broken link. this file not in TOC.
To create a dataset base connection, follow the steps outlined in the [dataset base connection tutorial](./create-dataset-base-connection.md).
-->

继续按照开发人员指南中概述的步骤操作，直到创建数据集基本连接为止。 获取并存储唯一标识符(`$id`)，然后继续将其用作创建目标连接的下一个步骤中的基本连接ID。

## 创建目标数据集

通过向[目录服务API](https://www.adobe.io/experience-platform-apis/references/catalog/)执行POST请求，在有效负载中提供目标架构的ID，可以创建目标数据集。

**API格式**

```http
POST /catalog/dataSets
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Leads Dataset {{$guid}}",
        "schemaRef": {
            "id": ""https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80"",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `schemaRef.id` | 目标XDM架构的ID。 |

**响应**

成功的响应将返回一个数组，该数组包含新创建的数据集的ID，格式为`"@/datasets/{DATASET_ID}"`。 数据集ID是系统生成的只读字符串，用于在API调用中引用数据集。 存储目标数据集ID，因为稍后创建目标连接和数据流时需要此ID。

```json
[
    "@/dataSets/5e7439b1ad55a618ad4c5102"
]
```

## 创建目标连接 {#target}

现在，您拥有数据集基本连接、目标架构和目标数据集的唯一标识符。 使用这些标识符，您可以使用[!DNL Flow Service] API创建目标连接，以指定将包含入站源数据的数据集。

**API格式**

```http
POST /targetConnections
```

**请求**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "baseConnectionId": "291257e3-c560-4e07-9257-e3c5606e07d1",
        "connectionSpec": {
            "id":"c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "name": "Target Connection {{$guid}}",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": ""https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80"",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5e7439b1ad55a618ad4c5102"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `baseConnectionId` | 数据集基本连接的ID。 |
| `data.schema.id` | 目标XDM架构的`$id`。 |
| `params.dataSetId` | 目标数据集的ID。 |
| `connectionSpec.id` | 云存储的连接规范ID。 |

**响应**

成功的响应返回新目标连接的唯一标识符(`id`)。 在后续步骤中根据需要存储此值。

```json
{
    "id": "9b3abc95-f2e9-47c1-babc-95f2e927c1ec",
    "etag": "\"7501936b-0000-0200-0000-5e743bcc0000\""
}
```

## 创建数据流

从第三方云存储中摄取Parquet数据的最后一步是创建数据流。 现在，您已准备以下必需值：

- [Source连接Id](#source)
- [目标连接ID](#target)

数据流负责从源中计划和收集数据。 您可以通过在有效负载中提供前面提到的值时执行POST请求来创建数据流。

**API格式**

```http
POST /flows
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Demo Parquet Ingestion Flow {{$guid}}",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "73bc8911-505a-4e46-bc89-11505a6e466f"
        ],
        "targetConnectionIds": [
            "9b3abc95-f2e9-47c1-babc-95f2e927c1ec"
        ],
        "scheduleParams": {
            "startTime": {{$timestamp}},
            "frequency": "minute",
            "interval": 1000,
            "backfill": true
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `sourceConnectionIds` | 在之前的步骤中检索的源连接ID。 |
| `targetConnectionIds` | 在之前的步骤中检索到的目标连接ID。 |

**响应**

成功的响应返回新创建的数据流的ID (`id`)。

```json
{
    "id": "89ff50ef-b082-426e-bf50-efb082d26e78",
    "etag": "\"890070b8-0000-0200-0000-5e743c040000\""
}
```

## 后续步骤

通过遵循本教程，您已创建一个源连接器，以按计划从第三方云存储系统收集Parquet数据。 下游[!DNL Experience Platform]服务（如[!DNL Real-Time Customer Profile]和[!DNL Data Science Workspace]）现在可以使用传入数据。 有关更多详细信息，请参阅以下文档：

- [实时客户轮廓概述](../../../profile/home.md)
- [数据科学工作区概述](../../../data-science-workspace/home.md)
