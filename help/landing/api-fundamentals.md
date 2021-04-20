---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Experience Platform API基础知识
topic: getting started
description: 本文档简要概述了与Experience Platform API相关的一些底层技术和语法。
translation-type: tm+mt
source-git-commit: ca5c8527b1b54856aa1e762a06ddbe404f30ec42
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 1%

---


# Experience Platform API基础知识

Adobe Experience Platform API采用了一些基础技术和语法，对于有效管理基于JSON的[!DNL Platform]资源而言，这些技术和语法非常重要。 本文档简要概述了这些技术，并提供了指向外部文档的链接以了解更多信息。

## JSON指针{#json-pointer}

JSON指针是用于标识JSON文档中特定值的标准字符串语法([RFC 6901](https://tools.ietf.org/html/rfc6901))。 JSON指针是由`/`字符分隔的令牌字符串，可指定对象键或数组索引，令牌可以是字符串或数字。 JSON指针字符串用于[!DNL Platform] API的许多PATCH操作，如本文档后面所述。 有关JSON指针的详细信息，请参阅[JSON指针概述文档](https://rapidjson.org/md_doc_pointer.html)。

### JSON模式对象示例

以下JSON表示一个简化的XDM模式，其字段可使用JSON指针字符串引用。 请注意，已使用自定义混音添加的所有字段（如`loyaltyLevel`）均以`_{TENANT_ID}`对象命名，而已使用核心混音添加的字段（如`fullName`）则不以名称命名。

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
| `"/properties/person/properties/name/properties/fullName"` | （返回对由核心混音器提供的`fullName`字段的引用。） |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | （返回对由自定义混音提供的`loyaltyLevel`字段的引用。） |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>处理[!DNL Experience Data Model](XDM)描述符的`xdm:sourceProperty`和`xdm:destinationProperty`属性时，任何`properties`键都必须是JSON指针字符串中的&#x200B;**排除的**。 有关详细信息，请参阅[描述符](../xdm/api/descriptors.md)上的[!DNL Schema Registry] API开发人员指南子指南。

## JSON修补程序{#json-patch}

[!DNL Platform] API有许多PATCH操作，它们接受JSON修补程序对象的请求负载。 JSON修补程序是用于描述对JSON文档所做的更改的标准化格式([RFC 6902](https://tools.ietf.org/html/rfc6902))。 它允许您定义JSON的部分更新，无需在请求主体中发送整个文档。

### JSON修补对象示例

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`:修补操作的类型。虽然JSONPATCH程序支持多种不同的操作类型，但并非[!DNL Platform] API中的所有操作都与每种操作类型兼容。 可用的操作类型有：
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`:要更新的JSON结构部分，使用JSON Pointernotation [进行](#json-pointer) 标识。

根据`op`中指示的操作类型，JSON Patch对象可能需要其他属性。 有关不同JSON修补程序操作及其所需语法的详细信息，请参阅[JSON修补程序文档](http://jsonpatch.com/)。

## JSON模式{#json-schema}

JSON模式是一种用于描述和验证JSON数据结构的格式。 [体验模式模型(XDM)利](../xdm/home.md) 用JSON功能，对所摄取的客户体验数据的结构和格式进行约束。有关JSON模式的详细信息，请参阅[官方文档](https://json-schema.org/)。

## 后续步骤

此文档引入了管理[!DNL Experience Platform]基于JSON的资源时涉及的一些技术和语法。 有关使用平台API的更多信息（包括最佳实践），请参阅[快速入门指南](api-guide.md)。 有关常见问题解答的解答，请参阅[平台疑难解答指南](troubleshooting.md)。