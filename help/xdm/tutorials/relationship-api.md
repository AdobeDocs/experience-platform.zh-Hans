---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；架构注册表；架构注册表；架构；架构；架构；关系；关系描述符；关系描述符；引用身份；引用身份；
title: 使用架构注册表API定义两个架构之间的关系
description: 本文档提供了一个教程，用于定义贵组织使用架构注册表API定义的两个架构之间的一对一关系。
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '1383'
ht-degree: 1%

---

# 使用定义两个架构之间的关系 [!DNL Schema Registry] API

能够了解客户之间的关系以及客户在不同渠道中与您的品牌的互动是Adobe Experience Platform的重要组成部分。 在的结构中定义这些关系 [!DNL Experience Data Model] (XDM)架构允许您对客户数据获得复杂的见解。

虽然可以通过使用合并架构和来推断架构关系 [!DNL Real-Time Customer Profile]，这仅适用于共享相同类的架构。 要在属于不同类的两个架构之间建立关系，必须将专用关系字段添加到 **源架构**，指示单独的身份 **引用模式**.

>[!NOTE]
>
>架构注册表API将引用架构称为“目标架构”。 请不要将它们与中的目标架构混淆 [数据准备映射集](../../data-prep/mapping-set.md) 或架构 [目标连接](../../destinations/home.md).

