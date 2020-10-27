---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;ad-hoc;ad hoc;adhoc;Ad-hoc;Ad hoc;Adhoc;tutorial;Tutorial;create;Create;schema;Schema
solution: Experience Platform
title: 创建点对点模式
description: 在特定情况下，可能需要创建一个体验数据模型(XDM)模式，其中的字段以仅由单个数据集使用的名称命名。 这称为“临时”模式。 临时模式用于各种Experience Platform数据获取工作流，包括获取CSV文件和创建某些类型的源连接。
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 097fe219e0d64090de758f388ba98e6024db2201
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 2%

---


# 创建点对点模式

在特定情况下，可能需要创建一个( [!DNL Experience Data Model] XDM)模式，其中的字段以名称命名，仅供单个数据集使用。 这称为“临时”模式。 临时模式用于各种数据获取工作流, [!DNL Experience Platform]包括获取CSV文件和创建某些类型的源连接。

此文档提供了使用模式注册表API创建点对点模式的 [一般步骤](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)。 它旨在与需要在工作流程中创 [!DNL Experience Platform] 建临时模式的其他教程结合使用。 这些文档中的每一个都提供了有关如何为其特定用例正确配置点对点模式的详细信息。

## 入门指南

本教程需要对(XDM)系 [!DNL Experience Data Model] 统有良好的了解。 在开始本教程之前，请查看以下XDM文档：

- [XDM系统概述](../home.md):XDM及其实施的高级概述 [!DNL Experience Platform]。
- [模式合成基础](../schema/composition.md):XDM模式的基本组件概述。

在开始本教程之前，请查 [看开发人员指南](../api/getting-started.md) ，了解成功调用API所需了解的重要 [!DNL Schema Registry] 信息。 这包括您 `{TENANT_ID}`的、“容器”的概念以及发出请求所需的标题（特别要注意“接受”标题及其可能的值）。

## 创建点对点类

XDM模式的数据行为由其基础类决定。 创建点对点模式的第一步是根据行为创建类 `adhoc` 。 这是通过向端点发出POST请求来完 `/tenant/classes` 成的。

**API格式**

```http
POST /tenant/classes
```

**请求**

以下请求将创建一个新的XDM类，该类由有效负荷中提供的属性进行配置。 通过提供 `$ref` 数组中 `https://ns.adobe.com/xdm/data/adhoc` 的属 `allOf` 性集，此类继承行 `adhoc` 为。 该请求还定义一 `_adhoc` 个对象，它包含类的自定义字段。

>[!NOTE]
>
>在下定义的自定 `_adhoc` 义字段因临时模式的用例而异。 请参考相应教程中的特定工作流，以了解根据用例需要的自定义字段。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `$ref` | 新类的数据行为。 对于点对点类，此值必须设置为 `https://ns.adobe.com/xdm/data/adhoc`。 |
| `properties._adhoc` | 包含类的自定义字段的对象，表示为字段名称和数据类型的键值对。 |

**响应**

成功的响应会返回新类的详细信息，将对 `properties._adhoc` 象的名称替换为系统生成的、只读的类唯一标识符的GUID。 该 `meta:datasetNamespace` 属性也自动生成并包含在响应中。

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
    "imsOrg": "{IMS_ORG}",
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
| `$id` | 用作新ad-hoc类的只读、系统生成的唯一标识符的URI。 此值用于创建临时模式的下一步。 |

## 创建点对点模式

创建点对点类后，可以创建新模式，通过向端点发出POST请求来实现该 `/tenant/schemas` 类。

**API格式**

```http
POST /tenant/schemas
```

**请求**

以下请求创建新模式，提`$ref`供() `$id` 对其负载中先前创建的点对点类的引用。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的响应会返回新创建模式的详细信息，包括其系统生成的只读 `$id`。

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
    "imsOrg": "{IMS_ORG}",
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

## 视图完整临时模式

>[!NOTE]
>
>此步骤是可选的。如果您不想检查临时模式的字段结构，可跳到本教 [程末尾的](#next-steps) “下一步”部分。

创建临时模式后，您可以发出查找(GET)请求，以视图其展开形式的模式。 在GET请求中使用相应的接受标头即可完成此操作，如下所示。

**API格式**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 要访问的 `$id` URL编 `meta:altId` 码的URI或临时模式的URI。 |

**请求**

以下请求使用“接受” `application/vnd.adobe.xed-full+json; version=1`标题，它返回模式的扩展形式。 请注意，从中检索特定资源时，请 [!DNL Schema Registry]求的“接受”标题必须包含相关资源的主要版本。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的响应会返回模式的详细信息，包括嵌套在下的所有字段 `properties`。

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
    "imsOrg": "{IMS_ORG}",
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

通过遵循本教程，您已成功创建了新的临时模式。 如果您是作为另一个教程的一部分被带到此文档的，您现在可以 `$id` 使用临时模式按照指示完成工作流。

有关使用API的详细 [!DNL Schema Registry] 信息，请参阅开发 [人员指南](../api/getting-started.md)。