---
keywords: Experience Platform；主页；热门主题；API;XDM;XDM系统；体验数据模型；体验数据模型；数据模型；数据模型；模式注册表；模式注册表；
solution: Experience Platform
title: 架构注册API快速入门
description: 本文档简要介绍在尝试调用架构注册表API之前需要了解的核心概念。
topic-legacy: developer guide
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: a26c8d43ff7874bcedd2adb3d6da995986198c96
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 0%

---

# 入门 [!DNL Schema Registry] API

的 [!DNL Schema Registry] API允许您创建和管理各种体验数据模型(XDM)资源。 本文档简要介绍在尝试调用 [!DNL Schema Registry] API。

## 先决条件

使用开发人员指南需要对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM) System]](../home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
   * [架构组合的基础知识](../schema/composition.md):了解XDM模式的基本构建块。
* [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

XDM使用JSON模式格式来描述和验证摄取的客户体验数据的结构。 因此，强烈建议您查看 [官方JSON模式文档](https://json-schema.org/) 以更好地了解这项基础技术。

## 读取示例API调用

的 [!DNL Schema Registry] API文档提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) (位于Experience Platform疑难解答指南中)。

## 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

中的所有资源 [!DNL Experience Platform]，包括属于 [!DNL Schema Registry]，与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定操作将在其中执行的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有关 [!DNL Platform]，请参阅 [沙盒文档](../../sandboxes/home.md).

对 [!DNL Schema Registry] 需要 `Accept` 标头，其值确定API返回的信息格式。 请参阅 [接受标头](#accept) 部分以了解更多详细信息。

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的标头：

* `Content-Type: application/json`

## 知晓您的TENANT_ID {#know-your-tenant_id}

在整个API指南中，您将看到对 `TENANT_ID`. 此ID用于确保您创建的资源具有正确命名空间，并包含在您的IMS组织内。 如果您不知道自己的ID，可以通过执行以下GET请求来访问它：

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

成功的响应会返回有关贵组织使用 [!DNL Schema Registry]. 这包括 `tenantId` 属性，其值是 `TENANT_ID`.

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

## 了解 `CONTAINER_ID` {#container}

调用 [!DNL Schema Registry] API需要使用 `CONTAINER_ID`. 可以对其进行API调用的容器有两个：the `global` 容器和 `tenant` 容器。

### 全局容器

的 `global` 容器包含所有标准Adobe和 [!DNL Experience Platform] 合作伙伴提供的类、架构字段组、数据类型和架构。 您只能对 `global` 容器。

使用的调用的示例 `global` 容器将如下所示：

```http
GET /global/classes
```

### 租户容器

不要与你的独特 `TENANT_ID`, `tenant` 容器包含由IMS组织定义的所有类、字段组、数据类型、架构和描述符。 这些IMS组织对每个组织都是唯一的，这意味着这些IMS组织不可见或无法管理。 您可以对在 `tenant` 容器。

使用的调用的示例 `tenant` 容器将如下所示：

```http
POST /tenant/fieldgroups
```

在中创建类、字段组、架构或数据类型时， `tenant` 容器中，它被保存到 [!DNL Schema Registry] 分配 `$id` 包含您的 `TENANT_ID`. 此 `$id` 在整个API中使用来引用特定资源。 示例 `$id` 值将在下一节中提供。

## 资源标识 {#resource-identification}

XDM资源通过 `$id` 属性，例如以下示例：

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

为了使URI对REST更友好，架构在名为的属性中还具有URI的点表示法编码 `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

调用 [!DNL Schema Registry] API将支持URL编码的 `$id` URI或 `meta:altId` （点符号格式）。 最佳实践是使用URL编码 `$id` 对API进行REST调用时的URI，如下所示：

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## 接受标头 {#accept}

在 [!DNL Schema Registry] API、 `Accept` 需要标头来确定API返回的数据格式。 查找特定资源时，还必须在 `Accept` 标题。

下表列出了兼容的 `Accept` 标头值，包括具有版本号的值，以及有关使用API时将返回哪些内容的描述。

| Accept | 描述 |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | 仅返回ID列表。 这最常用于列出资源。 |
| `application/vnd.adobe.xed+json` | 返回具有原始的完整JSON架构的列表 `$ref` 和 `allOf` 包含。 用于返回完整资源列表。 |
| `application/vnd.adobe.xed+json; version=1` | 原始XDM，包含 `$ref` 和 `allOf`. 具有标题和描述。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 属性和 `allOf` 已解决。 具有标题和描述。 |
| `application/vnd.adobe.xed-notext+json; version=1` | 原始XDM，包含 `$ref` 和 `allOf`. 无标题或描述。 |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 属性和 `allOf` 已解决。 无标题或描述。 |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 属性和 `allOf` 已解决。 包含描述符。 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>平台当前仅支持每个架构的一个主要版本(`1`)。 因此， `version` 必须始终 `1` 执行查找请求以返回架构的最新次要版本时。 有关架构版本控制的详细信息，请参阅下面的子部分。

### 架构版本控制 {#versioning}

架构版本由 `Accept` 架构注册表API和 `schemaRef.contentType` 下游平台服务API负载中的属性。

目前，平台仅支持单个主要版本(`1`)。 根据 [模式演化规则](../schema/composition.md#evolution)，则架构的每次更新都必须是无损的，这意味着架构的新次要版本(`1.2`, `1.3`等) 始终向后兼容以前的次要版本。 因此，在指定 `version=1`，架构注册表始终返回 **最新** 主要版本 `1` ，这表示不返回以前的次要版本。

>[!NOTE]
>
>仅当数据集引用了架构，并且满足以下任一情况后，才会执行架构演变的无损要求：
>
>* 已将数据摄取到数据集中。
>* 该数据集已启用，可在“实时客户资料”中使用（即使未摄取任何数据）。
>
>如果架构尚未与满足上述任一条件的数据集关联，则可以对其进行任何更改。 但是，在所有情况下， `version` 组件仍保持为 `1`.

## XDM字段约束和最佳实践

架构的字段列在 `properties` 对象。 每个字段本身就是一个对象，其中包含用于描述和约束字段可包含的数据的属性。 请参阅 [在API中定义自定义字段](../tutorials/custom-fields-api.md) 适用于最常用的数据类型的代码示例和可选约束。

以下示例字段说明了格式正确的XDM字段，并提供了有关命名约束和最佳实践的更多详细信息。 在定义包含相似属性的其他资源时，也可以应用这些实践。

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

* 字段对象的名称可能包含字母数字、短划线或下划线字符，但 **不能** 以下划线开头。
   * **正确：** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **错误：** `_fieldName`
* 字段对象的名称首选使用camelCase。 示例: `fieldName`
* 字段应包括 `title`，以标题大小写写。 示例: `Field Name`
* 字段需要 `type`.
   * 定义某些类型可能需要可选 `format`.
   * 如果需要特定的数据格式， `examples` 可以添加为数组。
   * 也可使用注册表中的任何数据类型来定义字段类型。 请参阅 [创建数据类型](./data-types.md#create) （详细信息）端点指南中的。
* 的 `description` 解释字段及有关字段数据的相关信息。 它应以完整的句子编写，并且使用清晰的语言，以便访问该模式的任何人都能够理解该字段的意图。

## 后续步骤

要开始使用 [!DNL Schema Registry] API，请选择一个可用的端点指南。
