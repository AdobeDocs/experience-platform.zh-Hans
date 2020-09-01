---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;class;Class;classes;Classes;create
solution: Experience Platform
title: 创建类
description: 模式的主要构建块是类。 类包含必须定义的最小字段集，才能捕获模式的核心数据。 例如，如果你为汽车和卡车设计模式，他们很可能使用一个叫做Vehicle的类，它描述了所有车辆的基本公共属性。
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---


# 创建类

模式的主要构建块是类。 类包含必须定义的最小字段集，才能捕获模式的核心数据。 例如，如果你为汽车和卡车设计模式，他们很可能使用一个叫做Vehicle的类，它描述了所有车辆的基本公共属性。

Adobe和其他合作伙伴提供了多个标准 [!DNL Experience Platform] 类，但您也可以定义自己的类并将它们保存到 [!DNL Schema Registry]。 然后，您可以构建实现您创建的类的模式，并定义与新定义的类兼容的混音。

>[!NOTE]
>
>在根据您定义的类编写模式时，您将无法使用标准混音。 每个mixin定义它们在其属性中兼容的 `meta:intendedToExtend` 类。 一旦开始定义与新类兼容的混音(通过使用混音 `$id` 字段中新类 `meta:intendedToExtend` 的混音)，您将能够在每次定义实现您定义的类的模式时重用这些混音。 有关详细信息， [请参阅](create-mixin.md) “创 [建混合](create-schema.md) 和创建模式”一节。

**API格式**

```http
POST /tenant/classes
```

**请求**

创建(POST)类的请求必须包含一个 `allOf` 属性，该属 `$ref` 性包含两个值之一： `https://ns.adobe.com/xdm/data/record` 或 `https://ns.adobe.com/xdm/data/time-series`者 这些值表示类所基于的行为（分别是记录或时间序列）。 有关记录数据与时间序列数据之间差异的详细信息，请参阅模式合成基础知识中有关 [行为类型的部分](../schema/composition.md)。

在定义类时，您还可以在类定义中包含混音或自定义字段。 这将导致添加的混音和字段包含在实现该类的所有模式中。 以下示例请求定义一个名为“Property”的类，它捕获有关公司拥有和操作的不同属性的信息。 它包括 `propertyId` 每次使用类时要包含的字段。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property",
        "description":"Properties owned and operated by the company.",
        "type":"object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property Identification Number",
                        "type": "string",
                        "description": "Unique Property identification number"
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `_{TENANT_ID}` | 组 `TENANT_ID` 织的命名空间。 您的组织创建的所有资源都必须包含此属性，以避免与中的其他资源发生冲突 [!DNL Schema Registry]。 |
| `allOf` | 新类要继承其属性的资源列表。 数组中 `$ref` 的一个对象定义类的行为。 在此示例中，类继承“记录”行为。 |

**响应**

成功的响应会返回HTTP状态201（已创建）和包含新创建类的详细信息（包括、和） `$id`的 `meta:altId`有效负荷 `version`。 这三个值是只读的，由指定 [!DNL Schema Registry]。

```JSON
{
    "title": "Property",
    "description": "Properties owned and operated by the company.",
    "type": "object",
    "definitions": {
        "property": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "property": {
                            "title": "Property Information",
                            "type": "object",
                            "description": "Information about different owned and operated properties.",
                            "properties": {
                                "propertyId": {
                                    "title": "Property Identification Number",
                                    "type": "string",
                                    "description": "Unique Property identification number",
                                    "meta:xdmType": "string"
                                }
                            },
                            "meta:xdmType": "object"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/data/record"
        },
        {
            "$ref": "#/definitions/property"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:extends": [
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "version": "1.0",
    "meta:resourceType": "classes",
    "meta:registryMetadata": {
        "repo:createDate": 1552086405448,
        "repo:lastModifiedDate": 1552086405448,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

执行GET请求以列表租户容器中的所有类现在将包括属性类。 您还可以使用URL编码的URI执行查找(GET)请 `$id` 求，以直接视图新类。 执行查找请求 `version` 时，请务必在“接受”标题中包含。
