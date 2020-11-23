---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;class registry;Schema Registry;class;Class;classes;Classes;create
solution: Experience Platform
title: 创建类
description: 模式注册表API中的/classes端点允许您在体验应用程序中以编程方式管理XDM类。
topic: developer guide
translation-type: tm+mt
source-git-commit: b79482635d87efd5b79cf4df781fc0a3a6eb1b56
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 1%

---


# 类端点

所有体验模式模型(XDM)必须基于类。 类确定基于该类的所有模式必须包含的公用属性的基结构，以及哪些混合符合在这些模式中使用的条件。 此外，模式的类决定模式将包含的数据的行为方面，其中有两种类型：

* **[!UICONTROL 记录]**:提供有关主题属性的信息。 主题可以是组织或个人。
* **[!UICONTROL 时间系列]**:提供记录主体直接或间接采取操作时系统的快照。

>[!NOTE]
>
>有关模式行为如何影响模式排版的更多信息类，请参阅排 [版的基础知识](../schema/composition.md)。

API `/classes` 中的端点 [!DNL Schema Registry] 允许您以编程方式管理体验应用程序中的类。

## 入门指南

本指南中使用的端点是API的一 [[!DNL Schema Registry] 部分](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml)。 在继续之前，请查 [看入门指南](./getting-started.md) ，了解相关文档的链接、阅读此文档中示例API调用的指南，以及成功调用任何Experience PlatformAPI所需标头的重要信息。

## 检索类列表 {#list}

您可以通过分别向或发出 `global` 列表 `tenant` 请求来容器或GET下 `/global/classes` 的所有 `/tenant/classes`类。

