---
keywords: Experience Platform；主页；热门主题；API;XDM;XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；数据模型；模式注册表；模式注册表；模式；模式；模式；模式；模式；模式；创建
solution: Experience Platform
title: 使用模式注册表API创建模式
type: Tutorial
description: 本教程使用架构注册表API来指导您完成使用标准类编写架构的步骤。
exl-id: fa487a5f-d914-48f6-8d1b-001a60303f3d
source-git-commit: 030874e91b88b18f7de0cc2d12200243b7ed1d31
workflow-type: tm+mt
source-wordcount: '2556'
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

在启动本教程之前，请查看 [开发人员指南](../api/getting-started.md) 以了解成功调用 [!DNL Schema Registry] API。 这包括您的 `{TENANT_ID}`、“容器”的概念以及发出请求所需的标头(请特别注意 `Accept` 标题及其可能值)。

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
  "$id": "https://ns.adobe.com/tenantId/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_tenantId.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673310304048,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "6d2ed8acd9c3b768a44de29e069fc6f71329d2550f708381d22fa8bf8c192366",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_tenantId"
}
```

### 查找架构

要查看新创建的架构，请使用 `meta:altId` 或URL编码 `$id` 架构的URI。

**API格式**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 的 `meta:altId` 或URL编码 `$id` 要查找的架构。 |

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

响应格式取决于 `Accept` 标头。 试试不同的 `Accept` 标题，以了解最符合您需求的标题。

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673310304048,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "6d2ed8acd9c3b768a44de29e069fc6f71329d2550f708381d22fa8bf8c192366",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:allFieldAccess": true
}
```

### 添加字段组 {#add-a-field-group}

现在，已创建并确认忠诚度会员架构，接下来可以向其添加字段组。

根据所选架构的类别，有不同的标准字段组可供使用。 每个字段组都包含 `intendedToExtend` 字段定义与该字段组兼容的类。

字段组定义了概念，如“name”或“address”，这些概念可在需要捕获相同信息的任何架构中重复使用。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 的 `meta:altId` 或URL编码 `$id` 要将字段组添加到的架构中。 |

**请求**

此请求会更新会员架构，以在 [[!UICONTROL 人口统计详细信息] 字段组](../field-groups/profile/demographic-details.md) (`profile-person-details`)。

通过添加 `profile-person-details` 字段组中，忠诚度成员架构现在可捕获忠诚度计划成员的人口统计信息，如其名字、姓氏和生日。

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
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.1",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673310912096,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "b480f28a35f356b237fc129e796074a3f33a7a67df273f6a8beaee1ec6465540",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:descriptorStatus": {
    "result": []
  }
}
```

### 添加更多字段组

忠诚度成员架构需要另外两个标准字段组，您可以通过使用其他字段组重复这些步骤来添加这些字段组。

>[!TIP]
>
>值得查看所有可用的字段组，以熟悉每个字段中包含的字段。 您可以列出(GET)所有可与特定类一起使用的字段组，方法是对“global”和“tenant”容器中的每个容器执行请求，并仅返回那些“meta:interedToExtend”字段与您使用的类匹配的字段组。 在这种情况下， [!DNL XDM Individual Profile] 类，所以 [!DNL XDM Individual Profile] `$id` 使用：
>
>
```http
>GET /global/fieldgroups?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
>GET /tenant/fieldgroups?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
>```

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 的 `meta:altId` 或URL编码 `$id` 正在更新的架构的子目录。 |

**请求**

此请求会更新忠诚度会员架构，以包含以下标准字段组中的字段：

* [[!UICONTROL 个人联系详细信息]](../field-groups/profile/personal-contact-details.md) (`profile-personal-details`):添加联系信息，如家庭地址、电子邮件地址和家庭电话。
* [[!UICONTROL 忠诚度详细信息]](../field-groups/profile/loyalty-details.md) (`profile-loyalty-details`):添加联系信息，如家庭地址、电子邮件地址和家庭电话。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"}},
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"}}
      ]'  
```

**响应**

响应会在 `meta:extends` 数组并包含 `$ref` 到 `allOf` 属性。

忠诚度会员架构现在应包含四个 `$ref` 值 `allOf` 数组： `profile`, `profile-person-details`, `profile-personal-details`和 `profile-loyalty-details` 如下所示。

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.2",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
    "https://ns.adobe.com/xdm/context/profile-personal-details",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
    "https://ns.adobe.com/xdm/context/profile-personal-details",
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673311559934,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "1de5ed1a07e3478719952f0a8c94d5e5390d5a9a998761adb4cf1989137fd6ea",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:descriptorStatus": {
    "result": []
  }
}
```

### 定义新字段组

而标准 [!UICONTROL 忠诚度详细信息] 字段组为架构提供了与忠诚度相关的有用字段，但任何标准字段组中都不包含其他忠诚度字段。

要添加这些字段，您可以在 `tenant` 容器。 这些字段组对您的组织是唯一的，并且组织外的任何人都不可见或无法编辑。

要创建(POST)新字段组，您的请求必须包含 `meta:intendedToExtend` 包含 `$id` 对于与字段组兼容的基类，以及字段组将包含的属性。

任何自定义属性都必须嵌套在 `TENANT_ID` 以避免与其他字段组或字段发生冲突。

**API格式**

```http
POST /tenant/fieldgroups
```

**请求**

此请求会创建一个新字段组，该字段组具有 `loyaltyTier` 包含特定于公司特定忠诚度计划的四个字段的对象： `id`, `effectiveDate`, `currentThreshold`和 `nextThreshold`.

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
        "title": "Loyalty Tier",
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "description": "Captures info about the current loyalty tier of a customer.",
        "definitions": {
          "loyaltyTier": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "loyaltyTier": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "title": "Loyalty Tier Identifier",
                        "type": "string",
                        "description": "Loyalty Tier Identifier."
                      },
                      "effectiveDate": {
                        "title": "Effective Date",
                        "type": "string",
                        "format": "date-time",
                        "description": "Date the member joined their current loyalty tier."
                      },
                      "currentThreshold": {
                        "title": "Current Point Threshold",
                        "type": "integer",
                        "description": "The minimum number of loyalty points the member must maintain to remain in the current tier."
                      },
                      "nextThreshold": {
                        "title": "Next Point Threshold",
                        "type": "integer",
                        "description": "The number of loyalty points the member must accrue to graduate to the next tier."
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
            "$ref": "#/definitions/loyaltyTier"
          }
        ]
      }'
```

