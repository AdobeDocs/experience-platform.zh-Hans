---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；数据模型；架构注册表；架构注册表；
solution: Experience Platform
title: 架构注册表API快速入门
description: 本文档介绍了在尝试调用Schema Registry API之前需要了解的核心概念。
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1364'
ht-degree: 5%

---

# [!DNL Schema Registry] API快速入门

[!DNL Schema Registry] API允许您创建和管理各种Experience Data Model (XDM)资源。 本文档介绍了在尝试调用[!DNL Schema Registry] API之前需要了解的核心概念。

## 先决条件

使用开发人员指南需要实际了解Adobe Experience Platform的以下组件：

* [[!DNL Experience Data Model (XDM) System]](../home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../schema/composition.md)：了解XDM架构的基本构建块。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。
* [[!DNL Sandboxes]](../../sandboxes/home.md)： [!DNL Experience Platform]提供了将单个[!DNL Experience Platform]实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

XDM使用JSON架构格式来描述和验证所摄取的客户体验数据的结构。 因此，强烈建议您查看[官方JSON架构文档](https://json-schema.org/)，以更好地了解此基础技术。

## 正在读取示例 API 调用

[!DNL Schema Registry] API文档提供了示例API调用，以演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅Experience Platform疑难解答指南中有关[如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。

## 收集所需标头的值

要调用[!DNL Experience Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Schema Registry]的资源）都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Experience Platform]中沙盒的更多信息，请参阅[沙盒文档](../../sandboxes/home.md)。

对[!DNL Schema Registry]的所有查找(GET)请求都需要额外的`Accept`标头，其值将决定API返回的信息格式。 有关更多详细信息，请参阅下面的[接受标头](#accept)部分。

包含负载 (POST、PUT、PATCH) 的所有请求都需要额外的标头：

* `Content-Type: application/json`

## 知道您的TENANT_ID {#know-your-tenant_id}

在整个API指南中，您将看到对`TENANT_ID`的引用。 此ID用于确保您创建的资源被正确命名并包含在您的组织中。 如果您不知道自己的ID，可以通过执行以下GET请求来访问它：

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回有关贵组织使用[!DNL Schema Registry]的信息。 这包含一个`tenantId`属性，其值是您的`TENANT_ID`。

```JSON
{
  "imsOrg":"{ORG_ID}",
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
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
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
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
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

调用[!DNL Schema Registry] API需要使用`CONTAINER_ID`。 有两个容器可针对其进行API调用： `global`容器和`tenant`容器。

### 全局容器

`global`容器包含所有标准Adobe和[!DNL Experience Platform]合作伙伴提供的类、架构字段组、数据类型和架构。 您只能对`global`容器执行列表和查找(GET)请求。

使用`global`容器的调用示例如下所示：

```http
GET /global/classes
```

### 租户容器

`tenant`容器包含组织定义的所有类、字段组、数据类型、架构和描述符，请不要与您的唯一`TENANT_ID`混淆。 这些功能对于每个组织都是独一无二的，这意味着其他组织无法看到或管理这些功能。 您可以对在`tenant`容器中创建的资源执行所有CRUD操作(GET、POST、PUT、PATCH、DELETE)。

使用`tenant`容器的调用示例如下所示：

```http
POST /tenant/fieldgroups
```

在`tenant`容器中创建类、字段组、架构或数据类型时，该容器将保存到[!DNL Schema Registry]并分配了包含您的`TENANT_ID`的`$id` URI。 此`$id`在整个API中用于引用特定资源。 下一节中提供了`$id`值的示例。

## 资源标识 {#resource-identification}

XDM资源使用URI形式的`$id`属性进行标识，如以下示例：

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

为了使URI更易于REST，架构在名为`meta:altId`的属性中还对URI进行了点表示法编码：

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

对[!DNL Schema Registry] API的调用将支持URL编码的`$id` URI或`meta:altId`（点表示法格式）。 最佳实践是在对API进行REST调用时使用URL编码的`$id` URI，如下所示：

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## 接受标头 {#accept}

在[!DNL Schema Registry] API中执行列表和查找(GET)操作时，需要`Accept`标头来确定API返回的数据格式。 查找特定资源时，`Accept`标头中还必须包含版本号。

下表列出了兼容的`Accept`标头值，包括那些具有版本号的值，以及使用API时该API将返回的内容的描述。

| 接受 | 描述 |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | 仅返回ID列表。 这最常用于列出资源。 |
| `application/vnd.adobe.xed+json` | 返回包含原始`$ref`和`allOf`的完整JSON架构列表。 用于返回完整资源的列表。 |
| `application/vnd.adobe.xed+json; version=1` | 带`$ref`和`allOf`的原始XDM。 具有标题和描述。 |
| `application/vnd.adobe.xed-full+json; version=1` | 已解决`$ref`属性和`allOf`。 具有标题和描述。 |
| `application/vnd.adobe.xed-notext+json; version=1` | 带`$ref`和`allOf`的原始XDM。 无标题或描述。 |
| `application/vnd.adobe.xed-full-notext+json; version=1` | 已解决`$ref`属性和`allOf`。 无标题或描述。 |
| `application/vnd.adobe.xed-full-desc+json; version=1` | 已解决`$ref`属性和`allOf`。 包含描述符。 |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref`和`allOf`已解决，具有标题和描述。 已弃用的字段用`deprecated`的`meta:status`属性表示。 |

{style="table-layout:auto"}

>[!NOTE]
>
>Experience Platform当前仅支持每个架构(`1`)有一个主要版本。 因此，在执行查找请求时，`version`的值必须始终为`1`，以便返回架构的最新次版本。 有关架构版本控制的更多信息，请参阅下面的子部分。

### 架构版本控制 {#versioning}

架构版本由架构注册表API中的`Accept`标头和下游Experience Platform服务API负载中的`schemaRef.contentType`属性引用。

目前，Experience Platform仅支持每个架构有一个主要版本(`1`)。 根据架构演变](../schema/composition.md#evolution)的[规则，对架构的每次更新都必须是非破坏性的，这意味着架构的新次要版本（`1.2`、`1.3`等）始终与以前的次要版本向后兼容。 因此，在指定`version=1`时，架构注册表始终返回架构的&#x200B;**latest**&#x200B;主要版本`1`，这意味着不返回以前的次要版本。

>[!NOTE]
>
>只有在数据集引用了架构并且以下情况之一为true后，才会强制实施架构演变的非破坏性要求：
>
>* 数据已摄取到数据集。
>* 该数据集已允许在实时客户档案中使用（即使未摄取任何数据）。
>
>如果架构尚未与符合上述条件之一的数据集关联，则可以对它进行任何更改。 但是，在所有情况下`version`组件仍保留在`1`。

## XDM字段限制和最佳实践

架构的字段在其`properties`对象中列出。 每个字段本身都是一个对象，包含用于描述和约束字段可以包含的数据的属性。 请参阅有关[在API](../tutorials/custom-fields-api.md)中定义自定义字段的指南，以获取代码示例和最常用数据类型的可选约束。

以下示例字段说明了正确格式化的XDM字段，下面提供了有关命名约束和最佳实践的更多详细信息。 在定义包含相似属性的其他资源时，也可以应用这些实践。

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

* 字段对象的名称可以包含字母数字、短划线或下划线字符，但&#x200B;**不能**&#x200B;以下划线开头。
   * **正确：** `fieldName`，`field_name2`，`Field-Name`，`field-name_3`
   * **不正确：** `_fieldName`
* 字段名称不区分大小写，并且在架构中的同一级别必须具有不同的名称。
* 字段对象的名称首选camelCase。 示例：`fieldName`
* 该字段应包含一个`title`，用大写字母写。 示例：`Field Name`
* 该字段需要`type`。
   * 定义某些类型可能需要可选的`format`。
   * 如果需要特定格式的数据，可将`examples`添加为数组。
   * 字段类型也可以使用注册表中的任何数据类型定义。 有关详细信息，请参阅数据类型端点指南中有关[创建数据类型](./data-types.md#create)的部分。
* `description`说明字段和有关字段数据的相关信息。 它应该用完整的句子写成，语言要清晰，以便任何访问模式的人能够理解该字段的意图。

## 后续步骤

要开始使用[!DNL Schema Registry] API进行调用，请选择一个可用的端点指南。
