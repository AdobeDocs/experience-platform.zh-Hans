---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；体验数据模型；数据模型；数据模型；架构注册表；架构注册表；架构；架构；架构；架构；创建
solution: Experience Platform
title: 架构API端点
description: 架构注册API中的/schemas端点允许您以编程方式管理体验应用程序中的XDM架构。
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1443'
ht-degree: 2%

---

# 架构端点

架构可以被视为您要摄取到Adobe Experience Platform的数据的蓝图。 每个架构由一个类和零个或多个架构字段组组成。 [!DNL Schema Registry] API中的`/schemas`端点允许您以编程方式管理体验应用程序中的架构。

## 快速入门

本指南中使用的API端点是[[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)的一部分。 在继续之前，请查看[快速入门指南](./getting-started.md)，以获取相关文档的链接、阅读本文档中示例API调用的指南，以及有关成功调用任何Experience PlatformAPI所需的所需标头的重要信息。

## 检索架构列表 {#list}

通过分别向`/global/schemas`或`/tenant/schemas`发出GET请求，可列出`global`或`tenant`容器下的所有架构。

>[!NOTE]
>
>列出资源时，架构注册表将结果集限制为300个项目。 要返回超出此限制的资源，必须使用分页参数。 还建议您使用其他查询参数来筛选结果并减少返回的资源数。 有关详细信息，请参阅附录文档中有关[查询参数](./appendix.md#query)的部分。

**API格式**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 存放要检索的架构的容器： `global`用于Adobe创建的架构，或者`tenant`用于您组织拥有的架构。 |
| `{QUERY_PARAMS}` | 用于筛选结果的可选查询参数。 有关可用参数的列表，请参阅[附录文档](./appendix.md#query)。 |

{style="table-layout:auto"}

**请求**

以下请求从`tenant`容器中检索架构列表，使用`orderby`查询参数按其`title`属性对结果进行排序。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

响应格式取决于请求中发送的`Accept`标头。 以下`Accept`标头可用于列出架构：

| `Accept`标头 | 描述 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每个资源的简短摘要。 这是列出资源的推荐标头。 （限制：300） |
| `application/vnd.adobe.xed+json` | 返回每个资源的完整JSON架构，包括原始`$ref`和`allOf`。 （限制：300） |

{style="table-layout:auto"}

**响应**

上述请求使用了`application/vnd.adobe.xed-id+json` `Accept`标头，因此响应只包含每个架构的`title`、`$id`、`meta:altId`和`version`属性。 使用其他`Accept`标头(`application/vnd.adobe.xed+json`)返回每个架构的所有属性。 根据您在响应中需要的信息，选择适当的`Accept`标头。

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/0238be93d3e7a06aec5e0655955901ec",
      "meta:altId": "_{TENANT_ID}.schemas.0238be93d3e7a06aec5e0655955901ec",
      "version": "1.4",
      "title": "Hotels"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/0ef4ce0d390f0809fad490802f53d30b",
      "meta:altId": "_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b",
      "version": "1.0",
      "title": "Loyalty Members"
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
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

## 查找架构 {#lookup}

您可以通过在路径中包含架构ID的GET请求来查找特定架构。

**API格式**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 包含您要检索的架构的容器：`global`用于Adobe创建的架构，或者`tenant`用于您组织拥有的架构。 |
| `{SCHEMA_ID}` | 要查找的架构的`meta:altId`或URL编码的`$id`。 |

{style="table-layout:auto"}

**请求**

以下请求检索由路径中其`meta:altId`值指定的架构。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
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
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref`和`allOf`已解决，具有标题和描述。 已弃用的字段用`deprecated`的`meta:status`属性表示。 |

{style="table-layout:auto"}

**响应**

成功的响应将返回架构的详细信息。 返回的字段取决于请求中发送的`Accept`标头。 尝试使用不同的`Accept`标头来比较响应并确定哪个标头最适合您的用例。

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/20af3f1d4b175f27ba59529d1b51a0c79fc25df454117c80",
  "meta:altId": "_{TENANT_ID}.schemas.20af3f1d4b175f27ba59529d1b51a0c79fc25df454117c80",
  "meta:resourceType": "schemas",
  "version": "1.1",
  "title": "Example schema",
  "type": "object",
  "description": "An example schema created within the tenant container.",
  "allOf": [
      {
          "$ref": "https://ns.adobe.com/xdm/context/profile",
          "type": "object",
          "meta:xdmType": "object"
      },
      {
          "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
          "type": "object",
          "meta:xdmType": "object"
      }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
      "https://ns.adobe.com/{TENANT_ID}/mixins/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
      "https://ns.adobe.com/xdm/common/auditable",
      "https://ns.adobe.com/xdm/data/record",
      "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
      "repo:createdDate": 1602872911226,
      "repo:lastModifiedDate": 1603381419889,
      "xdm:createdClientId": "{CLIENT_ID}",
      "xdm:lastModifiedClientId": "{CLIENT_ID}",
      "xdm:createdUserId": "{USER_ID}",
      "xdm:lastModifiedUserId": "{USER_ID}",
      "eTag": "84b4da79b7445a4bf1c59269e718065effddb983c492f48e223d49c049c6d589",
      "meta:globalLibVersion": "1.15.4"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 创建架构 {#create}

架构组合过程从指定类开始。 类定义数据的关键行为方面（记录或时间序列），以及描述将摄取的数据所需的最小字段。

>[!NOTE]
>
>以下示例调用只是一个基准示例，说明如何在API中创建架构，具有类的最低组合要求，并且没有字段组。 有关如何在API中创建架构的完整步骤，包括如何使用字段组和数据类型分配字段，请参阅[架构创建教程](../tutorials/create-schema-api.md)。

**API格式**

```http
POST /tenant/schemas
```

**请求**

该请求必须包含引用类的`$id`的`allOf`特性。 此属性定义架构将实施的“基类”。 在此示例中，基类是以前创建的“属性信息”类。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Information",
        "description": "Property-related information.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590" 
          } 
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `allOf` | 一个对象数组，每个对象引用架构实现其字段的类或字段组。 每个对象都包含一个属性(`$ref`)，其值表示新架构将实现的类或字段组的`$id`。 必须提供一个类，且不含或包含多个其他字段组。 在上述示例中，`allOf`数组中的单个对象是架构的类。 |

{style="table-layout:auto"}

**响应**

成功的响应返回HTTP状态201 （已创建）以及包含新创建架构的详细信息（包括`$id`、`meta:altId`和`version`）的有效负载。 这些值是只读的，由[!DNL Schema Registry]分配。

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088461236,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

执行GET请求[列出租户容器中的所有架构](#list)将包含新架构。 您可以使用URL编码的`$id` URI执行[查找(GET)请求](#lookup)以直接查看新架构。

要将其他字段添加到架构，您可以执行[PATCH操作](#patch)以将字段组添加到架构的`allOf`和`meta:extends`数组。

## 更新架构 {#put}

您可以通过PUT操作替换整个架构，从而本质上重新写入资源。 通过PUT请求更新架构时，正文必须包括在POST请求中[创建新架构](#create)时所需的所有字段。

>[!NOTE]
>
>如果只想更新部分架构而不是完全替换它，请参阅[更新部分架构](#patch)部分。

**API格式**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 要重写的架构的`meta:altId`或URL编码的`$id`。 |

{style="table-layout:auto"}

**请求**

以下请求替换了现有架构，更改了其`title`、`description`和`allOf`属性。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Commercial Property Information",
        "description": "Information related to commercial properties.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7" 
          } 
        ]
      }'
```

**响应**

成功的响应将返回已更新架构的详细信息。

```JSON
{
    "title":"Commercial Property Information",
    "description": "Information related to commercial properties.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088470592,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## 更新架构的一部分 {#patch}

您可以使用PATCH请求更新架构的一部分。 [!DNL Schema Registry]支持所有标准JSON修补程序操作，包括`add`、`remove`和`replace`。 有关JSON修补程序的详细信息，请参阅[API基础指南](../../landing/api-fundamentals.md#json-patch)。

>[!NOTE]
>
>如果要使用新值替换整个资源，而不是更新单个字段，请参阅[使用PUT操作替换架构](#put)部分。

最常见的PATCH操作之一是将以前定义的字段组添加到架构中，如下面的示例所示。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 要更新的架构的URL编码的`$id` URI或`meta:altId`。 |

{style="table-layout:auto"}

**请求**

下面的示例请求通过将字段组的`$id`值同时添加到`meta:extends`和`allOf`数组，向架构中添加了新的字段组。

请求正文采用数组的形式，每个列出的对象表示对单个字段的特定更改。 每个对象都包含要执行的操作(`op`)、应该对(`path`)执行该操作的字段，以及该操作中应该包含哪些信息(`value`)。

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { 
          "op": "add",
          "path": "/meta:extends/-",
          "value":  "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        },
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
          }
        }
      ]'
```

**响应**

响应显示两个操作均已成功执行。 字段组`$id`已添加到`meta:extends`数组，并且字段组`$id`的引用(`$ref`)现在显示在`allOf`数组中。

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## 启用架构以在实时客户档案中使用 {#union}

为了使架构参与[实时客户个人资料](../../profile/home.md)，您必须将`union`标记添加到架构的`meta:immutableTags`数组。 您可以通过对相关架构发出PATCH请求来实现这一点。

>[!IMPORTANT]
>
>不可变标记是旨在设置但不会移除的标记。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 要启用的架构的URL编码的`$id` URI或`meta:altId`。 |

{style="table-layout:auto"}

**请求**

下面的示例请求将`meta:immutableTags`数组添加到现有架构中，为该数组赋予`union`单个字符串值，以启用它以用于配置文件。

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "add",
          "path": "/meta:immutableTags",
          "value": ["union"]
        }
      ]'
```

**响应**

成功的响应返回更新架构的详细信息，表明已添加`meta:immutableTags`数组。

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    },
    "meta:immutableTags": [
      "union"
    ]
}
```

现在，您可以查看此架构的类的合并以确认架构的字段已显示。 有关详细信息，请参阅[联合终结点指南](./unions.md)。

## 删除架构 {#delete}

有时可能需要从架构注册表中删除架构。 可使用路径中提供的架构ID执行DELETE请求，从而达到此目的。

**API格式**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 要删除的架构的URL编码的`$id` URI或`meta:altId`。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态204（无内容）和一个空白正文。

您可以通过尝试对架构进行查找(GET)请求来确认删除。 您需要在请求中包含`Accept`标头，但应该会收到HTTP状态404 （未找到），因为架构已从架构注册表中删除。
