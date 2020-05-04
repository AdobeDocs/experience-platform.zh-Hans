---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用模式注册表API创建模式
topic: tutorials
translation-type: tm+mt
source-git-commit: 14cd3d17c7d9ba602d02925abddec9e0b246a8c8

---


# 使用模式注册表API创建模式

模式注册表用于访问Adobe Experience Platform中的模式库。 模式库包含Adobe、Experience Platform合作伙伴以及您所使用的应用程序供应商为您提供的资源。 注册表提供用户界面和RESTful API，可从中访问所有可用的库资源。

本教程使用模式注册表API指导您完成使用标准类构建模式的步骤。 如果您希望使用Experience Platform中的用户界面，模式编 [辑器教程将提供分步说明](create-schema-ui.md) ，以在模式编辑器中执行类似操作。

## 入门指南

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

* [体验数据模型(XDM)系统](../home.md): Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../schema/composition.md): 了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
* [实时客户用户档案](../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
* [沙箱](../../sandboxes/home.md): Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和改进数字体验应用程序。

在开始本教程之前，请查阅开 [发人员指南](../api/getting-started.md) ，了解成功调用模式注册表API所需了解的重要信息。 这包括您 `{TENANT_ID}`的、“容器”的概念以及发出请求所需的标题（特别要注意“接受”标题及其可能的值）。

本教程将逐步介绍如何编写一个“忠诚度会员”模式，该项目描述与零售忠诚度的成员相关的数据。 在开始之前，您可能希望预览附录 [中的完整“忠诚会员](#complete-schema) ”模式。

## 使用标准类编写模式

可以将模式视为您希望引入Experience Platform的数据的蓝图。 每个模式由一个类和零个或多个混音组成。 换句话说，您不必添加混音来定义模式，但在大多数情况下至少使用一个混音。

### 分配类

模式合成过程从选择类开始。 该类定义数据的关键行为方面（记录与时间序列）以及描述将要摄取的数据所需的最小字段。

您在本教程中进行的模式使用XDM单个用户档案类。 XDM个人用户档案是Adobe为定义记录行为提供的标准类。 有关行为的更多信息，请参 [阅模式合成基础](../schema/composition.md)。

要分配类，将进行API调用以在租户容器中创建(POST)新模式。 此调用包括模式将实现的类。 每个模式只能实现一个类。

**API格式**

```http
POST /tenant/schemas
```

**请求**

请求必须包含引 `allOf` 用类的属 `$id` 性的属性。 此属性定义模式将实现的“基类”。 在此示例中，基类是XDM Individual用户档案类。 XDM `$id` 单个用户档案类的值将用作以下数 `$ref` 组中的 `allOf` 字段值。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
  "type": "object",
  "title": "Loyalty Members",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile"
    }
  ]
}'
```

**响应**

成功的请求返回HTTP响应状态201（已创建），响应主体包含新创建模式的详细信息，包括 `$id`、 `meta:altIt`和 `version`。 这些值是只读的，由模式注册表指定。

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551836845496,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

### 查找模式

要视图新创建的模式，请使用模式的或URL编 `meta:altId` 码的URI执 `$id` 行查找(GET)请求。

**API格式**

```http
GET /tenant/schemas/{schema meta:altId or URL encoded $id URI}
```

**请求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F533ca5da28087c44344810891b0f03d9\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

**响应 **

响应格式取决于随请求一起发送的Accept头。 尝试使用不同的“接受”标题，看看哪个标题最适合您的需求。

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551836845496,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

### 添加混音 {#add-a-mixin}

现在已创建并确认“忠诚会员”模式，可以将混合添加到该客户中。

根据所选模式的类别，可使用的标准混音不同。 每个混音都包 `intendedToExtend` 含一个字段，该字段定义该混音与之兼容的类。

混合定义了“名称”或“地址”等概念，这些概念可在需要捕获相同信息的任何模式中重用。

**API格式**

```http
PATCH /tenant/schemas/{schema meta:altId or url encoded $id URI}
```

**请求**

此请求更新(PATCH)“忠诚会员”模式，以在“用户档案-人——详细信息”混合中包含字段。

通过添加“用户档案-人——细节”混音，忠诚度会员模式现在可以捕获有关忠诚度项目会员的信息，如其名字、姓氏和生日。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/context/profile-person-details"}}
      ]'
```

**响应**

该响应显示数组中新添加的 `meta:extends` 混音，并 `$ref` 在属性中包含混 `allOf` 音。

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551837227497,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

### 添加另一个混音

您现在可以使用另一个混音重复这些步骤，从而添加另一个标准混音。

>[!TIP] 值得查看所有可用的混音，以熟悉其中包含的字段。 您可以对“全局”和“租户”列表执行请求，只返回那些“meta:intededToExtend”字段与您所使用的类匹配的混合，从而容器(GET)可用于特定类的所有混合。 在这种情况下，它是XDM个人用户档案类，因此使用XDM个人用户档案 `$id` :

```http
GET /global/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
GET /tenant/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
```

**API格式**

```http
PATCH /tenant/schemas/{schema meta:altId or url encoded $id URI}
```

**请求**

此请求更新(PATCH)“忠诚会员”模式以在“用户档案-个人详细信息”混音中包含字段，并向模式添加“家庭地址”、“电子邮件地址”和“家庭电话”字段。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"}}
      ]'  
