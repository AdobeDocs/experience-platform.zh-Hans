---
keywords: Experience Platform；主页；热门主题；数据准备；api指南；模式;
solution: Experience Platform
title: 模式API端点
topic: 模式
description: '您可以使用Adobe Experience Platform API中的“/模式”端点以编程方式检索、创建和更新模式，以便与平台中的映射器一起使用。 '
translation-type: tm+mt
source-git-commit: 435d27f7187074c78209948c0e57b610b63d2055
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 3%

---



# 模式端点

模式可与映射器一起使用，以确保您已引入Adobe Experience Platform的数据与要摄取的数据匹配。 您可以使用`/schemas`端点以编程方式创建、列表和获取自定义模式，以便与平台中的映射器一起使用。

>[!NOTE]
>
>使用此端点创建的模式将专门与映射器和映射集一起使用。 要创建其他平台服务可访问的模式，请阅读[模式注册表开发人员指南](../../xdm/api/schemas.md)。

## 获取所有模式

您可以通过向`/schemas`端点发出列表请求，为IMS组织检索所有可用的映射器模式的GET。

**API格式**

`/schemas`端点支持多个查询参数，以帮助您筛选结果。 尽管这些参数大多是可选的，但强烈建议使用这些参数以帮助降低昂贵的开销。 但是，您必须在请求中同时包含`start`和`limit`参数。 可以包含多个参数，用&amp;符号(`&`)分隔。

```http
GET /schemas?limit={LIMIT}&start={START}
GET /schemas?limit={LIMIT}&start={START}&name={NAME}
GET /schemas?limit={LIMIT}&start={START}&orderBy={ORDER_BY}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{LIMIT}` | **必需**. 指定返回的模式数。 |
| `{START}` | **必需**. 指定结果页的偏移。 要获取结果的第一页，请将值设置为`start=0`。 |
| `{NAME}` | 过滤器基于名称的模式。 |
| `{ORDER_BY}` | 对结果的顺序排序。 支持的字段为`modifiedDate`和`createdDate`。 可以在属性前面添加`+`或`-`，以分别按升序或降序对其排序。 |

**请求**

以下请求将检索您的IMS组织最近创建的两个模式。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas&start=0&limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

以下响应返回HTTP状态200，并列表所请求的模式。

>[!NOTE]
>
>以下响应已被截断为空格。

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

## 创建模式

可以通过向`/schemas`端点发出POST请求来创建要验证的模式。 创建模式有三种方法：使用示例数据发送[JSON模式](https://json-schema.org/)或引用现有XDM模式。

```http
POST /schemas
```

### 使用JSON模式

**请求**

以下请求允许您通过发送[JSON模式](https://json-schema.org/)创建模式。

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的响应返回HTTP状态200，其中包含有关您新创建的模式的信息。

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

通过以下请求，您可以使用之前上传的示例数据创建模式。

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "sampleId": "45439a93d48d47d098d26e0f0840cc02"  
 }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `sampleId` | 您以模式为基础的示例数据的ID。 |

**响应**

成功的响应返回HTTP状态200，其中包含有关您新创建的模式的信息。

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

### 请参阅XDM模式

**请求**

以下请求允许您通过引用现有XDM模式创建模式。

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | 要创建的模式的名称。 |
| `schemaRef.id` | 您引用的模式的ID。 |
| `schemaRef.contentType` | 确定引用模式的响应格式。 有关此字段的详细信息，请参阅[模式注册表开发人员指南](../../xdm/api/schemas.md#lookup) |

**响应**

成功的响应返回HTTP状态200，其中包含有关您新创建的模式的信息。

>[!NOTE]
>
>以下响应已被截断为空格。

```json
{
    "id": "4b64daa51b774cb2ac21b61d80125ed0",
    "version": 0,
    "name": "schemaName",
    "jsonSchema": "{\"id\":null,\"schema\":null,\"_refId\":null,\"title\":\"SimpleUser\",...,\"imsOrg\":\"{IMS_ORG}\",\"$id\":\"https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96\"}",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96",
        "contentType": "application/vnd.adobe.xed+json;version=1.0"
    }
}
```

## 使用文件上传创建模式

您可以通过上传JSON文件创建要从中转换的模式。

**API格式**

```http
POST /schemas/upload
```

**请求**

以下请求允许您从已上载的JSON文件创建模式。

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas/upload \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: multipart/form-data' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -F 'file=@{PATH_TO_FILE}.json'
```

**响应**

成功的响应返回HTTP状态200，其中包含有关您新创建的模式的信息。

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

## 检索特定模式

您可以通过向`/schemas`端点发出GET请求并在请求路径中提供要检索的模式的ID来检索有关特定模式的信息。

**API格式**

```http
GET /schemas/{SCHEMA_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEMA_ID}` | 您查找的模式的ID。 |

**请求**

以下请求检索有关指定模式的信息。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas/0f868d3a1b804fb0abf738306290ae79 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，其中包含有关指定模式的信息。

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
