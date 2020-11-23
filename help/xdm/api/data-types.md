---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;data type registry;Schema Registry;data type;Data type;data types;Data types;create
solution: Experience Platform
title: 创建数据类型
description: 模式注册表API中的/datatypes端点允许您在体验应用程序中以编程方式管理XDM数据类型。
translation-type: tm+mt
source-git-commit: 0b55f18eabcf1d7c5c233234c59eb074b2670b93
workflow-type: tm+mt
source-wordcount: '1110'
ht-degree: 2%

---


# 数据类型端点

数据类型在类或混合中用作引用类型字段的方式与基本文本字段相同，关键区别在于数据类型可以定义多个子字段。 虽然与混音类似，它们允许多字段结构的一致使用，但数据类型更灵活，因为它们可以包含在模式结构中的任何位置，而混音只能添加在根级别。 API `/datatypes` 中的端点允许您 [!DNL Schema Registry] 以编程方式管理体验应用程序中的数据类型。

## 入门指南

本指南中使用的端点是API的一 [[!DNL Schema Registry] 部分](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/mixin-registry.yaml)。 在继续之前，请查 [看入门指南](./getting-started.md) ，了解相关文档的链接、阅读此文档中示例API调用的指南，以及成功调用任何Experience PlatformAPI所需标头的重要信息。

## 检索列表数据类型 {#list}

您可以分别向或列表发出 `global` GET请 `tenant` 求，以或容器下的 `/global/datatypes` 所有数据 `/tenant/datatypes`类型。

