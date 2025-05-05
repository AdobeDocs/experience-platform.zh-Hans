---
keywords: Experience Platform；主页；热门主题；流式摄取；摄取；记录数据；流记录数据；
solution: Experience Platform
title: 使用流式引入API流式记录数据
type: Tutorial
description: 本教程将帮助您开始使用流摄取API，它是Adobe Experience Platform数据摄取服务API的一部分。
exl-id: 097dfd5a-4e74-430d-8a12-cac11b1603aa
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 2%

---


# 使用流式引入API流式处理记录数据

本教程将帮助您开始使用流摄取API，它是Adobe Experience Platform [!DNL Data Ingestion Service] API的一部分。

## 快速入门

本教程需要具备各种Adobe Experience Platform服务的实际操作知识。 在开始本教程之前，请查看以下服务的文档：

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： [!DNL Experience Platform]用于组织体验数据的标准化框架。
   - [架构注册开发人员指南](../../xdm/api/getting-started.md)：一个全面的指南，涵盖[!DNL Schema Registry] API的每个可用端点以及如何调用它们。 这包括了解您在本教程的调用中显示的`{TENANT_ID}`，以及了解如何创建用于创建摄取数据集的架构。
- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个源的汇总数据，实时提供统一的使用者配置文件。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../landing/api-guide.md)指南。

## 根据[!DNL XDM Individual Profile]类构建架构

要创建数据集，您首先需要创建一个实现[!DNL XDM Individual Profile]类的新架构。 有关如何创建架构的更多信息，请参阅[架构注册API开发人员指南](../../xdm/api/getting-started.md)。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `title` | 要用于架构的名称。 此名称必须是唯一的。 |
| `description` | 对您正在创建的架构的有意义的描述。 |
| `meta:immutableTags` | 在此示例中，`union`标记用于将您的数据保留到[[!DNL Real-Time Customer Profile]](../../profile/home.md)中。 |

**响应**

成功的响应返回HTTP状态201以及新创建架构的详细信息。

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
    "imsOrg": "{ORG_ID}",
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
| `{TENANT_ID}` | 此ID用于确保您创建的资源被正确命名并包含在您的组织中。 有关租户ID的详细信息，请阅读[架构注册表指南](../../xdm/api/getting-started.md#know-your-tenant-id)。 |

请记下`$id`和`version`属性，因为创建数据集时将同时使用这两个属性。

## 为架构设置主标识描述符

接下来，将[身份描述符](../../xdm/api/descriptors.md)添加到上面创建的架构中，使用工作电子邮件地址属性作为主要标识符。 执行此操作将导致两个更改：

1. 工作电子邮件地址将成为必填字段。 这意味着在没有此字段的情况下发送的邮件将验证失败并且不会被摄取。

2. [!DNL Real-Time Customer Profile]将使用工作电子邮件地址作为标识符以帮助拼合有关该个人的更多信息。

### 请求

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `{SCHEMA_REF_ID}` | 您之前在撰写架构时收到的`$id`。 它应类似于下面的样子： `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>{0&#x200B;}身份命名空间代码{1&#x200B;}**&#x200B;**
>
> 请确保代码有效 — 上面的示例使用“email”，它是一个标准身份命名空间。 在[身份服务常见问题解答](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform)中可以找到其他常用的标准身份命名空间。
>
> 如果要创建自定义命名空间，请按照[身份命名空间概述](../../identity-service/home.md)中概述的步骤操作。

**响应**

成功的响应返回HTTP状态201，其中包含有关为架构新建的主标识描述符的信息。

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
    "imsOrg": "{ORG_ID}"
}
```

## 为记录数据创建数据集

创建架构后，您将需要创建一个数据集来摄取记录数据。

>[!NOTE]
>
>将为&#x200B;**[!DNL Real-Time Customer Profile]**&#x200B;和&#x200B;**[!DNL Identity Service]**&#x200B;启用此数据集。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d ' {
    "name": "Dataset name",
    "description": "Dataset description",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID},
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
    },
    "tags": {
        "unifiedIdentity": ["enabled:true"],
        "unifiedProfile": ["enabled:true"]
    }
}'
```

**响应**

成功的响应返回HTTP状态201和一个数组，该数组包含新创建的数据集的ID，格式为`@/dataSets/{DATASET_ID}`。

```json
[
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## 创建流连接

创建架构和数据集后，即可创建流连接

有关创建流连接的详细信息，请参阅[创建流连接教程](./create-streaming-connection.md)。

## 将记录数据摄取到流连接 {#ingest-data}

准备好数据集和流连接后，您可以摄取XDM格式的JSON记录以将记录数据摄取到[!DNL Experience Platform]。

**API格式**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 之前创建的流连接的`inletId`值。 |
| `syncValidation` | 用于开发目的的可选查询参数。 如果设置为`true`，则可用于即时反馈以确定请求是否成功发送。 默认情况下，此值设置为`false`。 请注意，如果您将此查询参数设置为`true`，则请求速率将限制为每`CONNECTION_ID`每分钟60次。 |

**请求**

可以将记录数据摄取到流连接，无论是否使用源名称。

以下示例请求向Experience Platform摄取缺少源名称的记录。 如果记录缺少源名称，它将从流连接定义中添加源ID。

>[!NOTE]
>
>以下API调用&#x200B;**不**&#x200B;需要任何身份验证标头。

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "flowId": "{FLOW_ID}",
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
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

如果要包含源名称，以下示例显示了如何包含该源名称。

```json
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample source name"
        }
    }
```

**响应**

成功的响应返回HTTP状态200，其中包含新流式传输[!DNL Profile]的详细信息。

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507,
    "syncValidation": {
        "status": "pass"
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 之前创建的流连接的ID。 |
| `xactionId` | 在服务器端为您刚刚发送的记录生成的唯一标识符。 此ID可帮助Adobe跟踪此记录在各种系统和调试中的生命周期。 |
| `receivedTimeMs` | 显示收到请求时间的时间戳（以毫秒为单位）。 |
| `syncValidation.status` | 由于添加了查询参数`syncValidation=true`，因此将显示此值。 如果验证成功，状态将为`pass`。 |

## 检索新摄取的记录数据

要验证以前摄取的记录，您可以使用[[!DNL Profile Access API]](../../profile/api/entities.md)检索记录数据。

>[!NOTE]
>
>如果未定义合并策略ID，并且`schema.name`或`relatedSchema.name`为`_xdm.context.profile`，则[!DNL Profile Access]将提取&#x200B;**所有**&#x200B;相关标识。

**API格式**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| 参数 | 描述 |
| --------- | ----------- |
| `schema.name` | **必填。**&#x200B;您正在访问的架构的名称。 |
| `entityId` | 实体的ID。 如果提供，则还必须提供实体命名空间。 |
| `entityIdNS` | 您尝试检索的ID的命名空间。 |

**请求**

您可以使用以下GET请求查看之前摄取的记录数据。

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，其中包含所请求实体的详细信息。 如您所见，这与之前成功摄取的记录相同。

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

通过阅读本文档，您现在了解如何使用流连接将记录数据摄取到[!DNL Experience Platform]。 您可以尝试使用不同的值发起更多调用并检索更新的值。 此外，您还可以通过[!DNL Experience Platform] UI开始监视摄取的数据。 有关详细信息，请参阅[监视数据摄取](../quality/monitor-data-ingestion.md)指南。

有关一般流式摄取的更多信息，请阅读[流式摄取概述](../streaming-ingestion/overview.md)。