**响应**

成功的请求会返回HTTP响应状态201（已创建），其中包含新创建字段组的详细信息(包括 `$id`, `meta:altIt`和 `version`. 这些值是只读的，由 [!DNL Schema Registry].

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:altId": "_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Loyalty Tier",
  "type": "object",
  "description": "Captures info about the current loyalty tier of a customer.",
  "definitions": {
    "loyaltyTier": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "loyaltyTier": {
              "type": "object",
              "properties": {
                "id": {
                  "title": "Loyalty Tier Identifier",
                  "type": "string",
                  "description": "Loyalty Tier Identifier.",
                  "meta:xdmType": "string"
                },
                "effectiveDate": {
                  "title": "Effective Date",
                  "type": "string",
                  "format": "date-time",
                  "description": "Date the member joined their current loyalty tier.",
                  "meta:xdmType": "date-time"
                },
                "currentThreshold": {
                  "title": "Current Point Threshold",
                  "type": "integer",
                  "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                  "meta:xdmType": "int"
                },
                "nextThreshold": {
                  "title": "Next Point Threshold",
                  "type": "integer",
                  "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                  "meta:xdmType": "int"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/loyaltyTier",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673313004645,
    "repo:lastModifiedDate": 1673313004645,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "98e5d48808f5a4d9655493777389568a2581cfce013351ab9e1595d82f698dd6",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

### 将自定义字段组添加到架构

您现在可以按照 [添加标准字段组](#add-a-field-group) 将新创建的字段组添加到架构。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 的 `meta:altId` 或URL编码 `$id` 模式。 |

**请求**

此请求会更新(PATCH)忠诚度会员架构，以包含新“忠诚度等级”字段组中的字段。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"}}
      ]'
```

**响应**

您可以看到字段组已成功添加，因为响应现在会在 `meta:extends` 数组并包含 `$ref` 到 `allOf` 属性。

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.3",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673313118938,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "6559b197a04bb3fda5bc80bf383a260cfbe32539d528f0139c5750711eebfba2",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:descriptorStatus": {
        "result": []
    }
}
```

### 查看当前架构

您现在可以执行GET请求以查看当前架构，并查看添加的字段组对架构整体结构的贡献情况。

**API格式**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 的 `meta:altId` 或URL编码 `$id` 模式。 |

**请求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1'
```

**响应**

通过使用 `application/vnd.adobe.xed-full+json; version=1` `Accept` 标题中，您可以看到显示所有属性的完整架构。 这些属性是类和字段组贡献的字段，这些字段组已用于组成架构。 在以下示例响应中，只显示最近添加的空格字段。 您可以在 [附录](#appendix) 在本文档末尾。

在 `"properties"`，您可以看到 `_{TENANT_ID}` 添加自定义字段组时创建的命名空间。 在该命名空间中， `loyaltyTier` 对象以及创建字段组时定义的字段。

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:altId": "_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Loyalty Tier",
  "type": "object",
  "description": "Captures info about the current loyalty tier of a customer.",
  "definitions": {
    "loyaltyTier": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "loyaltyTier": {
              "type": "object",
              "properties": {
                "id": {
                  "title": "Loyalty Tier Identifier",
                  "type": "string",
                  "description": "Loyalty Tier Identifier.",
                  "meta:xdmType": "string"
                },
                "effectiveDate": {
                  "title": "Effective Date",
                  "type": "string",
                  "format": "date-time",
                  "description": "Date the member joined their current loyalty tier.",
                  "meta:xdmType": "date-time"
                },
                "currentThreshold": {
                  "title": "Current Point Threshold",
                  "type": "integer",
                  "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                  "meta:xdmType": "int"
                },
                "nextThreshold": {
                  "title": "Next Point Threshold",
                  "type": "integer",
                  "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                  "meta:xdmType": "int"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/loyaltyTier",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673313004645,
    "repo:lastModifiedDate": 1673313004645,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "98e5d48808f5a4d9655493777389568a2581cfce013351ab9e1595d82f698dd6",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

### 创建数据类型

您创建的“忠诚度层”字段组包含可能在其他架构中有用的特定属性。 例如，数据可能会作为体验事件的一部分被摄取，或者由实现其他类的架构使用。 在这种情况下，将对象层次结构另存为数据类型是有意义的，以便在其他位置重用定义。

数据类型允许您定义对象层次结构一次，并在字段中引用它，就像任何其他标量类型的引用一样。

换言之，数据类型允许一致地使用多字段结构，比字段组更灵活，因为通过将它们添加为字段的“类型”，可以将它们包含在架构中的任意位置。

**API格式**

```http
POST /tenant/datatypes
```

**请求**

定义数据类型不需要 `meta:extends` 或 `meta:intendedToExtend` 字段和字段无需嵌套在租户ID下以避免冲突。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Loyalty Tier",
        "type": "object",
        "description": "Loyalty Tier data type",
        "definitions": {
          "loyaltyTier": {
            "type": "object",
            "properties": {
              "id": {
                "title": "Loyalty Tier Identifier",
                "type": "string",
                "description": "Loyalty Tier Identifier."
              },
              "effectiveDate": {
                "title": "Effective Date",
                "type": "string",
                "format": "date-time",
                "description": "Date the member joined their current loyalty tier."
              },
              "currentThreshold": {
                "title": "Current Point Threshold",
                "type": "integer",
                "description": "The minimum number of loyalty points the member must maintain to remain in the       current tier."
              },
              "nextThreshold": {
                "title": "Next Point Threshold",
                "type": "integer",
                "description": "The number of loyalty points the member must accrue to graduate to the next tier."
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/loyaltyTier"
          }
        ]
      }'
```

**响应**

成功的请求会返回HTTP响应状态201（已创建），其中包含新创建数据类型的详细信息(包括 `$id`, `meta:altIt`和 `version`. 这些值是只读的，由 [!DNL Schema Registry].

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
  "meta:altId": "_{TENANT_ID}.datatypes.c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Loyalty Tier",
  "type": "object",
  "description": "Loyalty Tier data type",
  "definitions": {
    "loyaltyTier": {
      "type": "object",
      "properties": {
        "id": {
          "title": "Loyalty Tier Identifier",
          "type": "string",
          "description": "Loyalty Tier Identifier.",
          "meta:xdmType": "string"
        },
        "effectiveDate": {
          "title": "Effective Date",
          "type": "string",
          "format": "date-time",
          "description": "Date the member joined their current loyalty tier.",
          "meta:xdmType": "date-time"
        },
        "currentThreshold": {
          "title": "Current Point Threshold",
          "type": "integer",
          "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
          "meta:xdmType": "int"
        },
        "nextThreshold": {
          "title": "Next Point Threshold",
          "type": "integer",
          "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
          "meta:xdmType": "int"
        }
      },
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/loyaltyTier",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673378256699,
    "repo:lastModifiedDate": 1673378256699,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "8afba84c0c9a68126a7a1389f8523a1112bdf4405badc6dcddbbb4a0e18f5cdb",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

您可以使用已编码的URL执行查找(GET)请求 `$id` 用于直接查看新数据类型的URI。 请务必将 `version` 在 `Accept` 查找请求的标头。

### 在架构中使用数据类型

现在，已创建忠诚度层数据类型，接下来您可以更新(PATCH) `loyaltyTier` 字段组中的字段，以引用数据类型来替换之前存在的字段。

**API格式**

```http
PATCH /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{FIELD_GROUP_ID}` | 的 `meta:altId` 或URL已编码 `$id` 要更新的字段组的列表。 |

**请求**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "replace",
          "path": "/definitions/loyaltyTier/properties/_{TENANT_ID}/properties",
          "value": {
            "loyaltyTier": {
              "title": "Loyalty Tier",
              "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
              "description": "Loyalty tier info"
            }
          }
        }
      ]'
```

**响应**

响应现在包含引用(`$ref`)到 `loyaltyTier` 对象，而不是之前定义的字段。

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:altId": "_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:resourceType": "mixins",
  "version": "1.1",
  "title": "Loyalty Tier",
  "type": "object",
  "description": "Captures info about the current loyalty tier of a customer.",
  "definitions": {
    "loyaltyTier": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "loyaltyTier": {
              "title": "Loyalty Tier",
              "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
              "description": "Loyalty tier info",
              "type": "object",
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/loyaltyTier",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673313004645,
    "repo:lastModifiedDate": 1673378970276,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "4df8fa56d00991590364606bb2e219e1ea8f5717a51c0e6ae57ca956830b6a27",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:descriptorStatus": {
    "result": []
  }
}
```

如果您立即执行GET请求以查找架构，则 `loyaltyTier` 属性显示对 `meta:referencedFrom`:

```JSON
"_{TENANT_ID}": {
  "type": "object",
  "meta:xdmType": "object",
  "properties": {
    "loyaltyTier": {
      "title": "Loyalty Tier",
      "description": "Loyalty tier info",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "id": {
          "title": "Loyalty Tier Identifier",
          "type": "string",
          "description": "Loyalty Tier Identifier.",
          "meta:xdmType": "string"
        },
        "effectiveDate": {
          "title": "Effective Date",
          "type": "string",
          "format": "date-time",
          "description": "Date the member joined their current loyalty tier.",
          "meta:xdmType": "date-time"
        },
        "currentThreshold": {
          "title": "Current Point Threshold",
          "type": "integer",
          "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
          "meta:xdmType": "int"
        },
        "nextThreshold": {
          "title": "Next Point Threshold",
          "type": "integer",
          "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
          "meta:xdmType": "int"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb"
    }
  }
}
```

### 定义标识描述符

架构用于将数据摄取到 [!DNL Experience Platform]. 此数据最终可跨多项服务使用，以创建单个统一视图。 为了帮助完成此过程，可将关键字段标记为“身份”，并且在摄取数据时，这些字段中的数据会插入该个人的“身份图”中。 然后，可以访问图形数据 [[!DNL Real-Time Customer Profile]](../../profile/home.md) 其他 [!DNL Experience Platform] 提供拼合的每个客户视图的服务。

通常标记为“身份”的字段包括：电子邮件地址，电话号码， [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hans)、CRM ID或其他唯一ID字段。 考虑特定于贵组织的任何唯一标识符，因为它们也可能是良好的标识字段。

身份描述符表示 `sourceProperty` 的 `sourceSchema` 是应视为标识的唯一标识符。

有关使用描述符的更多信息，请参阅 [架构注册开发人员指南](../api/getting-started.md).

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下请求在 `personalEmail.address` 字段。 这说明 [!DNL Experience Platform] 将忠诚会员的电子邮件地址用作标识符，以帮助拼合有关个人的信息。 此调用还会通过设置 `xdm:isPrimary` to `true`，这是 [启用架构以在实时客户资料中使用](#profile).

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
  "@id": "719a4391897c097786efbaa6d4262bb928a1cd88540344c6",
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "imsOrg": "{ORG_ID}",
  "version": "1",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": true,
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production"
}
```

## 启用在中使用的架构 [!DNL Real-Time Customer Profile] {#profile}

应用主标识描述符后，您可以启用会员架构以供使用 [!DNL Real-Time Customer Profile] 通过添加 `union` 标记 `meta:immutableTags` 属性。

>[!NOTE]
>
>有关使用并集视图的更多信息，请参阅 [工会](../api/unions.md) 在 [!DNL Schema Registry] 开发人员指南。

### 添加 `union` 标记

为了将架构包含在合并的并集视图中， `union` 标记必须添加到 `meta:immutableTags` 架构的属性。 这是通过PATCH请求来更新架构并添加 `meta:immutableTags` 值为 `union`.

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 的 `meta:altId` 或URL编码 `$id` 为“配置文件”启用的架构。 |

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
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.4",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
    "https://ns.adobe.com/xdm/context/profile-personal-details",
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
    "https://ns.adobe.com/xdm/context/profile-personal-details",
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673380280074,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "c590ccc7a293040d85c2b7d93276480ef4b4aa9a4fcd6991f50fbb47f58bced2",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:immutableTags": [
    "union"
  ],
  "meta:descriptorStatus": {
    "result": []
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

响应是一个经过筛选的架构列表，仅包含满足这两个要求的架构列表。 请记住，使用多个查询参数时，假定为AND关系。 列表响应的格式取决于 `Accept` 请求中发送的标头。

```JSON
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d29a200b5deb6cfb55d3b865ef627f33",
      "meta:altId": "_{TENANT_ID}.schemas.d29a200b5deb6cfb55d3b865ef627f33",
      "version": "1.2",
      "title": "Profile Schema"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/5d70026f5522fc60b3c81f6523b83c86",
      "meta:altId": "_{TENANT_ID}.schemas.5d70026f5522fc60b3c81f6523b83c86",
      "version": "1.3",
      "title": "CRM Onboarding"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/653e53eb04341d09453c9b6a5fb43d1b4ca9526ec274856d",
      "meta:altId": "_{TENANT_ID}.schemas.653e53eb04341d09453c9b6a5fb43d1b4ca9526ec274856d",
      "version": "1.1",
      "title": "Profile consents"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
      "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
      "version": "1.4",
      "title": "Loyalty Members"
    }
  ],
  "_page": {
    "orderby": "updated",
    "next": null,
    "count": 4
  },
  "_links": {
    "next": null,
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

架构实现 [!DNL XDM Individual Profile] 类和组合多个字段组。 它使用标准捕获有关忠诚会员的信息 [!DNL Demographic Details], [!UICONTROL 个人联系详细信息]和 [!UICONTROL 忠诚度详细信息] 字段组，以及通过在教程中定义的自定义忠诚度等级字段组。

以下显示了JSON格式的已完成会员架构：

+++查看完整架构

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.4",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "properties": {
    "_{TENANT_ID}": {
      "type": "object",
      "properties": {
        "loyaltyTier": {
          "title": "Loyalty Tier",
          "description": "Loyalty tier info",
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "id": {
              "title": "Loyalty Tier Identifier",
              "type": "string",
              "description": "Loyalty Tier Identifier.",
              "meta:xdmType": "string"
            },
            "effectiveDate": {
              "title": "Effective Date",
              "type": "string",
              "format": "date-time",
              "description": "Date the member joined their current loyalty tier.",
              "meta:xdmType": "date-time"
            },
            "currentThreshold": {
              "title": "Current Point Threshold",
              "type": "integer",
              "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
              "meta:xdmType": "int"
            },
            "nextThreshold": {
              "title": "Next Point Threshold",
              "type": "integer",
              "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
              "meta:xdmType": "int"
            }
          },
          "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb"
        }
      },
      "meta:xdmType": "object"
    },
    "_id": {
      "title": "Identifier",
      "type": "string",
      "format": "uri-reference",
      "description": "A unique identifier for the record.",
      "meta:xdmType": "string",
      "meta:xdmField": "@id"
    },
    "_repo": {
      "properties": {
        "createDate": {
          "type": "string",
          "format": "date-time",
          "meta:immutable": true,
          "meta:usereditable": false,
          "examples": [
            "2004-10-23T12:00:00-06:00"
          ],
          "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
          "meta:xdmType": "date-time",
          "meta:xdmField": "repo:createDate"
        },
        "modifyDate": {
          "type": "string",
          "format": "date-time",
          "meta:usereditable": false,
          "examples": [
            "2004-10-23T12:00:00-06:00"
          ],
          "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
          "meta:xdmType": "date-time",
          "meta:xdmField": "repo:modifyDate"
        }
      },
      "type": "object",
      "meta:xdmType": "object",
      "meta:xedConverted": true
    },
    "billingAddress": {
      "title": "Billing Address",
      "description": "Billing postal address.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_id": {
          "title": "Coordinates ID",
          "type": "string",
          "format": "uri-reference",
          "description": "The unique identifier of the coordinates.",
          "meta:xdmType": "string",
          "meta:xdmField": "@id"
        },
        "_repo": {
          "properties": {
            "createDate": {
              "type": "string",
              "format": "date-time",
              "meta:immutable": true,
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:createDate"
            },
            "modifyDate": {
              "type": "string",
              "format": "date-time",
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:modifyDate"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "_schema": {
          "properties": {
            "description": {
              "title": "Description",
              "type": "string",
              "description": "A description of what the coordinates identify.",
              "meta:xdmType": "string",
              "meta:xdmField": "schema:description"
            },
            "elevation": {
              "title": "Elevation",
              "type": "number",
              "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:elevation"
            },
            "latitude": {
              "title": "Latitude",
              "type": "number",
              "minimum": -90,
              "maximum": 90,
              "description": "The signed vertical coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:latitude"
            },
            "longitude": {
              "title": "Longitude",
              "type": "number",
              "minimum": -180,
              "maximum": 180,
              "description": "The signed horizontal coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:longitude"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "city": {
          "title": "City",
          "type": "string",
          "description": "The name of the city.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:city"
        },
        "country": {
          "title": "Country",
          "type": "string",
          "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:country"
        },
        "countryCode": {
          "title": "Country code",
          "type": "string",
          "pattern": "^[A-Z]{2}$",
          "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "createdByBatchID": {
          "title": "Created by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The dataset files in Catalog which has been originating the creation of the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:createdByBatchID"
        },
        "dmaID": {
          "title": "Designated market area",
          "type": "integer",
          "description": "The Nielsen media research designated market area.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:dmaID"
        },
        "label": {
          "title": "Label",
          "type": "string",
          "description": "Free form name of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:label"
        },
        "lastVerifiedDate": {
          "title": "Last verified date",
          "type": "string",
          "format": "date",
          "description": "The date that the address was last verified as still associated to the person.",
          "meta:xdmType": "date",
          "meta:xdmField": "xdm:lastVerifiedDate"
        },
        "modifiedByBatchID": {
          "title": "Modified by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:modifiedByBatchID"
        },
        "msaID": {
          "title": "Metropolitan statistical area",
          "type": "integer",
          "description": "The metropolitan statistical area in the United States where the observation occurred.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:msaID"
        },
        "postOfficeBox": {
          "title": "Post office box",
          "type": "string",
          "description": "Post office box of the address.",
          "maxLength": 20,
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postOfficeBox"
        },
        "postalCode": {
          "title": "Postal code",
          "type": "string",
          "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postalCode"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "region": {
          "title": "Region",
          "type": "string",
          "description": "The region, county, or district portion of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:region"
        },
        "repositoryCreatedBy": {
          "title": "Created by user identifier",
          "type": "string",
          "description": "User ID of who created the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryCreatedBy"
        },
        "repositoryLastModifiedBy": {
          "title": "Modified by user identifier",
          "type": "string",
          "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryLastModifiedBy"
        },
        "state": {
          "title": "State",
          "type": "string",
          "description": "The name of the State. This is a free-form field.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:state"
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
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:stateProvince"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the address.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "pending_verification": "Pending verification",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "street1": {
          "title": "Street 1",
          "type": "string",
          "description": "Primary street level information, apartment number, street number, and street name.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street1"
        },
        "street2": {
          "title": "Street 2",
          "type": "string",
          "description": "Optional street information second line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street2"
        },
        "street3": {
          "title": "Street 3",
          "type": "string",
          "description": "Optional street information third line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street3"
        },
        "street4": {
          "title": "Street 4",
          "type": "string",
          "description": "Optional street information fourth line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street4"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
      "meta:xdmField": "xdm:billingAddress"
    },
    "createdByBatchID": {
      "title": "Created by batch identifier",
      "type": "string",
      "format": "uri-reference",
      "description": "The dataset files in Catalog which has been originating the creation of the record.",
      "meta:xdmType": "string",
      "meta:xdmField": "xdm:createdByBatchID"
    },
    "faxPhone": {
      "title": "Fax Phone",
      "description": "Fax phone number.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "countryCode": {
          "title": "Country Calling Code",
          "type": "string",
          "description": "Country calling code (CC) as defined by E.164.",
          "minLength": 1,
          "maxLength": 3,
          "pattern": "^[0-9]{1,3}?$",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "extension": {
          "title": "Extension",
          "type": "string",
          "description": "The internal dialing number used to call from a private exchange, operator, or switchboard.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:extension"
        },
        "number": {
          "title": "Number",
          "type": "string",
          "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets '()', hyphens '-', or characters to indicate sub-dialing identifiers like extensions 'x' for example,  1-353(0)18391111 or +613 9403600x1234.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:number"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary phone number indicator. Unlike address or email address, there can be multiple primary phone numbers; one per communication channel. The communication channel is defined by the type: `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, and `fax`.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
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
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "validity": {
          "title": "Validity",
          "type": "string",
          "description": "A level of technical correctness of the phone number.",
          "meta:enum": {
            "consistent": "Consistent",
            "inconsistent": "Inconsistent",
            "incomplete": "Incomplete",
            "successfullyUsed": "Successfully used"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:validity"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
      "meta:xdmField": "xdm:faxPhone"
    },
    "homeAddress": {
      "title": "Home Address",
      "description": "A home postal address.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_id": {
          "title": "Coordinates ID",
          "type": "string",
          "format": "uri-reference",
          "description": "The unique identifier of the coordinates.",
          "meta:xdmType": "string",
          "meta:xdmField": "@id"
        },
        "_repo": {
          "properties": {
            "createDate": {
              "type": "string",
              "format": "date-time",
              "meta:immutable": true,
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:createDate"
            },
            "modifyDate": {
              "type": "string",
              "format": "date-time",
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:modifyDate"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "_schema": {
          "properties": {
            "description": {
              "title": "Description",
              "type": "string",
              "description": "A description of what the coordinates identify.",
              "meta:xdmType": "string",
              "meta:xdmField": "schema:description"
            },
            "elevation": {
              "title": "Elevation",
              "type": "number",
              "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:elevation"
            },
            "latitude": {
              "title": "Latitude",
              "type": "number",
              "minimum": -90,
              "maximum": 90,
              "description": "The signed vertical coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:latitude"
            },
            "longitude": {
              "title": "Longitude",
              "type": "number",
              "minimum": -180,
              "maximum": 180,
              "description": "The signed horizontal coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:longitude"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "city": {
          "title": "City",
          "type": "string",
          "description": "The name of the city.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:city"
        },
        "country": {
          "title": "Country",
          "type": "string",
          "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:country"
        },
        "countryCode": {
          "title": "Country code",
          "type": "string",
          "pattern": "^[A-Z]{2}$",
          "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "createdByBatchID": {
          "title": "Created by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The dataset files in Catalog which has been originating the creation of the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:createdByBatchID"
        },
        "dmaID": {
          "title": "Designated market area",
          "type": "integer",
          "description": "The Nielsen media research designated market area.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:dmaID"
        },
        "label": {
          "title": "Label",
          "type": "string",
          "description": "Free form name of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:label"
        },
        "lastVerifiedDate": {
          "title": "Last verified date",
          "type": "string",
          "format": "date",
          "description": "The date that the address was last verified as still associated to the person.",
          "meta:xdmType": "date",
          "meta:xdmField": "xdm:lastVerifiedDate"
        },
        "modifiedByBatchID": {
          "title": "Modified by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:modifiedByBatchID"
        },
        "msaID": {
          "title": "Metropolitan statistical area",
          "type": "integer",
          "description": "The metropolitan statistical area in the United States where the observation occurred.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:msaID"
        },
        "postOfficeBox": {
          "title": "Post office box",
          "type": "string",
          "description": "Post office box of the address.",
          "maxLength": 20,
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postOfficeBox"
        },
        "postalCode": {
          "title": "Postal code",
          "type": "string",
          "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postalCode"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "region": {
          "title": "Region",
          "type": "string",
          "description": "The region, county, or district portion of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:region"
        },
        "repositoryCreatedBy": {
          "title": "Created by user identifier",
          "type": "string",
          "description": "User ID of who created the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryCreatedBy"
        },
        "repositoryLastModifiedBy": {
          "title": "Modified by user identifier",
          "type": "string",
          "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryLastModifiedBy"
        },
        "state": {
          "title": "State",
          "type": "string",
          "description": "The name of the State. This is a free-form field.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:state"
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
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:stateProvince"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the address.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "pending_verification": "Pending verification",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "street1": {
          "title": "Street 1",
          "type": "string",
          "description": "Primary street level information, apartment number, street number, and street name.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street1"
        },
        "street2": {
          "title": "Street 2",
          "type": "string",
          "description": "Optional street information second line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street2"
        },
        "street3": {
          "title": "Street 3",
          "type": "string",
          "description": "Optional street information third line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street3"
        },
        "street4": {
          "title": "Street 4",
          "type": "string",
          "description": "Optional street information fourth line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street4"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
      "meta:xdmField": "xdm:homeAddress"
    },
    "homePhone": {
      "title": "Home Phone",
      "description": "Home phone number.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "countryCode": {
          "title": "Country Calling Code",
          "type": "string",
          "description": "Country calling code (CC) as defined by E.164.",
          "minLength": 1,
          "maxLength": 3,
          "pattern": "^[0-9]{1,3}?$",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "extension": {
          "title": "Extension",
          "type": "string",
          "description": "The internal dialing number used to call from a private exchange, operator, or switchboard.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:extension"
        },
        "number": {
          "title": "Number",
          "type": "string",
          "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets '()', hyphens '-', or characters to indicate sub-dialing identifiers like extensions 'x' for example,  1-353(0)18391111 or +613 9403600x1234.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:number"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary phone number indicator. Unlike address or email address, there can be multiple primary phone numbers; one per communication channel. The communication channel is defined by the type: `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, and `fax`.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
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
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "validity": {
          "title": "Validity",
          "type": "string",
          "description": "A level of technical correctness of the phone number.",
          "meta:enum": {
            "consistent": "Consistent",
            "inconsistent": "Inconsistent",
            "incomplete": "Incomplete",
            "successfullyUsed": "Successfully used"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:validity"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
      "meta:xdmField": "xdm:homePhone"
    },
    "loyalty": {
      "type": "object",
      "description": "Captures details related to the customer's loyalty rewards.",
      "properties": {
        "joinDate": {
          "title": "Program Join Date",
          "type": "string",
          "format": "date-time",
          "description": "Date which the visitor registered for the loyalty program.",
          "meta:xdmType": "date-time",
          "meta:xdmField": "xdm:joinDate"
        },
        "loyaltyID": {
          "title": "Program ID",
          "type": "array",
          "items": {
            "type": "string",
            "meta:xdmType": "string"
          },
          "description": "The loyalty program ID(s) associated with a specific user, if they are enrolled in the client's loyalty program.",
          "meta:xdmType": "array",
          "meta:xdmField": "xdm:loyaltyID"
        },
        "points": {
          "title": "Program Points Balance",
          "type": "number",
          "description": "Current balance of the loyalty points/awards in a visitor's loyalty account.",
          "meta:xdmType": "number",
          "meta:xdmField": "xdm:points"
        },
        "pointsExpiration": {
          "title": "Points Expiration",
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "pointsExpirationDate": {
                "type": "string",
                "format": "date-time",
                "description": "Date on which the given portion of the loyalty points expire.",
                "meta:xdmType": "date-time",
                "meta:xdmField": "xdm:pointsExpirationDate"
              },
              "pointsExpiring": {
                "title": "Points Expiring",
                "type": "number",
                "description": "Point balance expiring as of the associated expiration date.",
                "meta:xdmType": "number",
                "meta:xdmField": "xdm:pointsExpiring"
              }
            },
            "meta:xdmType": "object"
          },
          "meta:xdmType": "array",
          "meta:xdmField": "xdm:pointsExpiration"
        },
        "pointsRedeemed": {
          "title": "Points Redeemed",
          "type": "number",
          "description": "Amount of points applied toward a purchase or otherwise redeemed.",
          "meta:xdmType": "number",
          "meta:xdmField": "xdm:pointsRedeemed"
        },
        "program": {
          "title": "Program Name",
          "type": "string",
          "description": "This should define the loyalty progam in which a visitor is enrolled.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:program"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "Captures the visitor's loyalty progam status, such as active, disabled, or suspended.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "tier": {
          "title": "Tier",
          "type": "string",
          "description": "Captures the loyalty progam tier in which a visitor is enrolled.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:tier"
        },
        "upgradeDate": {
          "title": "Program Name",
          "type": "string",
          "description": "Date which the customer was upgraded to the next tier level.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:upgradeDate"
        }
      },
      "meta:xdmType": "object",
      "meta:xdmField": "xdm:loyalty"
    },
    "mailingAddress": {
      "title": "Mailing Address",
      "description": "Mailing postal address.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_id": {
          "title": "Coordinates ID",
          "type": "string",
          "format": "uri-reference",
          "description": "The unique identifier of the coordinates.",
          "meta:xdmType": "string",
          "meta:xdmField": "@id"
        },
        "_repo": {
          "properties": {
            "createDate": {
              "type": "string",
              "format": "date-time",
              "meta:immutable": true,
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:createDate"
            },
            "modifyDate": {
              "type": "string",
              "format": "date-time",
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:modifyDate"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "_schema": {
          "properties": {
            "description": {
              "title": "Description",
              "type": "string",
              "description": "A description of what the coordinates identify.",
              "meta:xdmType": "string",
              "meta:xdmField": "schema:description"
            },
            "elevation": {
              "title": "Elevation",
              "type": "number",
              "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:elevation"
            },
            "latitude": {
              "title": "Latitude",
              "type": "number",
              "minimum": -90,
              "maximum": 90,
              "description": "The signed vertical coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:latitude"
            },
            "longitude": {
              "title": "Longitude",
              "type": "number",
              "minimum": -180,
              "maximum": 180,
              "description": "The signed horizontal coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:longitude"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "city": {
          "title": "City",
          "type": "string",
          "description": "The name of the city.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:city"
        },
        "country": {
          "title": "Country",
          "type": "string",
          "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:country"
        },
        "countryCode": {
          "title": "Country code",
          "type": "string",
          "pattern": "^[A-Z]{2}$",
          "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "createdByBatchID": {
          "title": "Created by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The dataset files in Catalog which has been originating the creation of the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:createdByBatchID"
        },
        "dmaID": {
          "title": "Designated market area",
          "type": "integer",
          "description": "The Nielsen media research designated market area.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:dmaID"
        },
        "label": {
          "title": "Label",
          "type": "string",
          "description": "Free form name of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:label"
        },
        "lastVerifiedDate": {
          "title": "Last verified date",
          "type": "string",
          "format": "date",
          "description": "The date that the address was last verified as still associated to the person.",
          "meta:xdmType": "date",
          "meta:xdmField": "xdm:lastVerifiedDate"
        },
        "modifiedByBatchID": {
          "title": "Modified by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:modifiedByBatchID"
        },
        "msaID": {
          "title": "Metropolitan statistical area",
          "type": "integer",
          "description": "The metropolitan statistical area in the United States where the observation occurred.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:msaID"
        },
        "postOfficeBox": {
          "title": "Post office box",
          "type": "string",
          "description": "Post office box of the address.",
          "maxLength": 20,
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postOfficeBox"
        },
        "postalCode": {
          "title": "Postal code",
          "type": "string",
          "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postalCode"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "region": {
          "title": "Region",
          "type": "string",
          "description": "The region, county, or district portion of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:region"
        },
        "repositoryCreatedBy": {
          "title": "Created by user identifier",
          "type": "string",
          "description": "User ID of who created the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryCreatedBy"
        },
        "repositoryLastModifiedBy": {
          "title": "Modified by user identifier",
          "type": "string",
          "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryLastModifiedBy"
        },
        "state": {
          "title": "State",
          "type": "string",
          "description": "The name of the State. This is a free-form field.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:state"
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
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:stateProvince"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the address.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "pending_verification": "Pending verification",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "street1": {
          "title": "Street 1",
          "type": "string",
          "description": "Primary street level information, apartment number, street number, and street name.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street1"
        },
        "street2": {
          "title": "Street 2",
          "type": "string",
          "description": "Optional street information second line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street2"
        },
        "street3": {
          "title": "Street 3",
          "type": "string",
          "description": "Optional street information third line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street3"
        },
        "street4": {
          "title": "Street 4",
          "type": "string",
          "description": "Optional street information fourth line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street4"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
      "meta:xdmField": "xdm:mailingAddress"
    },
    "mobilePhone": {
      "title": "Mobile Phone",
      "description": "Mobile phone number.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "countryCode": {
          "title": "Country Calling Code",
          "type": "string",
          "description": "Country calling code (CC) as defined by E.164.",
          "minLength": 1,
          "maxLength": 3,
          "pattern": "^[0-9]{1,3}?$",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "extension": {
          "title": "Extension",
          "type": "string",
          "description": "The internal dialing number used to call from a private exchange, operator, or switchboard.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:extension"
        },
        "number": {
          "title": "Number",
          "type": "string",
          "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets '()', hyphens '-', or characters to indicate sub-dialing identifiers like extensions 'x' for example,  1-353(0)18391111 or +613 9403600x1234.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:number"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary phone number indicator. Unlike address or email address, there can be multiple primary phone numbers; one per communication channel. The communication channel is defined by the type: `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, and `fax`.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
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
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "validity": {
          "title": "Validity",
          "type": "string",
          "description": "A level of technical correctness of the phone number.",
          "meta:enum": {
            "consistent": "Consistent",
            "inconsistent": "Inconsistent",
            "incomplete": "Incomplete",
            "successfullyUsed": "Successfully used"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:validity"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
      "meta:xdmField": "xdm:mobilePhone"
    },
    "modifiedByBatchID": {
      "title": "Modified by batch identifier",
      "type": "string",
      "format": "uri-reference",
      "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
      "meta:xdmType": "string",
      "meta:xdmField": "xdm:modifiedByBatchID"
    },
    "person": {
      "title": "Person",
      "description": "An individual actor, contact, or owner.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "birthDate": {
          "title": "Birth date(YYYY-MM-DD)",
          "type": "string",
          "format": "date",
          "description": "The full date a person was born.",
          "meta:xdmType": "date",
          "meta:xdmField": "xdm:birthDate"
        },
        "birthDayAndMonth": {
          "title": "Birth date (MM-DD)",
          "type": "string",
          "pattern": "[0-1][0-9]-[0-9][0-9]",
          "description": "The day and month a person was born, in the format MM-DD. This field should be used when the day and month of a person's birth is known, but not the year.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:birthDayAndMonth"
        },
        "birthYear": {
          "title": "Birth year",
          "type": "integer",
          "description": "The year a person was born including the century, for example, 1983.  This field should be used when only the person's age is known, not the full birth date.",
          "minimum": 1,
          "maximum": 32767,
          "meta:xdmType": "short",
          "meta:xdmField": "xdm:birthYear"
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
            "non_specific": "Non-specific"
          },
          "description": "Gender identity of the person.\n",
          "default": "not_specified",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:gender"
        },
        "maritalStatus": {
          "title": "Marital Status",
          "type": "string",
          "enum": [
            "married",
            "single",
            "divorced",
            "widowed",
            "not_specified"
          ],
          "meta:enum": {
            "married": "Married",
            "single": "Single",
            "divorced": "Divorced",
            "widowed": "Widowed",
            "not_specified": "Not Specified"
          },
          "description": "Describes a person's relationship with a significant other.",
          "default": "not_specified",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:maritalStatus"
        },
        "name": {
          "title": "Full name",
          "description": "The person's full name.",
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "courtesyTitle": {
              "title": "Courtesy title",
              "type": "string",
              "description": "Normally an abbreviation of a persons title, honorific, or salutation. The `courtesyTitle` is used in front of full or last name in opening texts. For example, Mr. Miss. or Dr.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:courtesyTitle"
            },
            "firstName": {
              "title": "First name",
              "type": "string",
              "description": "The first segment of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the preferred personal or given name. The `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:firstName"
            },
            "fullName": {
              "title": "Full name",
              "type": "string",
              "description": "The full name of the person, in writing order most commonly accepted in the language of the name.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:fullName"
            },
            "lastName": {
              "title": "Last name",
              "type": "string",
              "description": "The last segment of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the inherited family name, surname, patronymic, or matronymic name. The `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:lastName"
            },
            "middleName": {
              "title": "Middle name",
              "type": "string",
              "description": "Middle, alternative, or additional names supplied between the first name and last name.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:middleName"
            },
            "suffix": {
              "title": "Suffix",
              "type": "string",
              "description": "A group of letters provided after a person's name to provide additional information. The `suffix` is used at the end of someones name. For example Jr., Sr., M.D., PhD, I, II, III, etc.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:suffix"
            }
          },
          "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person-name",
          "meta:xdmField": "xdm:name"
        },
        "nationality": {
          "title": "Nationality",
          "type": "string",
          "pattern": "^[A-Z]{2}$",
          "description": "The legal relationship between a person and their state represented using the ISO 3166-1 Alpha-2 code.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:nationality"
        },
        "taxId": {
          "title": "Tax ID",
          "type": "string",
          "description": "The Tax / Fiscal ID of the person, e.g. the TIN in the US or the CIF/NIF in Spain.",
          "meta:status": "deprecated",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:taxId"
        },
        "type": {
          "title": "Type",
          "type": "string",
          "description": "The type of individual in different business contexts like B2C.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:type"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person",
      "meta:xdmField": "xdm:person"
    },
    "personID": {
      "title": "Person ID",
      "description": "Unique identifier of Person/Profile fragment.",
      "type": "string",
      "meta:xdmType": "string",
      "meta:xdmField": "xdm:personID"
    },
    "personalEmail": {
      "title": "Personal Email",
      "description": "A personal email address.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "address": {
          "title": "Address",
          "type": "string",
          "format": "email",
          "description": "The technical address, for example, 'name@domain.com' as commonly defined in RFC2822 and subsequent standards.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:address",
          "minLength": 1
        },
        "label": {
          "title": "Label",
          "type": "string",
          "description": "Additional display information that maybe available, for example, Microsoft Outlook rich address controls display 'John Smith smithjr@company.uk', 'John Smith' part is data that would be placed in the label.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:label"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary email indicator. A profile can have only one `primary` email address at a given point of time.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the email address.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "pending_verification": "Pending verification",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "type": {
          "title": "Type",
          "type": "string",
          "description": "The way the account relates to the person for example 'work' or 'personal'.",
          "meta:enum": {
            "unknown": "Unknown",
            "personal": "Personal",
            "work": "Work",
            "education": "Education"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:type"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/context/emailaddress",
      "meta:xdmField": "xdm:personalEmail",
      "required": [
        "address"
      ]
    },
    "repositoryCreatedBy": {
      "title": "Created by user identifier",
      "type": "string",
      "description": "User ID of who created the record.",
      "meta:xdmType": "string",
      "meta:xdmField": "xdm:repositoryCreatedBy"
    },
    "repositoryLastModifiedBy": {
      "title": "Modified by user identifier",
      "type": "string",
      "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
      "meta:xdmType": "string",
      "meta:xdmField": "xdm:repositoryLastModifiedBy"
    },
    "shippingAddress": {
      "title": "Shipping Address",
      "description": "Shipping postal address.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_id": {
          "title": "Coordinates ID",
          "type": "string",
          "format": "uri-reference",
          "description": "The unique identifier of the coordinates.",
          "meta:xdmType": "string",
          "meta:xdmField": "@id"
        },
        "_repo": {
          "properties": {
            "createDate": {
              "type": "string",
              "format": "date-time",
              "meta:immutable": true,
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:createDate"
            },
            "modifyDate": {
              "type": "string",
              "format": "date-time",
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:modifyDate"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "_schema": {
          "properties": {
            "description": {
              "title": "Description",
              "type": "string",
              "description": "A description of what the coordinates identify.",
              "meta:xdmType": "string",
              "meta:xdmField": "schema:description"
            },
            "elevation": {
              "title": "Elevation",
              "type": "number",
              "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:elevation"
            },
            "latitude": {
              "title": "Latitude",
              "type": "number",
              "minimum": -90,
              "maximum": 90,
              "description": "The signed vertical coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:latitude"
            },
            "longitude": {
              "title": "Longitude",
              "type": "number",
              "minimum": -180,
              "maximum": 180,
              "description": "The signed horizontal coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:longitude"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "city": {
          "title": "City",
          "type": "string",
          "description": "The name of the city.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:city"
        },
        "country": {
          "title": "Country",
          "type": "string",
          "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:country"
        },
        "countryCode": {
          "title": "Country code",
          "type": "string",
          "pattern": "^[A-Z]{2}$",
          "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "createdByBatchID": {
          "title": "Created by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The dataset files in Catalog which has been originating the creation of the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:createdByBatchID"
        },
        "dmaID": {
          "title": "Designated market area",
          "type": "integer",
          "description": "The Nielsen media research designated market area.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:dmaID"
        },
        "label": {
          "title": "Label",
          "type": "string",
          "description": "Free form name of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:label"
        },
        "lastVerifiedDate": {
          "title": "Last verified date",
          "type": "string",
          "format": "date",
          "description": "The date that the address was last verified as still associated to the person.",
          "meta:xdmType": "date",
          "meta:xdmField": "xdm:lastVerifiedDate"
        },
        "modifiedByBatchID": {
          "title": "Modified by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:modifiedByBatchID"
        },
        "msaID": {
          "title": "Metropolitan statistical area",
          "type": "integer",
          "description": "The metropolitan statistical area in the United States where the observation occurred.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:msaID"
        },
        "postOfficeBox": {
          "title": "Post office box",
          "type": "string",
          "description": "Post office box of the address.",
          "maxLength": 20,
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postOfficeBox"
        },
        "postalCode": {
          "title": "Postal code",
          "type": "string",
          "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postalCode"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "region": {
          "title": "Region",
          "type": "string",
          "description": "The region, county, or district portion of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:region"
        },
        "repositoryCreatedBy": {
          "title": "Created by user identifier",
          "type": "string",
          "description": "User ID of who created the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryCreatedBy"
        },
        "repositoryLastModifiedBy": {
          "title": "Modified by user identifier",
          "type": "string",
          "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryLastModifiedBy"
        },
        "state": {
          "title": "State",
          "type": "string",
          "description": "The name of the State. This is a free-form field.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:state"
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
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:stateProvince"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the address.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "pending_verification": "Pending verification",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "street1": {
          "title": "Street 1",
          "type": "string",
          "description": "Primary street level information, apartment number, street number, and street name.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street1"
        },
        "street2": {
          "title": "Street 2",
          "type": "string",
          "description": "Optional street information second line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street2"
        },
        "street3": {
          "title": "Street 3",
          "type": "string",
          "description": "Optional street information third line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street3"
        },
        "street4": {
          "title": "Street 4",
          "type": "string",
          "description": "Optional street information fourth line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street4"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
      "meta:xdmField": "xdm:shippingAddress"
    }
  },
  "required": [
    "personalEmail"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
    "https://ns.adobe.com/xdm/context/profile-personal-details",
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673380280074,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "c590ccc7a293040d85c2b7d93276480ef4b4aa9a4fcd6991f50fbb47f58bced2",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:immutableTags": [
    "union"
  ],
  "meta:allFieldAccess": true
}
```

+++