>[!NOTE]
>
>列出资源时，模式注册表将结果集限制为300项。 要返回超出此限制的资源，必须使用分页参数。 还建议您使用其他查询参数来筛选结果并减少返回的资源数。 有关详细信息，请 [参阅附录](./appendix.md#query) 文档中有关查询参数的一节。

**API格式**

```http
GET /{CONTAINER_ID}/datatypes?{QUERY_PARAMS}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 要从以下位置检索数据类型的容器: `global` adobe创建的数据类型 `tenant` 或组织拥有的数据类型。 |
| `{QUERY_PARAMS}` | 可选查询参数，用于筛选结果。 有关可 [用参数的列表](./appendix.md#query) ，请参阅附录文档。 |

**请求**

以下请求从列表检索容器中的数据类 `tenant` 型，使用 `orderby` 查询参数按数据类型的属性对数据类型 `title` 排序。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

响应格式取决于在请 `Accept` 求中发送的标头。 下列标 `Accept` 头可用于列出数据类型：

| `Accept` 标题 | 描述 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每个资源的简短摘要。 这是列出资源的建议标头。 (限制：300) |
| `application/vnd.adobe.xed+json` | 为每个资源返回完整的JSON数据类型，其中包含 `$ref` 原始 `allOf` 资源。 (限制：300) |

**响应**

上述请求使用 `application/vnd.adobe.xed-id+json` 了标题， `Accept` 因此响应只包括每个数据 `title`类型的、 `$id`、 `meta:altId`和 `version` 属性。 使用其他标 `Accept` 题(`application/vnd.adobe.xed+json`)可返回每个数据类型的所有属性。 根据您在 `Accept` 响应中需要的信息选择相应的标题。

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/78570e371092c032260714dd8bfd6d44",
      "meta:altId": "_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44",
      "version": "1.0",
      "title": "Loyalty"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/4b0329b5573cbb7cb757db667d7fdf66",
      "meta:altId": "_{TENANT_ID}.datatypes.4b0329b5573cbb7cb757db667d7fdf66",
      "version": "1.0",
      "title": "Property Details"
    }
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 2
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/datatypes?orderby=title"
    }
  }
}
```

## 查找数据类型 {#lookup}

您可以通过在GET请求的路径中包含数据类型的ID来查找特定数据类型。

**API格式**

```http
GET /{CONTAINER_ID}/datatypes/{DATA_TYPE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 存放要检索的数据类型的容器: `global` adobe创建的数据类型或 `tenant` 您的组织拥有的数据类型。 |
| `{DATA_TYPE_ID}` | 要 `meta:altId` 查找的数 `$id` 据类型的或URL编码的。 |

**请求**

以下请求按路径中提供的 `meta:altId` 值检索数据类型。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44 \
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

成功的响应会返回数据类型的详细信息。 返回的字段取决于在请 `Accept` 求中发送的标题。 尝试不同 `Accept` 的标题以比较响应并确定最适合您的用例的标题。

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/78570e371092c032260714dd8bfd6d44",
  "meta:altId": "_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Loyalty",
  "type": "object",
  "description": "Loyalty object containing loyalty-specific fields.",
  "definitions": {
    "customFields": {
      "properties": {
        "loyaltyId": {
          "title": "Loyalty ID",
          "description": "Unique loyalty program member ID. Should be in the format of an email address.",
          "type": "string",
          "meta:xdmType": "string"
        },
        "memberSince": {
          "title": "Member Since",
          "description": "Date person joined loyalty program.",
          "type": "string",
          "format": "date",
          "meta:xdmType": "date"
        },
        "points": {
          "title": "Points",
          "description": "Accumulated loyalty points",
          "type": "integer",
          "meta:xdmType": "int"
        },
        "loyaltyLevel": {
          "title": "Loyalty Level",
          "description": "The current loyalty program level to which the individual member belongs.",
          "type": "string",
          "enum": [
            "platinum",
            "gold",
            "silver",
            "bronze"
          ],
          "meta:enum": {
            "platinum": "Platinum",
            "gold": "Gold",
            "silver": "Silver",
            "bronze": "Bronze"
          },
          "meta:xdmType": "string"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields"
    }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1557529442681,
    "repo:lastModifiedDate": 1557529442681,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "50b8008b588e911314f9685240dd4c23a247f37179a6d9ff6ba3877dc11ca504",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Create a data type {#create}

您可以通过发出容器请求在POST下 `tenant` 定义自定义数据类型。

**API格式**

```http
POST /tenant/datatypes
```

**请求**

定义数据类型不需要 `meta:extends` 或字 `meta:intendedToExtend` 段，也无需嵌套字段以避免冲突。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Construction",
        "description":"Information related to the property construction",
        "type":"object",
        "properties": {
          "yearBuilt": {
            "type":"integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type":"string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCenter": "Shopping Center"
            }
          }
        } 
      }'
```

**响应**

成功的响应会返回HTTP状态201（已创建）和包含新创建数据类型详细信息（包括、和） `$id`的 `meta:altId`有效负荷 `version`。 这三个值是只读的，由指定 [!DNL Schema Registry]。

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:altId": "_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Property Construction",
  "type": "object",
  "description": "Information related to the property construction",
  "properties": {
    "yearBuilt": {
      "type": "integer",
      "title": "Year Built",
      "description": "The year the property was constructed.",
      "meta:xdmType": "int"
    },
    "propertyType": {
      "type": "string",
      "title": "Property Type",
      "description": "Type of building or structure in which the property exists.",
      "enum": [
        "freeStanding",
        "mall",
        "shoppingCenter"
      ],
      "meta:enum": {
        "freeStanding": "Free Standing Building",
        "mall": "Mall Space",
        "shoppingCenter": "Shopping Center"
      },
      "meta:xdmType": "string"
    }
  },
  "refs": [],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1604524729435,
    "repo:lastModifiedDate": 1604524729435,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "1c838764342756868ca1297869f582a38d15f03ed0acfc97fda7532d22e942c7",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

执行GET请求以 [列表租户容器中的所有数据类型](#list) ，现在将包括属性详细信息数据类型，或者，您可以使 [用URL编码的URI执行查找](#lookup)`$id` (GET)请求以直接视图新的数据类型。

## 更新数据类型 {#put}

您可以通过PUT操作替换整个数据类型，实质上是重写资源。 在通过PUT请求更新数据类型时，主体必须包括在POST请求中创建新数据 [类型时所需的所](#create) 有字段。

>[!NOTE]
>
>如果您只想更新数据类型的一部分而不是完全替换它，请参阅有关更 [新数据类型的一部分的部分](#patch)。

**API格式**

```http
PUT /tenant/datatypes/{DATA_TYPE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DATA_TYPE_ID}` | 要 `meta:altId` 重写的 `$id` 数据类型或URL编码的数据类型。 |

**请求**

以下请求将重写现有数据类型，并添加新 `floorSize` 字段。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Construction",
        "description": "Information related to the property construction",
        "type": "object",
        "properties": {
          "yearBuilt": {
            "type":"integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type":"string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCenter": "Shopping Center"
            }
          },
          "floorSize" {
            "type": "integer",
            "title": "Floor Size",
            "description": "The floor size of the property, in square feet."
          }
        } 
      }'
```

**响应**

成功的响应会返回更新数据类型的详细信息。

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:altId": "_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Property Construction",
  "type": "object",
  "description": "Information related to the property construction",
  "properties": {
    "yearBuilt": {
      "type": "integer",
      "title": "Year Built",
      "description": "The year the property was constructed.",
      "meta:xdmType": "int"
    },
    "propertyType": {
      "type": "string",
      "title": "Property Type",
      "description": "Type of building or structure in which the property exists.",
      "enum": [
        "freeStanding",
        "mall",
        "shoppingCenter"
      ],
      "meta:enum": {
        "freeStanding": "Free Standing Building",
        "mall": "Mall Space",
        "shoppingCenter": "Shopping Center"
      },
      "meta:xdmType": "string"
    },
    "floorSize" {
      "type":  "integer",
      "title":  "Floor Size",
      "description":  "The floor size of the property, in square feet.",
      "meta:xdmType": "int"
    }
  },
  "refs": [],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1604524729435,
    "repo:lastModifiedDate": 1604524729435,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "1c838764342756868ca1297869f582a38d15f03ed0acfc97fda7532d22e942c7",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 更新数据类型的一部分 {#patch}

您可以使用PATCH请求更新数据类型的一部分。 支 [!DNL Schema Registry] 持所有标准JSON修补程序操作， `add`包括 `remove`、和 `replace`。 有关JSON修补程序的详细信息，请参阅 [API基础指南](../../landing/api-fundamentals.md#json-patch)。

>[!NOTE]
>
>如果要用新值替换整个资源，而不是更新单个字段，请参阅使用 [PUT操作替换数据类型一节](#put)。

**API格式**

```http
PATCH /tenant/data type/{DATA_TYPE_ID} 
```

| 参数 | 描述 |
| --- | --- |
| `{DATA_TYPE_ID}` | 要更新的 `$id` URL编 `meta:altId` 码的URI或数据类型。 |

**请求**

以下示例请求更新 `description` 现有数据类型，并添加新字 `floorSize` 段。

请求主体采用数组的形式，每个列出的对象代表对单个字段的特定更改。 每个对象包括要执行的(`op`)操作，该操作应在()上执行的字段`path`，以及该操作()应包括哪些信`value`息。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/description",
          "value": "Construction-related information for a company-operated property."
        },
        { 
          "op": "add",
          "path": "/properties/floorSize",
          "value": {
            "type": "integer",
            "title": "Floor Size",
            "description": "The floor size of the property, in square feet."
          }
        }
      ]'
```

**响应**

响应显示两个操作都成功执行。 已 `description` 更新，并已 `floorSize` 添加到 `definitions`。

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "datatypes",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a property operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type":"object",
        "properties": {
            "propertyName": {
              "type": "string",
              "title": "Property Name",
              "description": "Name of the property"
            },
            "propertyCity": {
              "title": "Property City",
              "description": "City where the property is located.",
              "type": "string"
            },
            "propertyCountry": {
              "title": "Property Country",
              "description": "Country where the property is located.",
              "type": "string"
            },
            "phoneNumber": {
              "title": "Phone Number",
              "description": "Primary phone number for the property.",
              "type": "string"
            },
            "propertyType": {
              "type": "string",
              "title": "Property Type",
              "description": "Type and primary use of property.",
              "enum": [
                  "retail",
                  "yoga",
                  "fitness"
              ],
              "meta:enum": {
                  "retail": "Retail Store",
                  "yoga": "Yoga Studio",
                  "fitness": "Fitness Center"
              }
            },
            "propertyConstruction": {
              "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1594941263588,
    "repo:lastModifiedDate": 1594941538433,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "5e8a5e508eb2ed344c08cb23ed27cfb60c841bec59a2f7513deda0f7af903021",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 删除数据类型 {#delete}

有时可能需要从模式注册表中删除数据类型。 这是通过使用路径中提供的DELETE类型ID执行数据请求来完成的。

**API格式**

```http
DELETE /tenant/datatypes/{DATA_TYPE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DATA_TYPE_ID}` | 要删除的 `$id` URL编 `meta:altId` 码的URI或数据类型。 |

**请求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态204（无内容）和空白正文。

您可以通过尝试对数据类 [型进行查找(GET](#lookup) )请求来确认删除。 您需要在请求中包含 `Accept` 一个头，但应收到HTTP状态404（未找到），因为模式注册表中已删除数据类型。