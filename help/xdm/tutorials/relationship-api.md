---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;schema;Schema;schemas;Schemas;relationship;Relationship;relationship descriptor;Relationship descriptor;reference identity;Reference identity;
solution: Experience Platform
title: 使用模式注册表API定义两个模式之间的关系
description: 本文档提供了一个教程，用于定义组织使用模式注册表API定义的两个模式之间的一对一关系。
topic: tutorials
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '1304'
ht-degree: 1%

---


# 使用API定义两个模式之间的关 [!DNL Schema Registry] 系

了解不同渠道客户之间的关系及其与您品牌的互动是Adobe Experience Platform的重要部分。 在(XDM)模式结构中定 [!DNL Experience Data Model] 义这些关系，使您能够对客户数据获得复杂的洞察。

虽然模式关系可以通过使用合并模式来推断， [!DNL Real-time Customer Profile]但这仅适用于共享同一类的模式。 要在属于不同类的两个模式之间建立关系，必 **须向源模式** (引用目标模式的标识)中添加一个专用的关系字段。

本文档提供了一个教程，用于定义组织使用[!DNL模式注册表API定义的两个模式之 [间的一对一关系](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)。

## 入门指南

本教程需要对(XDM) [!DNL Experience Data Model] 和进行有效的了解 [!DNL XDM System]。 在开始本教程之前，请查阅以下文档：

* [Experience Platform中的XDM系统](../home.md):XDM及其实施概述 [!DNL Experience Platform]。
   * [模式合成基础](../schema/composition.md):介绍XDM模式的构件。
* [[!DNL实时客户用户档案]](../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

在开始本教程之前，请查 [看开发人员指南](../api/getting-started.md) ，了解成功调用API所需了解的重要 [!DNL Schema Registry] 信息。 这包括您 `{TENANT_ID}`的、“容器”的概念以及发出请求所需的标题(尤其要注意标题及 [!DNL Accept] 其可能的值)。

## 定义源和目标模式 {#define-schemas}

您应已创建将在关系中定义的两个模式。 本教程在组织的当前忠诚度项目(在“”模式中定义)的成员与其喜爱的酒店(在“”模式中定义)之[!DNL Loyalty Members]间创建了[!DNL Hotels]一种关系。

模式关系由源 **模式表示** ，该源具有引用目标模式内的另 **一个字段**。 在接下来的步骤中，[!DNL Loyalty Members]“”将作为源模式，而“[!DNL Hotels]”将作为目标模式。

>[!IMPORTANT]
>
>要建立关系，两个模式必须定义主身份并启用 [!DNL Real-time Customer Profile]。 如果您需要有关如何 [相应配置模式的指导](./create-schema-api.md#profile) ，请参阅模式创建教程中有关启用模式以在用户档案中使用的部分。

要定义两个模式之间的关系，您必须首先获取两个 `$id` 模式的值。 如果您知道模式的显`title`示名称()，则可以通过 `$id` 在API中向端点发出GET请求 `/tenant/schemas` 来查找其 [!DNL Schema Registry] 值。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

>[!NOTE]
>
>标 [!DNL Accept] 题 `application/vnd.adobe.xed-id+json` 仅返回结果模式的标题、ID和版本。

**响应**

成功的响应会返回由您的组织定义的列表, `name`包括 `$id`其、 `meta:altId`和模式 `version`。

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

记录 `$id` 要定义之间关系的两个模式的值。 这些值将在后续步骤中使用。

## 为源模式定义引用字段

在关系数 [!DNL Schema Registry]据库表中，关系描述符的工作方式与外键相似：源模式中的字段用作对目标模式 **的主标识** 字段的引用。 如果您的源模式没有用于此目的的字段，您可能需要使用新字段创建混音并将其添加到模式。 此新字段的 `type` 值必须为“[!DNL string]”。

>[!IMPORTANT]
>
>与目标模式不同，源模式不能将其主标识用作引用字段。

在本教程中，目标模式“[!DNL Hotels]”包含 `email` 一个用作模式主标识的字段，因此也将用作其引用字段。 但是，源模式“[!DNL Loyalty Members]”没有要用作引用的专用字段，并且必须给出一个新的混音，以向模式添加新字段： `favoriteHotel`.

>[!NOTE]
>
>如果您的源模式已经有一个您计划用作引用字段的专用字段，则可以跳到创建引用描述符 [的步骤](#reference-identity)。

### 创建新混音

要向模式添加新字段，必须先在混音中定义该字段。 可以通过向端点发出POST请求来创建新混 `/tenant/mixins` 音。

**API格式**

```http
POST /tenant/mixins
```

**请求**

以下请求将创建一个新的混音，该混音 `favoriteHotel` 将在其 `_{TENANT_ID}` 添加到的任何命名空间的模式下添加一个字段。

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Favorite Hotel",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Favorite hotel mixin for the Loyalty Members schema.",
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

成功的响应会返回新创建的混音的详细信息。

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
    "description": "Favorite hotel mixin for the Loyalty Members schema.",
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
| `$id` | 只读，系统生成新混音的唯一标识符。 采用URI的形式。 |

记录 `$id` 混音的URI，在将混音添加到源模式的下一步中使用。

### 将混音添加到源模式

创建混音后，可以通过向端点发出模式请求将其添加到源PATCH `/tenant/schemas/{SCHEMA_ID}` 中。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | URL编码的 `$id` URI或 `meta:altId` 源模式的URI。 |

**请求**

以下请求将“[!DNL Favorite Hotel]”混音添加到“[!DNL Loyalty Members]”模式。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `op` | 要执行的PATCH操作。 此请求使用该 `add` 操作。 |
| `path` | 将添加新资源的模式字段的路径。 向模式添加混音时，值必须为“/allOf/-”。 |
| `value.$ref` | 要 `$id` 添加的混音。 |

**响应**

成功的响应会返回更新模式的详细信息，该现在 `$ref` 包括其数组下添加的混音的 `allOf` 值。

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
    "imsOrg": "{IMS_ORG}",
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

如果模式字段用作关系中其他模式的引用，则必须对其应用引用标识描述符。 由于“ `favoriteHotel` ”中的字[!DNL Loyalty Members]段将引用“”中的字段，因 `email` 此必须[!DNL Hotels]`email` 为其提供引用标识描述符。

通过向端点发出模式请求，为目标POST创建引用描述 `/tenant/descriptors` 符。

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下请求为目标模式“” `email` 中的字段创建引用描述[!DNL Hotels]符。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/email",
    "xdm:identityNamespace": "Email"
  }'
```

| 参数 | 描述 |
| --- | --- |
| `@type` | 要定义的描述符的类型。 对于引用描述符，该值必须为“xdm:descriptorReferenceIdentity”。 |
| `xdm:sourceSchema` | 目 `$id` 标模式的URL。 |
| `xdm:sourceVersion` | 目标模式的版本号。 |
| `sourceProperty` | 目标模式的主标识字段的路径。 |
| `xdm:identityNamespace` | 引用字段的标识命名空间。 这必须是定义字段作为命名空间主标识时使用的模式。 有关更多 [信息，请参阅](../../identity-service/home.md) “身份命名空间概述”。 |

**响应**

成功的响应会返回新创建的目标模式引用描述符的详细信息。

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/email",
    "xdm:identityNamespace": "Email",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## 创建关系描述符 {#create-descriptor}

关系描述符建立源模式和目标模式之间的一对一关系。 为目标模式定义引用描述符后，可以通过向端点发出POST请求来创建新的关系描述符 `/tenant/descriptors` 。

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下请求将创建一个新的关系描述符，[!DNL Loyalty Members]其中“”作为源模式,“[!DNL Legacy Loyalty Members]”作为目标模式。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/email"
  }'
```

| 参数 | 描述 |
| --- | --- |
| `@type` | 要创建的描述符的类型。 关 `@type` 系描述符的值为“xdm:descriptorOneToOne”。 |
| `xdm:sourceSchema` | 源 `$id` 模式的URL。 |
| `xdm:sourceVersion` | 源模式的版本号。 |
| `xdm:sourceProperty` | 源模式中引用字段的路径。 |
| `xdm:destinationSchema` | 目 `$id` 标模式的URL。 |
| `xdm:destinationVersion` | 目标模式的版本号。 |
| `xdm:destinationProperty` | 目标模式中引用字段的路径。 |

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

通过遵循本教程，您成功地创建了两个模式之间的一对一关系。 有关使用API使用描述符的更 [!DNL Schema Registry] 多信息，请参 [阅模式注册开发人员指南](../api/descriptors.md)。 有关如何在UI中定义模式关系的步骤，请参阅使用模式编 [辑器定义模式关系的教程](relationship-ui.md)。