此文档提供了一个教程，用于定义贵组织使用的两个架构之间的一对一关系。 [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## 快速入门

本教程需要您实际了解 [!DNL Experience Data Model] (XDM)和 [!DNL XDM System]. 在开始本教程之前，请查看以下文档：

* [Experience Platform中的XDM系统](../home.md)：XDM及其在中的实施概述 [!DNL Experience Platform].
   * [模式组合基础](../schema/composition.md)：XDM架构的构建块简介。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
* [沙盒](../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

在开始本教程之前，请查看 [开发人员指南](../api/getting-started.md) 如需了解成功调用 [!DNL Schema Registry] API。 这包括您的 `{TENANT_ID}`、“容器”的概念以及发出请求所需的标头(请特别注意 [!DNL Accept] 标头及其可能值)。

## 定义源和引用架构 {#define-schemas}

您应已创建将在关系中定义的两个架构。 本教程在组织当前的忠诚度计划(在“[!DNL Loyalty Members]”架构)和他们最喜爱的酒店(在“[!DNL Hotels]”架构)。

架构关系由表示 **源架构** 有一个字段引用中的另一个字段 **引用模式**. 在接下来的步骤中， ”[!DNL Loyalty Members]“ ”将是源架构，而“[!DNL Hotels]”将用作参考模式。

>[!IMPORTANT]
>
>为了建立关系，两个架构都必须定义主身份并启用 [!DNL Real-Time Customer Profile]. 请参阅以下部分： [启用架构以在配置文件中使用](./create-schema-api.md#profile) 模式创建教程中，如果您需要有关如何相应地配置模式的指导。

要定义两个架构之间的关系，您必须先获取 `$id` 两个架构的值。 如果您知道显示名称(`title`)，您可以找到它们的 `$id` 值，方法是向发出一个GET请求 `/tenant/schemas` 中的端点 [!DNL Schema Registry] API。

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
>此 [!DNL Accept] 标头 `application/vnd.adobe.xed-id+json` 仅返回生成的架构的标题、ID和版本。

**响应**

成功响应将返回由您的组织定义的架构列表，包括它们的 `name`， `$id`， `meta:altId`、和 `version`.

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

## 为源架构定义参考字段

在 [!DNL Schema Registry]，关系描述符的工作方式类似于关系数据库表中的外键：源架构中的字段用作对引用架构的主标识字段的引用。 如果您的源架构中没有用于此目的的字段，则可能需要使用新字段创建架构字段组，并将其添加到架构中。 此新字段必须具有 `type` 值 `string`.

>[!IMPORTANT]
>
>源架构不能使用其主标识作为引用字段。

在本教程中，参考模式»[!DNL Hotels]”包含 `hotelId` 用作架构主要标识的字段。 但是，源架构&quot;[!DNL Loyalty Members]”没有要用作引用的专用字段 `hotelId`，因此需要创建一个自定义字段组，才能向架构中添加新字段： `favoriteHotel`.

>[!NOTE]
>
>如果您的源架构已有计划用作参考字段的专用字段，则可以跳至上的步骤 [创建引用描述符](#reference-identity).

### 创建新字段组

要向架构添加新字段，必须首先在字段组中定义它。 您可以通过向以下对象发出POST请求来创建新的字段组： `/tenant/fieldgroups` 端点。

**API格式**

```http
POST /tenant/fieldgroups
```

**请求**

以下请求将创建一个添加字段的新字段组 `favoriteHotel` 下的字段 `_{TENANT_ID}` 添加到的任何架构的命名空间。

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

成功响应将返回新创建的字段组的详细信息。

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
| `$id` | 系统生成的只读新字段组的唯一标识符。 采用URI的形式。 |

{style="table-layout:auto"}

记录 `$id` 字段组的URI，将在将字段组添加到源架构的下一个步骤中使用。

### 将字段组添加到源架构

创建字段组后，您可以通过向以下对象发出PATCH请求来将其添加到源架构： `/tenant/schemas/{SCHEMA_ID}` 端点。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | URL编码 `$id` URI或 `meta:altId` 源架构的。 |

{style="table-layout:auto"}

**请求**

以下请求添加了&quot;[!DNL Favorite Hotel]”字段组添加到“[!DNL Loyalty Members]”架构。

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
| `path` | 将添加新资源的架构字段的路径。 将字段组添加到架构时，该值必须为“/allOf/ — ”。 |
| `value.$ref` | 此 `$id` 要添加的字段组的。 |

{style="table-layout:auto"}

**响应**

成功响应将返回已更新架构的详细信息，其中现在包含 `$ref` 添加字段组在其下的值 `allOf` 数组。

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

如果架构字段用作对关系中其他架构的引用，则必须应用引用身份描述符。 由于 `favoriteHotel` ”中的字段[!DNL Loyalty Members]”将指 `hotelId` ”中的字段[!DNL Hotels]“， `favoriteHotel` 必须为指定引用身份描述符。

通过对以下对象发出POST请求，为源架构创建引用描述符： `/tenant/descriptors` 端点。

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下请求为创建引用描述符 `favoriteHotel` 字段”[!DNL Loyalty Members]“。

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
| `@type` | 正在定义的描述符的类型。 对于引用描述符，该值必须为 `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | 此 `$id` 源架构的URL。 |
| `xdm:sourceVersion` | 源架构的版本号。 |
| `sourceProperty` | 源架构中用于引用引用架构主要标识的字段的路径。 |
| `xdm:identityNamespace` | 引用字段的身份命名空间。 此命名空间必须与引用架构的主要身份相同。 请参阅 [身份命名空间概述](../../identity-service/home.md) 了解更多信息。 |

{style="table-layout:auto"}

**响应**

成功响应将返回新创建的源字段的引用描述符的详细信息。

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

关系描述符在源架构和引用架构之间建立一对一的关系。 一旦为源架构中的相应字段定义了引用身份描述符，就可以通过向以下对象发出POST请求来创建新的关系描述符： `/tenant/descriptors` 端点。

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下请求使用&quot;[!DNL Loyalty Members]”作为源架构和“[!DNL Hotels]”作为引用架构。

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
| `@type` | 要创建的描述符的类型。 此 `@type` 关系描述符的值是 `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | 此 `$id` 源架构的URL。 |
| `xdm:sourceVersion` | 源架构的版本号。 |
| `xdm:sourceProperty` | 源架构中引用字段的路径。 |
| `xdm:destinationSchema` | 此 `$id` 引用架构的URL。 |
| `xdm:destinationVersion` | 引用架构的版本号。 |
| `xdm:destinationProperty` | 引用架构中主标识字段的路径。 |

{style="table-layout:auto"}

### 响应

成功响应将返回新创建的关系描述符的详细信息。

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

通过阅读本教程，您已成功创建了两个架构之间的一对一关系。 有关使用描述符的详细信息 [!DNL Schema Registry] API，请参见 [Schema Registry开发人员指南](../api/descriptors.md). 有关如何在UI中定义架构关系的步骤，请参阅关于的教程 [使用架构编辑器定义架构关系](relationship-ui.md).
