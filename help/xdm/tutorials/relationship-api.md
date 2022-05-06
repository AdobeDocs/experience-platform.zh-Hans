---
keywords: Experience Platform；主页；热门主题；API;XDM;XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；数据模型；架构注册；架构注册；架构；架构；架构；架构；关系；关系描述符；关系描述符；引用标识；引用标识；
solution: Experience Platform
title: 使用模式注册表API定义两个模式之间的关系
description: 本文档提供了一个教程，用于定义由贵组织使用架构注册API定义的两个架构之间的一对一关系。
topic-legacy: tutorial
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 2%

---

# 使用 [!DNL Schema Registry] API

了解客户之间的关系以及客户与品牌在各种渠道中的交互是Adobe Experience Platform的重要组成部分。 在 [!DNL Experience Data Model] (XDM)模式允许您对客户数据进行复杂的分析。

而架构关系可以通过使用并集架构和 [!DNL Real-time Customer Profile]，这仅适用于共享同一类的架构。 要在属于不同类的两个架构之间建立关系，必须将专用关系字段添加到源架构中，该源架构引用目标架构的标识。

本文档提供了一个教程，用于定义由贵组织使用 [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## 快速入门

本教程需要对 [!DNL Experience Data Model] (XDM)和 [!DNL XDM System]. 在开始使用本教程之前，请查阅以下文档：

* [XDM系统在Experience Platform](../home.md):XDM及其在 [!DNL Experience Platform].
   * [架构组合的基础知识](../schema/composition.md):介绍XDM模式的构建基块。
* [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

在启动本教程之前，请查看 [开发人员指南](../api/getting-started.md) 以了解成功调用 [!DNL Schema Registry] API。 这包括您的 `{TENANT_ID}`、“容器”的概念以及发出请求所需的标头(请特别注意 [!DNL Accept] 标题及其可能值)。

## 定义源架构和目标架构 {#define-schemas}

您应该已经创建了将在关系中定义的两个架构。 本教程将在组织当前忠诚度计划(在[!DNL Loyalty Members]“模式”和他们最喜爱的酒店(在“[!DNL Hotels]“架构”)。

架构关系由 **源模式** 具有引用 **目标架构**. 在后续步骤中，“[!DNL Loyalty Members]“ ”将是源架构，而“[!DNL Hotels]“ ”将用作目标架构。

>[!IMPORTANT]
>
>要建立关系，两个架构都必须定义了主标识，并启用 [!DNL Real-time Customer Profile]. 请参阅 [启用模式以在用户档案中使用](./create-schema-api.md#profile) 在架构创建教程中，如果您需要有关如何相应地配置架构的指导。

要定义两个架构之间的关系，您必须首先获取 `$id` 两个架构的值。 如果您知道显示名称(`title`)，您可以找到 `$id` 值 `/tenant/schemas` 的端点 [!DNL Schema Registry] API。

**API格式**

```http
GET /tenant/schemas
```

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

>[!NOTE]
>
>的 [!DNL Accept] 标题 `application/vnd.adobe.xed-id+json` 仅返回生成架构的标题、ID和版本。

**响应**

成功响应会返回由您的组织定义的架构列表，包括其 `name`, `$id`, `meta:altId`和 `version`.

```json
{
    "results": [
        {
            "title": "Newsletter Subscriptions",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/192a66930afad02408429174c311ae73",
            "meta:altId": "_{TENANT_ID}.schemas.192a66930afad02408429174c311ae73",
            "version": "1.2"
        },
        {
            "title": "Loyalty Members",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
            "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
            "version": "1.5"
        },
        {
            "title": "Hotels",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
            "meta:altId": "_{TENANT_ID}.schemas.d4ad4b8463a67f6755f2aabbeb9e02c7",
            "version": "1.0"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform-stage.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

记录 `$id` 要定义两者之间关系的两个架构的值。 这些值将在后续步骤中使用。

## 为源架构定义引用字段

在 [!DNL Schema Registry]，关系描述符的工作方式与关系数据库表中的外键类似：源架构中的字段用作对目标架构的主标识字段的引用。 如果您的源架构没有用于此目的的字段，则您可能需要使用新字段创建架构字段组并将其添加到架构中。 此新字段必须具有 `type` 值“[!DNL string]&quot;

>[!IMPORTANT]
>
>与目标架构不同，源架构不能将其主标识用作引用字段。

在本教程中，目标架构“[!DNL Hotels]&quot;包含 `hotelId` 字段作为架构的主标识，因此也将用作其引用字段。 但是，源架构“[!DNL Loyalty Members]&quot;没有要用作引用的专用字段，并且必须为添加新字段组以向架构添加新字段： `favoriteHotel`.

>[!NOTE]
>
>如果您的源架构已经有一个您计划用作引用字段的专用字段，则可以跳到 [创建引用描述符](#reference-identity).

### 创建新字段组

要向架构添加新字段，必须首先在字段组中定义该字段。 您可以通过向 `/tenant/fieldgroups` 端点。

**API格式**

```http
POST /tenant/fieldgroups
```

**请求**

以下请求会创建一个新字段组，该字段组将 `favoriteHotel` 字段 `_{TENANT_ID}` 添加到的任何架构的命名空间。

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Favorite Hotel",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Favorite hotel field group for the Loyalty Members schema.",
        "definitions": {
            "favoriteHotel": {
              "properties": {
                "_{TENANT_ID}": {
                  "type":"object",
                  "properties": {
                    "favoriteHotel": {
                      "title": "Favorite Hotel",
                      "type": "string",
                      "description": "Favorite hotel for a Loyalty Member."
                    }
                  }
                }
              }
            }
        },
        "allOf": [
            {
              "$ref": "#/definitions/favoriteHotel"
            }
        ]
      }'
```

**响应**

成功的响应会返回新创建字段组的详细信息。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220",
    "meta:altId": "_{TENANT_ID}.mixins.3387945212ad76ee59b6d2b964afb220",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "type": "object",
    "title": "Favorite Hotel",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Favorite hotel field group for the Loyalty Members schema.",
    "definitions": {
        "favoriteHotel": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "favoriteHotel": {
                            "title": "Favorite Hotel",
                            "type": "string",
                            "description": "Favorite hotel for a Loyalty Member.",
                            "meta:xdmType": "string"
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
            "$ref": "#/definitions/favoriteHotel"
        }
    ],
    "meta:xdmType": "object",
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:registryMetadata": {
        "eTag": "quM2aMPyb2NkkEiZHNCs/MG34E4=",
        "palm:sandboxName": "prod"
    }
}
```

| 属性 | 描述 |
| --- | --- |
| `$id` | 只读，系统生成的新字段组的唯一标识符。 采用URI的形式。 |

{style=&quot;table-layout:auto&quot;}

记录 `$id` 字段组的URI，用于将字段组添加到源架构的下一步。

### 将字段组添加到源架构

创建字段组后，您可以通过向 `/tenant/schemas/{SCHEMA_ID}` 端点。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | URL编码 `$id` URI或 `meta:altId` 源架构的URL。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求将“[!DNL Favorite Hotel]“ ”字段组[!DNL Loyalty Members]“架构”。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    { 
      "op": "add", 
      "path": "/allOf/-", 
      "value":  {
        "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
      }
    }
  ]'
```

| 属性 | 描述 |
| --- | --- |
| `op` | 要执行的PATCH操作。 此请求使用 `add` 操作。 |
| `path` | 将添加新资源的架构字段的路径。 向架构添加字段组时，值必须为“/allOf/ — ”。 |
| `value.$ref` | 的 `$id` 的字段组。 |

{style=&quot;table-layout:auto&quot;}

**响应**

成功的响应会返回更新架构的详细信息，该架构现在包括 `$ref` 其 `allOf` 数组。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
    "meta:resourceType": "schemas",
    "version": "1.1",
    "type": "object",
    "title": "Loyalty Members",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
        }
    ],
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:tenantNamespace": "_{TENANT_ID}",
    "imsOrg": "{ORG_ID}",
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3",
        "https://ns.adobe.com/{TENANT_ID}/mixins/61969bc646b66a6230a7e8840f4a4d33"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557525483804,
        "repo:lastModifiedDate": 1566419670915,
        "xdm:createdClientId": "{API_KEY}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "eTag": "ITNzu8BVTO5pw9wfCtTTpk6U4WY="
    }
}
```

## 创建引用标识描述符 {#reference-identity}

如果架构字段用作关系中其他架构的引用，则它们必须应用引用标识描述符。 自 `favoriteHotel` 字段[!DNL Loyalty Members]“”将表示 `hotelId` 字段[!DNL Hotels]&quot;, `hotelId` 必须提供引用标识描述符。

通过向发出POST请求，为目标模式创建引用描述符 `/tenant/descriptors` 端点。

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下请求会为 `hotelId` 目标架构“[!DNL Hotels]&quot;

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "Hotel ID"
  }'
```

