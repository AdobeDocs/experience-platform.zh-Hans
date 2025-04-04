---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；体验数据模型；数据模型；数据模型；架构注册表；架构注册表；架构；架构；架构；架构；关系；关系；关系描述符；关系描述符；引用身份；引用身份；
title: 使用架构注册表API定义两个架构之间的关系
description: 本文档提供了一个教程，用于定义贵组织使用架构注册表API定义的两个架构之间的一对一关系。
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 1%

---

# 使用[!DNL Schema Registry] API定义两个架构之间的关系

了解客户之间的关系以及客户在不同渠道中与您的品牌之间的互动是Adobe Experience Platform的重要组成部分。 通过在[!DNL Experience Data Model] (XDM)架构的结构中定义这些关系，您可以获得有关客户数据的复杂洞察。

虽然可以使用合并架构和[!DNL Real-Time Customer Profile]推断架构关系，但这仅适用于共享相同类的架构。 若要在属于不同类的两个架构之间建立关系，必须将专用关系字段添加到&#x200B;**源架构**&#x200B;中，该字段指示单独&#x200B;**引用架构**&#x200B;的标识。

>[!NOTE]
>
>架构注册表API将架构引用为“目标架构”。 不应与[数据准备映射集](../../data-prep/mapping-set.md)中的目标架构或[目标连接](../../destinations/home.md)的架构混淆。

