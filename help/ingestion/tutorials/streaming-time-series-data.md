---
keywords: Experience Platform；主页；热门主题；流摄取；摄取；时间系列数据；流时间系列数据；
solution: Experience Platform
title: 使用流摄取API流式传输时间系列数据
topic-legacy: tutorial
type: Tutorial
description: 本教程将帮助您开始使用流摄取API，这是Adobe Experience Platform数据摄取服务API的一部分。
exl-id: 720b15ea-217c-4c13-b68f-41d17b54d500
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 2%

---

# 使用流摄取API流式传输时间系列数据

本教程将帮助您开始使用流摄取API，这是Adobe Experience Platform的一部分 [!DNL Data Ingestion Service] API。

## 快速入门

本教程需要对各种Adobe Experience Platform服务有一定的工作知识。 在开始本教程之前，请查阅以下服务的文档：

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):标准化框架， [!DNL Platform] 组织体验数据。
- [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据，实时提供统一的消费者用户档案。
- [架构注册开发人员指南](../../xdm/api/getting-started.md):涵盖 [!DNL Schema Registry] API以及如何对其进行调用。 这包括了解您的 `{TENANT_ID}`，此过程会显示在本教程中的调用中，并且了解如何创建模式（用于创建用于摄取的数据集）。

此外，本教程还要求您已创建流连接。 有关创建流连接的更多信息，请阅读 [创建流连接教程](./create-streaming-connection.md).

以下部分提供了成功调用流摄取API所需了解的其他信息。

### 读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定操作将在其中执行的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关 [!DNL Platform]，请参阅 [沙盒概述文档](../../sandboxes/home.md).

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的标头：

- Content-Type:application/json

## 基于XDM ExperienceEvent类构建架构

要创建数据集，您首先需要创建一个用于实施 [!DNL XDM ExperienceEvent] 类。 有关如何创建模式的更多信息，请阅读 [架构注册API开发人员指南](../../xdm/api/getting-started.md).

**API格式**

```http
POST /schemaregistry/tenant/schemas
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "type": "object",
    "title": "{SCHEMA_NAME}",
    "description": "{SCHEMA_DESCRIPTION}",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-environment-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-commerce"
        },
        {  
         "$ref":"https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details"
        }
    ],
    "meta:immutableTags": [
        "union"
    ]
}'
```

| 属性 | 描述 |
| -------- | ----------- |
| `title` | 要用于架构的名称。 此名称必须唯一。 |
| `description` | 对要创建的架构进行有意义的描述。 |
| `meta:immutableTags` | 在本例中， `union` 标记，用于将数据保留到 [[!DNL Real-time Customer Profile]](../../profile/home.md). |

**响应**

成功响应会返回HTTP状态201，其中包含新创建架构的详细信息。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "1",
    "type": "object",
    "title": "{SCHEMA_NAME}",
    "description": "{SCHEMA_DESCRIPTION}",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-commerce",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/experienceevent-commerce",
        "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details",
        "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
        "https://ns.adobe.com/xdm/context/experienceevent"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
    "required": [
        "@id",
        "xdm:timestamp"
    ],
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/experienceevent",
        "https://ns.adobe.com/xdm/data/time-series",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
        "https://ns.adobe.com/xdm/context/experienceevent-commerce",
        "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
    "meta:registryMetadata": {
        "repo:createDate": 1551229957987,
        "repo:lastModifiedDate": 1551229957987,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    },
    "meta:tenantNamespace": "{NAMESPACE}"
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{TENANT_ID}` | 此ID用于确保您创建的资源具有正确命名空间，并包含在您的IMS组织内。 有关租户ID的更多信息，请阅读 [模式注册指南](../../xdm/api/getting-started.md#know-your-tenant-id). |

请注意 `$id` 以及 `version` 属性，因为创建数据集时将同时使用这两个属性。

## 为架构设置主标识描述符

接下来，添加 [标识描述符](../../xdm/api/descriptors.md) 到上面创建的架构，使用工作电子邮件地址属性作为主要标识符。 这样做将导致两项更改：

1. 工作电子邮件地址将成为必填字段。 这意味着在未使用此字段的情况下发送的消息将验证失败且不会被摄取。

2. [!DNL Real-time Customer Profile] 将使用工作电子邮件地址作为标识符，以帮助拼合有关该个人的更多信息。

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
    "xdm:sourceProperty":"/_experience/campaign/message/profileSnapshot/workEmail/address",
    "xdm:property":"xdm:code",
    "xdm:isPrimary":true,
    "xdm:namespace":"Email",
    "xdm:sourceSchema":"{SCHEMA_REF_ID}",
    "xdm:sourceVersion":1
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEMA_REF_ID}` | 的 `$id` 之前在构建架构时收到的信息。 它应该如下所示： `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B;**身份命名空间代码**
>
> 请确保代码有效 — 以上示例使用“email”（标准身份命名空间）。 在 [Identity服务常见问题解答](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> 如果要创建自定义命名空间，请按照 [身份命名空间概述](../../identity-service/home.md).

**响应**

成功响应会返回HTTP状态201，其中包含有关新创建的架构主标识命名空间的信息。

```json
{
    "xdm:property": "xdm:code",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "xdm:namespace": "Email",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceVersion": 1,
    "xdm:isPrimary": true,
    "xdm:sourceProperty": "/_experience/campaign/message/profileSnapshot/workEmail/address",
    "@id": "ec31c09e0906561861be5a71fcd964e29ebe7923b8eb0d1e",
    "meta:containerId": "tenant",
    "version": "1",
    "imsOrg": "{ORG_ID}"
}
```

## 为时间系列数据创建数据集

创建架构后，您将需要创建一个数据集以摄取记录数据。

>[!NOTE]
>
>此数据集将启用 **[!DNL Real-time Customer Profile]** 和 **[!DNL Identity]** 设置相应的标记。

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
  -d '{
    "name": "{DATASET_NAME}",
    "description": "{DATASET_DESCRIPTION}",
    "schemaRef": {
        "id": "{SCHEMA_REF_ID}",
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
    },
    "tags": {
        "unifiedIdentity": ["enabled:true"],
        "unifiedProfile": ["enabled:true"]
    }
}'
```

**响应**

成功响应会返回HTTP状态201和一个数组，该数组包含新创建的数据集的ID，格式为 `@/dataSets/{DATASET_ID}`.

```json
[
    "@/dataSets/5e72608b10f6e318ad2dee0f"
]
```


## 创建流连接

创建架构和数据集后，您需要创建流连接以摄取数据。

有关创建流连接的更多信息，请阅读 [创建流连接教程](./create-streaming-connection.md).

## 将时间系列数据摄取到流连接

创建数据集、流连接和数据流后，您可以摄取XDM格式的JSON记录，以在 [!DNL Platform].

**API格式**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 的 `id` 新建流连接的值。 |
| `syncValidation` | 用于开发目的的可选查询参数。 如果设置为 `true`，则可用于立即反馈以确定请求是否成功发送。 默认情况下，此值设置为 `false`. 请注意，如果将此查询参数设置为 `true` 请求的速率将限制为每分钟60次 `CONNECTION_ID`. |

**请求**

将时间系列数据摄取到流连接可以使用源名称或不使用源名称来完成。

以下示例请求将源名称缺失的时间系列数据摄取到平台。 如果数据缺少源名称，它将从流连接定义添加源ID。

两者兼有 `xdmEntity._id` 和 `xdmEntity.timestamp` 是时间系列数据的必填字段。 的 `xdmEntity._id` 属性表示记录本身的唯一标识符， **not** 记录的人员或设备的唯一ID。

您需要生成自己的 `xdmEntity._id` 和 `xdmEntity.timestamp` 以保持一致的方式（如果需要重新摄取记录）来记录。 理想情况下，源系统将包含这些值。 如果ID不可用，请考虑将记录中其他字段的值连接在一起，以创建一个唯一值，该唯一值可在重新摄取时从记录中始终重新生成。

>[!NOTE]
>
>以下API调用会执行 **not** 需要任何身份验证标头。

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "{SCHEMA_REF_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "flowId": "{FLOW_ID}",
        "datasetId": "{DATASET_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity":{
            "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
            "timestamp": "2019-02-23T22:07:01Z",
            "environment": {
                "browserDetails": {
                    "userAgent": "Mozilla\/5.0 (Windows NT 5.1) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/29.0.1547.57 Safari\/537.36 OPR\/16.0.1196.62",
                    "acceptLanguage": "en-US",
                    "cookiesEnabled": true,
                    "javaScriptVersion": "1.6",
                    "javaEnabled": true
                },
                "colorDepth": 32,
                "viewportHeight": 799,
                "viewportWidth": 414
            },
            "productListItems": [
                {
                    "SKU": "CC",
                    "name": "Fernie Snow",
                    "quantity": 30,
                    "priceTotal": 7.8
                }
            ],
            "commerce": {
                "productViews": {
                    "value": 1
                }
            },
            "_experience": {
                "campaign": {
                    "message": {
                        "profileSnapshot": {
                            "workEmail":{
                                "address": "janedoe@example.com"
                            }
                        }
                    }
                }
            }
        }
    }
}'
```

如果要包含源名称，以下示例将显示如何包含该源名称。

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

成功的响应会返回HTTP状态200，其中包含新流式处理的详细信息 [!DNL Profile].

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
| `{CONNECTION_ID}` | 的 `inletId` 流连接的URL。 |
| `xactionId` | 您刚刚发送的记录在服务器端生成的唯一标识符。 此ID可帮助Adobe通过各种系统和调试来跟踪此记录的生命周期。 |
| `receivedTimeMs`:时间戳（以毫秒为单位），显示收到请求的时间。 |
| `syncValidation.status` | 由于查询参数 `syncValidation=true` 添加后，将显示此值。 如果验证成功，则状态将为 `pass`. |

## 检索新摄取的时间系列数据

要验证之前摄取的记录，您可以使用 [[!DNL Profile Access API]](../../profile/api/entities.md) 来检索时间系列数据。 这可以使用对的GET请求来完成 `/access/entities` 端点和使用可选查询参数。 可以使用多个参数，并用与号(&amp;)分隔。”

>[!NOTE]
>
>如果未定义合并策略ID，并且 `schema.name` 或 `relatedSchema.name` is `_xdm.context.profile`, [!DNL Profile Access] 将会获取 **全部** 相关身份。

**API格式**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email
```

