---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；体验数据模型；数据模型；数据模型；数据类型注册表；数据类型；数据类型；数据类型；创建
solution: Experience Platform
title: 数据类型API端点
description: 架构注册API中的/datatypes端点允许您以编程方式管理体验应用程序中的XDM数据类型。
exl-id: 2a58d641-c681-40cf-acc8-7ad842cd6243
source-git-commit: 6e58f070c0a25d7434f1f165543f92ec5a081e66
workflow-type: tm+mt
source-wordcount: '1247'
ht-degree: 2%

---

# 数据类型端点

数据类型在类或架构字段组中用作引用类型字段的方式与基本文本字段相同，主要区别在于数据类型可以定义多个子字段。 虽然与字段组类似，它们允许一致地使用多字段结构，但数据类型更加灵活，因为它们可以包含在架构结构中的任意位置，而字段组只能在根级别添加。 [!DNL Schema Registry] API中的`/datatypes`端点允许您以编程方式管理体验应用程序中的数据类型。

>[!NOTE]
>
>如果字段被定义为特定数据类型，则无法在另一个架构中创建具有不同数据类型的相同字段。 此限制适用于您组织的租户。

## 快速入门

本指南中使用的终结点是[[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)的一部分。 在继续之前，请查看[快速入门指南](./getting-started.md)，以获取相关文档的链接、阅读本文档中示例API调用的指南，以及有关成功调用任何Experience PlatformAPI所需的所需标头的重要信息。

## 检索数据类型列表 {#list}

通过分别向`/global/datatypes`或`/tenant/datatypes`发出GET请求，可列出`global`或`tenant`容器下的所有数据类型。

>[!NOTE]
>
>列出资源时，架构注册表将结果集限制为300个项目。 要返回超出此限制的资源，必须使用分页参数。 还建议您使用其他查询参数来筛选结果并减少返回的资源数。 有关详细信息，请参阅附录文档中有关[查询参数](./appendix.md#query)的部分。

**API格式**

```http
GET /{CONTAINER_ID}/datatypes?{QUERY_PARAMS}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 您要从中检索数据类型的容器： `global`用于Adobe创建的数据类型，或者`tenant`用于您的组织拥有的数据类型。 |
| `{QUERY_PARAMS}` | 用于筛选结果的可选查询参数。 有关可用参数的列表，请参阅[附录文档](./appendix.md#query)。 |

{style="table-layout:auto"}

**请求**

以下请求从`tenant`容器中检索数据类型列表，使用`orderby`查询参数按数据类型的`title`属性对这些数据类型进行排序。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

响应格式取决于请求中发送的`Accept`标头。 以下`Accept`标头可用于列出数据类型：

| `Accept`标头 | 描述 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每个资源的简短摘要。 这是列出资源的推荐标头。 （限制：300） |
| `application/vnd.adobe.xed+json` | 返回每个资源的完整JSON数据类型，包括原始`$ref`和`allOf`。 （限制：300） |

{style="table-layout:auto"}

**响应**

上述请求使用了`application/vnd.adobe.xed-id+json` `Accept`标头，因此响应仅包含每个数据类型的`title`、`$id`、`meta:altId`和`version`属性。 使用其他`Accept`标头(`application/vnd.adobe.xed+json`)将返回每种数据类型的所有属性。 根据您在响应中需要的信息，选择适当的`Accept`标头。

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

通过在GET请求的路径中包含数据类型的ID，您可以查找特定数据类型。

**API格式**

```http
GET /{CONTAINER_ID}/datatypes/{DATA_TYPE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 包含您要检索的数据类型的容器： `global`用于Adobe创建的数据类型，或者`tenant`用于您的组织拥有的数据类型。 |
| `{DATA_TYPE_ID}` | 要查找的数据类型的`meta:altId`或URL编码的`$id`。 |

{style="table-layout:auto"}

**请求**

以下请求通过路径中提供的`meta:altId`值检索数据类型。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44 \
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

成功的响应将返回数据类型的详细信息。 返回的字段取决于请求中发送的`Accept`标头。 尝试使用不同的`Accept`标头来比较响应并确定哪个标头最适合您的用例。

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
  "imsOrg": "{ORG_ID}",
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

## 创建数据类型 {#create}

您可以通过发出POST请求在`tenant`容器下定义自定义数据类型。

**API格式**

```http
POST /tenant/datatypes
```

**请求**

与字段组不同，定义数据类型不需要`meta:extends`或`meta:intendedToExtend`字段，也不需要嵌套字段以避免冲突。

在定义数据类型本身的字段结构时，您可以使用基元类型（如`string`或`object`），也可以通过`$ref`属性引用其他现有数据类型。 有关不同XDM字段类型的预期格式的详细指导，请参阅[在API](../tutorials/custom-fields-api.md)中定义自定义XDM字段的指南。

以下请求创建具有子属性`yearBuilt`、`propertyType`和`location`的“属性构造”对象数据类型：

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Construction",
        "description": "Information related to the property construction",
        "type": "object",
        "properties": {
          "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
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
            }
          },
          "location": {
            "title": "Location",
            "description": "The physical location of the property.",
            "$ref": "https://ns.adobe.com/xdm/common/address"
          }
        }
      }'
