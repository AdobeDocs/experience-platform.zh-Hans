---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 模式注册表API开发人员指南
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 0%

---


# 模式注册表API开发人员指南

模式注册表用于访问Adobe Experience Platform中的模式库，提供可从中访问所有可用库资源的用户界面和RESTful API。

使用模式注册表API，您可以执行基本的CRUD操作，以视图和管理Adobe Experience Platform内所有可用的模式和相关资源。 这包括由Adobe、Experience Platform合作伙伴以及您使用其应用程序的供应商定义的应用程序。 您还可以使用API调用为您的组织创建新模式和资源，以及视图和编辑您已定义的资源。

此开发人员指南提供帮助您使用模式注册表API进行开始的步骤。 然后，该指南提供了使用模式注册表执行键操作的示例API调用。

## 先决条件

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

* [体验数据模型(XDM)系统](../home.md): Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../schema/composition.md): 了解XDM模式的基本构件。
* [实时客户用户档案](../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
* [沙箱](../../sandboxes/home.md): Experience Platform提供虚拟沙箱，将单个平台实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

以下各节提供了成功调用模式注册表API所需了解的其他信息。

## 读取示例API调用

本指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用的章节。

## 收集所需标题的值

要调用平台API，您必须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* 授权： 承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源，包括属于模式注册表的资源，都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

对模式注册表的所有查找(GET)请求都需要附加的“接受”头，其值决定API返回的信息格式。 有关更多详 [细信息](#accept) ，请参阅下面的接受标题部分。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

* 内容类型： application/json

## 了解您的TENANT_ID {#know-your-tenant_id}

在本指南中，您将看到对的引用 `TENANT_ID`。 此ID用于确保您创建的资源命名正确且包含在IMS组织中。 如果您不知道自己的ID，可以通过执行以下GET请求来访问它：

**API格式**

```http
GET /stats
```

**请求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回有关贵组织使用模式注册表的信息。 这包括一 `tenantId` 个属性，其值是您的属 `TENANT_ID`性。

```JSON
{
  "imsOrg":"{IMS_ORG}",
  "tenantId":"{TENANT_ID}",
  "counts": {
    "schemas": 4,
    "mixins": 3,
    "datatypes": 1,
    "classes": 2,
    "unions": 0,
  },
  "recentlyCreatedResources": [ 
    {
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
      "meta:resourceType": "mixins",
      "meta:created": "Sat Feb 02 2019 00:24:30 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/5bdb5582be0c0f3ebfc1c603b705764f",
      "title": "Tenant Class",
      "description": "Tenant Defined Class",
      "meta:resourceType": "classes",
      "meta:created": "Fri Feb 01 2019 22:46:21 GMT+0000 (UTC)",
      "version": "1.0"
    } 
  ],
  "recentlyUpdatedResources": [
    {
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
      "meta:resourceType": "mixins",
      "meta:updated": "Sat Feb 02 2019 00:34:06 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "title": "Data Schema",
      "description": "Schema for Data Information",
      "meta:resourceType": "schemas",
      "meta:updated": "Fri Feb 01 2019 23:47:43 GMT+0000 (UTC)",
      "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab",
      "meta:classTitle": "Sample Class",
      "version": "1.1"
    }
 ],
 "classUsage": {
    "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "title": "Tenant Data Schema",
        "description": "Schema for tenant-specific data."
      }
    ],
    "https://ns.adobe.com/xdm/context/profile": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/3ac6499f0a43618bba6b138226ae3542",
        "title": "Simple Profile",
        "description": "A simple profile schema."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "title": "Program Schema",
        "description": "Schema for program-related data."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/4025a705890c6d4a4a06b16f8cf6f4ca",
        "title": "Sample Schema",
        "description": "A sample schema."
      }
    ]
  }
 }
```

* `tenantId`: IMS `TENANT_ID` 组织的价值。

## 了解 `CONTAINER_ID` {#container}

调用模式注册表API需要使用 `CONTAINER_ID`。 有两种容器可以对其进行API调用： 全 **局容器** 和租 **户容器**。

### 全球容器

全球容器包含所有标准Adobe和Experience Platform合作伙伴提供的类、混音、数据类型和模式。 您只能对全局列表执行容器和查找(GET)请求。

### 租户容器

不要与您的独特性混淆，租 `TENANT_ID`户容器包含由IMS组织定义的所有类、混合、数据类型、模式和描述符。 这是每个组织特有的，这意味着它们不会被其他IMS组织看到或管理。 您可以对您在租户容器中创建的资源执行所有CRUD操作(GET、POST、PUT、PATCH、DELETE)。

在租户容器中创建类、混音、模式或数据类型时，该类会保存到模式注册表，并为其分配一个 `$id` 包含您的URI `TENANT_ID`。 它 `$id` 在整个API中用于引用特定资源。 值的示 `$id` 例在下一节中提供。

## 模式识别 {#schema-identification}

模式以URI形 `$id` 式标识为属性，如：
* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

为使URI更适合REST,模式还在名为： `meta:altId`
* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

调用模式注册表API将支持URL编 `$id` 码的URI `meta:altId` 或（点记号格式）。 最佳实践是在对API进 `$id` 行REST调用时使用URL编码的URI，如：
* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## 接受标题 {#accept}

在模式注册表API中执行列表和查找(GET)操作时，需要一个“接受”标头来确定API返回的数据格式。 查找特定资源时，“接受”标题中还必须包含版本号。

下表列表兼容的Accept头值，包括版本号，以及API在使用时将返回的描述。

| 接受 | 描述 |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | 仅返回列表ID。 这最常用于列出资源。 |
| `application/vnd.adobe.xed+json` | 返回包含原始的完整JSON列表 `$ref` 模式 `allOf` 符。 这用于返回一列表完整资源。 |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | 包含和的 `$ref` 原始 `allOf`XDM 有标题和说明。 |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` 属性和已 `allOf` 解析。 有标题和说明。 |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | 包含和的 `$ref` 原始 `allOf`XDM 无标题或描述。 |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` 属性和已 `allOf` 解析。 无标题或描述。 |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` 属性和已 `allOf` 解析。 包含描述符。 |

>[!NOTE]
>
>如果仅 `major` 提供版本（例如1、2、3），注册表将返回最 `minor` 新版本(例如， .1、.2、.3)。

## XDM现场限制和最佳实践

模式的字段列在其对象 `properties` 中。 每个字段本身就是一个对象，包含用于描述和约束字段可包含的数据的属性。

有关在API中定义字段类型的更多信息，请参 [阅本指南](appendix.md) 的附录，包括代码示例和最常用数据类型的可选约束。

以下示例字段说明了格式正确的XDM字段，其中提供了有关命名约束和最佳实践的更多详细信息。 在定义包含相似属性的其他资源时，也可以应用这些做法。

```JSON
"fieldName": {
    "title": "Field Name",
    "type": "string",
    "format": "date-time",
    "examples": [
        "2004-10-23T12:00:00-06:00"
    ],
    "description": "Full sentence describing the field, using proper grammar and punctuation.",
}
```

* 字段对象的名称可能包含字母数字、短划线或下划线字符，但 **不能** 以下划线开始。
   * **正确：** `fieldName`, `field_name2`, `Field-Name``field-name_3`
   * **不正确：** `_fieldName`
* 字段对象的名称首选使用camelCase。 示例: `fieldName`
* 该字段应包含一个 `title`以标题大小写写写的字段。 示例: `Field Name`
* 该字段需要 `type`。
   * 定义某些类型可能需要可选 `format`。
   * 当需要特定格式化数据时，可 `examples` 以将其添加为数组。
   * 也可使用注册表中的任何数据类型来定义字段类型。 有关详细信息， [请参阅本指南](create-data-type.md) 中有关创建数据类型的部分。
* 本文 `description` 介绍了有关现场数据的现场和相关信息。 它应该用完整的句子写成，并有清晰的语言，这样任何访问模式的人都能够理解该领域的意图。

有关如何 [在API](appendix.md) 中定义字段类型的详细信息，请参阅附录。

## 后续步骤

此文档涵盖了调用模式注册表API所需的必备知识，包括必需的身份验证凭据。 您现在可以继续访问本开发人员指南中提供的示例调用，并按照其说明进行操作。 有关如何在API中制作模式的完整分步演练，请参阅以下教 [程](../tutorials/create-schema-api.md)。
