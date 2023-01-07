---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Experience PlatformAPI基础知识
description: 本文档简要概述了与Experience PlatformAPI相关的一些基础技术和语法。
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 1%

---

# Experience PlatformAPI基础知识

Adobe Experience Platform API使用了一些基础技术和语法，要有效管理基于JSON的数据，这些技术和语法非常重要 [!DNL Platform] 资源。 本文档简要概述了这些技术，并提供了指向外部文档的链接以了解更多信息。

## JSON指针 {#json-pointer}

JSON指针是一个标准化的字符串语法([RFC 6901](https://tools.ietf.org/html/rfc6901))来标识JSON文档中的特定值。 JSON指针是由 `/` 字符，可指定对象键或数组索引，令牌可以是字符串或数字。 JSON指针字符串用于的许多PATCH操作 [!DNL Platform] API，如本文档后文所述。 有关JSON指针的更多信息，请参阅 [JSON指针概述文档](https://rapidjson.org/md_doc_pointer.html).

### JSON模式对象示例

以下JSON表示一个简化的XDM架构，其字段可以使用JSON指针字符串引用。 请注意，已使用自定义架构字段组添加的所有字段(例如 `loyaltyLevel`)的名称位于 `_{TENANT_ID}` 对象，而使用核心字段组添加的字段(例如 `fullName`)不会。

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

### 基于架构对象的JSON指针示例

| JSON指针 | 解析为 |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | (返回对 `fullName` 字段，由核心字段组提供。) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (返回对 `loyaltyLevel` 字段，由自定义字段组提供。) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>在处理 `xdm:sourceProperty` 和 `xdm:destinationProperty` 属性 [!DNL Experience Data Model] (XDM)描述符，任何 `properties` 键必须 **排除** 从JSON指针字符串中。 请参阅 [!DNL Schema Registry] 关于的API开发人员指南子指南 [描述符](../xdm/api/descriptors.md) 以了解更多信息。

## JSON修补程序 {#json-patch}

有许多PATCH操作 [!DNL Platform] 接受JSON修补程序对象以获取其请求负载的API。 JSON修补程序是一种标准化格式([RFC 6902](https://tools.ietf.org/html/rfc6902))，以描述对JSON文档所做的更改。 它允许您定义对JSON的部分更新，而无需在请求正文中发送整个文档。

### JSON修补程序对象示例

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`:修补程序操作的类型。 虽然JSON修补程序支持多种不同的操作类型，但并非中的所有PATCH操作 [!DNL Platform] API与每种操作类型都兼容。 可用的操作类型包括：
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`:要更新的JSON结构的部分，使用 [JSON指针](#json-pointer) 符号。

根据 `op`，则JSON修补程序对象可能需要其他属性。 有关不同JSON修补程序操作及其所需语法的更多信息，请参阅 [JSON修补程序文档](https://datatracker.ietf.org/doc/html/rfc6902).

## JSON架构 {#json-schema}

JSON模式是用于描述和验证JSON数据结构的格式。 [体验数据模型(XDM)](../xdm/home.md) 利用JSON架构功能对摄取的客户体验数据的结构和格式实施限制。 有关JSON架构的更多信息，请参阅 [官方文档](https://json-schema.org/).

## 后续步骤

本文档介绍了与管理基于JSON的 [!DNL Experience Platform]. 请参阅 [入门指南](api-guide.md) 有关使用Platform API的更多信息，包括最佳实践。 有关常见问题解答的解答，请参阅 [平台疑难解答指南](troubleshooting.md).
