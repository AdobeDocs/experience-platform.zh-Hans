---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；体验数据模型；数据模型；架构注册表；架构注册表；ad-hoc；ad-hoc；Ad-hoc；Ad-hoc；教程；教程；创建；架构；架构
solution: Experience Platform
title: 创建临时架构
description: 在特定情况下，可能需要创建体验数据模型(XDM)架构，该架构具有仅供单个数据集使用的命名字段。 这称为“临时”模式。 临时架构用在各种数据摄取工作流中用于Experience Platform，包括摄取CSV文件和创建特定类型的源连接。
type: Tutorial
exl-id: bef01000-909a-4594-8cf4-b9dbe0b358d5
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 2%

---

# 创建临时架构

在特定情况下，可能需要创建一个[!DNL Experience Data Model] (XDM)架构，该架构具有仅供单个数据集使用的命名字段。 这称为“临时”模式。 在[!DNL Experience Platform]的各种数据引入工作流中使用了临时架构，包括引入CSV文件和创建特定类型的源连接。

本文档提供了使用[架构注册表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)创建临时架构的一般步骤。 它旨在与其他[!DNL Experience Platform]教程结合使用，这些教程需要创建临时架构作为其工作流的一部分。 其中每个文档都提供了有关如何为其特定用例正确配置临时模式的详细信息。

## 快速入门

本教程要求您对[!DNL Experience Data Model] (XDM)系统有一定的了解。 在开始本教程之前，请查看以下XDM文档：

- [XDM系统概述](../home.md)： [!DNL Experience Platform]中XDM及其实现的高级概述。
- [架构组合的基础知识](../schema/composition.md)： XDM架构的基本组件概述。

在开始本教程之前，请查看[开发人员指南](../api/getting-started.md)以了解成功调用[!DNL Schema Registry] API所需了解的重要信息。 这包括您的`{TENANT_ID}`、“容器”的概念以及发出请求所需的标头（请特别注意“接受”标头及其可能的值）。

## 创建临时类

XDM架构的数据行为由其底层类决定。 创建临时架构的第一步是基于`adhoc`行为创建类。 这是通过对`/tenant/classes`终结点发出POST请求来完成的。

**API格式**

```http
POST /tenant/classes
```

**请求**

以下请求创建一个新XDM类，该类由有效负载中提供的属性进行配置。 通过在`allOf`数组中提供`$ref`属性设置为`https://ns.adobe.com/xdm/data/adhoc`，该类继承`adhoc`行为。 该请求还定义了一个`_adhoc`对象，其中包含类的自定义字段。

>[!NOTE]
>
>在`_adhoc`下定义的自定义字段因临时架构的用例而异。 有关基于用例的必需自定义字段，请参阅相应教程中的特定工作流。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New ad-hoc class",
        "description": "New ad-hoc class description",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/xdm/data/adhoc"
          },
          {
            "properties": {
              "_adhoc": {
                "type":"object",
                "properties": {
                  "field1": {
                    "type":"string"
                  },
                  "field2": {
                    "type":"string"
                  }
                }
              }
            }
          }
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `$ref` | 新类的数据行为。 对于临时类，此值必须设置为`https://ns.adobe.com/xdm/data/adhoc`。 |
| `properties._adhoc` | 包含类的自定义字段的对象，以字段名称和数据类型的键值对表示。 |

{style="table-layout:auto"}

**响应**

成功的响应将返回新类的详细信息，将`properties._adhoc`对象的名称替换为该类的系统生成的只读唯一标识符GUID。 `meta:datasetNamespace`属性也会自动生成，并包含在响应中。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:altId": "_{TENANT_ID}.classes.6395cbd58812a6d64c4e5344f7b9120f",
    "meta:resourceType": "classes",
    "version": "1.0",
    "title": "New Class",
    "description": "New class description",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/data/adhoc"
        },
        {
            "properties": {
                "_6395cbd58812a6d64c4e5344f7b9120f": {
                    "type": "object",
                    "properties": {
                        "field1": {
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "field2": {
                            "type": "string",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:extends": [
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557527784822,
        "repo:lastModifiedDate": 1557527784822,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

| 属性 | 描述 |
| --- | --- |
| `$id` | 用作新临时类的只读、系统生成的唯一标识符的URI。 此值将在创建临时模式的下一个步骤中使用。 |

{style="table-layout:auto"}

## 创建临时架构

创建临时类后，可以通过向`/tenant/schemas`端点发出POST请求来创建实现该类的新架构。

**API格式**

```http
POST /tenant/schemas
```

**请求**

以下请求创建一个新架构，提供对其有效负载中之前创建的临时类的`$id`的引用(`$ref`)。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New Schema",
        "description": "New schema description.",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
          }
        ]
      }'
```

**响应**

成功的响应返回新创建架构的详细信息，包括其系统生成的只读`$id`。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
        }
    ],
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

## 查看完整的临时架构

>[!NOTE]
>
>此步骤是可选的。如果您不想检查临时架构的字段结构，可以跳至本教程末尾的[后续步骤](#next-steps)部分。

创建临时架构后，您可以发出查找(GET)请求以查看其展开形式的架构。 可通过在GET请求中使用适当的接受标头来做到这一点，如下所示。

**API格式**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 要访问的临时架构的URL编码的`$id` URI或`meta:altId`。 |

{style="table-layout:auto"}

**请求**

以下请求使用Accept标头`application/vnd.adobe.xed-full+json; version=1`，该标头返回架构的展开形式。 请注意，从[!DNL Schema Registry]检索特定资源时，请求的“接受”标头必须包含相关资源的主要版本。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的响应返回架构的详细信息，包括嵌套在`properties`下的所有字段。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "properties": {
        "_6395cbd58812a6d64c4e5344f7b9120f": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "field1": {
                    "type": "string",
                    "meta:xdmType": "string"
                },
                "field2": {
                    "type": "string",
                    "meta:xdmType": "string"
                }
            }
        }
    },
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "bTogM1ON2LO/F7rlcc1iOWmNVy0="
    }
}
```

## 后续步骤 {#next-steps}

通过遵循本教程，您已成功创建新的临时架构。 如果您是作为另一个教程的一部分被带到此文档的，您现在可以使用临时架构的`$id`按照指示完成工作流。

有关使用[!DNL Schema Registry] API的更多信息，请参阅[开发人员指南](../api/getting-started.md)。