| 参数 | 描述 |
| --------- | ----------- |
| `schema.name` | **必需。** 您正在访问的架构的名称。 |
| `relatedSchema.name` | **必需。** 由于您正在访问 `_xdm.context.experienceevent`，此值指定与时间系列事件相关的用户档案实体架构。 |
| `relatedEntityId` | 相关实体的ID。 如果提供，则还必须提供实体命名空间。 |
| `relatedEntityIdNS` | 您尝试检索的ID的命名空间。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**响应**

成功响应会返回HTTP状态200，其中包含所请求实体的详细信息。 如您所见，这是先前摄取的相同时间系列数据。

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "9af5adcc-db9c-4692-b826-65d3abe68c22",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
            "entityId": "9af5adcc-db9c-4692-b826-65d3abe68c22",
            "timestamp": 1582495621000,
            "entity": {
                "environment": {
                    "browserDetails": {
                        "javaScriptVersion": "1.6",
                        "cookiesEnabled": true,
                        "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
                        "acceptLanguage": "en-US",
                        "javaEnabled": true
                    },
                    "colorDepth": 32,
                    "viewportHeight": 799,
                    "viewportWidth": 414
                },
                "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
                "commerce": {
                    "productViews": {
                        "value": 1
                    }
                },
                "productListItems": [
                    {
                        "name": "Fernie Snow",
                        "quantity": 30,
                        "SKU": "CC",
                        "priceTotal": 7.8
                    }
                ],
                "_experience": {
                    "campaign": {
                        "message": {
                            "profileSnapshot": {
                                "workEmail": {
                                    "address": "janedoe@example.com"
                                }
                            }
                        }
                    }
                },
                "timestamp": "2020-02-23T22:07:01Z"
            },
            "lastModifiedAt": "2020-03-18T18:51:19Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

## 后续步骤

通过阅读本文档，您现在可以了解如何将记录数据摄取到 [!DNL Platform] 使用流连接。 您可以尝试使用不同的值发起更多调用并检索更新的值。 此外，您还可以通过 [!DNL Platform] UI。 欲知更多信息，请阅读 [监控数据摄取](../quality/monitor-data-ingestion.md) 的双曲余切值。

有关流式摄取的更多一般信息，请阅读 [流摄取概述](../streaming-ingestion/overview.md).