```

**响应**

该响应显示数组中新添加的 `meta:extends` 混音，并 `$ref` 在属性中包含混 `allOf` 音。

Loyalty Members模式现在应包含 `$ref` 数组中的三 `allOf` 个值： “用户档案”、“用户档案-个人——详细信息”和“用户档案-个人——详细信息”，如下所示。

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.2",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551837356241,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

### 定义新混音

忠诚度会员模式需要捕获忠诚度项目特有的信息。 此信息不包括在任何标准混音中。

模式注册表允许您在租户容器中定义自己的混合，从而说明这一点。 这些混合是您的组织特有的，IMS组织外的任何人都无法看到或编辑。

要创建(POST)新的混音，您的请求必须包含一个字 `meta:intendedToExtend` 段，其中 `$id` 包含混音与之兼容的基类以及混音将包含的属性。

任何自定义属性都必须嵌套在您的 `TENANT_ID` 下方，以避免与其他混音或字段发生冲突。

**API格式**

```http
POST /tenant/mixins
```

**请求**

此请求创建一个新的混音，该混音具有一个“loyalty”对象，其中包含四个特定于忠诚度的项目字段： “loyaltyId”、“loyaltyLevel”、“loyaltyPoints”和“memberSince”。

```SHELL
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Loyalty Member Details",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Loyalty Program Mixin.",
        "definitions": {
            "loyalty": {
              "properties": {
                "_{TENANT_ID}": {
                  "type":"object",
                  "properties": {
                    "loyalty": {
                      "type": "object",
                      "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier."
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "type": "string"
                        },
                        "loyaltyPoints": {
                            "title": "Loyalty Points",
                            "type": "integer",
                            "description": "Loyalty points total."
                        },
                        "memberSince": {
                            "title": "Member Since",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined the Loyalty Program."
                        }
                      }
                    }
                  }
                }
              }
            }
        },
        "allOf": [
            {
            "$ref": "#/definitions/loyalty"
            }
        ]
      }'
```

**响应**

成功的请求返回HTTP响应状态201（已创建），响应主体包含新创建的混合的详细信息，包括 `$id`、 `meta:altIt`和 `version`。 这些值是只读的，由模式注册表指定。

```JSON
{
    "type": "object",
    "title": "Loyalty Member Details",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Loyalty Program Mixin.",
    "definitions": {
        "loyalty": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "loyalty": {
                            "type": "object",
                            "properties": {
                                "loyaltyId": {
                                    "title": "Loyalty Identifier",
                                    "type": "string",
                                    "description": "Loyalty Identifier.",
                                    "meta:xdmType": "string"
                                },
                                "loyaltyLevel": {
                                    "title": "Loyalty Level",
                                    "type": "string",
                                    "meta:xdmType": "string"
                                },
                                "loyaltyPoints": {
                                    "title": "Loyalty Points",
                                    "type": "integer",
                                    "description": "Loyalty points total.",
                                    "meta:xdmType": "int"
                                },
                                "memberSince": {
                                    "title": "Member Since",
                                    "type": "string",
                                    "format": "date-time",
                                    "description": "Date the member joined the Loyalty Program.",
                                    "meta:xdmType": "date-time"
                                }
                            },
                            "meta:xdmType": "object"
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
            "$ref": "#/definitions/loyalty"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.mixins.bb118e507bb848fd85df68fedea70c62",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62",
    "version": "1.1",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1551838135803,
        "repo:lastModifiedDate": 1552078296885,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

### 将自定义混音添加到模式

您现在可以按照相同的步骤 [添加标准混音](#add-a-mixin) ，将新创建的混音添加到模式。

**API格式**

```http
PATCH /tenant/schemas/{schema meta:altId or url encoded $id URI}
```

**请求**

此请求更新(PATCH)“忠诚会员”模式，以在新的“忠诚会员详细信息”混合中包含字段。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"}}
      ]'
```

**响应**

您可以看到混音已成功添加，因为响应现在在数组中显示新添加的混 `meta:extends` 音，并 `$ref` 在属性中包含 `allOf` 混音。

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
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
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.3",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551838484129,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

### 视图当前模式

您现在可以执行GET请求来视图当前模式，并查看添加的混音对模式整体结构的贡献。

**API格式**

```http
GET /tenant/schemas/{schema meta:altId or URL encoded $id URI}
```

**请求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1'
```

**响应**

通过使用 `application/vnd.adobe.xed-full+json; version=1` Accept头，您可以看到显示所有属性的完整模式。 这些属性是类和混合所贡献的字段，它们已用于构成模式。 在此示例响应中，单个属性属性已最小化为空间。 您可以视图此文档末尾的附录中的完整模式, [包括](#appendix) 所有属性及其属性。

在下 `"properties"`面，您可以看 `_{TENANT_ID}` 到在添加自定义混音时创建的命名空间。 在该命名空间中是“loyalty”对象和创建混合时定义的字段。

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "properties": {
        "repositoryCreatedBy": {},
        "repositoryLastModifiedBy": {},
        "createdByBatchID": { },
        "modifiedByBatchID": {},
        "_repo": {},
        "identityMap": {},
        "_id": {},
        "timeSeriesEvents": {},
        "person": {},
        "homeAddress": {},
        "personalEmail": {},
        "homePhone": {},
        "mobilePhone": {},
        "faxPhone": {},
        "_{TENANT_ID}": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "loyalty": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "loyaltyPoints": {
                            "title": "Loyalty Points",
                            "type": "integer",
                            "description": "Loyalty points total.",
                            "meta:xdmType": "int"
                        },
                        "memberSince": {
                            "title": "Member Since",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined the Loyalty Program.",
                            "meta:xdmType": "date-time"
                        }
                    }
                }
            }
        }
    },
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.4",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551843052271,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

### 创建数据类型

您创建的忠诚度混合包含可能在其他模式有用的特定忠诚度属性。 例如，数据可能作为体验事件的一部分被摄取，或由实现不同类的模式使用。 在这种情况下，将对象层次结构另存为数据类型是有意义的，以便更轻松地在其他位置重用定义。

数据类型允许您定义对象层次结构一次，并像在任何其他标量类型中一样在字段中引用它。

换句话说，数据类型允许多字段结构的一致使用，比混音更灵活，因为通过将它们添加为字段的“类型”，它们可以包含在模式的任何位置。

**API格式**

```http
POST /tenant/datatypes
```

**请求**

