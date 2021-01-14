---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;class registry;Schema Registry;class;Class;classes;Classes;create
solution: Experience Platform
title: 创建类
description: 模式注册表API中的/classes端点允许您在体验应用程序中以编程方式管理XDM类。
topic: developer guide
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 1%

---


# 类端点

所有体验模式模型(XDM)必须基于类。 类确定基于该类的所有模式必须包含的公用属性的基结构，以及哪些混合符合在这些模式中使用的条件。 此外，模式的类决定模式将包含的数据的行为方面，其中有两种类型：

* **[!UICONTROL 记录]**:提供有关主题属性的信息。主题可以是组织或个人。
* **[!UICONTROL 时间系列]**:提供记录主体直接或间接采取操作时系统的快照。

>[!NOTE]
>
>有关数据行为类对模式合成的影响的详细信息，请参阅[模式合成基础知识](../schema/composition.md)。

[!DNL Schema Registry] API中的`/classes`端点允许您以编程方式管理体验应用程序中的类。

## 入门指南

本指南中使用的端点是[[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml)的一部分。 在继续之前，请查看[入门指南](./getting-started.md)，了解相关文档的链接、阅读此文档中示例API调用的指南，以及成功调用任何Experience PlatformAPI所需的重要头信息。

## 检索类{#list}的列表

您可以通过分别向`/global/classes`或`/tenant/classes`发出列表请求，来GET`global`或`tenant`容器下的所有类。

>[!NOTE]
>
>列出资源时，模式注册表将结果集限制为300项。 要返回超出此限制的资源，必须使用分页参数。 还建议您使用其他查询参数来筛选结果并减少返回的资源数。 有关详细信息，请参见附录文档中的[查询参数](./appendix.md#query)一节。

**API格式**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 要从以下位置检索类的容器:`global`用于Adobe创建的类，或`tenant`用于您的组织拥有的类。 |
| `{QUERY_PARAMS}` | 可选查询参数，用于筛选结果。 有关可用参数的列表，请参见[附录文档](./appendix.md#query)。 |

**请求**

以下请求从`tenant`列表检索类的容器，使用`orderby`查询参数按类的`title`属性对类进行排序。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

响应格式取决于请求中发送的`Accept`头。 以下`Accept`标头可用于列出类：

| `Accept` 标题 | 描述 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每个资源的简短摘要。 这是列出资源的建议标头。 (限制：300) |
| `application/vnd.adobe.xed+json` | 为每个资源返回完整的JSON类，其中包含原始`$ref`和`allOf`。 (限制：300) |

**响应**

上述请求使用`application/vnd.adobe.xed-id+json` `Accept`头，因此响应仅包括每个类的`title`、`$id`、`meta:altId`和`version`属性。 使用其他`Accept`头(`application/vnd.adobe.xed+json`)返回每个类的所有属性。 根据您在响应中需要的信息，选择相应的`Accept`头。

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
      "meta:altId": "_{TENANT_ID}.classes.01b7b1745e8ac4ed1e8784ec91b6afa7",
      "version": "1.0",
      "title": "Hotel"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/d43b86253676af50da3f671ecdd26ff9",
      "meta:altId": "_{TENANT_ID}.classes.d43b86253676af50da3f671ecdd26ff9",
      "version": "1.1",
      "title": "Property"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/366f015dbfea802455fbc46c3b27f771",
      "meta:altId": "_{TENANT_ID}.classes.366f015dbfea802455fbc46c3b27f771",
      "version": "1.0",
      "title": "Subscription"
    }
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 3
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/classes"
    }
  }
}
```

## 查找类{#lookup}

您可以通过在GET请求路径中包含该类的ID来查找特定类。

**API格式**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 存放要检索的类的容器:`global`表示Adobe创建的类，或`tenant`表示您的组织拥有的类。 |
| `{CLASS_ID}` | 要查找的类的`meta:altId`或URL编码的`$id`。 |

**请求**

以下请求按路径中提供的`meta:altId`值检索类。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

响应格式取决于请求中发送的`Accept`头。 所有查找请求都要求`version`包含在`Accept`标头中。 以下`Accept`标头可用：

| `Accept` 标题 | 描述 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | 具有`$ref`和`allOf`的原始数据具有标题和说明。 |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` 并 `allOf` 且有标题和说明。 |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | 没有标题或说明的原始数据，具有`$ref`和`allOf`。 |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` 并解 `allOf` 析，无标题或说明。 |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` 和包 `allOf` 含的描述符。 |

