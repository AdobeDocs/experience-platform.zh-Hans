---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；数据模型；架构注册表；架构注册表；
solution: Experience Platform
title: 架构注册表API快速入门
description: 本文档介绍了在尝试调用Schema Registry API之前需要了解的核心概念。
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1350'
ht-degree: 0%

---

# 入门 [!DNL Schema Registry] API

此 [!DNL Schema Registry] API允许您创建和管理各种Experience Data Model (XDM)资源。 本文档介绍了在尝试调用 [!DNL Schema Registry] API。

## 先决条件

使用开发人员指南需要深入了解Adobe Experience Platform的以下组件：

* [[!DNL Experience Data Model (XDM) System]](../home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   * [模式组合基础](../schema/composition.md)：了解XDM架构的基本构建基块。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
* [[!DNL Sandboxes]](../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

XDM使用JSON架构格式来描述和验证所摄取的客户体验数据的结构。 因此，强烈建议您查看 [官方JSON架构文档](https://json-schema.org/) 以更好地了解这一基础技术。

## 正在读取示例API调用

此 [!DNL Schema Registry] API文档提供了示例API调用，以演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在Experience Platform疑难解答指南中。

## 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将提供所有中所有所需标头的值 [!DNL Experience Platform] API调用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有资源 [!DNL Experience Platform]，包括那些属于 [!DNL Schema Registry]，与特定的虚拟沙盒隔离。 的所有请求 [!DNL Platform] API需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信息 [!DNL Platform]，请参见 [沙盒文档](../../sandboxes/home.md).

对的所有查找(GET)请求 [!DNL Schema Registry] 需要附加 `Accept` 标头，其值确定API返回的信息格式。 请参阅 [接受标头](#accept) 部分，以了解更多详细信息。

包含有效负载(POST、PUT、PATCH)的所有请求都需要额外的标头：

* `Content-Type: application/json`

## 知道您的TENANT_ID {#know-your-tenant_id}

在整个API指南中，您将看到对 `TENANT_ID`. 此ID用于确保您创建的资源被正确命名并包含在您的组织中。 如果您不知道自己的ID，可以通过执行以下GET请求来访问它：

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

成功的响应会返回有关贵组织使用的信息 [!DNL Schema Registry]. 这包括 `tenantId` 属性，其值是您的 `TENANT_ID`.

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

## 了解 `CONTAINER_ID` {#container}

调用 [!DNL Schema Registry] API需要使用 `CONTAINER_ID`. 有两个容器可用于进行API调用： `global` 容器和 `tenant` 容器。

### 全局容器

此 `global` container包含所有标准Adobe和 [!DNL Experience Platform] partner提供的类、架构字段组、数据类型和架构。 您只能对执行列表和查找(GET)请求 `global` 容器。

使用 `global` 容器将如下所示：

```http
GET /global/classes
```

### 租户容器

别和你的独特性混淆 `TENANT_ID`，则 `tenant` container包含由组织定义的所有类、字段组、数据类型、架构和描述符。 这些内容对每个组织都是独一无二的，这意味着其他组织无法看到或管理这些内容。 您可以对在中创建的资源执行所有CRUD操作(GET、POST、PUT、PATCH、DELETE) `tenant` 容器。

使用 `tenant` 容器将如下所示：

```http
POST /tenant/fieldgroups
```

在中创建类、字段组、架构或数据类型时 `tenant` 容器，则会保存到 [!DNL Schema Registry] 并分配了 `$id` 包含您的 `TENANT_ID`. 此 `$id` 在整个API中使用来引用特定资源。 示例 `$id` 值在下一节中提供。

## 资源标识 {#resource-identification}

XDM资源由标识 `$id` URI形式的属性，如以下示例：

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

为了使URI更适合REST，架构在名为的属性中还具有URI的点表示法编码 `meta:altId`：

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

调用 [!DNL Schema Registry] API将支持URL编码的 `$id` URI或 `meta:altId` （点表示法格式）。 最佳实践为使用URL编码 `$id` 对API进行REST调用时的URI，如下所示：

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## 接受标头 {#accept}

在中执行列表和查找(GET)操作时 [!DNL Schema Registry] API，一个 `Accept` 标头是确定API返回的数据的格式所必需的。 在查找特定资源时，版本号也必须包含在 `Accept` 标头。

下表列出了兼容项 `Accept` 标头值（包括带有版本号的标头值），以及使用API时返回内容的描述。

| Accept | 描述 |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | 仅返回ID列表。 这最常用于列出资源。 |
| `application/vnd.adobe.xed+json` | 返回具有原始的完整JSON架构列表 `$ref` 和 `allOf` 包括。 用于返回完整资源的列表。 |
| `application/vnd.adobe.xed+json; version=1` | 原始XDM，带 `$ref` 和 `allOf`. 具有标题和描述。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 属性和 `allOf` 已解决。 具有标题和描述。 |
| `application/vnd.adobe.xed-notext+json; version=1` | 原始XDM，带 `$ref` 和 `allOf`. 无标题或描述。 |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 属性和 `allOf` 已解决。 无标题或描述。 |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 属性和 `allOf` 已解决。 包含描述符。 |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` 和 `allOf` 已解决，具有标题和描述。 已弃用的字段由表示 `meta:status` 属性 `deprecated`. |

{style="table-layout:auto"}

>[!NOTE]
>
>Platform当前仅支持每个架构有一个主要版本(`1`)。 因此，值 `version` 必须始终为 `1` 执行查找请求以返回架构的最新次要版本时。 有关架构版本控制的更多信息，请参阅下面的子部分。

### 架构版本控制 {#versioning}

架构版本由引用 `Accept` 架构注册表API和中的标头 `schemaRef.contentType` 属性。

目前，Platform仅支持单个主要版本(`1`)。 根据 [模式演化规则](../schema/composition.md#evolution)，架构的每次更新都必须是非破坏性的，这意味着架构的新次要版本(`1.2`， `1.3`、等) 始终向后兼容以前的次要版本。 因此，在指定 `version=1`，则架构注册表始终返回 **最新** 主要版本 `1` 架构，这意味着不返回以前的次要版本。

>[!NOTE]
>
>架构演化的非破坏性要求仅在架构被数据集引用并且以下情况之一为真后才实施：
>
>* 数据已引入数据集。
>* 数据集已允许在实时客户档案中使用（即使未摄取任何数据）。
>
>如果架构尚未与符合上述条件之一的数据集关联，则可以对它进行任何更改。 但是，在所有情况下 `version` 组件仍保留在 `1`.

## XDM字段限制和最佳实践

架构的字段列在其中 `properties` 对象。 每个字段本身都是一个对象，包含用于描述和约束字段可以包含的数据的属性。 请参阅指南，网址为 [在API中定义自定义字段](../tutorials/custom-fields-api.md) 最常用数据类型的代码示例和可选约束。

以下示例字段说明了格式正确的XDM字段，下面提供了有关命名约束和最佳实践的更多详细信息。 在定义包含相似属性的其他资源时，也可以应用这些实践。

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

* 字段对象的名称可以包含字母数字、短划线或下划线字符，但是 **可能不会** 从下划线开始。
   * **正确：** `fieldName`， `field_name2`， `Field-Name`， `field-name_3`
   * **不正确：** `_fieldName`
* 字段对象的名称首选camelCase。 示例：`fieldName`
* 该字段应包括 `title`，用大写字母写。 示例：`Field Name`
* 字段需要 `type`.
   * 定义某些类型可能需要一个可选字段 `format`.
   * 如果需要特定格式的数据， `examples` 可以添加为数组。
   * 字段类型也可以使用注册表中的任何数据类型来定义。 请参阅以下部分： [创建数据类型](./data-types.md#create) 有关更多信息，请参阅数据类型端点指南。
* 此 `description` 说明字段和有关字段数据的相关信息。 它应该写成句子完整，语言清楚，以便任何访问模式的人能够了解该领域的意图。

## 后续步骤

要开始使用 [!DNL Schema Registry] API中，选择一个可用的端点指南。
