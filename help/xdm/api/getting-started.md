---
keywords: Experience Platform；主题；热门主题；api;API;XDM;XDM系统；体验数据模型；体验数据模型；数据模型；模式注册；模式注册；
solution: Experience Platform
title: 模式注册表API入门
description: 本文档介绍了在尝试调用模式注册表API之前需要了解的核心概念。
topic: developer guide
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
translation-type: tm+mt
source-git-commit: 610ce5c6dca5e7375b941e7d6f550382da10ca27
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 0%

---

# [!DNL Schema Registry] API入门

[!DNL Schema Registry] API允许您创建和管理各种体验数据模型(XDM)资源。 本文档介绍了在尝试调用[!DNL Schema Registry] API之前需要了解的核心概念。

## 先决条件

使用开发人员指南需要对Adobe Experience Platform的以下组件有充分的了解：

* [[!DNL Experience Data Model (XDM) System]](../home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [模式合成的基础](../schema/composition.md):了解XDM模式的基本构建块。
* [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单 [!DNL Platform] 独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

XDM使用JSON模式格式描述和验证所摄取的客户体验数据的结构。 因此，强烈建议您查看[官方JSON模式文档](https://json-schema.org/)，以便更好地了解此基础技术。

## 读取示例API调用

[!DNL Schema Registry] API文档提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关文档中用于示例API调用的约定的信息，请参阅Experience Platform疑难解答指南中关于如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。[

## 收集所需标题的值

要调用[!DNL Platform] API，您必须首先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Schema Registry]的资源）都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个头，该头指定操作将在中执行的沙箱的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Platform]中沙箱的详细信息，请参阅[沙箱文档](../../sandboxes/home.md)。

对[!DNL Schema Registry]的所有查找(GET)请求都需要额外的`Accept`头，其值决定API返回的信息格式。 有关详细信息，请参阅下面的[接受标题](#accept)部分。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

* `Content-Type: application/json`

## 了解您的TENANT_ID {#know-your-tenant_id}

在整个API指南中，您会看到对`TENANT_ID`的引用。 此ID用于确保您创建的资源命名正确且包含在IMS组织中。 如果您不知道自己的ID，可以通过执行以下GET请求来访问它：

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

成功的响应会返回有关您的组织对[!DNL Schema Registry]的使用的信息。 这包括`tenantId`属性，其值为`TENANT_ID`。

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

## 了解`CONTAINER_ID` {#container}

对[!DNL Schema Registry] API的调用需要使用`CONTAINER_ID`。 有两种容器可对其进行API调用：`global`容器和`tenant`容器。

### 全球容器

`global`容器包含所有标准Adobe和[!DNL Experience Platform]合作伙伴提供的类、混合、数据类型和模式。 您只能对`global`容器执行列表和查找(GET)请求。

使用`global`容器的调用示例如下所示：

```http
GET /global/classes
```

### 租户容器

不要与您的唯一`TENANT_ID`混淆，`tenant`容器包含由IMS组织定义的所有类、混合、数据类型、模式和描述符。 这是每个组织特有的，这意味着它们不可见或无法由其他IMS组织管理。 您可以对您在`tenant`容器中创建的资源执行所有CRUD操作(GET、POST、PUT、PATCH、DELETE)。

使用`tenant`容器的调用示例如下所示：

```http
POST /tenant/mixins
```

在`tenant`容器中创建类、mixin、模式或数据类型时，会将其保存到[!DNL Schema Registry]，并为其分配包含`TENANT_ID`的`$id` URI。 此`$id`用于整个API中引用特定资源。 下一节提供了`$id`值的示例。

## 资源标识{#resource-identification}

XDM资源以URI形式使用`$id`属性进行标识，例如：

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

要使URI更易于REST，模式还在名为`meta:altId`的属性中对URI进行点记号编码：

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

对[!DNL Schema Registry] API的调用将支持URL编码的`$id` URI或`meta:altId`（点记号格式）。 最佳实践是在对API进行REST调用时使用URL编码的`$id` URI，如下所示：

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## 接受标头{#accept}

在[!DNL Schema Registry] API中执行列表和查找(GET)操作时，需要`Accept`头来确定API返回的数据的格式。 查找特定资源时，`Accept`标头中还必须包含版本号。

下表列表了兼容`Accept`标头值，包括版本号的标头值，以及API在使用时将返回的描述。

| Accept | 描述 |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | 仅返回ID的列表。 这最常用于列出资源。 |
| `application/vnd.adobe.xed+json` | 返回包含原始`$ref`和`allOf`的完整JSON模式列表。 这用于返回一列表完整资源。 |
| `application/vnd.adobe.xed+json; version=1` | 具有`$ref`和`allOf`的原始XDM。 有标题和说明。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 属性和已 `allOf` 解析。有标题和说明。 |
| `application/vnd.adobe.xed-notext+json; version=1` | 具有`$ref`和`allOf`的原始XDM。 无标题或描述。 |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 属性和已 `allOf` 解析。无标题或描述。 |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 属性和已 `allOf` 解析。包含描述符。 |

>[!NOTE]
>
>平台当前仅支持每个模式的一个主版本(`1`)。 因此，执行查找请求时，`version`的值必须始终为`1`，以返回模式的最新次要版本。 有关模式版本控制的详细信息，请参阅下面的子节。

### 模式版本{#versioning}

模式版本由模式 Registry API中的`Accept`头和下游平台服务API负载中的`schemaRef.contentType`属性中的头引用。

目前，平台仅支持每个模式的单个主版本(`1`)。 根据[模式演化规则](../schema/composition.md#evolution)，对模式的每次更新都必须是无损的，这意味着模式的新次版本（`1.2`、`1.3`等） 始终向后兼容以前的次要版本。 因此，指定`version=1`时，模式注册表始终返回模式的&#x200B;**最新**&#x200B;主版本`1` ，这意味着不返回以前的次版本。

>[!NOTE]
>
>只有在模式被数据集引用且以下情况之一为true后，才会强制执行模式演化的非破坏性要求：
>
>* 数据已被收录到数据集中。
>* 数据集已启用，可在“实时客户”用户档案中使用（即使未摄取任何数据）。

>
>
如果模式尚未与符合上述条件之一的数据集关联，则可以对其进行任何更改。 但是，在所有情况下，`version`组件仍保留在`1`。

## XDM现场限制和最佳做法

模式的字段列在其`properties`对象中。 每个字段本身都是一个对象，包含描述和约束字段可包含的数据的属性。

有关在API中定义字段类型的详细信息，请参阅本指南的[字段约束指南](../schema/field-constraints.md)，包括代码示例和最常用数据类型的可选约束。

以下示例字段说明了格式正确的XDM字段，并提供了以下有关命名约束和最佳实践的更多详细信息。 在定义包含相似属性的其他资源时，也可以应用这些做法。

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

* 字段对象的名称可能包含字母数字、短划线或下划线字符，但&#x200B;**不能**&#x200B;带下划线的开始。
   * **正确：** `fieldName`, `field_name2`, `Field-Name`  `field-name_3`
   * **不正确：** `_fieldName`
* field对象的名称首选使用camelCase。 示例: `fieldName`
* 该字段应包括`title`，在“标题大小写”中写入。 示例: `Field Name`
* 该字段需要`type`。
   * 定义某些类型可能需要可选的`format`。
   * 当需要特定格式化数据时，可以将`examples`添加为数组。
   * 也可以使用注册表中的任何数据类型来定义字段类型。 有关详细信息，请参阅数据类型端点指南中有关创建数据类型](./data-types.md#create)的部分。[
* `description`说明了有关字段数据的字段和相关信息。 它应用语言明确的全句写成，以便任何访问模式的人都能够理解该领域的意图。

有关如何在API中定义不同字段类型的详细信息，请参阅[字段约束](../schema/field-constraints.md)上的文档。

## 后续步骤

要开始使用[!DNL Schema Registry] API进行调用，请选择可用的端点指南之一。