**响应**

成功的响应会返回类的详细信息。 返回的字段取决于请求中发送的`Accept`头。 尝试不同的`Accept`标头，比较响应并确定最适合您的用例的标头。

```json
{
  "$id":"https://ns.adobe.com/{TENANT_ID}/classes/f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:altId":"_{TENANT_ID}.classes.f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:resourceType":"classes",
  "version":"1.1",
  "title":"Hotel",
  "type":"object",
  "description":"Base class for the Hotels schema",
  "definitions":{
    "customFields":{
      "type":"object",
      "properties":{
        "_{TENANT_ID}":{
          "type":"object",
          "properties":{
            "Address":{
              "title":"Address",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/common/address",
              "type":"object",
              "meta:xdmType":"object"
            },
            "phoneNumber":{
              "title":"Phone Number",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/context/phonenumber",
              "type":"object",
              "meta:xdmType":"object"
            },
            "brand":{
              "title":"Brand",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            },
            "hotelId":{
              "title":"Hotel ID",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            }
          },
          "meta:xdmType":"object"
        }
      },
      "meta:xdmType":"object"
    }
  },
  "allOf":[
    {
      "$ref":"https://ns.adobe.com/xdm/data/record",
      "type":"object",
      "meta:xdmType":"object"
    },
    {
      "$ref":"#/definitions/customFields",
      "type":"object",
      "meta:xdmType":"object"
    }
  ],
  "imsOrg":"{IMS_ORG}",
  "meta:extensible":true,
  "meta:abstract":true,
  "meta:extends":[
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:xdmType":"object",
  "meta:registryMetadata":{
    "repo:createdDate":1593643258779,
    "repo:lastModifiedDate":1597246362579,
    "xdm:createdClientId":"{CLIENT_ID}",
    "xdm:lastModifiedClientId":"{CLIENT_ID}",
    "xdm:createdUserId":"{USER_ID}",
    "xdm:lastModifiedUserId":"{USER_ID}",
    "eTag":"502f89ee16b8ab2e6b4ea09ecf0ab1e5614907db755051c1f3c65a273001d725",
    "meta:globalLibVersion":"1.15.4"
  },
  "meta:containerId":"tenant",
  "meta:tenantNamespace":"_{TENANT_ID}"
}
```

## 创建类{#create}

您可以通过发出容器请求在`tenant`POST下定义自定义类。

