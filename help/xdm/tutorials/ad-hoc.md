---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 创建临时模式
topic: tutorials
translation-type: tm+mt
source-git-commit: 956d1e5b4a994c9ea52d818f3dd6d3ff88cb16b6

---


# 创建临时模式

在特定情况下，可能需要创建一个体验数据模型(XDM)模式，其中的字段以仅由单个数据集使用的名称命名。 这称为&quot;临时&quot;模式。 Ad-hoc模式用于Experience Platform的各种数据摄取工作流，包括摄取CSV文件和创建某些类型的源连接。

此文档提供了使用模式注册表API创建临时模式的一 [般步骤](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)。 它旨在与其他需要在工作流程中创建临时模式的Experience Platform教程结合使用。 每个文档都提供有关如何为其特定用例正确配置临时模式的详细信息。

## 入门指南

本教程需要对体验数据模型(XDM)系统有一个有效的了解。 在开始本教程之前，请查看以下XDM文档：

- [XDM系统概述](../home.md):XDM及其在Experience Platform中实施的高级概述。
- [模式合成的基础知识](../schema/composition.md):XDM模式的基本组件概述。

在开始本教程之前，请查看开 [发人员指南](../api/getting-started.md) ，了解成功调用模式注册表API所需了解的重要信息。 这包括您 `{TENANT_ID}`的“容器”概念以及发出请求所需的标题（特别注意“接受”标题及其可能的值）。

## 创建点对点类

XDM模式的数据行为由其基础类决定。 创建临时模式的第一步是根据行为创建类。 `adhoc` 这是通过向端点发出POST请求来完 `/tenant/classes` 成的。

**API格式**

```http
POST /tenant/classes
```

**请求**

以下请求将创建一个新的XDM类，该类由有效负荷中提供的属性进行配置。 通过提供 `$ref` 数组中设置 `https://ns.adobe.com/xdm/data/adhoc` 的属 `allOf` 性，该类继承了行 `adhoc` 为。 该请求还定义一 `_adhoc` 个对象，该对象包含类的自定义字段。

>[!NOTE] 根据临时模式的 `_adhoc` 用例，在下定义的自定义字段会有所不同。 请参考相应教程中的特定工作流，以了解根据用例需要的自定义字段。

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
| `properties._adhoc` | 包含类的自定义字段的对象，表示为字段名和数据类型的键值对。 |

**响应**

成功的响应返回新类的详细信息，将对象的名称替换为GUID，该GUID是系统生成的类的只读唯一标识符。 `properties._adhoc` 该属 `meta:datasetNamespace` 性也会自动生成并包含在响应中。

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
| `$id` | 用作新ad-hoc类的只读、系统生成的唯一标识符的URI。 该值用于创建临时模式的下一步。 |

## 创建临时模式

创建点对点类后，可以创建新模式，通过向端点发出POST请求来实现该类。 `/tenant/schemas`

**API格式**

```http
POST /tenant/schemas
```

**请求**

以下请求创建新模式，提供(`$ref`)对其有效负荷中先前 `$id` 创建的临时类的引用。

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

成功的响应会返回新创建的模式的详细信息，包括其系统生成的只读内容 `$id`。

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

## 视图全面特设模式

>[!NOTE] 此步骤是可选的。 如果您不想检查临时模式的字段结构，可跳到本教程结 [尾的后续步骤](#next-steps) 。

创建临时模式后，您可以发出查找(GET)请求，以视图其展开形式的模式。 在GET请求中使用适当的“接受”标头即可完成此操作，如下所示。

**API格式**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | URL编码的 `$id` URI或 `meta:altId` 要访问的临时模式的URI。 |

**请求**

以下请求使用“接受”标 `application/vnd.adobe.xed-full+json; version=1`题，它返回模式的扩展形式。 请注意，从模式注册表检索特定资源时，请求的“接受”标题必须包含相关资源的主要版本。

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

成功的响应会返回模式的详细信息，包括嵌套在下面的所有字段 `properties`。

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

通过遵循本教程，您已成功创建了一个新的临时模式。 如果您是作为另一个教程的一部分被带到本文档的，您现在可以使用临时模式按照指示完成工作流。 `$id`

有关使用模式注册表API的详细信息，请参阅开发人 [员指南](../api/getting-started.md)。