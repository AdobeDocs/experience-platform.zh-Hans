---
keywords: Experience Platform；主页；热门主题；数据准备；API指南；架构；
solution: Experience Platform
title: 架构API端点
description: 您可以使用Adobe Experience Platform API中的“/schemas”端点以编程方式检索、创建和更新架构，以便与Experience Platform中的映射器一起使用。
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 3%

---



# 架构端点

架构可与映射器一起使用，以确保您摄取到Adobe Experience Platform的数据与您要摄取的数据相匹配。 您可以使用`/schemas`端点以编程方式创建、列出和获取自定义架构，以便与Experience Platform中的映射器一起使用。

>[!NOTE]
>
>使用此端点创建的架构仅与映射器和映射集一起使用。 若要创建其他Experience Platform服务可访问的架构，请阅读[架构注册开发人员指南](../../xdm/api/schemas.md)。

## 获取所有架构

您可以通过向`/schemas`端点发出GET请求来检索组织的所有可用映射器架构列表。

**API格式**

`/schemas`端点支持多个查询参数以帮助您筛选结果。 虽然这些参数中的大多数是可选的，但强烈建议使用这些参数以帮助减少昂贵的开销。 但是，您必须在请求中同时包含`start`和`limit`参数。 可以包含多个参数，以&amp;符号(`&`)分隔。

```http
GET /schemas?limit={LIMIT}&start={START}
GET /schemas?limit={LIMIT}&start={START}&name={NAME}
GET /schemas?limit={LIMIT}&start={START}&orderBy={ORDER_BY}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{LIMIT}` | **必需**。 指定返回的架构数。 |
| `{START}` | **必需**。 指定结果页面的偏移量。 若要获取结果的第一页，请将值设置为`start=0`。 |
| `{NAME}` | 根据名称筛选架构。 |
| `{ORDER_BY}` | 对结果的顺序进行排序。 支持的字段为`modifiedDate`和`createdDate`。 您可以在属性前加上`+`或`-`，以分别按升序或降序排序。 |

**请求**

以下请求检索为您的组织创建的最后两个架构。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas&start=0&limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

以下响应返回HTTP状态200，其中包含所请求架构的列表。

>[!NOTE]
>
>以下响应已因空间而被截断。

```json
{
    "data": [
        {
            "id": "823ac494f35e4e84bcb2f061378fcca6",
            "version": 0,
            "jsonSchema": {
                "title": "Sample schema",
                "type": "object",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "description": "A unique identifier for the record.",
                        "type": "string",
                        "format": "uri-reference",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "city": {
                        "title": "City",
                        "description": "The name of the city.",
                        "type": "string",
                        "meta:xdmField": "xdm:city",
                        "meta:xdmType": "string"
                    }
                }
            },
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc",
                "contentType": "1.0"
            }
        },
        {
            "id": "0f868d3a1b804fb0abf738306290ae79",
            "version": 0,
            "jsonSchema": {
                "title": "Sample schema 2",
                "type": "object",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "description": "A unique identifier for the record.",
                        "type": "string",
                        "format": "uri-reference",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "city": {
                        "title": "City",
                        "description": "The name of the city.",
                        "type": "string",
                        "meta:xdmField": "xdm:city",
                        "meta:xdmType": "string"
                    }
                }
            },
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/0f868d3a1b804fb0abf738306290ae79",
                "contentType": "1.0"
            }
        }
    ],
    "_page": {
        "count": 2,
        "limit": 2
    }
}
```

## 创建架构

