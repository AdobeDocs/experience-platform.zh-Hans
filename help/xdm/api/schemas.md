---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;schema;Schema;schemas;Schemas;create
solution: Experience Platform
title: 创建模式
description: 模式注册表API中的/模式端点允许您在体验应用程序中以编程方式管理XDM模式。
topic: developer guide
translation-type: tm+mt
source-git-commit: 0b55f18eabcf1d7c5c233234c59eb074b2670b93
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 2%

---


# 模式端点

模式可以被视为您希望收录到Adobe Experience Platform的数据的蓝图。 每个模式由一个类和零个或多个混音组成。 API `/schemas` 中的端点 [!DNL Schema Registry] 允许您以编程方式管理体验应用程序中的模式。

## 入门指南

本指南中使用的API端点是API的一 [[!DNL Schema Registry] 部分](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)。 在继续之前，请查 [看入门指南](./getting-started.md) ，了解相关文档的链接、阅读此文档中示例API调用的指南，以及成功调用任何Experience PlatformAPI所需标头的重要信息。

## 检索列表模式 {#list}

您可以通过分别向或发出 `global` 列表请 `tenant` 求，GET或容器下的 `/global/schemas` 所有 `/tenant/schemas`模式。

>[!NOTE]
>
>列出资源时，模式注册表将结果集限制为300项。 要返回超出此限制的资源，必须使用分页参数。 还建议您使用其他查询参数来筛选结果并减少返回的资源数。 有关详细信息，请 [参阅附录](./appendix.md#query) 文档中有关查询参数的一节。

**API格式**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 存放要检索的模式的容器: `global` adobe创建的模式 `tenant` 或您组织拥有的模式。 |
| `{QUERY_PARAMS}` | 可选查询参数，用于筛选结果。 有关可 [用参数的列表](./appendix.md#query) ，请参阅附录文档。 |

**请求**

以下请求从列表检索一模式容器，使 `tenant` 用查询参数 `orderby` 按结果的属性对结果进行 `title` 排序。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

响应格式取决于在请 `Accept` 求中发送的标头。 列出模式 `Accept` 时可使用以下标题：

| `Accept` 标题 | 描述 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每个资源的简短摘要。 这是列出资源的建议标头。 (限制：300) |
| `application/vnd.adobe.xed+json` | 返回每个资源的完整JSON模式，其中包 `$ref` 含原始 `allOf` 资源。 (限制：300) |

**响应**

上述请求使用 `application/vnd.adobe.xed-id+json` 了标 `Accept` 头，因此响应只包括每个 `title`模式的、 `$id``meta:altId`和 `version` 属性。 使用其他 `Accept` 标题(`application/vnd.adobe.xed+json`)可返回每个模式的所有属性。 根据您在 `Accept` 响应中需要的信息选择相应的标题。

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

## 查找模式 {#lookup}

您可以通过发出在路径中包含模式ID的GET请求来查找特定模式。

**API格式**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 存放要检索的模式的容器: `global` adobe创建的模式或 `tenant` 您组织拥有的模式。 |
| `{SCHEMA_ID}` | 要 `meta:altId` 查找的模式 `$id` 的或URL编码的。 |

**请求**

以下请求检索由路径中其值 `meta:altId` 指定的模式。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
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

成功的响应会返回模式的详细信息。 返回的字段取决于在请 `Accept` 求中发送的标题。 尝试不同 `Accept` 的标题以比较响应并确定最适合您的用例的标题。

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

## 创建模式 {#create}

模式合成流程从分配类开始。 该类定义数据（记录或时间序列）的关键行为方面以及描述将要摄取的数据所需的最小字段。

>[!NOTE]
>
>以下示例调用仅是如何在API中创建模式的基准示例，类的最小合成要求没有混合。 有关如何在API中创建模式的完整步骤（包括如何使用混音和数据类型分配字段），请参阅 [模式创建教程](../tutorials/create-schema-api.md)。

**API格式**

```http
POST /tenant/schemas
```

**请求**

请求必须包含引 `allOf` 用类的属 `$id` 性的属性。 此属性定义模式将实现的“基类”。 在此示例中，基类是先前创建的“属性信息”类。

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
| `allOf` | 对象的数组，每个对象引用一个类或混合，模式实现其字段。 每个对象都包含一个属`$ref`性()，其值表示 `$id` 将实现的类或新模式中的混合。 必须提供一个类，并且不提供或多个附加混音。 在上例中，数组中的单个 `allOf` 对象是模式的类。 |

**响应**

成功的响应会返回HTTP状态201（已创建）和包含新创建模式的详细信息（包括、和） `$id`的 `meta:altId`有效负荷 `version`。 这些值是只读的，由指定 [!DNL Schema Registry]。

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

执行GET请求以 [列表租户容器](#list) 中的所有模式，现在将包括新模式。 您可以使用 [URL编码的](#lookup) URI执行查 `$id` 找(GET)请求，以直接视图新模式。

要向模式添加其他字段，可以执行 [PATCH操作](#patch) ，向模式和阵列 `allOf` 添加混 `meta:extends` 合。

## 更新模式 {#put}

您可以通过PUT操作替换整个模式，实质上是重写资源。 在通过模式请求更新PUT时，主体必须包括在POST请求中创建新模式时 [需要的所](#create) 有字段。

>[!NOTE]
>
>如果只想更新模式的一部分而不是完全替换它，请参阅有关更 [新模式的一部分的部分](#patch)。

**API格式**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 要 `meta:altId` 重写的模式 `$id` 的或URL编码的数据。 |

**请求**

以下请求将替换现有模式，并更改 `title`其 `description`、属 `allOf` 性。

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

成功的响应会返回更新模式的详细信息。

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

您可以使用模式请求更新PATCH的一部分。 支 [!DNL Schema Registry] 持所有标准JSON修补程序操作， `add`包括 `remove`、和 `replace`。 有关JSON修补程序的详细信息，请参阅 [API基础指南](../../landing/api-fundamentals.md#json-patch)。

>[!NOTE]
>
>如果要用新值替换整个资源，而不是更新单个字段，请参阅使用 [模式操作替换PUT一节](#put)。

最常见的PATCH操作之一涉及向模式添加以前定义的混音，如下例所示。

**API格式**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | URL编码 `$id` 的URI `meta:altId` 或要更新的模式。 |

**请求**

以下示例请求通过将混音的值添加到数组和数组，将 `$id` 新的混音添 `meta:extends` 加到 `allOf` 模式。

请求主体采用数组的形式，每个列出的对象代表对单个字段的特定更改。 每个对象包括要执行的(`op`)操作，该操作应在()上执行的字段`path`，以及该操作()应包括哪些信`value`息。

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

响应显示两个操作都成功执行。 混音已 `$id` 添加到数组 `meta:extends` 中，现在在数组中显示对混`$ref`音的引用( `$id``allOf` )。

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

## 启用模式以用于实时客户用户档案 {#union}

为了让模式参与实 [时客户用户档案](../../profile/home.md)，您必须在 `union` 模式阵列中添加标 `meta:immutableTags` 签。 您可以通过向相关PATCH发出模式请求来完成此操作。

>[!IMPORTANT]
>
>不可变标记是要设置但从不删除的标记。

**API格式**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 要启用的 `$id` URL编 `meta:altId` 码的URI或模式。 |

**请求**

下面的示例请求向现 `meta:immutableTags` 有模式添加一个数组，为该数组提供一个字符串值 `union` ，使其能够用于用户档案。

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

成功的响应会返回更新模式的详细信息，显示已 `meta:immutableTags` 添加阵列。

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

您现在可以视图此模式类的合并，以确认表示模式的字段。 See the [unions endpoint guide](./unions.md) for more information.

## 删除模式 {#delete}

有时可能需要从模式注册表中删除模式。 这是通过使用路径中提供的DELETEID执行模式请求来完成的。

**API格式**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | URL编码 `$id` 的URI `meta:altId` 或要删除的模式。 |

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

成功的响应返回HTTP状态204（无内容）和空白正文。

您可以通过尝试对GET进行查找(模式)请求来确认删除。 您需要在请求中 `Accept` 包含一个头，但应收到HTTP状态404（未找到），因为模式已从模式注册表中删除。