---
keywords: Experience Platform；主页；热门主题；API;XDM;XDM；系统；体验数据模型；体验数据模型；数据模型；模式注册；模式注册；ad-hoc;adhoc;ad-hoc;Ad-hoc;Ad-hoc；教程；教程；创建；模式;模式
solution: Experience Platform
title: 创建点对点模式
description: 在特定情况下，可能需要创建一个体验数据模型(XDM)模式，其中的字段以仅由单个数据集使用的名称命名。 这称为“临时”模式。 临时模式用于各种Experience Platform数据获取工作流，包括获取CSV文件和创建某些类型的源连接。
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 2%

---


# 创建点对点模式

在特定情况下，可能需要创建一个[!DNL Experience Data Model](XDM)模式，其中的字段以仅由单个数据集使用的名称命名。 这称为“临时”模式。 专门模式用于[!DNL Experience Platform]的各种数据获取工作流，包括获取CSV文件和创建某些类型的源连接。

此文档提供了使用[模式注册表API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)创建点对点模式的一般步骤。 它旨在与其他需要创建临时模式作为其工作流程的一部分的[!DNL Experience Platform]教程结合使用。 这些文档中的每一个都提供了有关如何为其特定用例正确配置点对点模式的详细信息。

## 入门指南

本教程需要对[!DNL Experience Data Model](XDM)系统有正确的了解。 在开始本教程之前，请查看以下XDM文档：

- [XDM系统概述](../home.md):XDM及其实施的高级概述 [!DNL Experience Platform]。
- [模式合成基础](../schema/composition.md):XDM模式的基本组件概述。

在开始本教程之前，请查看[开发人员指南](../api/getting-started.md)，了解成功调用[!DNL Schema Registry] API所需了解的重要信息。 这包括您的`{TENANT_ID}`、“容器”的概念以及发出请求所需的标头（特别要注意“接受”标头及其可能的值）。

## 创建点对点类

XDM模式的数据行为由其基础类决定。 创建点对点模式的第一步是根据`adhoc`行为创建类。 这是通过向`/tenant/classes`端点发出POST请求来完成的。

**API格式**

```http
POST /tenant/classes
```

**请求**

以下请求将创建一个新的XDM类，该类由有效负荷中提供的属性进行配置。 通过提供设置为`allOf`数组中`https://ns.adobe.com/xdm/data/adhoc`的`$ref`属性，此类继承了`adhoc`行为。 请求还定义一个`_adhoc`对象，该对象包含类的自定义字段。

>[!NOTE]
>
>在`_adhoc`下定义的自定义字段因临时模式的用例而异。 请参考相应教程中的特定工作流，以了解根据用例需要的自定义字段。

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
| `$ref` | 新类的数据行为。 对于点对点类，此值必须设置为`https://ns.adobe.com/xdm/data/adhoc`。 |
| `properties._adhoc` | 包含类的自定义字段的对象，表示为字段名称和数据类型的键值对。 |

**响应**

成功的响应会返回新类的详细信息，将`properties._adhoc`对象的名称替换为系统生成的、只读的类唯一标识符的GUID。 `meta:datasetNamespace`属性也会自动生成并包含在响应中。

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

创建点对点类后，可以创建新模式，通过向`/tenant/schemas`端点发出POST请求来实现该类。

**API格式**

```http
POST /tenant/schemas
```

**请求**

以下请求创建新模式，为先前创建的点对点类在其负载中的`$id`提供引用(`$ref`)。

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

成功的响应会返回新创建模式的详细信息，包括系统生成的只读`$id`。

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
>此步骤是可选的。如果您不想检查临时模式的字段结构，可跳到本教程末尾的[后续步骤](#next-steps)部分。

创建临时模式后，您可以发出查找(GET)请求，以视图其展开形式的模式。 在GET请求中使用相应的接受标头即可完成此操作，如下所示。

**API格式**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 要访问的临时模式的URL编码的`$id` URI或`meta:altId`。 |

**请求**

以下请求使用Accept头`application/vnd.adobe.xed-full+json; version=1`，它返回模式的扩展形式。 请注意，从[!DNL Schema Registry]检索特定资源时，请求的“接受”标头必须包含相关资源的主要版本。

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

成功的响应返回模式的详细信息，包括嵌套在`properties`下的所有字段。

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

通过遵循本教程，您已成功创建了新的临时模式。 如果您是作为另一个教程的一部分被带到此文档的，您现在可以按照指示使用临时模式的`$id`来完成工作流。

有关使用[!DNL Schema Registry] API的详细信息，请参阅[开发人员指南](../api/getting-started.md)。