| 参数 | 描述 |
| --- | --- |
| `@type` | 定义的描述符类型。 对于引用描述符，值必须为“xdm:descriptorReferenceIdentity”。 |
| `xdm:sourceSchema` | 的 `$id` 目标架构的URL。 |
| `xdm:sourceVersion` | 目标架构的版本号。 |
| `sourceProperty` | 目标架构的主标识字段的路径。 |
| `xdm:identityNamespace` | 引用字段的标识命名空间。 该命名空间必须与定义字段作为架构主标识时使用的命名空间相同。 请参阅 [身份命名空间概述](../../identity-service/home.md) 以了解更多信息。 |

{style=&quot;table-layout:auto&quot;}

**响应**

成功的响应会返回为目标架构新建引用描述符的详细信息。

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "Hotel ID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## 创建关系描述符 {#create-descriptor}

关系描述符在源模式和目标模式之间建立一对一关系。 在为目标架构定义引用描述符后，您可以通过向 `/tenant/descriptors` 端点。

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下请求将创建一个新的关系描述符，其中“[!DNL Loyalty Members]“ ”作为源架构和“[!DNL Legacy Loyalty Members]”作为目标架构。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId"
  }'
```

| 参数 | 描述 |
| --- | --- |
| `@type` | 要创建的描述符的类型。 的 `@type` 关系描述符的值为“xdm:descriptorOneToOne”。 |
| `xdm:sourceSchema` | 的 `$id` 源架构的URL。 |
| `xdm:sourceVersion` | 源架构的版本号。 |
| `xdm:sourceProperty` | 源架构中引用字段的路径。 |
| `xdm:destinationSchema` | 的 `$id` 目标架构的URL。 |
| `xdm:destinationVersion` | 目标架构的版本号。 |
| `xdm:destinationProperty` | 目标架构中引用字段的路径。 |

{style=&quot;table-layout:auto&quot;}

### 响应

成功的响应会返回新创建的关系描述符的详细信息。

```json
{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId",
    "meta:containerId": "tenant",
    "@id": "76f6cc7105f4eaab7eb4a5e1cb4804cadc741669"
}
```

## 后续步骤

通过阅读本教程，您成功地在两个架构之间创建了一对一关系。 有关使用描述符的更多信息 [!DNL Schema Registry] API，请参阅 [架构注册开发人员指南](../api/descriptors.md). 有关如何在UI中定义架构关系的步骤，请参阅 [使用架构编辑器定义架构关系](relationship-ui.md).
