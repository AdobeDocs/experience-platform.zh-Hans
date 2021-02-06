---
keywords: Experience Platform；主题；流摄取；摄取；记录数据；流记录数据；
solution: Experience Platform
title: 使用流摄取API的流记录数据
topic: tutorial
type: Tutorial
description: 本教程将帮助您开始使用流式摄取API，它是Adobe Experience Platform数据摄取服务API的一部分。
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 2%

---


# 使用流摄取API的流记录数据

本教程将帮助您开始使用流式摄取API，它是Adobe Experience Platform[!DNL Data Ingestion Service] API的一部分。

## 入门指南

本教程需要对Adobe Experience Platform各项服务有一定的工作知识。 在开始本教程之前，请查看以下服务的相关文档：

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):用于组织体验数据 [!DNL Platform] 的标准化框架。
- [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据实时提供统一的消费者用户档案。
- [模式注册开发人员指南](../../xdm/api/getting-started.md):全面的指南，涵盖API的每个可用端点 [!DNL Schema Registry] 以及如何向它们发出调用。这包括了解您的`{TENANT_ID}`（在本教程的调用中显示）以及如何创建模式（用于创建数据集以进行摄取）。

此外，本教程要求您已创建流连接。 有关创建流连接的详细信息，请阅读[创建流连接教程](./create-streaming-connection.md)。

以下各节提供了成功调用流式摄取API所需了解的其他信息。

### 读取示例API调用

本指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参见[!DNL Experience Platform]疑难解答指南中关于如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的一节。[

### 收集所需标题的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

- 授权：载体`{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有资源都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Platform]中沙箱的详细信息，请参阅[沙箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要附加标头：

- 内容类型：application/json

## 根据[!DNL XDM Individual Profile]类编写模式

要创建数据集，您首先需要创建实现[!DNL XDM Individual Profile]类的新模式。 有关如何创建模式的详细信息，请阅读[模式注册表API开发人员指南](../../xdm/api/getting-started.md)。

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
| `meta:immutableTags` | 在此示例中，`union`标记用于将数据保留到[[!DNL Real-time Customer Profile]](../../profile/home.md)中。 |

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
| `{TENANT_ID}` | 此ID用于确保您创建的资源命名正确且包含在IMS组织中。 有关租户ID的详细信息，请阅读[模式注册表指南](../../xdm/api/getting-started.md#know-your-tenant-id)。 |

请注意`$id`和`version`属性，因为创建数据集时将同时使用这两个属性。

## 为模式设置主标识描述符

然后，将[标识描述符](../../xdm/api/descriptors.md)添加到以上创建的模式，使用工作电子邮件地址属性作为主标识符。 执行此操作将导致两个更改：

1. 工作电子邮件地址将成为必填字段。 这意味着，未使用此字段发送的消息将无法通过验证，且不会被摄取。

2. [!DNL Real-time Customer Profile] 将使用工作电子邮件地址作为标识符，帮助拼凑有关该个人的更多信息。

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
| `{SCHEMA_REF_ID}` | 您之前在编写模式时收到的`$id`。 它应该是这样的：`"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B;&#x200B;**身份命名空间码**
>
> 请确保代码有效——上例使用“email”，它是标准身份命名空间。 在[Identity Service FAQ](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform)中可找到其他常用的标准身份命名空间。
>
> 如果要创建自定义命名空间，请按照[标识命名空间概述](../../identity-service/home.md)中概述的步骤操作。

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
>此数据集将启用&#x200B;**[!DNL Real-time Customer Profile]**&#x200B;和&#x200B;**[!DNL Identity Service]**。

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

成功的响应返回HTTP状态201和一个数组，该数组包含格式为`@/dataSets/{DATASET_ID}`的新创建数据集的ID。

```json
[
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## 将记录数据引入流连接

在数据集和流连接到位后，您可以收录XDM格式的JSON记录，将记录数据收录到[!DNL Platform]中。

**API格式**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 先前创建的流连接的`id`值。 |
| `synchronousValidation` | 用于开发目的的可选查询参数。 如果设置为`true`，则可以立即进行反馈，以确定请求是否成功发送。 默认情况下，此值设置为`false`。 |

**请求**

可以将记录数据引入流连接，无论是否使用源名称。

以下示例请求将缺少源名称的记录引入平台。 如果记录缺少源名称，它将从流连接定义添加源ID。

>[!NOTE]
>
>以下API调用不&#x200B;**不**&#x200B;需要任何身份验证头。

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

如果要包含源名称，以下示例将显示如何包含它。

```json
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample source name"
        }
    }
```

**响应**

成功的响应返回HTTP状态200，其中包含新流[!DNL Profile]的详细信息。

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
| `xactionId` | 您刚刚发送的记录在服务器端生成的唯一标识符。 此ID可帮助Adobe跟踪记录在各种系统中的生命周期并进行调试。 |
| `receivedTimeMs` | 显示接收请求的时间的时间戳（以毫秒为单位）。 |
| `synchronousValidation.status` | 由于添加了查询参数`synchronousValidation=true`，因此将显示此值。 如果验证成功，状态将为`pass`。 |

## 检索新摄取的记录数据

要验证之前摄取的记录，可使用[[!DNL Profile Access API]](../../profile/api/entities.md)检索记录数据。

>[!NOTE]
>
>如果未定义合并策略ID，且`schema.name`或`relatedSchema.name`为`_xdm.context.profile`,[!DNL Profile Access]将获取&#x200B;**所有**&#x200B;相关标识。

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

通过阅读此文档，您现在了解如何使用流连接将记录数据引入[!DNL Platform]。 您可以尝试使用不同的值进行更多调用并检索更新的值。 此外，您还可以通过[!DNL Platform] UI开始监视所摄取的数据。 有关详细信息，请阅读[监视数据摄取](../quality/monitor-data-ingestion.md)指南。

有关流摄取的详细信息，请阅读[流摄取概述](../streaming-ingestion/overview.md)。