>[!NOTE]
>
>列出资源时，模式注册表将结果集限制为300项。 要返回超出此限制的资源，必须使用分页参数。 还建议您使用其他查询参数来筛选结果并减少返回的资源数。 有关详细信息，请 [参阅附录](./appendix.md#query) 文档中有关查询参数的一节。

**API格式**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 要从以下位置检索类的容器: `global` 用于Adobe创建的类 `tenant` 或您的组织拥有的类。 |
| `{QUERY_PARAMS}` | 可选查询参数，用于筛选结果。 有关可 [用参数的列表](./appendix.md#query) ，请参阅附录文档。 |

**请求**

以下请求从列表中检索类容器, `tenant` 使用查询 `orderby` 参数按类的属性对类进行 `title` 排序。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

响应格式取决于在请 `Accept` 求中发送的标头。 列出类 `Accept` 时可以使用以下标题：

| `Accept` 标题 | 描述 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每个资源的简短摘要。 这是列出资源的建议标头。 (限制：300) |
| `application/vnd.adobe.xed+json` | 为每个资源返回完整的JSON类，其中包含 `$ref` 原始 `allOf` 资源。 (限制：300) |

**响应**

上述请求使用 `application/vnd.adobe.xed-id+json` 了标 `Accept` 头，因此响应只包括每个类的 `title`、 `$id`、 `meta:altId`和 `version` 属性。 使用其他 `Accept` 标题(`application/vnd.adobe.xed+json`)返回每个类的所有属性。 根据您在 `Accept` 响应中需要的信息选择相应的标题。

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

## 查找课程 {#lookup}

您可以通过在GET请求路径中包含该类的ID来查找特定类。

**API格式**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 存放要检索的类的容器: `global` 用于Adobe创建的类 `tenant` 或您的组织拥有的类。 |
| `{CLASS_ID}` | 要 `meta:altId` 查找的类 `$id` 的或URL编码的类。 |

**请求**

以下请求按路径中提供的 `meta:altId` 类值检索类。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

响应格式取决于在请 `Accept` 求中发送的标头。 所有查找请求都 `version` 需要包含在标 `Accept` 头中。 The following `Accept` headers are available:

| `Accept` 标题 | 描述 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | 包含和 `$ref` 的 `allOf`原始数据，有标题和说明。 |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` 并 `allOf` 且有标题和说明。 |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | 原始数 `$ref` 据， `allOf`无标题或说明。 |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` 并解 `allOf` 析，无标题或说明。 |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` 和包 `allOf` 含的描述符。 |

**响应**

成功的响应会返回类的详细信息。 返回的字段取决于在请 `Accept` 求中发送的标题。 尝试不同 `Accept` 的标题以比较响应并确定最适合您的用例的标题。

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

## 创建类 {#create}

您可以通过发出容器请求 `tenant` 在POST下定义自定义类。

>[!IMPORTANT]
>
>当根据您定义的自定义类编写模式时，您将无法使用标准混音。 每个mixin定义它们在其属性中兼容的 `meta:intendedToExtend` 类。 一旦开始定义与新类兼容的混音(通过使用混音 `$id` 字段中新类 `meta:intendedToExtend` 的混音)，您将能够在每次定义实现您定义的类的模式时重用这些混音。 有关详细信息， [请参阅](./mixins.md#create)[各端点指](./schemas.md#create) 南中有关创建混合和创建模式的部分。
>
>如果您计划在实时客户用户档案中使用基于自定义类的模式，还必须记住，合并模式只基于共享同一类的模式构建。 如果要在合并中包含XDM Individual模式或 [!UICONTROL XDM ExperienceEvent等其他类的自定义类用户档案] , 则必须与使用该类的其他模式建立关系。 有关详细信 [息，请参阅有关在API中两个模式之间建立关系](../tutorials/relationship-api.md) 的教程。

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

执行GET请求 [以容器中](#list) 的所 `tenant` 有类列表现在将包括属性类。 您还可 [以使用URL编码](#lookup) ，执行查找( `$id` GET)请求，以直接视图新类。

## 更新类 {#put}

您可以通过PUT操作替换整个类，实质上是重写资源。 在通过PUT请求更新类时，主体必须包括在POST请求中创建新类时 [需要的所](#create) 有字段。

>[!NOTE]
>
>如果只想更新某个类的一部分而不是完全替换它，请参阅有关更 [新某个类的一部分的部分](#patch)。

**API格式**

```http
PUT /tenant/classes/{CLASS_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CLASS_ID}` | 要 `meta:altId` 重写的 `$id` 类的或URL编码的类。 |

**请求**

以下请求重写现有类，更改其 `description` 和其 `title` 中一个字段的值。

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

## 更新类的一部分 {#patch}

您可以使用PATCH请求更新类的一部分。 支 [!DNL Schema Registry] 持所有标准JSON修补程序操作， `add`包括 `remove`、和 `replace`。 有关JSON修补程序的详细信息，请参阅 [API基础指南](../../landing/api-fundamentals.md#json-patch)。

>[!NOTE]
>
>如果要用新值替换整个资源，而不是更新单个字段，请参阅使用 [PUT操作替换类的一节](#put)。

**API格式**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| 参数 | 描述 |
| --- | --- |
| `{CLASS_ID}` | 要更新的 `$id` 类 `meta:altId` 的URL编码URI。 |

**请求**

以下示例请求更 `description` 新现有类及其某 `title` 个字段的更新。

请求主体采用数组的形式，每个列出的对象代表对单个字段的特定更改。 每个对象包括要执行的(`op`)操作，该操作应在()上执行的字段`path`，以及该操作()应包括哪些信`value`息。

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

响应显示两个操作都成功执行。 已 `description` 更新该字段以 `title` 及该字 `propertyId` 段。

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

## 删除类 {#delete}

有时可能需要从模式注册表中删除类。 这是通过使用路径中提供的类ID执行DELETE请求来完成的。

**API格式**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CLASS_ID}` | 要删除的 `$id` URL编 `meta:altId` 码的URI或类的URL。 |

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

您可以通过尝试类的查 [找(GET)请求](#lookup) ，确认删除。 您需要在请求中 `Accept` 包含一个头，但应收到HTTP状态404（未找到），因为类已从模式注册表中删除。