```

**响应**

成功的响应返回HTTP状态201 （已创建）以及包含新创建的数据类型的详细信息（包括`$id`、`meta:altId`和`version`）的有效负载。 这三个值是只读的，由[!DNL Schema Registry]分配。

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/669ffcc61cf5e94e8640dbe6a15f0f24eb3cd1ddbbfb6b36",
  "meta:altId": "_{TENANT_ID}.datatypes.669ffcc61cf5e94e8640dbe6a15f0f24eb3cd1ddbbfb6b36",
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
    "location": {
      "title": "Location",
      "description": "The physical location of the property.",
      "$ref": "https://ns.adobe.com/xdm/common/address",
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "refs": [
    "https://ns.adobe.com/xdm/common/address"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1670885230789,
    "repo:lastModifiedDate": 1670885230789,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "d3cc803a1f8daa06b7c150d882bd337d88f4d5d5f08d36cfc4c2849dc0255f7e",
    "meta:globalLibVersion": "1.38.3.1"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

执行GET请求以[列出租户容器中的所有数据类型](#list)将包括“属性详细信息”数据类型，或者您可以[使用URL编码的`$id` URI执行查找(GET)请求](#lookup)以直接查看新数据类型。

## 更新数据类型 {#put}

您可以通过PUT操作替换整个数据类型，从而本质上重新写入资源。 通过PUT请求更新数据类型时，正文必须包括在POST请求中[创建新数据类型](#create)时所需的所有字段。

>[!NOTE]
>
>如果只想更新部分数据类型而不是完全替换它，请参阅[更新部分数据类型](#patch)部分。

**API格式**

```http
PUT /tenant/datatypes/{DATA_TYPE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DATA_TYPE_ID}` | 要重写的数据类型的`meta:altId`或URL编码的`$id`。 |

{style="table-layout:auto"}

**请求**

以下请求重写现有数据类型，并添加新的`floorSize`字段。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Construction",
        "description": "Information related to the property construction",
        "type": "object",
        "properties": {
          "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
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

成功的响应将返回更新数据类型的详细信息。

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
  "imsOrg": "{ORG_ID}",
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

## 更新数据类型的部分 {#patch}

您可以使用PATCH请求更新数据类型的某个部分。 [!DNL Schema Registry]支持所有标准JSON修补程序操作，包括`add`、`remove`和`replace`。 有关JSON修补程序的详细信息，请参阅[API基础指南](../../landing/api-fundamentals.md#json-patch)。

>[!NOTE]
>
>如果要使用新值替换整个资源，而不是更新单个字段，请参阅[使用PUT操作替换数据类型](#put)一节。

**API格式**

```http
PATCH /tenant/data type/{DATA_TYPE_ID} 
```

| 参数 | 描述 |
| --- | --- |
| `{DATA_TYPE_ID}` | 要更新的数据类型的URL编码的`$id` URI或`meta:altId`。 |

{style="table-layout:auto"}

**请求**

下面的示例请求更新了现有数据类型的`description`，并添加了一个新的`floorSize`字段。

请求正文采用数组的形式，每个列出的对象表示对单个字段的特定更改。 每个对象都包含要执行的操作(`op`)、应该对(`path`)执行该操作的字段，以及该操作中应该包含哪些信息(`value`)。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

响应显示两个操作均已成功执行。 `description`已更新，`floorSize`已添加到`definitions`下。

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
        "type": "object",
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
  "imsOrg": "{ORG_ID}",
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

有时可能需要从架构注册表中删除数据类型。 可使用路径中提供的数据类型ID执行DELETE请求，从而达到此目的。

**API格式**

```http
DELETE /tenant/datatypes/{DATA_TYPE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DATA_TYPE_ID}` | 要删除的数据类型的URL编码的`$id` URI或`meta:altId`。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态204（无内容）和一个空白正文。

您可以通过尝试对数据类型进行[查找(GET)请求](#lookup)来确认删除。 您需要在请求中包含`Accept`标头，但应该会收到HTTP状态404 （未找到），因为该数据类型已从架构注册表中删除。
