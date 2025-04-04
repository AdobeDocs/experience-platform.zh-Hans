---
keywords: Experience Platform；首页；热门话题
solution: Experience Platform
title: Experience Platform API基础
description: 本文档简要概述了Experience Platform API涉及的一些底层技术和语法。
role: Developer
feature: API
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 1%

---

# Experience Platform API基础

Adobe Experience Platform API使用多种基础技术和语法，这些技术和语法对于有效管理基于JSON的[!DNL Experience Platform]资源非常重要。 本文档提供了这些技术的简要概述，以及指向外部文档的链接以了解更多信息。

## JSON指针 {#json-pointer}

JSON指针是一个标准化的字符串语法([RFC 6901](https://tools.ietf.org/html/rfc6901))，用于标识JSON文档中的特定值。 JSON指针是以`/`字符分隔的令牌字符串，用于指定对象键或数组索引，并且令牌可以是字符串或数字。 JSON指针字符串在[!DNL Experience Platform] API的许多PATCH操作中使用，如本文档后面所述。 有关JSON指针的更多信息，请参阅[JSON指针概述文档](https://rapidjson.org/md_doc_pointer.html)。

### 示例JSON模式对象

以下JSON表示简化的XDM架构，其字段可以使用JSON指针字符串引用。 请注意，使用自定义架构字段组（如`loyaltyLevel`）添加的所有字段都在`_{TENANT_ID}`对象下命名空间，而使用核心字段组（如`fullName`）添加的字段则不是。

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/85a4bdaa168b01bf44384e049fbd3d2e9b2ffaca440d35b9",
  "meta:altId": "_{TENANT_ID}.schemas.85a4bdaa168b01bf44384e049fbd3d2e9b2ffaca440d35b9",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Example schema",
  "type": "object",
  "description": "This is an example schema.",
  "properties": {
    "_{TENANT_ID}": {
      "type": "object",
      "properties": {
        "loyaltyLevel": {
          "title": "Loyalty Level",
          "description": "",
          "type": "string",
          "isRequired": false,
          "enum": [
            "platinum",
            "gold",
            "silver",
            "bronze"
          ]
        }
      }
    },
    "person": {
      "title": "Person",
      "description": "An individual actor, contact, or owner.",
      "type": "object",
      "properties": {
        "name": {
          "title": "Full name",
          "description": "The person's full name.",
          "type": "object",
          "properties": {
            "fullName": {
              "title": "Full name",
              "type": "string",
              "description": "The full name of the person, in writing order most commonly accepted in the language of the name.",
            },
            "suffix": {
              "title": "Suffix",
              "type": "string",
              "description": "A group of letters provided after a person's name to provide additional information. The `suffix` is used at the end of someones name. For example Jr., Sr., M.D., PhD, I, II, III, etc.",
            }
          },
          "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person-name",
          "meta:xdmField": "xdm:name"
        }
      }
    }
  }
}
```

### 基于模式对象的JSON指针示例

| JSON指针 | 解析为 |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | （返回由核心字段组提供的`fullName`字段的引用。） |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | （返回对自定义字段组提供的`loyaltyLevel`字段的引用。） |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>在处理[!DNL Experience Data Model] (XDM)描述符的`xdm:sourceProperty`和`xdm:destinationProperty`属性时，任何`properties`键都必须从JSON指针字符串中&#x200B;**排除**。 有关详细信息，请参阅[描述符](../xdm/api/descriptors.md)上的[!DNL Schema Registry] API开发人员指南子指南。

## JSON修补程序 {#json-patch}

对于[!DNL Experience Platform] API，有许多接受JSON修补程序对象作为其请求负载的PATCH操作。 JSON修补程序是一种用于描述JSON文档更改的标准化格式([RFC 6902](https://tools.ietf.org/html/rfc6902))。 它允许您定义对JSON的部分更新，而无需在请求正文中发送整个文档。

### 示例JSON修补程序对象

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`：修补操作的类型。 虽然JSON修补程序支持多种不同的操作类型，但并非所有[!DNL Experience Platform] API中的PATCH操作都与每种操作类型兼容。 可用的操作类型包括：
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`：要更新的JSON结构部分，使用[JSON指针](#json-pointer)表示法标识。

根据`op`中指示的操作类型，JSON修补程序对象可能需要其他属性。 有关不同的JSON修补程序操作及其所需语法的更多信息，请参阅[JSON修补程序文档](https://datatracker.ietf.org/doc/html/rfc6902)。

## JSON架构 {#json-schema}

JSON模式是一种用于描述和验证JSON数据结构的格式。 [体验数据模型(XDM)](../xdm/home.md)利用JSON架构功能对摄取的客户体验数据的结构和格式实施约束。 有关JSON架构的更多信息，请参阅[官方文档](https://json-schema.org/)。

## 后续步骤

本文档介绍了与管理[!DNL Experience Platform]的基于JSON的资源相关的一些技术和语法。 有关使用Experience Platform API（包括最佳实践）的更多信息，请参阅[快速入门指南](api-guide.md)。 有关常见问题的解答，请参阅[Experience Platform疑难解答指南](troubleshooting.md)。
