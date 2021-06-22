---
keywords: Experience Platform；主页；热门主题；API;XDM;XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；数据模型；模式注册表；模式注册表；模式；模式；模式；模式；模式；模式；创建
solution: Experience Platform
title: 架构API端点
description: 架构注册表API中的/schemas端点允许您以编程方式管理体验应用程序中的XDM架构。
topic-legacy: developer guide
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: e4bf5bb77ac4186b24580329699d74d653310d93
workflow-type: tm+mt
source-wordcount: '1458'
ht-degree: 4%

---

# 架构端点

可以将架构视为要摄取到Adobe Experience Platform中的数据的蓝图。 每个架构都由一个类和一个或多个架构字段组组成。 [!DNL Schema Registry] API中的`/schemas`端点允许您以编程方式管理体验应用程序中的模式。

## 快速入门

本指南中使用的API端点是[[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)的一部分。 在继续操作之前，请查阅[快速入门指南](./getting-started.md) ，以获取相关文档的链接、本文档中API调用示例的阅读指南，以及成功调用任何Experience PlatformAPI所需的标头的重要信息。

## 检索架构列表 {#list}

您可以通过分别向`/global/schemas`或`/tenant/schemas`发出GET请求，在`global`或`tenant`容器下列出所有架构。

>[!NOTE]
>
>列出资源时，方案注册表将结果集限制为300个项目。 要返回超出此限制的资源，您必须使用分页参数。 还建议您使用其他查询参数来筛选结果并减少返回的资源数。 有关详细信息，请参阅附录文档中关于[查询参数](./appendix.md#query)的部分。

**API格式**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 存放要检索的架构的容器：`global`用于Adobe创建的架构，或`tenant`用于您的组织拥有的架构。 |
| `{QUERY_PARAMS}` | 用于按筛选结果的可选查询参数。 有关可用参数的列表，请参阅[附录文档](./appendix.md#query)。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求从`tenant`容器中检索架构列表，使用`orderby`查询参数按结果的`title`属性对结果进行排序。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

响应格式取决于请求中发送的`Accept`标头。 以下`Accept`标头可用于列出架构：

| `Accept` 标题 | 描述 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每个资源的简短摘要。 这是列出资源的建议标头。 (限制：300) |
| `application/vnd.adobe.xed+json` | 为每个资源返回完整的JSON架构，其中包含原始的`$ref`和`allOf`。 (限制：300) |

{style=&quot;table-layout:auto&quot;}

**响应**

上述请求使用了`application/vnd.adobe.xed-id+json` `Accept`标头，因此响应仅包含每个架构的`title`、`$id`、`meta:altId`和`version`属性。 使用另一个`Accept`标头(`application/vnd.adobe.xed+json`)可返回每个架构的所有属性。 根据响应中需要的信息选择相应的`Accept`标头。

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

您可以通过发出GET请求来查找特定架构，该请求将架构的ID包含在路径中。

**API格式**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 存放要检索的架构的容器：`global`用于Adobe创建的架构，或`tenant`用于您的组织拥有的架构。 |
| `{SCHEMA_ID}` | 要查找的架构的`meta:altId`或URL编码的`$id`。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求检索路径中由其`meta:altId`值指定的架构。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

响应格式取决于请求中发送的`Accept`标头。 所有查找请求都要求`version`包含在`Accept`标头中。 以下`Accept`标头可用：

| `Accept` 标题 | 描述 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | 具有`$ref`和`allOf`的Raw具有标题和描述。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 和 `allOf` 已解析，有标题和描述。 |
| `application/vnd.adobe.xed-notext+json; version=1` | 具有`$ref`和`allOf`的原始文件，没有标题或描述。 |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 和解 `allOf` 析后，不会显示标题或描述。 |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 和已 `allOf` 解析的描述符。 |

{style=&quot;table-layout:auto&quot;}

**响应**

成功的响应会返回架构的详细信息。 返回的字段取决于请求中发送的`Accept`标头。 尝试使用不同的`Accept`标头来比较响应并确定哪个标头最适合您的用例。

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
  "imsOrg": "{IMS_ORG}",
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

架构组合过程从分配类开始。 类定义数据（记录或时间序列）的关键行为方面，以及描述将要摄取的数据所需的最小字段。

>[!NOTE]
>
>以下示例调用只是一个基准示例，用于说明如何在API中创建架构，且类的组合要求最低，没有字段组。 有关如何在API中创建架构的完整步骤，包括如何使用字段组和数据类型分配字段，请参阅[架构创建教程](../tutorials/create-schema-api.md)。

**API格式**

```http
POST /tenant/schemas
```

**请求**

请求必须包含引用类`$id`的`allOf`属性。 此属性定义架构将实现的“基类”。 在本例中，基类是之前创建的“属性信息”类。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `allOf` | 对象数组，每个对象引用其模式实现的字段的类或字段组。 每个对象都包含一个属性(`$ref`)，其值表示新架构将实施的类或字段组的`$id`。 必须提供一个类，其中包含零个或多个附加字段组。 在上例中，`allOf`数组中的单个对象是架构的类。 |

{style=&quot;table-layout:auto&quot;}

**响应**

成功响应会返回HTTP状态201（已创建）和包含新创建架构详细信息（包括`$id`、`meta:altId`和`version`）的有效负载。 这些值是只读的，由[!DNL Schema Registry]分配。

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
    "imsOrg": "{IMS_ORG}",
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

对[列出租户容器中所有架构](#list)执行GET请求时，现在将包含新架构。 您可以使用URL编码的`$id` URI执行[查找(GET)请求](#lookup) ，以直接查看新架构。

要向架构添加其他字段，可以执行[PATCH操作](#patch) ，以将字段组添加到架构的`allOf`和`meta:extends`数组。

## 更新架构 {#put}

您可以通过PUT操作替换整个架构，实质上是重写资源。 通过PUT请求更新架构时，主体必须包含在POST请求中创建新架构](#create)时需要填写的所有字段。[

>[!NOTE]
>
>如果只想更新架构的一部分而不是完全替换它，请参阅[更新架构的一部分](#patch)中的部分。

**API格式**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 要重写的架构的`meta:altId`或URL编码的`$id`。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求会替换现有架构，并更改其`title`、`description`和`allOf`属性。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的响应会返回更新架构的详细信息。

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
    "imsOrg": "{IMS_ORG}",
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

## 更新模式的一部分 {#patch}

您可以使用PATCH请求更新架构的一部分。 [!DNL Schema Registry]支持所有标准的JSON修补程序操作，包括`add`、`remove`和`replace`。 有关JSON修补程序的更多信息，请参阅[API基础知识指南](../../landing/api-fundamentals.md#json-patch)。

>[!NOTE]
>
>如果要使用新值替换整个资源，而不是更新单个字段，请参阅[中使用PUT操作](#put)替换架构的部分。

最常见的PATCH操作之一是将之前定义的字段组添加到架构，如以下示例所示。

**API格式**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 要更新的架构的URL编码的`$id` URI或`meta:altId`。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下示例请求通过将字段组的`$id`值添加到`meta:extends`和`allOf`数组，将新字段组添加到架构中。

请求正文采用数组的形式，每个列出的对象都表示对单个字段的特定更改。 每个对象包括要执行的操作(`op`)，该操作应在(`path`)上执行的字段，以及该操作中应包含哪些信息(`value`)。

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

响应显示两个操作均已成功执行。 字段组`$id`已添加到`meta:extends`数组中，对字段组`$id`的引用(`$ref`)现在显示在`allOf`数组中。

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
    "imsOrg": "{IMS_ORG}",
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

## 启用架构以在实时客户资料中使用 {#union}

为了使架构参与[实时客户配置文件](../../profile/home.md)，您必须向架构的`meta:immutableTags`阵列添加`union`标记。 为此，您可以对相关架构发出PATCH请求。

>[!IMPORTANT]
>
>不可变标记是指要设置但从不删除的标记。

**API格式**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 要启用的架构的URL编码的`$id` URI或`meta:altId`。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下示例请求将`meta:immutableTags`数组添加到现有架构，为该数组提供单个字符串值`union`，以便在“配置文件”中使用。

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的响应会返回更新的架构的详细信息，其中显示已添加`meta:immutableTags`数组。

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
    "imsOrg": "{IMS_ORG}",
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

现在，您可以查看此架构类的并集，以确认已表示架构的字段。 有关更多信息，请参阅[unions端点指南](./unions.md)。

## 删除架构 {#delete}

有时可能需要从架构注册表中删除架构。 这是通过使用路径中提供的架构ID执行DELETE请求来完成的。

**API格式**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 要删除的架构的URL编码的`$id` URI或`meta:altId`。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态204（无内容）和空白正文。

您可以通过尝试对架构进行查询(GET)请求来确认删除。 您需要在请求中包含`Accept`标头，但应会收到HTTP状态404（未找到），因为架构已从架构注册表中删除。
