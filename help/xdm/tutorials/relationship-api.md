---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用模式注册表API定义两个模式之间的关系
topic: tutorials
translation-type: tm+mt
source-git-commit: 7e867ee12578f599c0c596decff126420a9aca01

---


# 使用模式注册表API定义两个模式之间的关系


了解客户之间的关系以及他们与不同渠道品牌之间的交互是Adobe Experience Platform的重要组成部分。 在体验数据模型(XDM)模式的结构中定义这些关系使您能够获得对客户数据的复杂洞察。

本文档提供了一个教程，用于定义组织使用模式注册表API定义的两个模式之间的一对一 [关系](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)。

## 入门指南

本教程需要对体验数据模型(XDM)和XDM系统有良好的了解。 在开始本教程之前，请查看以下文档：

* [体验平台中的XDM系统](../home.md):XDM及其在Experience Platform中实施的概述。
   * [模式合成的基础知识](../schema/composition.md):介绍XDM模式的构件。
* [实时客户用户档案](../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。
* [沙箱](../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

在开始本教程之前，请查看开 [发人员指南](../api/getting-started.md) ，了解成功调用模式注册表API所需了解的重要信息。 这包括您 `{TENANT_ID}`的“容器”概念以及发出请求所需的标题（特别注意“接受”标题及其可能的值）。

## 定义源和目标模式 {#define-schemas}

您应已创建将在关系中定义的两个模式。 本教程在组织的当前忠诚度项目(在“忠诚度会员”模式中定义)的成员与其喜爱的酒店(在“酒店”模式中定义)之间建立了关系。

模式关系由具有引 **用目标模式内的其他字段的** 源模式 **表示**。 在接下来的步骤中，“忠诚会员”将作为源模式，而“酒店”将作为目的地模式。

要定义两个模式之间的关系，您必须首先获取两个模式 `$id` 的值。 如果您知道模式的显示名称(`title`)，则可以通过向注册表API中的端点发出GET请求来查 `$id``/tenant/schemas` 找这些模式的值。

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

>[!NOTE] “接受” `application/vnd.adobe.xed-id+json` 标题仅返回所生成模式的标题、ID和版本。

**响应**

成功的响应会返回由您的组织定义的一列表模式, `name`包括 `$id`其、 `meta:altId`和 `version`。

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

记录 `$id` 要定义之间关系的两个模式的值。 这些值将用于后续步骤。

## 定义两个模式的引用字段

在模式注册表中，关系描述符的工作方式与SQL表中的外键类似：源模式中的字段用作对目标模式的字段的引用。 定义关系时，每个模式必须有一个专用字段作为对其他模式的引用。

>[!IMPORTANT] 如果要启用模式以在实时客户 [用户档案中使用](../../profile/home.md)，则目标模式的引用字段必须是其主要 **标识**。 本教程的稍后部分将对此进行更详细的说明。

如果任一模式没有用于此目的的字段，您可能需要使用新字段创建混音并将其添加到模式。 此新字段的值必 `type` 须为“string”。

就本教程而言，目标模式“酒店”已包含一个用于此目的的字段： `hotelId`. 但是，源模式“忠诚会员”没有此字段，并且必须给予新混音，以在其命名空间下添加 `favoriteHotel`新字 `TENANT_ID` 段。

### 创建新混音

要向模式添加新字段，必须首先在混音中定义该字段。 您可以通过向端点发出POST请求来创建新混音 `/tenant/mixins` 符。

**API格式**

```http
POST /tenant/mixins
```

**请求**

以下请求将创建一个新的混音，该混音 `favoriteHotel` 在它添加到的 `TENANT_ID` 任何模式的命名空间下添加字段。

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

记录 `$id` mixin的URI，以在将mixin添加到源模式的下一步中使用。

### 将混音添加到源模式

创建混音后，可以通过向端点发出PATCH请求将其添加到源模式 `/tenant/schemas/{SCHEMA_ID}` 中。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | URL编码的 `$id` URI或 `meta:altId` 源模式的URI。 |

**请求**

以下请求将“Favorite Hotel”混音添加到“Loyalty Members”模式。

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
| `path` | 添加新资源的模式字段的路径。 向模式添加混音时，值必须为 `/allOf/-`。 |
| `value.$ref` | 要 `$id` 添加的混音的范围。 |

**响应**

成功的响应会返回更新的模式的详细信息，该详细信息现在包括其 `$ref` 数组下添加的混音的 `allOf` 值。

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

## 为两个模式定义主标识字段

>[!NOTE] 此步骤仅对启用在实时客户模式中 [的用户档案是必需的](../../profile/home.md)。 如果您不希望任何模式参与合并，或者如果您的模式已定义主标识，则可以跳到为目标模式创建引用标识描述符的下 [一步](#create-descriptor) 。

要使模式能够在实时客户用户档案中使用，他们必须定义主要标识。 此外，关系的目标模式必须使用其主要标识作为其引用字段。

就本教程而言，源模式已定义主标识，但目标模式没有。 可以通过创建标识描述符将模式字段标记为主标识字段。 这是通过向端点发出POST请求来完 `/tenant/descriptors` 成的。

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下请求创建了一个新的标识描述符，该描述符将目标模式“ `hotelId` Hotels”的字段定义为主标识字段。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:namespace": "ECID",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true
  }'
```

| 参数 | 描述 |
| --- | --- |
| `@type` | 要创建的描述符的类型。 标识 `@type` 描述符的值是 `xdm:descriptorIdentity`。 |
| `xdm:sourceSchema` | 目标 `$id` 模式的值，在上一步中获 [得](#define-schemas)。 |
| `xdm:sourceVersion` | 模式的版本号。 |
| `sourceProperty` | 将用作模式主标识的特定字段的路径。 此路径应以“/”开头，而不以“/”结尾，同时也排除任何“属性”命名空间。 例如，上述请求使 `/_{TENANT_ID}/hotelId` 用代替 `/properties/_{TENANT_ID}/properties/hotelId`。 |
| `xdm:namespace` | 标识字段的标识命名空间。 `hotelId` 是本例中的ECID值，因此使用“ECID”命名空间。 有关可 [用命名空间的列表](../../identity-service/home.md) ，请参阅标识命名空间概述。 |
| `xdm:isPrimary` | 一个布尔属性，用于确定标识字段是否将是模式的主要标识。 由于此请求定义主标识，因此值设置为true。 |

**响应**

成功的响应会返回新创建的标识描述符的详细信息。

```json
{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:namespace": "ECID",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true,
    "meta:containerId": "tenant",
    "@id": "e3cfa302d06dc27080e6b54663511a02dd61316f"
}
```

## 创建引用标识描述符

如果模式字段用作关系中其他模式的引用，则必须对它们应用引用标识描述符。 由于“ `favoriteHotel` 忠诚会员”中的字段将引用“酒店” `hotelId` 中的字段，因此必须为 `hotelId` 该字段提供引用标识描述符。

通过向端点发出POST请求，为目标模式创建引用描述 `/tenant/descriptors` 符。

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下请求为目标模式“Hotels”中的 `hotelId` 字段创建引用描述符。

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
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "ECID"
  }'
```

| 参数 | 描述 |
| --- | --- |
| `xdm:sourceSchema` | 目 `$id` 标模式的URL。 |
| `xdm:sourceVersion` | 目标模式的版本号。 |
| `sourceProperty` | 目标模式的主标识字段的路径。 |
| `xdm:identityNamespace` | 引用字段的标识命名空间。 `hotelId` 是本例中的ECID值，因此使用“ECID”命名空间。 有关可 [用命名空间的列表](../../identity-service/home.md) ，请参阅标识命名空间概述。 |

**响应**

成功的响应会返回新创建的目标模式引用描述符的详细信息。

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "ECID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## 创建关系描述符 {#create-descriptor}

关系描述符建立源模式和目标模式之间的一对一关系。 可以通过向端点发出POST请求来创建新的关系描述 `/tenant/descriptors` 符。

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下请求将创建一个新的关系描述符，其中“忠诚会员”作为源模式,“传统忠诚会员”作为目标模式。

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
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId"
  }'
```

| 参数 | 描述 |
| --- | --- |
| `@type` | 要创建的描述符的类型。 关系 `@type` 描述符的值为 `xdm:descriptorOneToOne`。 |
| `xdm:sourceSchema` | 源 `$id` 模式的URL。 |
| `xdm:sourceVersion` | 源模式的版本号。 |
| `sourceProperty`： | 源模式中引用字段的路径。 |
| `xdm:destinationSchema` | 目 `$id` 标模式的URL。 |
| `xdm:destinationVersion` | 目标模式的版本号。 |
| `destinationProperty`： | 目标模式中引用字段的路径。 |

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

通过遵循本教程，您成功地创建了两个模式之间的一对一关系。 有关使用模式注册表API使用描述符的详细信息，请参阅《模式注册 [表开发人员指南》](../api/getting-started.md)。 有关如何在UI中定义模式关系的步骤，请参阅有关使用模式编 [辑器定义模式关系的教程](relationship-ui.md)。