您可以通过向`/schemas`端点发出POST请求来创建要验证的架构。 可通过三种方式创建架构：发送[JSON架构](https://json-schema.org/)、使用示例数据或引用现有XDM架构。

```http
POST /schemas
```

### 使用JSON架构

**请求**

以下请求允许您通过发送[JSON架构](https://json-schema.org/)来创建架构。

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}'
```

**响应**

成功的响应返回HTTP状态200，其中包含有关新创建的架构的信息。

```json
{
    "id": "6daffabf14b1425292add3719afc8fab",
    "version": 0,
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}
```

### 使用示例数据

**请求**

以下请求允许您使用之前上传的示例数据创建一个架构。

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "sampleId": "45439a93d48d47d098d26e0f0840cc02"  
 }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `sampleId` | 架构所基于的示例数据的ID。 |

**响应**

成功的响应返回HTTP状态200，其中包含有关新创建的架构的信息。

```json
{
    "id": "b2ee78bd55ac45f781a93fb8b90d99b2",
    "version": 0,
    "jsonSchema": {
        "title": "SampleSchema:45439a93d48d47d098d26e0f0840cc02",
        "type": "object",
        "properties": {
            "gender": {
                "title": "gender",
                "type": "string"
            },
            "last_name": {
                "title": "last_name",
                "type": "string"
            },
            "id": {
                "title": "id",
                "type": "string"
            },
            "ip_address": {
                "title": "ip_address",
                "type": "string"
            },
            "first_name": {
                "title": "first_name",
                "type": "string"
            },
            "email": {
                "title": "email",
                "type": "string"
            }
        }
    },
    "sampleId": "45439a93d48d47d098d26e0f0840cc02"
}
```

### 请参阅XDM架构

**请求**

以下请求允许您通过引用现有XDM架构来创建架构。

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "name": "outputSchema1",
     "schemaRef": {
         "id": "https://ns.adobe.com/{TENANT_ID}/schemas/0d555890502224d187b619f23c35c8d1",
         "contentType": "application/vnd.adobe.xed-full+json;version=1"
     }  
 }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 要创建的架构的名称。 |
| `schemaRef.id` | 您正在引用的架构的ID。 |
| `schemaRef.contentType` | 确定所引用架构的响应格式。 有关详细信息，请参阅[架构注册表开发人员指南](../../xdm/api/schemas.md#lookup) |

**响应**

成功的响应返回HTTP状态200，其中包含有关新创建的架构的信息。

>[!NOTE]
>
>以下响应已因空间而被截断。

```json
{
    "id": "4b64daa51b774cb2ac21b61d80125ed0",
    "version": 0,
    "name": "schemaName",
    "jsonSchema": "{\"id\":null,\"schema\":null,\"_refId\":null,\"title\":\"SimpleUser\",...,\"imsOrg\":\"{ORG_ID}\",\"$id\":\"https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96\"}",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96",
        "contentType": "application/vnd.adobe.xed+json;version=1.0"
    }
}
```

## 使用文件上载创建架构

您可以通过上传要从中转换的JSON文件来创建架构。

**API格式**

```http
POST /schemas/upload
```

**请求**

以下请求允许您从上传的JSON文件创建架构。

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas/upload \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: multipart/form-data' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -F 'file=@{PATH_TO_FILE}.json'
```

**响应**

成功的响应返回HTTP状态200，其中包含有关新创建的架构的信息。

```json
{
    "id": "292add3716daffabf14b14259afc8fab",
    "version": 0,
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}
```

## 检索特定架构

您可以通过向`/schemas`端点发出GET请求并在请求路径中提供要检索的架构的ID，来检索有关特定架构的信息。

**API格式**

```http
GET /schemas/{SCHEMA_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEMA_ID}` | 正在查找的架构的ID。 |

**请求**

以下请求检索有关指定架构的信息。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas/0f868d3a1b804fb0abf738306290ae79 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，其中包含有关指定架构的信息。

```json
{
    "id": "0f868d3a1b804fb0abf738306290ae79",
    "version": 0,
    "jsonSchema": {
        "title": "Sample schema",
        "description": "Sample description",
        "type": "object",
        "properties": {
            "_id": {
                "title": "Identifier",
                "description": "A unique identifier for the record.",
                "type": "string",
                "format": "uri-reference",
                "meta:xdmField": "@id",
                "meta:xdmType": "string"
            },
            "personalEmail": {
                "title": "Personal Email",
                "description": "A personal email address.",
                "type": "object",
                "properties": {
                    "primary": {
                        "title": "Primary",
                        "description": "Primary email indicator.\n\nA Profile can have only one `primary` email address at a given point of time.\n",
                        "type": "boolean",
                        "meta:xdmField": "xdm:primary",
                        "meta:xdmType": "boolean"
                    },
                    "address": {
                        "title": "Address",
                        "description": "The technical address, e.g 'name@domain.com' as commonly defined in RFC2822 and subsequent standards.",
                        "type": "string",
                        "format": "email",
                        "meta:xdmField": "xdm:address",
                        "meta:xdmType": "string"
                    }
                },
                "meta:xdmField": "xdm:personalEmail",
                "meta:referencedFrom": "https://ns.adobe.com/xdm/context/emailaddress",
                "meta:xdmType": "object"
            }
        },
        "imsOrg": "6A29340459CA8D350A49413A@AdobeOrg",
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc"
    },
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc",
        "contentType": "1.0"
    }
}
```