>[!IMPORTANT]
>
>当根据您定义的自定义类编写模式时，您将无法使用标准混音。 每个mixin定义它们在其`meta:intendedToExtend`属性中兼容的类。 一旦开始定义与新类兼容的混音（通过在混音的`meta:intendedToExtend`字段中使用新类的`$id`），您就可以在每次定义实现所定义类的模式时重用这些混音。 有关详细信息，请参见[创建mixin](./mixins.md#create)和[创建模式](./schemas.md#create)的相关部分。
>
>如果您计划在实时客户用户档案中使用基于自定义类的模式，还必须记住，合并模式只基于共享同一类的模式构建。 如果要在合并中包含另一个类(如[!UICONTROL XDM单个用户档案]或[!UICONTROL XDM ExperienceEvent])的自定义类模式，则必须与使用该类的另一个模式建立关系。 有关详细信息，请参阅教程中的[在API](../tutorials/relationship-api.md)中建立两个模式之间的关系。

**API格式**

```http
POST /tenant/classes
```

**请求**

创建(POST)类的请求必须包含`allOf`属性，该属性包含`$ref`到以下两个值之一：`https://ns.adobe.com/xdm/data/record`或`https://ns.adobe.com/xdm/data/time-series`。 这些值表示类所基于的行为（分别是记录或时间序列）。 有关记录数据和时间序列数据之间差异的详细信息，请参见[模式合成基础知识](../schema/composition.md)中有关行为类型的一节。

在定义类时，您还可以在类定义中包含混音或自定义字段。 这将导致添加的混音和字段包含在实现该类的所有模式中。 以下示例请求定义一个名为“Property”的类，它捕获有关公司拥有和操作的不同属性的信息。 它包含每次使用类时要包含的`propertyId`字段。

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
| `_{TENANT_ID}` | 您的组织的`TENANT_ID`命名空间。 您的组织创建的所有资源都必须包含此属性，以避免与[!DNL Schema Registry]中的其他资源发生冲突。 |
| `allOf` | 新类要继承其属性的资源列表。 数组中的`$ref`对象之一定义类的行为。 在此示例中，类继承“记录”行为。 |

**响应**

成功的响应返回HTTP状态201（已创建）和包含新创建类的详细信息（包括`$id`、`meta:altId`和`version`）的有效负荷。 这三个值是只读的，由[!DNL Schema Registry]指定。

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

执行对[的GET请求，列表`tenant`容器中的所有类](#list)现在将包括属性类。 您还可以[使用URL编码的`$id`执行查找(GET)请求](#lookup)以直接视图新类。

## 更新类{#put}

您可以通过PUT操作替换整个类，实质上是重写资源。 当通过PUT请求更新类时，主体必须包括在POST请求中创建新类](#create)时所需的所有字段。[

>[!NOTE]
>
>如果只想更新某个类的一部分，而不是完全替换它，请参阅[更新该类的某一部分的部分。](#patch)

**API格式**

```http
PUT /tenant/classes/{CLASS_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CLASS_ID}` | 要重写的类的`meta:altId`或URL编码的`$id`。 |

**请求**

以下请求重写现有类，更改其其中一个字段的`description`和`title`。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property",
        "description": "Base class for properties operated by a company.",
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
                        "title": "Property ID",
                        "type": "string",
                        "description": "Unique Property ID string."
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

**响应**

成功的响应会返回更新类的详细信息。

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
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
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
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

## 更新类{#patch}的一部分

您可以使用PATCH请求更新类的一部分。 [!DNL Schema Registry]支持所有标准JSON修补程序操作，包括`add`、`remove`和`replace`。 有关JSON修补程序的详细信息，请参阅[API基础指南](../../landing/api-fundamentals.md#json-patch)。

>[!NOTE]
>
>如果要用新值替换整个资源，而不是更新单个字段，请参阅[中的使用PUT操作](#put)替换类的部分。

**API格式**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| 参数 | 描述 |
| --- | --- |
| `{CLASS_ID}` | 要更新的类的URL编码的`$id` URI或`meta:altId`。 |

**请求**

以下示例请求更新现有类的`description`及其其中一个字段的`title`。

请求主体采用数组的形式，每个列出的对象代表对单个字段的特定更改。 每个对象都包括要执行的操作(`op`)，应在(`path`)上执行该操作的字段，以及该操作应包括哪些信息(`value`)。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "replace", "path": "/description", "value":  "Base class for properties operated by a company."},
        { "op": "replace", "path": "/definitions/property/properties/_{TENANT_ID}/properties/property/properties/propertyId/title", "value": "Unique Property ID string" }
      ]'
```

**响应**

响应显示两个操作都成功执行。 `description`和`propertyId`字段的`title`已更新。

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
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
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
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

## 删除类{#delete}

有时可能需要从模式注册表中删除类。 这是通过使用路径中提供的类ID执行DELETE请求来完成的。

**API格式**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CLASS_ID}` | 要删除的类的URL编码的`$id` URI或`meta:altId`。 |

**请求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态204（无内容）和空白正文。

可以尝试对类使用[查找(GET)请求](#lookup)来确认删除。 您需要在请求中包含`Accept`头，但应接收HTTP状态404（找不到），因为类已从模式注册表中删除。