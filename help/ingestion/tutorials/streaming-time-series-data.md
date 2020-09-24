---
keywords: Experience Platform;home;popular topics;streaming ingestion;ingestion;time series data;stream time series data;
solution: Experience Platform
title: 流式时间序列数据
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 2%

---


# 将时间序列数据流化到Adobe Experience Platform

本教程将帮助您开始使用流式摄取API，它是Adobe Experience PlatformAPI的一 [!DNL Data Ingestion Service] 部分。

## 入门指南

本教程需要对Adobe Experience Platform各项服务有一定的工作知识。 在开始本教程之前，请查看以下服务的相关文档：

- [[!DNL体验数据模型(XDM)]](../../xdm/home.md):组织体验数据 [!DNL Platform] 的标准化框架。
- [[!DNL实时客户用户档案]](../../profile/home.md):根据来自多个来源的汇总数据实时提供统一的消费者用户档案。
- [模式注册开发人员指南](../../xdm/api/getting-started.md):全面的指南，涵盖API的每个可用端点 [!DNL Schema Registry] 以及如何向它们发出调用。 这包括了解您 `{TENANT_ID}`在本教程中的调用，以及了解如何创建模式，该数据用于创建用于摄取的数据集。

此外，本教程要求您已创建流连接。 有关创建流连接的详细信息，请阅读创 [建流连接教程](./create-streaming-connection.md)。

以下各节提供了成功调用流式摄取API所需了解的其他信息。

### 读取示例API调用

本指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

- 授权：承载者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有资源 [!DNL Experience Platform] 都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信 [!DNL Platform]息，请参阅 [沙箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要附加标头：

- 内容类型：application/json

## 根据XDM ExperienceEvent类编写模式

要创建数据集，您首先需要创建实现该类的新模式 [!DNL XDM ExperienceEvent] 集。 有关如何创建模式的更多信息，请阅读 [模式注册API开发人员指南](../../xdm/api/getting-started.md)。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `title` | 要用于模式的名称。 此名称必须唯一。 |
| `description` | 您正在创建的模式的有意义描述。 |
| `meta:immutableTags` | 在本例中，标 `union` 签用于将您的数据 [保留到[!DNL实时客户用户档案]](../../profile/home.md)。 |

**响应**

成功的响应会返回HTTP状态201，其中包含您新创建的模式的详细信息。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "{SCHEMA_VERSION}",
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
    "imsOrg": "{IMS_ORG}",
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
    "imsOrg": "{IMS_ORG}",
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
| `{TENANT_ID}` | 此ID用于确保您创建的资源命名正确且包含在IMS组织中。 有关租户ID的详细信息，请阅读 [模式注册指南](../../xdm/api/getting-started.md#know-your-tenant-id)。 |

请注意属性 `$id` 和属性，因 `version` 为创建数据集时将同时使用这两个属性。

## 为模式设置主标识描述符

接下来，将标识 [描述符添加](../../xdm/api/descriptors.md) 到上面创建的模式，使用工作电子邮件地址属性作为主标识符。 执行此操作将导致两个更改：

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
| `{SCHEMA_REF_ID}` | 您 `$id` 之前在构建模式时收到的内容。 它应该是这样的： `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B; &#x200B; Identity命名空间代码&#x200B;****
>
> 请确保代码有效——上例使用“email”，它是标准身份命名空间。 其他常用的标准身份命名空间可在Identity Service常见问 [题解答中找到](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform)。
>
> 如果要创建自定义命名空间，请按照标识命名空间概述中概 [述的步骤操作](../../identity-service/home.md)。
**响应**

成功的响应返回HTTP状态201，其中包含有关该模式新创建的主标识命名空间的信息。

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
    "imsOrg": "{IMS_ORG}"
}
```

## 为时间序列数据创建数据集

创建模式后，您需要创建数据集以采集记录数据。

>[!NOTE]
>
>此数据集将通过设 **[!DNL Real-time Customer Profile]** 置相 **[!DNL Identity]** 应的标记启用。

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
  -d '{
    "name": "{DATASET_NAME}",
    "description": "{DATASET_DESCRIPTION}",
    "schemaRef": {
        "id": "{SCHEMA_REF_ID}",
        "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
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
    "@/dataSets/5e72608b10f6e318ad2dee0f"
]
```

## 将时间序列数据引入流连接

在数据集和流连接到位后，您可以收集XDM格式的JSON记录，以在中收集时间序列数 [!DNL Platform]据。

**API格式**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 新 `id` 创建的流连接的值。 |
| `synchronousValidation` | 用于开发目的的可选查询参数。 如果设置为 `true`，则可以使用它进行即时反馈，以确定请求是否成功发送。 默认情况下，此值设置为 `false`。 |

**请求**

>[!NOTE]
>
>您需要生成自己的和 `xdmEntity._id` 产 `xdmEntity.timestamp`品。 生成ID的一个好方法是使用UUID。 此外，以下API调用不 **需要** 任何身份验证头。


```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "{SCHEMA_REF_ID}",
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

**响应**

成功的响应会返回HTTP状态200，其中包含新流的详细信息 [!DNL Profile]。

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
| `receivedTimeMs`:显示接收请求的时间的时间戳（以毫秒为单位）。 |
| `synchronousValidation.status` | 由于添加了查询 `synchronousValidation=true` 参数，因此将显示此值。 如果验证成功，则状态为 `pass`。 |

## 检索新摄取的时间序列数据

要验证之前摄取的记录，可 [以使用[!DNL用户档案访问API]](../../profile/api/entities.md) 检索时间序列数据。 这可以使用对端点的GET请求和 `/access/entities` 可选的查询参数来完成。 可以使用多个参数，用和号(&amp;)分隔。”

>[!NOTE]
>
>如果未定义合并策略ID，且 `schema.name` 或 `relatedSchema.name` 为 `_xdm.context.profile`，将 [!DNL Profile Access] 获取所 **有相关** 标识。

**API格式**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email
```

| 参数 | 描述 |
| --------- | ----------- |
| `schema.name` | **必需。** 您访问的模式的名称。 |
| `relatedSchema.name` | **必需。** 由于您访问的 `_xdm.context.experienceevent`是用户档案实体，因此此值指定与时间序列事件相关的模式。 |
| `relatedEntityId` | 相关实体的ID。 如果提供，则还必须提供实体命名空间。 |
| `relatedEntityIdNS` | 您尝试检索的ID的命名空间。 |

**请求**

```shell
curl -X GET \
  https://platform-stage.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**响应**

成功的响应返回HTTP状态200，其中包含所请求实体的详细信息。 正如您所看到的，这是之前摄取的同一时间序列数据。

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

通过阅读此文档，您现在了解如何使用流连接将记录 [!DNL Platform] 数据引入。 您可以尝试使用不同的值进行更多调用并检索更新的值。 此外，您还可以通过UI开始监视所摄 [!DNL Platform] 数据。 有关详细信息，请阅读监 [视数据获取指南](../quality/monitor-data-flows.md) 。

有关流摄取的详细信息，请阅读流摄 [取概述](../streaming-ingestion/overview.md)。
