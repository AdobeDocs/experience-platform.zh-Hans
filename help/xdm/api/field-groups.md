---
keywords: Experience Platform；主页；热门主题；API;XDM;XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；数据模型；架构注册表；字段组；字段组；字段组；创建
solution: Experience Platform
title: 字段组API端点
description: 架构注册表API中的/fieldgroups端点允许您以编程方式管理体验应用程序中的XDM架构字段组。
topic-legacy: developer guide
exl-id: d26257e4-c7d5-4bff-b555-7a2997c88c74
source-git-commit: a26c8d43ff7874bcedd2adb3d6da995986198c96
workflow-type: tm+mt
source-wordcount: '1216'
ht-degree: 3%

---

# 架构字段组端点

架构字段组是可重用的组件，用于定义一个或多个表示特定概念的字段，例如个人、邮寄地址或Web浏览器环境。 字段组将作为实现兼容类的架构的一部分包含在内，具体取决于它们表示的数据（记录或时间序列）的行为。 的 `/fieldgroups` 的端点 [!DNL Schema Registry] API允许您以编程方式管理体验应用程序中的字段组。

## 快速入门

本指南中使用的端点是 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). 在继续之前，请查看 [入门指南](./getting-started.md) 有关相关文档的链接，请参阅本文档中的API调用示例指南，以及有关成功调用任何Experience PlatformAPI所需标头的重要信息。

## 检索字段组列表 {#list}

您可以在 `global` 或 `tenant` 容器，方法是向 `/global/fieldgroups` 或 `/tenant/fieldgroups`，分别为。