此文档提供了一个教程，用于定义贵组织使用[[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/)定义的两个架构之间的一对一关系。

## 快速入门

本教程需要对[!DNL Experience Data Model] (XDM)和[!DNL XDM System]有一定的了解。 在开始本教程之前，请查看以下文档：

* Experience Platform中的[XDM System](../home.md)： [!DNL Experience Platform]中的XDM及其实现的概述。
   * [架构组合的基础知识](../schema/composition.md)： XDM架构的构建块简介。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。
* [沙盒](../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

在开始本教程之前，请查看[开发人员指南](../api/getting-started.md)以了解成功调用[!DNL Schema Registry] API所需了解的重要信息。 这包括您的`{TENANT_ID}`、“容器”的概念以及发出请求所需的标头（请特别注意[!DNL Accept]标头及其可能的值）。

## 定义源和引用架构 {#define-schemas}

您应已创建将在关系中定义的两个架构。 本教程在组织当前忠诚度计划（在“[!DNL Loyalty Members]”架构中定义）的成员与其喜爱的酒店（在“[!DNL Hotels]”架构中定义）之间创建关系。

架构关系由&#x200B;**源架构**&#x200B;表示，该架构具有引用&#x200B;**引用架构**&#x200B;内其他字段的字段。 在接下来的步骤中，“[!DNL Loyalty Members]”将用作源架构，而“[!DNL Hotels]”将用作参考架构。

>[!IMPORTANT]
>
>为了建立关系，两个架构都必须定义主标识并启用[!DNL Real-Time Customer Profile]。 如果您需要有关如何相应地配置架构的指导，请参阅架构创建教程中有关[启用架构以用于配置文件](./create-schema-api.md#profile)的部分。

要定义两个架构之间的关系，必须首先获取两个架构的`$id`值。 如果您知道架构的显示名称(`title`)，则可以通过向[!DNL Schema Registry] API中的`/tenant/schemas`端点发出GET请求来查找其`$id`值。

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
>[!DNL Accept]标题`application/vnd.adobe.xed-id+json`仅返回生成的架构的标题、ID和版本。

**响应**

成功的响应将返回由您的组织定义的架构列表，包括它们的`name`、`$id`、`meta:altId`和`version`。

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

记录要定义两者之间关系的两个架构的`$id`值。 这些值将在后面的步骤中使用。

## 为源架构定义参考字段

在[!DNL Schema Registry]中，关系描述符的工作方式与关系数据库表中的外键类似：源架构中的字段用作对引用架构的主标识字段的引用。 如果您的源架构中没有用于此目的的字段，您可能需要使用新字段创建架构字段组，并将其添加到架构中。 此新字段的`type`值必须为`string`。

>[!IMPORTANT]
>
>源架构不能将其主标识用作引用字段。

在本教程中，引用架构“[!DNL Hotels]”包含用作架构主标识的`hotelId`字段。 但是，源架构“[!DNL Loyalty Members]”没有要用作引用`hotelId`的专用字段，因此需要创建自定义字段组才能向架构中添加新字段：`favoriteHotel`。

>[!NOTE]
>
>如果您的源架构已有计划用作引用字段的专用字段，则可以跳到[创建引用描述符](#reference-identity)的步骤。

### 创建新字段组

要向架构添加新字段，必须首先在字段组中定义它。 您可以通过向`/tenant/fieldgroups`端点发出POST请求来创建新的字段组。

**API格式**

```http
POST /tenant/fieldgroups
```

**请求**

以下请求创建一个新的字段组，该字段组将在其添加到的任何架构的`_{TENANT_ID}`命名空间下添加`favoriteHotel`字段。

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

成功的响应将返回新创建的字段组的详细信息。

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
| `$id` | 系统生成的只读新字段组的唯一标识符。 采用URI形式。 |

{style="table-layout:auto"}

记录字段组的`$id` URI，以用于将该字段组添加到源架构的下一步骤。

### 将字段组添加到源架构

创建字段组后，您可以通过向`/tenant/schemas/{SCHEMA_ID}`端点发出PATCH请求来将其添加到源架构中。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | URL编码的源架构的`$id` URI或`meta:altId`。 |

{style="table-layout:auto"}

**请求**

以下请求将“[!DNL Favorite Hotel]”字段组添加到“[!DNL Loyalty Members]”架构。

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
| `op` | 要执行的PATCH操作。 此请求使用`add`操作。 |
| `path` | 将添加新资源的架构字段的路径。 将字段组添加到架构时，该值必须为“/allOf/ — ”。 |
| `value.$ref` | 要添加的字段组的`$id`。 |

{style="table-layout:auto"}

**响应**

成功的响应返回已更新架构的详细信息，该架构现在包括其`allOf`数组下添加字段组的`$ref`值。

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

## 创建引用身份描述符 {#reference-identity}

架构字段必须具有应用于它们的引用身份描述符，才能用作对关系中其他架构的引用。 由于“[!DNL Loyalty Members]”中的`favoriteHotel`字段将引用“[!DNL Hotels]”中的`hotelId`字段，因此必须为`favoriteHotel`指定引用标识描述符。

通过向`/tenant/descriptors`端点发出POST请求，为源架构创建引用描述符。

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下请求在源架构“[!DNL Loyalty Members]”中为`favoriteHotel`字段创建引用描述符。

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
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:identityNamespace": "Hotel ID"
  }'
```

| 参数 | 描述 |
| --- | --- |
| `@type` | 正在定义的描述符类型。 对于引用描述符，该值必须为`xdm:descriptorReferenceIdentity`。 |
| `xdm:sourceSchema` | 源架构的`$id` URL。 |
| `xdm:sourceVersion` | 源架构的版本号。 |
| `sourceProperty` | 源架构中用于引用引用架构主要标识的字段的路径。 |
| `xdm:identityNamespace` | 引用字段的身份命名空间。 此命名空间必须与引用架构的主要身份相同。 有关详细信息，请参阅[身份命名空间概述](../../identity-service/home.md)。 |

{style="table-layout:auto"}

**响应**

成功的响应将返回新创建的源字段的引用描述符的详细信息。

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:identityNamespace": "Hotel ID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## 创建关系描述符 {#create-descriptor}

关系描述符在源架构和引用架构之间建立一对一的关系。 一旦在源架构中为相应的字段定义了引用身份描述符，就可以通过对`/tenant/descriptors`端点发起POST请求来创建新的关系描述符。

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下请求创建新的关系描述符，“[!DNL Loyalty Members]”作为源架构，“[!DNL Hotels]”作为引用架构。

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
| `@type` | 要创建的描述符的类型。 关系描述符的`@type`值为`xdm:descriptorOneToOne`。 |
| `xdm:sourceSchema` | 源架构的`$id` URL。 |
| `xdm:sourceVersion` | 源架构的版本号。 |
| `xdm:sourceProperty` | 源架构中引用字段的路径。 |
| `xdm:destinationSchema` | 引用架构的`$id` URL。 |
| `xdm:destinationVersion` | 引用架构的版本号。 |
| `xdm:destinationProperty` | 引用架构中主标识字段的路径。 |

{style="table-layout:auto"}

### 响应

成功的响应将返回新创建的关系描述符的详细信息。

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

通过学习本教程，您已成功创建了两个架构之间的一对一关系。 有关使用[!DNL Schema Registry] API使用描述符的更多信息，请参阅[架构注册表开发人员指南](../api/descriptors.md)。 有关如何在UI中定义架构关系的步骤，请参阅有关[使用架构编辑器定义架构关系的教程](relationship-ui.md)。
