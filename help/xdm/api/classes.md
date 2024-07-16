---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；体验数据模型；数据模型；数据模型；类注册表；架构注册表；类；类；类；创建
solution: Experience Platform
title: 类API端点
description: 架构注册表API中的/classes端点允许您以编程方式管理体验应用程序中的XDM类。
exl-id: 7beddb37-0bf2-4893-baaf-5b292830f368
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 1%

---

# 类端点

所有Experience Data Model (XDM)架构都必须基于类。 类确定基于该类的所有架构都必须包含的公共属性的基本结构，以及哪些架构字段组适合在这些架构中使用。 此外，架构的类确定架构将包含的数据的行为方面，其中有两种类型：

* **[!UICONTROL 记录]**：提供有关主题属性的信息。 主体可以是组织，也可以是个人。
* **[!UICONTROL 时间序列]**：提供记录主体直接或间接执行操作时系统的快照。

>[!NOTE]
>
>有关数据行为如何影响架构组合的详细信息，请参阅[架构组合基础知识](../schema/composition.md)。

[!DNL Schema Registry] API中的`/classes`端点允许您以编程方式管理体验应用程序中的类。

## 快速入门

本指南中使用的终结点是[[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)的一部分。 在继续之前，请查看[快速入门指南](./getting-started.md)，以获取相关文档的链接、阅读本文档中示例API调用的指南，以及有关成功调用任何Experience PlatformAPI所需的所需标头的重要信息。

## 检索类列表 {#list}

通过分别向`/global/classes`或`/tenant/classes`发出GET请求，可以列出`global`或`tenant`容器下的所有类。

>[!NOTE]
>
>列出资源时，架构注册表将结果集限制为300个项目。 要返回超出此限制的资源，必须使用分页参数。 还建议您使用其他查询参数来筛选结果并减少返回的资源数。 有关详细信息，请参阅附录文档中有关[查询参数](./appendix.md#query)的部分。

**API格式**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 要从中检索类的容器： `global`用于Adobe创建的类，或`tenant`用于组织拥有的类。 |
| `{QUERY_PARAMS}` | 用于筛选结果的可选查询参数。 有关可用参数的列表，请参阅[附录文档](./appendix.md#query)。 |

{style="table-layout:auto"}

**请求**

以下请求从`tenant`容器中检索类列表，使用`orderby`查询参数按类的`title`属性对类进行排序。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

响应格式取决于请求中发送的`Accept`标头。 以下`Accept`标头可用于列出类：

| `Accept`标头 | 描述 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每个资源的简短摘要。 这是列出资源的推荐标头。 （限制：300） |
| `application/vnd.adobe.xed+json` | 返回每个资源的完整JSON类，包括原始`$ref`和`allOf`。 （限制：300） |

{style="table-layout:auto"}

**响应**

上述请求使用了`application/vnd.adobe.xed-id+json` `Accept`标头，因此响应只包含每个类的`title`、`$id`、`meta:altId`和`version`属性。 使用其他`Accept`标头(`application/vnd.adobe.xed+json`)返回每个类的所有属性。 根据您在响应中需要的信息，选择适当的`Accept`标头。

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

## 查找类 {#lookup}

通过在GET请求的路径中包含类的ID，您可以查找特定类。

**API格式**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 包含您要检索的类的容器：`global`用于Adobe创建的类，或者`tenant`用于您的组织拥有的类。 |
| `{CLASS_ID}` | 要查找的类的`meta:altId`或URL编码的`$id`。 |

{style="table-layout:auto"}

**请求**

以下请求检索路径中提供的类的`meta:altId`值。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

响应格式取决于请求中发送的`Accept`标头。 所有查找请求都要求在`Accept`标头中包含`version`。 以下`Accept`标头可用：

| `Accept`标头 | 描述 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | 具有`$ref`和`allOf`的原始，具有标题和描述。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref`和`allOf`已解决，具有标题和描述。 |
| `application/vnd.adobe.xed-notext+json; version=1` | 原始为`$ref`和`allOf`，无标题或描述。 |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref`和`allOf`已解决，无标题或描述。 |
| `application/vnd.adobe.xed-full-desc+json; version=1` | 已解决`$ref`和`allOf`，包含描述符。 |

{style="table-layout:auto"}

**响应**

成功的响应将返回类的详细信息。 返回的字段取决于请求中发送的`Accept`标头。 尝试使用不同的`Accept`标头来比较响应并确定哪个标头最适合您的用例。

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
  "imsOrg":"{ORG_ID}",
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

您可以通过发出POST请求在`tenant`容器下定义自定义类。

>[!IMPORTANT]
>
>根据定义的自定义类构成架构时，您将无法使用标准字段组。 每个字段组在其`meta:intendedToExtend`属性中定义其兼容的类。 一旦开始定义与新类兼容的字段组（通过使用字段组的`meta:intendedToExtend`字段中的新类的`$id`），每次定义实现所定义类的架构时，您将能够重用这些字段组。 有关详细信息，请参阅各自端点指南中有关[创建字段组](./field-groups.md#create)和[创建架构](./schemas.md#create)的部分。
>
>如果您计划基于实时客户档案中的自定义类使用架构，则还必须记住，合并架构仅基于共享同一类的架构进行构建。 如果要在诸如[!UICONTROL XDM Individual Profile]或[!UICONTROL XDM ExperienceEvent]之类的另一个类的合并中包含自定义类架构，则必须与使用该类的另一个架构建立关系。 有关详细信息，请参阅有关[在API](../tutorials/relationship-api.md)中的两个架构之间建立关系的教程。

**API格式**

```http
POST /tenant/classes
```

**请求**

创建(POST)类的请求必须包括`allOf`特性，该特性包含`$ref`到两个值之一：`https://ns.adobe.com/xdm/data/record`或`https://ns.adobe.com/xdm/data/time-series`。 这些值表示类所基于的行为（分别为记录或时间序列）。 有关记录数据与时序数据之间差异的更多信息，请参阅架构组合基础[中的行为类型部分](../schema/composition.md)。

定义类时，还可以在类定义中包含字段组或自定义字段。 这将导致添加的字段组和字段包含在实现该类的所有架构中。 以下示例请求定义了一个名为“Property”的类，该类捕获有关公司拥有和运营的不同属性的信息。 它包含每次使用类时要包含的`propertyId`字段。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `_{TENANT_ID}` | 您组织的`TENANT_ID`命名空间。 您的组织创建的所有资源都必须包含此属性，以避免与[!DNL Schema Registry]中的其他资源发生冲突。 |
| `allOf` | 新类将继承其属性的资源列表。 数组中的`$ref`对象之一定义了类的行为。 在此示例中，类继承“记录”行为。 |

{style="table-layout:auto"}

**响应**

成功的响应返回HTTP状态201 （已创建）以及包含新创建类的详细信息（包括`$id`、`meta:altId`和`version`）的有效负载。 这三个值是只读的，由[!DNL Schema Registry]分配。

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
  "imsOrg": "{ORG_ID}",
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

现在执行对[列出`tenant`容器中所有类](#list)的GET请求将包含Property类。 您也可以[使用URL编码的`$id`执行查找(GET)请求](#lookup)以直接查看新类。

## 更新类 {#put}

您可以通过PUT操作替换整个类，从而基本上重写资源。 通过PUT请求更新类时，正文必须包括在POST请求中[创建新类](#create)时所需的所有字段。

>[!NOTE]
>
>如果只想更新类的一部分而不是完全替换它，请参阅[更新类](#patch)的一部分部分。

**API格式**

```http
PUT /tenant/classes/{CLASS_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CLASS_ID}` | 要重写的类的`meta:altId`或URL编码的`$id`。 |

{style="table-layout:auto"}

**请求**

以下请求重写现有类，更改其`description`及其某个字段的`title`。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

成功的响应将返回已更新类的详细信息。

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
  "imsOrg": "{ORG_ID}",
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

可以使用PATCH请求更新类的一部分。 [!DNL Schema Registry]支持所有标准JSON修补程序操作，包括`add`、`remove`和`replace`。 有关JSON修补程序的详细信息，请参阅[API基础指南](../../landing/api-fundamentals.md#json-patch)。

>[!NOTE]
>
>如果要使用新值替换整个资源，而不是更新单个字段，请参阅[使用PUT操作替换类](#put)一节。

**API格式**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| 参数 | 描述 |
| --- | --- |
| `{CLASS_ID}` | 要更新的类的URL编码的`$id` URI或`meta:altId`。 |

{style="table-layout:auto"}

**请求**

下面的示例请求更新了现有类的`description`及其某个字段的`title`。

请求正文采用数组的形式，每个列出的对象表示对单个字段的特定更改。 每个对象都包含要执行的操作(`op`)、应该对(`path`)执行该操作的字段，以及该操作中应该包含哪些信息(`value`)。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "replace", "path": "/description", "value":  "Base class for properties operated by a company."},
        { "op": "replace", "path": "/definitions/property/properties/_{TENANT_ID}/properties/property/properties/propertyId/title", "value": "Unique Property ID string" }
      ]'
```

**响应**

响应显示两个操作均已成功执行。 已更新`description`以及`propertyId`字段的`title`。

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
  "imsOrg": "{ORG_ID}",
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

有时可能需要从架构注册表中删除类。 这是通过使用路径中提供的类ID执行DELETE请求来完成的。

**API格式**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CLASS_ID}` | 要删除的类的URL编码的`$id` URI或`meta:altId`。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态204（无内容）和一个空白正文。

您可以通过尝试对类进行[查找(GET)请求](#lookup)来确认删除。 您需要在请求中包含`Accept`标头，但应该会收到HTTP状态404 （未找到），因为该类已从架构注册表中删除。