>[!NOTE]
>
>列出资源时，方案注册表将结果集限制为300个项目。 要返回超出此限制的资源，您必须使用分页参数。 还建议您使用其他查询参数来筛选结果并减少返回的资源数。 请参阅 [查询参数](./appendix.md#query) ，以了解详细信息。

**API格式**

```http
GET /{CONTAINER_ID}/fieldgroups?{QUERY_PARAMS}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 要从以下位置检索字段组的容器： `global` 用于Adobe创建的字段组或 `tenant` 适用于您的组织拥有的字段组。 |
| `{QUERY_PARAMS}` | 用于按筛选结果的可选查询参数。 请参阅 [附录文档](./appendix.md#query) ，以获取可用参数列表。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求从 `tenant` 容器，使用 `orderby` 查询参数，以按字段组的 `title` 属性。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

响应格式取决于 `Accept` 请求中发送的标头。 以下 `Accept` 标头可用于列出字段组：

| `Accept` 标题 | 描述 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每个资源的简短摘要。 这是列出资源的建议标头。 (限制：300) |
| `application/vnd.adobe.xed+json` | 为每个资源返回完整的JSON字段组（原始） `$ref` 和 `allOf` 包含。 (限制：300) |

{style=&quot;table-layout:auto&quot;}

**响应**

上述请求使用 `application/vnd.adobe.xed-id+json` `Accept` 标头，因此响应仅包含 `title`, `$id`, `meta:altId`和 `version` 属性。 使用其他 `Accept` 标题(`application/vnd.adobe.xed+json`)会返回每个字段组的所有属性。 选择相应的 `Accept` 标头，具体取决于您在响应中需要的信息。

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/6ece98e9842907c78c651f5b249d9f09",
      "meta:altId": "_{TENANT_ID}.mixins.6ece98e9842907c78c651f5b249d9f09",
      "version": "1.0",
      "title": "CRM Data"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/6386ee478a30914964c6e676ad55603c",
      "meta:altId": "_{TENANT_ID}.mixins.6386ee478a30914964c6e676ad55603c",
      "version": "1.9",
      "title": "Loyalty Member Details"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/67626b2830db3d3ea6c8f9d007aa5797",
      "meta:altId": "_{TENANT_ID}.mixins.67626b2830db3d3ea6c8f9d007aa5797",
      "version": "1.0",
      "title": "Restaurant"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/2583b25b613fec704da6ef70cf527688",
      "meta:altId": "_{TENANT_ID}.mixins.2583b25b613fec704da6ef70cf527688",
      "version": "1.1",
      "title": "Retail Customer Preferences"
    },
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 3
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/fieldgroups"
    }
  }
}
```

## 查找字段组 {#lookup}

您可以通过在GET请求的路径中包含字段组的ID来查找特定的字段组。

**API格式**

```http
GET /{CONTAINER_ID}/fieldgroups/{FIELD_GROUP_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 存放要检索的字段组的容器： `global` 用于Adobe创建的字段组或 `tenant` 适用于您的组织拥有的字段组。 |
| `{FIELD_GROUP_ID}` | 的 `meta:altId` 或URL编码 `$id` 的字段组。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求会按其 `meta:altId` 值。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

响应格式取决于 `Accept` 请求中发送的标头。 所有查找请求都需要 `version` 包括在 `Accept` 标题。 以下 `Accept` 标头可用：

| `Accept` 标题 | 描述 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | 原始 `$ref` 和 `allOf`的标题和描述。 |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` 和 `allOf` 已解析，具有标题和描述。 |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | 原始 `$ref` 和 `allOf`，无标题或描述。 |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` 和 `allOf` 已解析，无标题或描述。 |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` 和 `allOf` 已解析，包含描述符。 |

{style=&quot;table-layout:auto&quot;}

**响应**

成功的响应会返回字段组的详细信息。 返回的字段取决于 `Accept` 请求中发送的标头。 试验 `Accept` 标头来比较响应并确定最适合您的用例的标头。

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
  "version": "1.2",
  "title": "Favorite Hotel",
  "type": "object",
  "description": "",
  "definitions": {
    "customFields": {
      "type": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "favoriteHotel": {
              "title": "Favorite Hotel",
              "description": "Reference field for hotel schema.",
              "type": "string",
              "isRequired": false,
              "meta:xdmType": "string"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "meta:xdmType": "object"
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

## 创建字段组 {#create}

您可以在 `tenant` 容器，方法是发出POST请求。

**API格式**

```http
POST /tenant/fieldgroups
```

**请求**

定义新字段组时，必须包括 `meta:intendedToExtend` 属性，列出 `$id` 与字段组兼容的类的。 在本例中，字段组与 `Property` 之前定义的类。 自定义字段必须嵌套在 `_{TENANT_ID}` （如示例中所示）以避免与类和其他字段组提供的类似字段发生任何冲突。

>[!NOTE]
>
>有关如何定义要包含在字段组中的不同字段类型的详细信息，请参阅 [在API中定义自定义字段](../tutorials/custom-fields-api.md#define-fields).

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Details",
        "description":"Detailed information related to the properties owned and operated by the company.",
        "type":"object",
        "meta:intendedToExtend":["https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"],
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
                "$ref": "#/definitions/property"
            }
        ]
}'
```

**响应**

成功响应会返回HTTP状态201（已创建）和包含新创建字段组详细信息(包括 `$id`, `meta:altId`和 `version`. 这些值是只读的，由 [!DNL Schema Registry].

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Detailed information related to the properties owned and operated by the company.",
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

执行GET请求 [列出所有字段组](#list) 现在，在租户容器中将包含“属性详细信息”字段组，或者您可以 [执行查找(GET)请求](#lookup) 使用URL编码 `$id` 用于直接查看新字段组的URI。

## 更新字段组 {#put}

您可以通过PUT操作替换整个字段组，实质上是重写资源。 通过PUT请求更新字段组时，主体必须包含在 [创建新字段组](#create) POST请求中。

>[!NOTE]
>
>如果只想更新字段组的一部分而不是完全替换它，请参阅 [更新字段组的一部分](#patch).

**API格式**

```http
PUT /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{FIELD_GROUP_ID}` | 的 `meta:altId` 或URL编码 `$id` 要重写的字段组。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求会重写现有字段组，并添加新字段组 `propertyCountry` 字段。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Details",
        "description": "Detailed information related to the properties owned and operated by the company.",
        "type": "object",
        "meta:intendedToExtend": ["https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"],
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
                "$ref": "#/definitions/property"
            }
        ]
      }'
```

**响应**

成功的响应会返回更新的字段组的详细信息。

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Detailed information related to the properties owned and operated by the company.",
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

## 更新字段组的一部分 {#patch}

您可以使用PATCH请求更新字段组的一部分。 的 [!DNL Schema Registry] 支持所有标准JSON修补程序操作，包括 `add`, `remove`和 `replace`. 有关JSON修补程序的更多信息，请参阅 [API基础知识指南](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>如果要使用新值而不是更新单个字段替换整个资源，请参阅 [使用PUT操作替换字段组](#put).

**API格式**

```http
PATCH /tenant/fieldgroups/{FIELD_GROUP_ID} 
```

| 参数 | 描述 |
| --- | --- |
| `{FIELD_GROUP_ID}` | URL编码 `$id` URI或 `meta:altId` 要更新的字段组。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下示例请求更新了 `description` ，并添加 `propertyCity` 字段。

请求正文采用数组的形式，每个列出的对象都表示对单个字段的特定更改。 每个对象都包括要执行的操作(`op`)，应对(`path`)，以及该操作中应包含哪些信息(`value`)。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/description",
          "value": "Details relating to a property operated by the company."
        },
        { 
          "op": "add",
          "path": "/definitions/property/properties/_{TENANT_ID}/properties/propertyCity",
          "value": {
            "title": "Property City",
            "description": "City where the property is located.",
            "type": "string"
          }
        }
      ]'
```

**响应**

响应显示两个操作均已成功执行。 的 `description` 已更新，并且 `propertyCountry` 已添加到 `definitions`.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.mixins.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "mixins",
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

## 删除字段组 {#delete}

有时可能需要从架构注册表中删除字段组。 这是通过使用路径中提供的字段组ID执行DELETE请求来完成的。

**API格式**

```http
DELETE /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{FIELD_GROUP_ID}` | URL编码 `$id` URI或 `meta:altId` 的字段组。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态204（无内容）和空白正文。

您可以通过尝试 [查找(GET)请求](#lookup) 到字段组。 您需要包含 `Accept` 标头，但应会收到HTTP状态404（未找到），因为字段组已从架构注册表中删除。
