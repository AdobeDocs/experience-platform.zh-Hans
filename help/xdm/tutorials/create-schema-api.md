---
keywords: Experience Platform；主页；热门主题；API;XDM;XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；数据模型；模式注册表；模式注册表；模式；模式；模式；模式；模式；模式；创建
solution: Experience Platform
title: 使用模式注册表API创建模式
topic-legacy: tutorial
type: Tutorial
description: 本教程使用架构注册表API来指导您完成使用标准类编写架构的步骤。
exl-id: fa487a5f-d914-48f6-8d1b-001a60303f3d
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2422'
ht-degree: 1%

---

# 使用创建架构 [!DNL Schema Registry] API

的 [!DNL Schema Registry] 用于访问 [!DNL Schema Library] 在Adobe Experience Platform。 的 [!DNL Schema Library] 包含按Adobe提供给您的资源， [!DNL Experience Platform] 合作伙伴以及您使用其应用程序的供应商。 注册表提供了用户界面和RESTful API，所有可用库资源均可从中访问。

本教程使用 [!DNL Schema Registry] 用于指导您完成使用标准类构建架构的步骤的API。 如果您希望在 [!DNL Experience Platform], [模式编辑器教程](create-schema-ui.md) 提供了在架构编辑器中执行类似操作的分步说明。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM) System]](../home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
   * [架构组合的基础知识](../schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

在启动本教程之前，请查看 [开发人员指南](../api/getting-started.md) 以了解成功调用 [!DNL Schema Registry] API。 这包括您的 `{TENANT_ID}`、“容器”的概念以及发出请求所需的标头（请特别注意接受标头及其可能值）。

本教程将指导您完成构建忠诚度会员架构的步骤，该架构描述与零售忠诚度计划成员相关的数据。 开始之前，您可能希望预览 [完整的会员架构](#complete-schema) 中。

## 使用标准类撰写架构

可以将架构视为要摄取到中的数据的蓝图 [!DNL Experience Platform]. 每个架构都由一个类和一个或多个架构字段组组成。 换言之，您无需添加字段组即可定义架构，但在大多数情况下，至少需要使用一个字段组。

### 分配类

架构组合过程从选择类开始。 该类定义数据的关键行为方面（记录与时间系列），以及描述将要摄取的数据所需的最小字段。

您在本教程中创建的架构使用 [!DNL XDM Individual Profile] 类。 [!DNL XDM Individual Profile] 是由Adobe提供的用于定义记录行为的标准类。 有关行为的详细信息，请参阅 [架构组合基础知识](../schema/composition.md).

要分配类，需要进行API调用，以在租户容器中创建(POST)新架构。 此调用包括架构将实现的类。 每个架构只能实现一个类。

**API格式**

```http
POST /tenant/schemas
```

**请求**

请求必须包含 `allOf` 引用 `$id` 班上的。 此属性定义架构将实现的“基类”。 在本例中，基类是 [!DNL XDM Individual Profile] 类。 的 `$id` 的 [!DNL XDM Individual Profile] 类用作 `$ref` 字段 `allOf` 数组。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

成功的请求会返回HTTP响应状态201（已创建），其中包含包含新创建架构详细信息(包括 `$id`, `meta:altIt`和 `version`. 这些值是只读的，由 [!DNL Schema Registry].

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
    "imsOrg": "{ORG_ID}",
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

### 查找架构

要查看新创建的架构，请使用 `meta:altId` 或URL编码 `$id` 架构的URI。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

**响应**

响应格式取决于随请求发送的Accept标头。 尝试使用不同的接受标头，以了解哪个标头最符合您的需求。

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
    "imsOrg": "{ORG_ID}",
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

### 添加字段组 {#add-a-field-group}

现在，已创建并确认忠诚度会员架构，接下来可以向其添加字段组。

根据所选架构的类别，有不同的标准字段组可供使用。 每个字段组都包含 `intendedToExtend` 字段定义与该字段组兼容的类。

字段组定义了概念，如“name”或“address”，这些概念可在需要捕获相同信息的任何架构中重复使用。

**API格式**

```http
PATCH /tenant/schemas/{schema meta:altId or url encoded $id URI}
```

**请求**

此请求会更新(PATCH)忠诚度会员架构，以包含“profile-person-details”字段组中的字段。

通过添加“profile-person-details”字段组，忠诚度会员架构现在可捕获有关忠诚度计划成员的信息，如其名字、姓氏和生日。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/context/profile-person-details"}}
      ]'
```

**响应**

响应将显示 `meta:extends` 数组并包含 `$ref` 到 `allOf` 属性。

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
    "imsOrg": "{ORG_ID}",
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

### 添加其他字段组

现在，您可以通过重复使用其他字段组执行的步骤来添加其他标准字段组。

>[!TIP]
>
>值得查看所有可用的字段组，以熟悉每个字段中包含的字段。 您可以列出(GET)所有可与特定类一起使用的字段组，方法是对“global”和“tenant”容器中的每个容器执行请求，并仅返回那些“meta:interedToExtend”字段与您使用的类匹配的字段组。 在这种情况下， [!DNL XDM Individual Profile] 类，所以 [!DNL XDM Individual Profile] `$id` 使用：

```http
GET /global/fieldgroups?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
GET /tenant/fieldgroups?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
```

**API格式**

```http
PATCH /tenant/schemas/{schema meta:altId or url encoded $id URI}
```

**请求**

此请求会更新(PATCH)忠诚会员架构，以将“profile-personal-details”字段组中的字段包含在该架构中，并向该模式添加“home address”、“email address”和“home phone”字段。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"}}
      ]'  
```

**响应**

响应将显示 `meta:extends` 数组并包含 `$ref` 到 `allOf` 属性。

忠诚度会员架构现在应包含三个 `$ref` 值 `allOf` 数组：“profile”、“profile-person-details”和“profile-personal-details”，如下所示。

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
    "imsOrg": "{ORG_ID}",
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

### 定义新字段组

忠诚度会员架构需要捕获忠诚度计划特有的信息。 此信息未包含在任何标准字段组中。

的 [!DNL Schema Registry] 通过允许您在租户容器中定义自己的字段组，可以解决此问题。 这些字段组对您的组织是唯一的，IMS组织外的任何人都不可见或编辑。

要创建(POST)新字段组，您的请求必须包含 `meta:intendedToExtend` 包含 `$id` 对于与字段组兼容的基类，以及字段组将包含的属性。

任何自定义属性都必须嵌套在 `TENANT_ID` 以避免与其他字段组或字段发生冲突。

**API格式**

```http
POST /tenant/fieldgroups
```

**请求**

此请求将创建一个新字段组，该字段组具有一个“忠诚度”对象，其中包含四个特定于忠诚度计划的字段：“loyatyId”、“loyatyLevel”、“loyatyPoints”和“memberSince”。

```SHELL
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Loyalty Member Details",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Loyalty Program Field Group.",
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

成功的请求会返回HTTP响应状态201（已创建），其中包含新创建字段组的详细信息(包括 `$id`, `meta:altIt`和 `version`. 这些值是只读的，由 [!DNL Schema Registry].

```JSON
{
    "type": "object",
    "title": "Loyalty Member Details",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Loyalty Program Field Group.",
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
    "imsOrg": "{ORG_ID}",
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

### 将自定义字段组添加到架构

您现在可以按照 [添加标准字段组](#add-a-field-group) 将新创建的字段组添加到架构。

**API格式**

```http
PATCH /tenant/schemas/{schema meta:altId or url encoded $id URI}
```

**请求**

此请求会更新(PATCH)忠诚度会员架构，以包含新“忠诚度会员详细信息”字段组中的字段。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"}}
      ]'
```

**响应**

您可以看到字段组已成功添加，因为响应现在会在 `meta:extends` 数组并包含 `$ref` 到 `allOf` 属性。

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
    "imsOrg": "{ORG_ID}",
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

### 查看当前架构

您现在可以执行GET请求以查看当前架构，并查看添加的字段组对架构整体结构的贡献情况。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1'
```

**响应**

通过使用 `application/vnd.adobe.xed-full+json; version=1` 接受标头后，您可以看到显示所有属性的完整架构。 这些属性是类和字段组贡献的字段，这些字段组已用于组成架构。 在此示例响应中，单个属性属性已在空间上最小化。 您可以在 [附录](#appendix) 在本文档末尾。

在 `"properties"`，您可以看到 `_{TENANT_ID}` 添加自定义字段组时创建的命名空间。 在该命名空间中是“忠诚度”对象以及创建字段组时定义的字段。

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
    "imsOrg": "{ORG_ID}",
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

您创建的忠诚度字段组包含可能在其他架构中有用的特定忠诚度属性。 例如，数据可能会作为体验事件的一部分被摄取，或者由实现其他类的架构使用。 在这种情况下，将对象层次结构另存为数据类型是有意义的，以便在其他位置重用定义。

数据类型允许您定义对象层次结构一次，并在字段中引用它，就像任何其他标量类型的引用一样。

换言之，数据类型允许一致地使用多字段结构，比字段组更灵活，因为通过将它们添加为字段的“类型”，可以将它们包含在架构中的任意位置。

**API格式**

```http
POST /tenant/datatypes
```

**请求**

定义数据类型不需要 `meta:extends` 或 `meta:intendedToExtend` 字段，也无需嵌套字段以避免冲突。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

成功的请求会返回HTTP响应状态201（已创建），其中包含新创建数据类型的详细信息(包括 `$id`, `meta:altIt`和 `version`. 这些值是只读的，由 [!DNL Schema Registry].

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
    "imsOrg": "{ORG_ID}",
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

您可以使用已编码的URL执行查找(GET)请求 `$id` 用于直接查看新数据类型的URI。 请务必将 `version` 在您的接受标头中查找请求。

### 在架构中使用数据类型

现在，已创建“忠诚度详细信息”数据类型，接下来您可以更新(PATCH)您创建的字段组中的“忠诚度”字段，以引用数据类型，而不是之前所在的字段。

**API格式**

```http
PATCH /tenant/fieldgroups/{field group meta:altId or URL encoded $id URI}
```

**请求**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.bb118e507bb848fd85df68fedea70c62 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

响应现在包含引用(`$ref`)，而不是之前定义的字段。

```JSON
{
    "type": "object",
    "title": "Loyalty Member Details",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Loyalty Program Field Group.",
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
    "imsOrg": "{ORG_ID}",
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

执行GET请求以查找架构时，现在会在“properties/_{TENANT_ID}”下显示对数据类型的引用，如下所示：

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

架构用于将数据摄取到 [!DNL Experience Platform]. 此数据最终可跨多项服务使用，以创建单个统一视图。 为了帮助完成此过程，可将关键字段标记为“身份”，并且在摄取数据时，这些字段中的数据会插入该个人的“身份图”中。 然后，可以访问图形数据 [[!DNL Real-Time Customer Profile]](../../profile/home.md) 其他 [!DNL Experience Platform] 提供拼合的每个客户视图的服务。

通常标记为“身份”的字段包括：电子邮件地址，电话号码， [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hans)、CRM ID或其他唯一ID字段。

考虑特定于贵组织的任何唯一标识符，因为它们也可能是良好的标识字段。

标识描述符表示“sourceSchema”的“sourceProperty”是应视为“Identity”的唯一标识符。

有关使用描述符的更多信息，请参阅 [架构注册开发人员指南](../api/getting-started.md).

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下请求在“loyatyId”字段中定义标识描述符。 这说明 [!DNL Experience Platform] 要使用唯一忠诚度计划成员标识符（在本例中为成员的电子邮件地址）来帮助拼合有关个人的信息。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

>[!NOTE]
>
>您可以列出可用的“xdm:namespace”值，或使用 [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service). “xdm:property”的值可以是“xdm:code”或“xdm:id”，具体取决于使用的“xdm:namespace”。

**响应**

成功的响应会返回HTTP状态201（已创建），其中包含新创建描述符的详细信息(包括其 `@id`. 的 `@id` 是由 [!DNL Schema Registry] 和用于在API中引用描述符。

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

## 启用在中使用的架构 [!DNL Real-Time Customer Profile] {#profile}

通过将“union”标记添加到 `meta:immutableTags` 属性时，您可以启用会员架构以供使用 [!DNL Real-Time Customer Profile].

有关使用并集视图的更多信息，请参阅 [工会](../api/unions.md) 在 [!DNL Schema Registry] 开发人员指南。

### 添加“union”标记

要将架构包含在合并的并集视图中，必须将“并集”标记添加到 `meta:immutableTags` 架构的属性。 这可通过PATCH请求来更新架构并添加 `meta:immutableTags` 值为“union”的数组。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/meta:immutableTags", "value": ["union"]}
      ]'
```

**响应**

响应显示操作已成功执行，并且架构现在包含顶级属性， `meta:immutableTags`，这是一个包含值“union”的数组。

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
    "imsOrg": "{ORG_ID}",
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

### 在并集中列出架构

现在，您已成功将架构添加到 [!DNL XDM Individual Profile] 并集。 要查看属于同一并集的所有架构的列表，您可以使用查询参数执行GET请求以过滤响应。

使用 `property` 查询参数，您可以指定仅包含 `meta:immutableTags` 具有 `meta:class` 等于 `$id` 的 [!DNL XDM Individual Profile] 类。

**API格式**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

**请求**

以下示例请求返回属于 [!DNL XDM Individual Profile] 并集。

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应是一个经过筛选的架构列表，仅包含满足这两个要求的架构列表。 请记住，使用多个查询参数时，假定为AND关系。 列表响应的格式取决于请求中发送的Accept标头。

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

通过阅读本教程，您已使用标准字段组和您定义的字段组成功构建了架构。 您现在可以使用此架构创建数据集并将记录数据摄取到Adobe Experience Platform。

在本教程中创建的完整忠诚会员架构，位于以下附录中。 在查看架构时，您可以看到字段组对整体结构的贡献情况，以及哪些字段可用于数据摄取。

创建多个架构后，您可以使用关系描述符定义它们之间的关系。 请参阅教程 [定义两个架构之间的关系](relationship-api.md) 以了解更多信息。 有关如何在注册表中执行所有操作(GET、POST、PUT、PATCH和DELETE)的详细示例，请参阅 [架构注册开发人员指南](../api/getting-started.md) 使用API时。

## 附录 {#appendix}

以下信息补充了API教程。

## 完整的会员架构 {#complete-schema}

在本教程中，我们构建了一个架构来描述零售忠诚度计划的成员。

架构实现 [!DNL XDM Individual Profile] 类和组合多个字段组；使用标准“人员详细信息”和“个人详细信息”字段组，以及通过教程中定义的“忠诚度详细信息”字段组，引入有关忠诚度会员的信息。

以下显示了JSON格式的已完成会员架构：

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
    "imsOrg": "{ORG_ID}",
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
                            "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
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
                    "description": "The state, or province portion of the observation. The format follows the ISO 3166-2 (country and subdivision) standard.",
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
                        "denylist": "Deny List",
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
                        "denylist": "Deny List",
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
                        "denylist": "Deny List",
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
                        "denylist": "Deny List",
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
                        "denylist": "Deny List",
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