定义数据类型不需要 `meta:extends` 或字 `meta:intendedToExtend` 段，也无需嵌套字段以避免冲突。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Loyalty Details",
        "type": "object",
        "description": "Loyalty Member Details data type",
        "definitions": {
            "loyalty": {
                "type": "object",
                "properties": {
                    "loyaltyId": {
                    "title": "Loyalty Identifier",
                    "type": "string",
                    "description": "Loyalty Identifier."
                    },
                    "loyaltyLevel": {
                    "title": "Loyalty Level",
                    "type": "string"
                    },
                    "loyaltyPoints": {
                    "title": "Loyalty Points",
                    "type": "integer",
                    "description": "Loyalty points total."
                    },
                    "memberSince": {
                    "title": "Member Since",
                    "type": "string",
                    "format": "date-time",
                    "description": "Date the member joined the Loyalty Program."
                    }
                }
            }
        },
        "allOf": [
            {
            "$ref": "#/definitions/loyalty"
            }
        ]
      }'
```

**响应**

成功的请求返回HTTP响应状态201（已创建），响应主体包含新创建的数据类型的详细信息，包括、 `$id`和 `meta:altIt`和 `version`。 这些值是只读的，由模式注册表指定。

```JSON
{
    "title": "Loyalty Details",
    "type": "object",
    "description": "Loyalty Member Details data type",
    "definitions": {
        "loyalty": {
            "properties": {
                "loyaltyId": {
                    "title": "Loyalty Identifier",
                    "type": "string",
                    "description": "Loyalty Identifier.",
                    "meta:xdmType": "string"
                },
                "loyaltyLevel": {
                    "title": "Loyalty Level",
                    "type": "string",
                    "meta:xdmType": "string"
                },
                "loyaltyPoints": {
                    "title": "Loyalty Points",
                    "type": "integer",
                    "description": "Loyalty points total.",
                    "meta:xdmType": "int"
                },
                "memberSince": {
                    "title": "Member Since",
                    "type": "string",
                    "format": "date-time",
                    "description": "Date the member joined the Loyalty Program.",
                    "meta:xdmType": "date-time"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/loyalty"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.datatypes.49b594dabe6bec545c8a6d1a0991a4dd",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
    "version": "1.0",
    "meta:resourceType": "datatypes",
    "meta:registryMetadata": {
        "repo:createDate": 1551840599469,
        "repo:lastModifiedDate": 1551840599469,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

您可以使用URL编码的URI执行查找(GET)请 `$id` 求，以直接视图新数据类型。 请务必在查找请 `version` 求的“接受”标题中包含该标题。

### 在模式中使用数据类型

现在已创建“忠诚度详细信息”数据类型，您可以更新(PATCH)您创建的混音中的“loyalty”字段，以引用数据类型代替之前所在的字段。

**API格式**

```http
PATCH /tenant/mixins/{mixin meta:altId or URL encoded $id URI}
```

**请求**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.bb118e507bb848fd85df68fedea70c62 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
      [
        {
            "op": "replace",
            "path": "/definitions/loyalty/properties/_{TENANT_ID}/properties",
            "value": {
                "loyalty": {
                    "title": "Loyalty",
                    "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
                    "description": "Loyalty Info"
                }
            }
        }
      ]'
```

**响应**

响应现在包括对“`$ref`loyalty”对象中数据类型的引用()，而不是之前定义的字段。

```JSON
{
    "type": "object",
    "title": "Loyalty Member Details",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Loyalty Program Mixin.",
    "definitions": {
        "loyalty": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "loyalty": {
                            "title": "Loyalty",
                            "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
                            "description": "Loyalty Info"
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
            "$ref": "#/definitions/loyalty"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.mixins.bb118e507bb848fd85df68fedea70c62",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62",
    "version": "1.2",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1551838135803,
        "repo:lastModifiedDate": 1552080570051,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

执行GET请求以查找模式，现在在“properties/_{TENANT_ID}”下显示对数据类型的引用，如下所示：

```JSON
"_{TENANT_ID}": {
    "type": "object",
    "meta:xdmType": "object",
    "properties": {
        "loyalty": {
            "title": "Loyalty",
            "description": "Loyalty Info",
            "type": "object",
            "meta:xdmType": "object",
            "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
            "properties": {
                "loyaltyId": {
                    "title": "Loyalty Identifier",
                    "type": "string",
                    "description": "Loyalty Identifier.",
                    "meta:xdmType": "string"
                },
                "loyaltyLevel": {
                    "title": "Loyalty Level",
                    "type": "string",
                    "meta:xdmType": "string"
                },
                "loyaltyPoints": {
                    "title": "Loyalty Points",
                    "type": "integer",
                    "description": "Loyalty points total.",
                    "meta:xdmType": "int"
                },
                "memberSince": {
                    "title": "Member Since",
                    "type": "string",
                    "format": "date-time",
                    "description": "Date the member joined the Loyalty Program.",
                    "meta:xdmType": "date-time"
                }
            }
        }
    }
}
```

### 定义标识描述符

模式用于将数据引入Experience Platform。 此视图最终可跨多个服务使用，以创建单一、统一的个人数据。 为帮助完成此过程，关键字段可标记为“身份”，在数据获取时，这些字段中的数据将插入到该个人的“身份图”中。 然后，实时客户用户档案和其 [他体验平台服务可以访问图形](../../profile/home.md) ，为每位客户提供一个拼接的视图。

通常标为“身份”的字段包括： 电子邮件地址、电 [话号码、Experience Cloud ID(ECID)](https://docs.adobe.com/content/help/zh-Hans/id-service/using/home.html)、CRM ID或其他唯一ID字段。

考虑您的组织特定的所有唯一标识符，因为它们可能也是良好的标识字段。

标识描述符表示“sourceSchema”的“sourceProperty”是应被视为“Identity”的唯一标识符。

有关使用描述符的详细信息，请参阅 [模式注册表开发人员指南](../api/getting-started.md)。

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下请求在“loyaltyId”字段上定义标识描述符。 这会告知Experience Platform使用唯一的忠诚度项目会员标识符（本例中为会员的电子邮件地址）来帮助拼凑有关个人的信息。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/_{TENANT_ID}/loyalty/loyaltyId",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

>[!NOTE] 您可以列表可用的“xdm:命名空间”值，或使用Identity Service API创建 [新值](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)。 “xdm:property”的值可以是“xdm:code”或“xdm:id”，具体取决于使用的“xdm:命名空间”。

**响应**

成功的响应返回HTTP状态201（已创建），响应主体包含新创建的描述符（包括其）的详细信息 `@id`。 该 `@id` 是由模式注册表分配的只读字段，用于在API中引用描述符。

```JSON
{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/loyalty/loyaltyId",
    "xdm:namespace": "Email",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": false,
    "meta:containerId": "tenant",
    "@id": "e52fc732507e5aa9d63d00caa838d3c9fd97aa56"
}
```

## 启用模式以用于实时客户用户档案

通过向属性添加“合并”标 `meta:immutableTags` 签，您可以启用“忠诚会员”模式供实时客户用户档案使用。

有关使用合并视图的详细信息，请参阅《模式注册表开 [发人](../api/unions.md) 员指南》中有关合并的部分。

### 添加“合并”标记

要将模式包含在合并合并视图中，必须将“合并”标记添加到模式 `meta:immutableTags` 的属性中。 这是通过PATCH请求完成的，该请求用于更新模式 `meta:immutableTags` 并添加值为“合并”的阵列。

**API格式**

```http
PATCH /tenant/schemas/{meta:altId or the url encoded $id URI}
```

**请求**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/meta:immutableTags", "value": ["union"]}
      ]'
```

**响应**

响应显示操作已成功执行，并且模式现在包含顶级属性 `meta:immutableTags`，该属性是包含值“合并”的数组。

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
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
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.4",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551843052271,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

### 列表模式

您现在已成功将模式添加到XDM单个用户档案合并。 为了查看属于同一合并的所有模式的列表，您可以使用查询参数来过滤响应，从而执行GET请求。

使用 `property` 查询参数，您可以指定只返回包含 `meta:immutableTags` 字段的模式, `meta:class` 该字段与XDM单 `$id` 个用户档案类的字段相等。

**API格式**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

**请求**

以下示例请求返回属于XDM单个模式合并的所有用户档案。

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应是筛选的模式列表，只包含满足这两个要求的响应。 请记住，使用多个查询参数时，会假定AND关系。 列表响应的格式取决于请求中发送的接受头。

```JSON
{
    "results": [
        {
            "title": "Loyalty Members",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
            "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
            "version": "1.4"
        },
        {
            "title": "Schema 2",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e7297a6ddfc7812ab3a7b504a1ab98da",
            "meta:altId": "_{TENANT_ID}.schemas.e7297a6ddfc7812ab3a7b504a1ab98da",
            "version": "1.5"
        },
        {
            "title": "Schema 3",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/50f960bb810e99a21737254866a477bf",
            "meta:altId": "_{TENANT_ID}.schemas.50f960bb810e99a21737254866a477bf",
            "version": "1.2"
        },
        {
            "title": "Schema 4",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/dfebb19b93827b70bbad006137812537",
            "meta:altId": "_{TENANT_ID}.schemas.dfebb19b93827b70bbad006137812537",
            "version": "1.7"
        }
    ],
    "_links": {
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile"
        }
    }
}
```

## 后续步骤

通过遵循本教程，您已成功地使用您定义的标准混音和混音合成模式。 您现在可以使用此模式创建数据集并将记录数据引入Adobe Experience Platform。

在本教程中创建的完整“忠诚会员”模式，可在以下附录中找到。 当您查看模式时，您可以了解混音对总体结构的贡献以及哪些字段可用于数据获取。

创建多个模式后，您可以使用关系描述符定义它们之间的关系。 有关详细信息， [请参阅定义两个模式之间关系](relationship-api.md) 的教程。 有关如何在注册表中执行所有操作（GET、POST、PUT、PATCH和DELETE）的详细示例，请在使用API时参阅 [模式注册表开发人员指南](../api/getting-started.md) 。

## 附录 {#appendix}

以下信息是对API教程的补充。

## 完整忠诚度会员模式 {#complete-schema}

在本教程中，将编写一个模式来描述零售忠诚度项目的成员。

模式实现了XDM个人用户档案类，并将多个混音组合； 使用标准“人员详细信息”和“个人详细信息”混音，以及通过教程中定义的“忠诚度详细信息”混音导入有关忠诚度会员的信息。

以下显示了JSON格式的完成的“忠诚会员”模式:

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "properties": {
        "repositoryCreatedBy": {
            "title": "Created by User Identifier",
            "type": "string",
            "description": "User id who has created the entity.",
            "meta:xdmField": "xdm:repositoryCreatedBy",
            "meta:xdmType": "string"
        },
        "repositoryLastModifiedBy": {
            "title": "Modified by User Identifier",
            "type": "string",
            "description": "User id who last modified the entity. At creation time, `modifiedByUser` is set as `createdByUser`.",
            "meta:xdmField": "xdm:repositoryLastModifiedBy",
            "meta:xdmType": "string"
        },
        "createdByBatchID": {
            "title": "Created by Batch Identifier",
            "type": "string",
            "format": "uri-reference",
            "description": "The Data Set Files in Catalog Services which has been originating the creation of the entity.",
            "meta:xdmField": "xdm:createdByBatchID",
            "meta:xdmType": "string"
        },
        "modifiedByBatchID": {
            "title": "Modified by Batch Identifier",
            "type": "string",
            "format": "uri-reference",
            "description": "The last Data Set Files in Catalog Services which has modified the entity. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
            "meta:xdmField": "xdm:modifiedByBatchID",
            "meta:xdmType": "string"
        },
        "_repo": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "createDate": {
                    "type": "string",
                    "format": "date-time",
                    "meta:immutable": true,
                    "meta:usereditable": false,
                    "examples": [
                        "2004-10-23T12:00:00-06:00"
                    ],
                    "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The Date Time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                    "meta:xdmField": "repo:createDate",
                    "meta:xdmType": "date-time"
                },
                "modifyDate": {
                    "type": "string",
                    "format": "date-time",
                    "meta:usereditable": false,
                    "examples": [
                        "2004-10-23T12:00:00-06:00"
                    ],
                    "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The Date Time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                    "meta:xdmField": "repo:modifyDate",
                    "meta:xdmType": "date-time"
                }
            }
        },
        "identityMap": {
            "type": "object",
            "meta:xdmType": "map",
            "meta:xdmField": "xdm:identityMap",
            "additionalProperties": {
                "type": "array",
                "meta:xdmType": "array",
                "items": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:referencedFrom": "https://ns.adobe.com/xdm/context/identityitem",
                    "properties": {
                        "id": {
                            "title": "Identifier",
                            "type": "string",
                            "description": "Identity of the consumer in the related namespace.",
                            "meta:xdmField": "xdm:id",
                            "meta:xdmType": "string"
                        },
                        "authenticatedState": {
                            "description": "The state this identity is authenticated as for this observed ExperienceEvent.",
                            "type": "string",
                            "default": "ambiguous",
                            "enum": [
                                "ambiguous",
                                "authenticated",
                                "loggedOut"
                            ],
                            "meta:enum": {
                                "ambiguous": "Ambiguous",
                                "authenticated": "User identified by a login or simular action that was valid at the time of the event observation.",
                                "loggedOut": "User was identified by a login action at some point of time previously, but is not currently logged in."
                            },
                            "meta:xdmField": "xdm:authenticatedState",
                            "meta:xdmType": "string"
                        },
                        "primary": {
                            "title": "Primary",
                            "type": "boolean",
                            "default": false,
                            "description": "Indicates this identity is the preferred identity. Is used as a hint to help systems better organize how identities are queried.",
                            "meta:xdmField": "xdm:primary",
                            "meta:xdmType": "boolean"
                        }
                    }
                }
            }
        },
        "_id": {
            "title": "Identifier",
            "type": "string",
            "format": "uri-reference",
            "description": "A unique identifier for the record.",
            "meta:xdmField": "@id",
            "meta:xdmType": "string"
        },
        "timeSeriesEvents": {
            "title": "Time-series Events",
            "description": "List of time-series based events that relate to schemas based on record.",
            "type": "array",
            "meta:xdmField": "xdm:timeSeriesEvents",
            "meta:xdmType": "array",
            "items": {
                "type": "object",
                "meta:xdmType": "object",
                "meta:referencedFrom": "https://ns.adobe.com/xdm/data/time-series",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "type": "string",
                        "format": "uri-reference",
                        "description": "A unique identifier for the time-series event.",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "timestamp": {
                        "title": "Timestamp",
                        "type": "string",
                        "format": "date-time",
                        "description": "The time when an event or observation occurred.",
                        "meta:xdmField": "xdm:timestamp",
                        "meta:xdmType": "date-time"
                    },
                    "eventType": {
                        "title": "Event Type",
                        "type": "string",
                        "description": "The primary event type for this timeseries record.",
                        "meta:enum": {
                            "advertising.completes": "Indicates if a timed media asset was watched to completion - this does not necessarily mean the viewer watched the whole video; viewer could have skipped ahead.",
                            "advertising.timePlayed": "Describes the amount of time spent by a user on a specific timed media asset.",
                            "advertising.federated": "Indicates if an experience event was created through data federation (data sharing between customers).",
                            "advertising.clicks": "Click(s) actions on an advertisement.",
                            "advertising.conversions": "A customer pre-defined action(s) which triggers an event for performance evaluation.",
                            "advertising.firstQuartiles": "A digital video ad has played through 25% of its duration at normal speed.",
                            "advertising.impressions": "Impression(s) of an advertisement to an end user with the potential of being viewed.",
                            "advertising.midpoints": "A digital video ad has played through 50% of its duration at normal speed.",
                            "advertising.starts": "A digital video ad has started playing.",
                            "advertising.thirdQuartiles": "A digital video ad has played through 75% of its duration at normal speed.",
                            "web.webpagedetails.pageViews": "View(s) of a webpage has occurred.",
                            "web.webinteraction.linkClicks": "Click of a web-link has occurred.",
                            "commerce.checkouts": "An action during a checkout process of a product list, there can be more than one checkout event if there are multiple steps in a checkout process. If there are multiple steps the event time information and referenced page or experience is used to identify the step individual events represent in order.",
                            "commerce.productListAdds": "Addition of a product to the product list. Example a product is added to a shopping cart.",
                            "commerce.productListOpens": "Initializations of a new product list. Example a shopping cart is created.",
                            "commerce.productListRemovals": "Removal(s) of a product entry from a product list. Example a product is removed from a shopping cart.",
                            "commerce.productListReopens": "A product list that was no longer accessible(abandoned) has been re-activated by the user. Example via a re-marketing activity.",
                            "commerce.productListViews": "View(s) of a product-list has occurred.",
                            "commerce.productViews": "View(s) of a product have occurred.",
                            "commerce.purchases": "An order has been accepted. Purchase is the only required action in a commerce conversion. Purchase must have a product list referenced.",
                            "commerce.saveForLaters": "Product list is saved for future use. Example a product wish list."
                        },
                        "meta:xdmField": "xdm:eventType",
                        "meta:xdmType": "string"
                    }
                }
            }
        },
        "person": {
            "title": "Person",
            "description": "An individual actor, contact, or owner.",
            "meta:xdmField": "xdm:person",
            "type": "object",
            "meta:xdmType": "object",
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person",
            "properties": {
                "name": {
                    "title": "Full name",
                    "description": "The person's full name",
                    "meta:xdmField": "xdm:name",
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person-name",
                    "properties": {
                        "firstName": {
                            "title": "First name",
                            "type": "string",
                            "description": "The first segment of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the preferred personal or given name.\n\nThe `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable.",
                            "meta:xdmField": "xdm:firstName",
                            "meta:xdmType": "string"
                        },
                        "lastName": {
                            "title": "Last name",
                            "type": "string",
                            "description": "The last segment of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the inherited family name, surname, patronymic, or matronymic name.\n\nThe `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable.",
                            "meta:xdmField": "xdm:lastName",
                            "meta:xdmType": "string"
                        },
                        "middleName": {
                            "title": "Middle name",
                            "type": "string",
                            "description": "Middle, alternative, or additional names supplied between the first name and last name.",
                            "meta:xdmField": "xdm:middleName",
                            "meta:xdmType": "string"
                        },
                        "courtesyTitle": {
                            "title": "Courtesy title",
                            "type": "string",
                            "description": "Normally an abbreviation of a persons *title*, *honorific*, or *salutation*.\nThe `courtesyTitle` is used in front of full or last name in opening texts.\ne.g Mr. Miss. or Dr J. Smith.\n",
                            "meta:xdmField": "xdm:courtesyTitle",
                            "meta:xdmType": "string"
                        },
                        "fullName": {
                            "title": "Full name",
                            "type": "string",
                            "description": "The full name of the person, in writing order most commonly accepted in the language of the name.",
                            "meta:xdmField": "xdm:fullName",
                            "meta:xdmType": "string"
                        }
                    }
                },
                "birthDate": {
                    "title": "Birth Date",
                    "type": "string",
                    "format": "date",
                    "description": "The full date a person was born.",
                    "meta:xdmField": "xdm:birthDate",
                    "meta:xdmType": "date"
                },
                "birthDayAndMonth": {
                    "title": "Birth Date",
                    "type": "string",
                    "pattern": "[0-1][0-9]-[0-9][0-9]",
                    "description": "The day and month a person was born, in the format MM-DD. This field should be used when the day and month of a person's birth is known, but not the year.",
                    "meta:xdmField": "xdm:birthDayAndMonth",
                    "meta:xdmType": "string"
                },
                "birthYear": {
                    "title": "Birth year",
                    "type": "integer",
                    "description": "The year a person was born including the century (yyyy, e.g 1983).  This field should be used when only the person's age is known, not the full birth date.",
                    "minimum": 1,
                    "maximum": 32767,
                    "meta:xdmField": "xdm:birthYear",
                    "meta:xdmType": "short"
                },
                "gender": {
                    "title": "Gender",
                    "type": "string",
                    "enum": [
                        "male",
                        "female",
                        "not_specified",
                        "non_specific"
                    ],
                    "meta:enum": {
                        "male": "Male",
                        "female": "Female",
                        "not_specified": "Not Specified",
                        "non_specific": "Nonspecific"
                    },
                    "description": "Gender identity of the person.\n",
                    "default": "not_specified",
                    "meta:xdmField": "xdm:gender",
                    "meta:xdmType": "string"
                },
                "repositoryCreatedBy": {
                    "title": "Created by User Identifier",
                    "type": "string",
                    "description": "User id who has created the entity.",
                    "meta:xdmField": "xdm:repositoryCreatedBy",
                    "meta:xdmType": "string"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by User Identifier",
                    "type": "string",
                    "description": "User id who last modified the entity. At creation time, `modifiedByUser` is set as `createdByUser`.",
                    "meta:xdmField": "xdm:repositoryLastModifiedBy",
                    "meta:xdmType": "string"
                },
                "createdByBatchID": {
                    "title": "Created by Batch Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The Data Set Files in Catalog Services which has been originating the creation of the entity.",
                    "meta:xdmField": "xdm:createdByBatchID",
                    "meta:xdmType": "string"
                },
                "modifiedByBatchID": {
                    "title": "Modified by Batch Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The last Data Set Files in Catalog Services which has modified the entity. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
                    "meta:xdmField": "xdm:modifiedByBatchID",
                    "meta:xdmType": "string"
                },
                "_repo": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:immutable": true,
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The Date Time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmField": "repo:createDate",
                            "meta:xdmType": "date-time"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The Date Time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmField": "repo:modifyDate",
                            "meta:xdmType": "date-time"
                        }
                    }
                }
            }
        },
        "homeAddress": {
            "title": "Home Address",
            "description": "A home postal address.",
            "meta:xdmField": "xdm:homeAddress",
            "type": "object",
            "meta:xdmType": "object",
            "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
            "properties": {
                "_id": {
                    "title": "Coordinates ID",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The unique identifier of the coordinates.",
                    "meta:xdmField": "@id",
                    "meta:xdmType": "string"
                },
                "_schema": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                        "description": {
                            "title": "Description",
                            "type": "string",
                            "description": "A description of what the coordinates identify.",
                            "meta:xdmField": "schema:description",
                            "meta:xdmType": "string"
                        },
                        "latitude": {
                            "title": "Latitude",
                            "type": "number",
                            "minimum": -90,
                            "maximum": 90,
                            "description": "The signed vertical coordinate of a geographic point.",
                            "meta:xdmField": "schema:latitude",
                            "meta:xdmType": "number"
                        },
                        "longitude": {
                            "title": "Longitude",
                            "type": "number",
                            "minimum": -180,
                            "maximum": 180,
                            "description": "The signed horizontal coordinate of a geographic point.",
                            "meta:xdmField": "schema:longitude",
                            "meta:xdmType": "number"
                        },
                        "elevation": {
                            "title": "Elevation",
                            "type": "number",
                            "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
                            "meta:xdmField": "schema:elevation",
                            "meta:xdmType": "number"
                        }
                    }
                },
                "countryCode": {
                    "title": "Country code",
                    "type": "string",
                    "pattern": "^[A-Z]{2}$",
                    "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
                    "meta:xdmField": "xdm:countryCode",
                    "meta:xdmType": "string"
                },
                "stateProvince": {
                    "title": "State or province",
                    "type": "string",
                    "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
                    "examples": [
                        "US-CA",
                        "DE-BB",
                        "JP-13"
                    ],
                    "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
                    "meta:xdmField": "xdm:stateProvince",
                    "meta:xdmType": "string"
                },
                "city": {
                    "title": "City",
                    "type": "string",
                    "description": "The name of the city.",
                    "meta:xdmField": "xdm:city",
                    "meta:xdmType": "string"
                },
                "postalCode": {
                    "title": "Postal code",
                    "type": "string",
                    "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
                    "meta:xdmField": "xdm:postalCode",
                    "meta:xdmType": "string"
                },
                "dmaID": {
                    "title": "Designated Market Area",
                    "type": "integer",
                    "description": "The Nielsen Media Research designated market area.",
                    "meta:xdmField": "xdm:dmaID",
                    "meta:xdmType": "int"
                },
                "msaID": {
                    "title": "Metropolitan Statistical Area",
                    "type": "integer",
                    "description": "The Metropolitan Statistical Area in the USA where the observation occurred.",
                    "meta:xdmField": "xdm:msaID",
                    "meta:xdmType": "int"
                },
                "repositoryCreatedBy": {
                    "title": "Created by User Identifier",
                    "type": "string",
                    "description": "User id who has created the entity.",
                    "meta:xdmField": "xdm:repositoryCreatedBy",
                    "meta:xdmType": "string"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by User Identifier",
                    "type": "string",
                    "description": "User id who last modified the entity. At creation time, `modifiedByUser` is set as `createdByUser`.",
                    "meta:xdmField": "xdm:repositoryLastModifiedBy",
                    "meta:xdmType": "string"
                },
                "createdByBatchID": {
                    "title": "Created by Batch Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The Data Set Files in Catalog Services which has been originating the creation of the entity.",
                    "meta:xdmField": "xdm:createdByBatchID",
                    "meta:xdmType": "string"
                },
                "modifiedByBatchID": {
                    "title": "Modified by Batch Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The last Data Set Files in Catalog Services which has modified the entity. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
                    "meta:xdmField": "xdm:modifiedByBatchID",
                    "meta:xdmType": "string"
                },
                "_repo": {
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:immutable": true,
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The Date Time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmField": "repo:createDate",
                            "meta:xdmType": "date-time"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The Date Time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmField": "repo:modifyDate",
                            "meta:xdmType": "date-time"
                        }
                    }
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary address indicator. A Profile can have only one `primary` address at a given point of time.\n",
                    "meta:xdmField": "xdm:primary",
                    "meta:xdmType": "boolean"
                },
                "label": {
                    "title": "Label",
                    "type": "string",
                    "description": "Free form name of the address.",
                    "meta:xdmField": "xdm:label",
                    "meta:xdmType": "string"
                },
                "street1": {
                    "title": "Street 1",
                    "type": "string",
                    "description": "Primary Street level information, apartment number, street number and street name.",
                    "meta:xdmField": "xdm:street1",
                    "meta:xdmType": "string"
                },
                "street2": {
                    "title": "Street 2",
                    "type": "string",
                    "description": "Optional street information second line.",
                    "meta:xdmField": "xdm:street2",
                    "meta:xdmType": "string"
                },
                "street3": {
                    "title": "Street 3",
                    "type": "string",
                    "description": "Optional street information third line.",
                    "meta:xdmField": "xdm:street3",
                    "meta:xdmType": "string"
                },
                "street4": {
                    "title": "Street 4",
                    "type": "string",
                    "description": "Optional street information fourth line.",
                    "meta:xdmField": "xdm:street4",
                    "meta:xdmType": "string"
                },
                "region": {
                    "title": "Region",
                    "type": "string",
                    "description": "The region, county, or district portion of the address.",
                    "meta:xdmField": "xdm:region",
                    "meta:xdmType": "string"
                },
                "postOfficeBox": {
                    "title": "Post Office Box",
                    "type": "string",
                    "description": "Post office box of the address.",
                    "maxLength": 20,
                    "meta:xdmField": "xdm:postOfficeBox",
                    "meta:xdmType": "string"
                },
                "country": {
                    "title": "Country",
                    "type": "string",
                    "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
                    "meta:xdmField": "xdm:country",
                    "meta:xdmType": "string"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the address.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "pending_verification": "Pending Verification",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmField": "xdm:status",
                    "meta:xdmType": "string"
                },
                "statusReason": {
                    "title": "Status Reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmField": "xdm:statusReason",
                    "meta:xdmType": "string"
                },
                "lastVerifiedDate": {
                    "title": "Last Verified Date",
                    "type": "string",
                    "format": "date",
                    "description": "The date that the address was last verified as still belonging to the person.",
                    "meta:xdmField": "xdm:lastVerifiedDate",
                    "meta:xdmType": "date"
                }
            }
        },
        "personalEmail": {
            "title": "Personal Email",
            "description": "A personal email address.",
            "meta:xdmField": "xdm:personalEmail",
            "type": "object",
            "meta:xdmType": "object",
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/emailaddress",
            "properties": {
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary email indicator.\n\nA Profile can have only one `primary` email address at a given point of time.\n",
                    "meta:xdmField": "xdm:primary",
                    "meta:xdmType": "boolean"
                },
                "address": {
                    "title": "Address",
                    "type": "string",
                    "format": "email",
                    "description": "The technical address, e.g 'name@domain.com' as commonly defined in RFC2822 and subsequent standards.",
                    "meta:xdmField": "xdm:address",
                    "meta:xdmType": "string"
                },
                "label": {
                    "title": "Label",
                    "type": "string",
                    "description": "Additional display information that maybe available, e.g MS Outlook rich address controls display 'John Smith smithjr@company.uk', the 'John Smith' part is data that would be placed in the label.",
                    "meta:xdmField": "xdm:label",
                    "meta:xdmType": "string"
                },
                "type": {
                    "title": "Type",
                    "type": "string",
                    "description": "The way the account relates to the person. e.g 'work' or 'personal'",
                    "meta:enum": {
                        "unknown": "Unknown",
                        "personal": "Personal",
                        "work": "Work",
                        "education": "Education"
                    },
                    "meta:xdmField": "xdm:type",
                    "meta:xdmType": "string"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the email address.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "pending_verification": "Pending Verification",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmField": "xdm:status",
                    "meta:xdmType": "string"
                },
                "statusReason": {
                    "title": "Status Reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmField": "xdm:statusReason",
                    "meta:xdmType": "string"
                }
            }
        },
        "homePhone": {
            "title": "Home Phone",
            "description": "Home phone number.",
            "meta:xdmField": "xdm:homePhone",
            "type": "object",
            "meta:xdmType": "object",
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
            "properties": {
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary phone number indicator.\n\nUnlike for Address or EmailAddress, there can be multiple primary phone numbers; one per communication channel.\nThe communication channel is defined by the type:\n\n* `textMessaging`: type = `mobile`\n* `phone`: type = `home` | `work` | `unknown`\n* `fax`: type = `fax`\n",
                    "meta:xdmField": "xdm:primary",
                    "meta:xdmType": "boolean"
                },
                "number": {
                    "title": "Number",
                    "type": "string",
                    "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets (), hyphens - or characters to indicate sub dialing identifiers like extensions x. E.g 1-353(0)18391111 or +613 9403600x1234.",
                    "meta:xdmField": "xdm:number",
                    "meta:xdmType": "string"
                },
                "extension": {
                    "title": "Extension",
                    "type": "string",
                    "description": "The internal dialing number used to call from a private exchange, operator or switchboard.",
                    "meta:xdmField": "xdm:extension",
                    "meta:xdmType": "string"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the phone number.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmField": "xdm:status",
                    "meta:xdmType": "string"
                },
                "statusReason": {
                    "title": "Status Reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmField": "xdm:statusReason",
                    "meta:xdmType": "string"
                },
                "validity": {
                    "title": "Validity",
                    "type": "string",
                    "description": "A level of technical correctness of the phone number.",
                    "meta:enum": {
                        "consistent": "Consistent",
                        "inconsistent": "Inconsistent",
                        "incomplete": "Incomplete",
                        "successfullyUsed": "Successfully Used"
                    },
                    "meta:xdmField": "xdm:validity",
                    "meta:xdmType": "string"
                }
            }
        },
        "mobilePhone": {
            "title": "Mobile Phone",
            "description": "Mobile phone number.",
            "meta:xdmField": "xdm:mobilePhone",
            "type": "object",
            "meta:xdmType": "object",
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
            "properties": {
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary phone number indicator.\n\nUnlike for Address or EmailAddress, there can be multiple primary phone numbers; one per communication channel.\nThe communication channel is defined by the type:\n\n* `textMessaging`: type = `mobile`\n* `phone`: type = `home` | `work` | `unknown`\n* `fax`: type = `fax`\n",
                    "meta:xdmField": "xdm:primary",
                    "meta:xdmType": "boolean"
                },
                "number": {
                    "title": "Number",
                    "type": "string",
                    "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets (), hyphens - or characters to indicate sub dialing identifiers like extensions x. E.g 1-353(0)18391111 or +613 9403600x1234.",
                    "meta:xdmField": "xdm:number",
                    "meta:xdmType": "string"
                },
                "extension": {
                    "title": "Extension",
                    "type": "string",
                    "description": "The internal dialing number used to call from a private exchange, operator or switchboard.",
                    "meta:xdmField": "xdm:extension",
                    "meta:xdmType": "string"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the phone number.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmField": "xdm:status",
                    "meta:xdmType": "string"
                },
                "statusReason": {
                    "title": "Status Reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmField": "xdm:statusReason",
                    "meta:xdmType": "string"
                },
                "validity": {
                    "title": "Validity",
                    "type": "string",
                    "description": "A level of technical correctness of the phone number.",
                    "meta:enum": {
                        "consistent": "Consistent",
                        "inconsistent": "Inconsistent",
                        "incomplete": "Incomplete",
                        "successfullyUsed": "Successfully Used"
                    },
                    "meta:xdmField": "xdm:validity",
                    "meta:xdmType": "string"
                }
            }
        },
        "faxPhone": {
            "title": "Fax Phone",
            "description": "Fax phone number.",
            "meta:xdmField": "xdm:faxPhone",
            "type": "object",
            "meta:xdmType": "object",
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
            "properties": {
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary phone number indicator.\n\nUnlike for Address or EmailAddress, there can be multiple primary phone numbers; one per communication channel.\nThe communication channel is defined by the type:\n\n* `textMessaging`: type = `mobile`\n* `phone`: type = `home` | `work` | `unknown`\n* `fax`: type = `fax`\n",
                    "meta:xdmField": "xdm:primary",
                    "meta:xdmType": "boolean"
                },
                "number": {
                    "title": "Number",
                    "type": "string",
                    "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets (), hyphens - or characters to indicate sub dialing identifiers like extensions x. E.g 1-353(0)18391111 or +613 9403600x1234.",
                    "meta:xdmField": "xdm:number",
                    "meta:xdmType": "string"
                },
                "extension": {
                    "title": "Extension",
                    "type": "string",
                    "description": "The internal dialing number used to call from a private exchange, operator or switchboard.",
                    "meta:xdmField": "xdm:extension",
                    "meta:xdmType": "string"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the phone number.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmField": "xdm:status",
                    "meta:xdmType": "string"
                },
                "statusReason": {
                    "title": "Status Reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmField": "xdm:statusReason",
                    "meta:xdmType": "string"
                },
                "validity": {
                    "title": "Validity",
                    "type": "string",
                    "description": "A level of technical correctness of the phone number.",
                    "meta:enum": {
                        "consistent": "Consistent",
                        "inconsistent": "Inconsistent",
                        "incomplete": "Incomplete",
                        "successfullyUsed": "Successfully Used"
                    },
                    "meta:xdmField": "xdm:validity",
                    "meta:xdmType": "string"
                }
            }
        },
        "_{TENANT_ID}": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "loyalty": {
                    "title": "Loyalty",
                    "description": "Loyalty Info",
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "loyaltyPoints": {
                            "title": "Loyalty Points",
                            "type": "integer",
                            "description": "Loyalty points total.",
                            "meta:xdmType": "int"
                        },
                        "memberSince": {
                            "title": "Member Since",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined the Loyalty Program.",
                            "meta:xdmType": "date-time"
                        }
                    }
                }
            }
        }
    },
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.4",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551843052271,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```
