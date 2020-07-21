---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 流记录数据
topic: tutorial
translation-type: tm+mt
source-git-commit: 6a371aab5435bac97f714e5cf96a93adf4aa0303
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 2%

---


# 流记录数据到Adobe Experience Platform

本教程将帮助您开始使用流式摄取API，它是Adobe Experience Platform数据摄取服务API的一部分。

## 入门指南

本教程需要掌握各种Adobe Experience Platform服务的工作知识。 在开始本教程之前，请查看以下服务的相关文档：

- [体验数据模型(XDM)](../../xdm/home.md): 平台组织体验数据的标准化框架。
- [实时客户用户档案](../../profile/home.md): 根据来自多个来源的汇总数据实时提供统一的消费者用户档案。
- [模式注册开发人员指南](../../xdm/api/getting-started.md): 全面的指南，涵盖模式注册表API的每个可用端点以及如何调用它们。 这包括了解您 `{TENANT_ID}`在本教程中的调用，以及了解如何创建模式，该数据用于创建用于摄取的数据集。

此外，本教程要求您已创建流连接。 有关创建流连接的详细信息，请阅读创 [建流连接教程](./create-streaming-connection.md)。

以下各节提供了成功调用流式摄取API所需了解的其他信息。

### 读取示例API调用

本指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用的章节。

### 收集所需标题的值

要调用平台API，您必须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

- 授权： 承载者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都隔离到特定虚拟沙箱。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

- 内容类型： application/json

## 基于XDM个人模式类编写用户档案

要创建数据集，您首先需要创建实现XDM单个模式类的新用户档案。 有关如何创建模式的更多信息，请阅读 [模式注册API开发人员指南](../../xdm/api/getting-started.md)。

**API格式**

```http
POST /schemaregistry/tenant/schemas
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "type": "object",
    "title": "Sample schema",
    "description": "Sample description",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        }
    ],
    "meta:immutableTags": [
        "union"
    ]
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `title` | 要用于模式的名称。 此名称必须唯一。 |
| `description` | 您正在创建的模式的有意义描述。 |
| `meta:immutableTags` | 在此示例中，标 `union` 签用于将您的数据保 [留到实时客户用户档案](../../profile/home.md)。 |

**响应**

成功的响应会返回HTTP状态201，其中包含您新创建的模式的详细信息。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "type": "object",
    "title": "Sample schema",
    "description": "Sample description",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/cpmtext/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "meta:immutableTags": [
        "union"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createDate": 1551376506996,
        "repo:lastModifiedDate": 1551376506996,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{TENANT_ID}` | 此ID用于确保您创建的资源命名正确且包含在IMS组织中。 有关租户ID的详细信息，请阅读 [模式注册指南](../../xdm/api/getting-started.md#know-your-tenant-id)。 |

请注意属性 `$id` 和属性，因 `version` 为创建数据集时将同时使用这两个属性。

## 为模式设置主标识描述符

接下来，将标识 [描述符添加](../../xdm/api/descriptors.md) 到上面创建的模式，使用工作电子邮件地址属性作为主标识符。 执行此操作将导致两个更改：

1. 工作电子邮件地址将成为必填字段。 这意味着，未使用此字段发送的消息将无法通过验证，且不会被摄取。

2. 实时客户用户档案将使用工作电子邮件地址作为标识符，帮助拼凑有关该个人的更多信息。

### 请求

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "@type":"xdm:descriptorIdentity",
    "xdm:sourceProperty":"/workEmail/address",
    "xdm:property":"xdm:code",
    "xdm:isPrimary":true,
    "xdm:namespace":"Email",
    "xdm:sourceSchema":"{SCHEMA_REF_ID}",
    "xdm:sourceVersion":1
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEMA_REF_ID}` | 您 `$id` 之前在构建模式时收到的内容。 它应该是这样的： `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B; &#x200B; Identity命名空间代码&#x200B;****
>
> 请确保代码有效——上例使用“email”，它是标准身份命名空间。 其他常用的标准身份命名空间可在Identity Service常见问 [题解答中找到](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform)。
>
> 如果要创建自定义命名空间，请按照标识命名空间概述中概 [述的步骤操作](../../identity-service/home.md)。

**响应**

成功的响应返回HTTP状态201，其中包含有关该模式新创建的主标识描述符的信息。

