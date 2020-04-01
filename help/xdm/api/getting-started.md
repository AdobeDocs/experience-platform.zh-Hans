---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 模式注册API开发人员指南
topic: developer guide
translation-type: tm+mt
source-git-commit: eec5b07427aa9daa44d23f09cfaf1b38f8e811f3

---


# 模式注册API开发人员指南

模式注册表用于访问Adobe Experience Platform中的模式库，提供可从中访问所有可用库资源的用户界面和RESTful API。

使用模式注册表API，您可以执行基本的CRUD操作，以便在Adobe Experience Platform中视图和管理所有可用的模式和相关资源。 这包括由Adobe、Experience Platform合作伙伴以及您使用其应用程序的供应商定义的应用程序。 您还可以使用API调用为您的组织创建新模式和资源，以及视图和编辑已定义的资源。

此开发人员指南提供了帮助您使用模式注册API进行开始的步骤。 然后，该指南提供了使用模式注册表执行键操作的示例API调用。

## 先决条件

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

* [体验数据模型(XDM)系统](../home.md):Experience Platform组织客户体验数据的标准化框架。
   * [模式合成的基础知识](../schema/composition.md):了解XDM模式的基本构建块。
* [实时客户用户档案](../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。
* [沙箱](../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

以下各节提供了成功调用模式注册表API所需了解的其他信息。

## 读取示例API调用

本指南提供示例API调用，以演示如何设置请求的格式。 这些包括路径、必需的标题和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑难解答指南 [中有关如何阅读示例API调用的部分](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

## 收集所需标题的值

要调用平台API，您必须首先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

* 授权：承载人 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源(包括属于模式注册表的资源)都隔离到特定虚拟沙箱。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

对模式注册表的所有查找(GET)请求都需要额外的“接受”标头，其值决定了API返回的信息格式。 有关更多详 [细信息，请参阅下面的](#accept) “接受标题”部分。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

* 内容类型：application/json

## 了解您的TENANT_ID {#know-your-tenant-id}

在本指南中，您将看到对的引用 `TENANT_ID`。 此ID用于确保您创建的资源命名正确并包含在IMS组织中。 如果您不知道自己的ID，则可以通过执行以下GET请求来访问它：

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

如果响应成功，将返回有关贵组织使用模式注册表的信息。 这包括一 `tenantId` 个属性，其值是您的属性 `TENANT_ID`。

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

* `tenantId`:IMS `TENANT_ID` 组织的值。

## 了解 `CONTAINER_ID`{#container}

调用模式注册表API需要使用 `CONTAINER_ID`。 有两个容器可以对其进行API调用：全 **球容器** ，租 **户容器**。

### 全球容器

该全球容器包含所有标准Adobe和Experience Platform合作伙伴提供的类、混音、数据类型和模式。 您只能对全局列表执行容器和查找(GET)请求。

### 租户容器

不要与您的独特性混淆，租户容器 `TENANT_ID`将保存由IMS组织定义的所有类、混音、数据类型、模式和描述符。 这是每个组织特有的，这意味着它们不可见或无法由其他IMS组织管理。 您可以针对您在租户容器中创建的资源执行所有CRUD操作(GET、POST、PUT、PATCH、DELETE)。

在租户容器中创建类、混音、模式或数据类型时，该类会保存到模式注册表中，并为其分配一个包含您的URI `$id``TENANT_ID`。 它 `$id` 在整个API中用于引用特定资源。 值的示 `$id` 例在下一节中提供。

## 模式识别 {#schema-identification}

模式以URI形 `$id` 式的属性进行标识，如：
* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

为了使URI对REST更友好，模式还在名为 `meta:altId`:
* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

调用模式注册表API将支持URL编码的 `$id` URI或(点 `meta:altId` 记号格式)。 最佳实践是在对API进行REST调 `$id` 用时使用URL编码的URI，如下所示：
* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## 接受标题 {#accept}

在模式注册表API中执行列表和查找(GET)操作时，需要一个“接受”标头来确定API返回的数据的格式。 查找特定资源时，“接受”标题中还必须包含版本号。

下表列表兼容的Accept头值（包括版本号）以及API在使用时将返回的描述。

| 接受 | 描述 |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | 仅返回列表ID。 这最常用于列出资源。 |
| `application/vnd.adobe.xed+json` | 返回包含原始和包含的完全JSON列表 `$ref` 的 `allOf` 模式。 这用于返回一列表完整资源。 |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | 原始XDM `$ref` 和 `allOf`。 有标题和说明。 |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` 属性和已 `allOf` 解析。 有标题和说明。 |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | 原始XDM `$ref` 和 `allOf`。 无标题或说明。 |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` 属性和已 `allOf` 解析。 无标题或说明。 |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` 属性和已 `allOf` 解析。 包含描述符。 |

>[!NOTE] 如果仅 `major` 提供版本（例如1、2、3），则注册表将返回最 `minor` 新版本(例如，.1、.2、.3)。

## XDM现场限制和最佳做法

模式的字段列在其对象中。 `properties` 每个字段本身都是一个对象，包含用于描述和约束字段可包含的数据的属性。

有关在API中定义字段类型的更多信息，请参阅本指南的附 [录](appendix.md) ，包括代码示例和最常用数据类型的可选约束。

以下示例字段说明了格式正确的XDM字段，其中提供了有关命名约束和最佳做法的更多详细信息。 在定义包含相似属性的其他资源时，也可以应用这些做法。

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

* 字段对象的名称可能包含字母数字、短划线或下划线字符，但 **不能以下划线** 开始。
   * **正确：**`fieldName`, `field_name2``Field-Name`, `field-name_3`
   * **错误：** `_fieldName`
* field对象的名称首选驼峰大小写。 示例: `fieldName`
* 该字段应包含以“标 `title`题大小写”写成的字段。 示例: `Field Name`
* 字段需要 `type`。
   * 定义某些类型可能需要可选 `format`。
   * 如果需要特定格式的数据，可 `examples` 以添加为数组。
   * 也可使用注册表中的任何数据类型来定义字段类型。 有关详细信息， [请参阅本指南中](create-data-type.md) 有关创建数据类型的部分。
* 说明 `description` 了有关现场数据的现场和相关信息。 它应当用明确的语言写成完整的句子，以便访问该模式的任何人都能了解该领域的意图。

有关如何 [在API中定义字段类型的详细信息](appendix.md) ，请参阅附录。

## 后续步骤

本文档涵盖了对模式注册表API进行调用所需的入门级知识，包括必需的身份验证凭据。 您现在可以继续阅读本开发人员指南中提供的示例调用，并按照其说明进行操作。 有关如何在API中制作模式的完整分步演练，请参阅以下教 [程](../tutorials/create-schema-api.md)。