```json
{
    "xdm:property": "xdm:code",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "xdm:namespace": "Email",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceVersion": 1,
    "xdm:isPrimary": true,
    "xdm:sourceProperty": "/workEmail/address",
    "@id": "17aaebfa382ce8fc0a40d3e43870b6470aab894e1c368d16",
    "meta:containerId": "tenant",
    "version": "1",
    "imsOrg": "{IMS_ORG}"
}
```

## 创建用于记录数据的数据集

创建模式后，您需要创建数据集以采集记录数据。

>[!NOTE]
>
>此数据集将启用 **实时客户用户档案****和Identity Service**。

**API格式**

```http
POST /catalog/dataSets
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d ' {
    "name": "Dataset name",
    "description": "Dataset description",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID},
        "contentType": "application/vnd.adobe.xed-full+json;version=1.0"
    },
    "tags": {
        "unifiedIdentity": ["enabled:true"],
        "unifiedProfile": ["enabled:true"]
    }
}'
```

**响应**

成功的响应返回HTTP状态201和一个数组，该数组包含格式为新创建数据集的ID `@/dataSets/{DATASET_ID}`。

```json
[
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## 将记录数据引入流连接

数据集和流连接就位后，您可以收录XDM格式的JSON记录以将记录数据录入平台。

**API格式**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 先前 `id` 创建的流连接的值。 |
| `synchronousValidation` | 用于开发目的的可选查询参数。 如果设置为 `true`，则可以使用它进行即时反馈，以确定请求是否成功发送。 默认情况下，此值设置为 `false`。 |

**请求**

>[!NOTE]
>
>以下API调用不需 **要** 任何身份验证头。

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
            }
        },
        "xdmEntity": {
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                },
                "birthDate": "1969-03-14",
                "gender": "female"
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "type": "work",
                "status": "active"
            }
        }
    }
}'
```

**响应**

成功的响应会返回HTTP状态200，其中包含新流用户档案的详细信息。

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507,
    "synchronousValidation": {
        "status": "pass"
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 先前创建的流连接的ID。 |
| `xactionId` | 您刚刚发送的记录在服务器端生成的唯一标识符。 此ID可帮助Adobe跟踪记录在各种系统和调试过程中的生命周期。 |
| `receivedTimeMs` | 显示接收请求的时间的时间戳（以毫秒为单位）。 |
| `synchronousValidation.status` | 由于添加了查询 `synchronousValidation=true` 参数，因此将显示此值。 如果验证成功，则状态为 `pass`。 |

## 检索新摄取的记录数据

要验证之前摄取的记录，可以使 [用用户档案访问](../../profile/api/entities.md) API检索记录数据。

>[!NOTE]
>
>如果未定义合并策略ID和模式。</span>name或relatedSchema</span>.name是 `_xdm.context.profile`,用户档案访问将获取所 **有相关** 的身份。

**API格式**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| 参数 | 描述 |
| --------- | ----------- |
| `schema.name` | **必需。** 您访问的模式的名称。 |
| `entityId` | 实体的ID。 如果提供，则还必须提供实体命名空间。 |
| `entityIdNS` | 您尝试检索的ID的命名空间。 |

**请求**

您可以使用以下GET请求查看以前摄取的记录数据。

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，其中包含所请求实体的详细信息。 如您所见，这是之前成功摄取的相同记录。

```json
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "mergePolicy": {
            "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56"
        },
        "sources": [
            "5e30d7986c0cc218a85cee65"
        ],
        "tags": [
            "1580346827274:2478:215"
        ],
        "identityGraph": [
            "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA"
        ],
        "entity": {
            "person": {
                "name": {
                    "lastName": "Doe",
                    "middleName": "F",
                    "firstName": "Jane"
                },
                "gender": "female",
                "birthDate": "1969-03-14"
            },
            "workEmail": {
                "type": "work",
                "address": "janedoe@example.com",
                "status": "active",
                "primary": true
            },
            "identityMap": {
                "email": [
                    {
                        "id": "janedoe@example.com"
                    }
                ]
            }
        },
        "lastModifiedAt": "2020-01-30T01:13:59Z"
    }
}
```

## 后续步骤

通过阅读此文档，您现在了解如何使用流连接将记录数据引入平台。 您可以尝试使用不同的值进行更多调用并检索更新的值。 此外，您还可以通过平台UI开始监视所摄数据。 有关详细信息，请阅读监 [视数据获取指南](../quality/monitor-data-flows.md) 。

有关流摄取的详细信息，请阅读流摄 [取概述](../streaming-ingestion/overview.md)。


