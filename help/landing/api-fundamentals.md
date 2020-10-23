---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience PlatformAPI基础知识
topic: getting started
translation-type: tm+mt
source-git-commit: fac4b3d02a6e58a9d2c298f9b849fa7345e4fa93
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 2%

---


# Adobe Experience PlatformAPI基础知识

Adobe Experience PlatformAPI采用若干基础技术和语法，这些技术和语法对于有效管理基于JSON的资源非常重要。 [!DNL Platform] 本文档简要概述了这些技术，并提供了指向外部文档的链接以了解更多信息。

## JSON指针 {#json-pointer}

JSON指针是用于标识JSON文档中特[定值的标准字符串语法](https://tools.ietf.org/html/rfc6901)(RFC 6901)。 JSON指针是由字符分隔的标记 `/` 字符串，它指定对象键或数组索引，标记可以是字符串或数字。 JSON指针字符串用于API的许多PATCH [!DNL Platform] 操作，如本文档后面所述。 有关JSON指针的详细信息，请参阅JSON [指针概述文档](https://rapidjson.org/md_doc_pointer.html)。

### JSON模式对象示例

以下JSON表示一个简化的XDM模式，其字段可使用JSON指针字符串引用。 请注意，已使用自定义混音添加的所有字段(如 `loyaltyLevel`)在对象下以命名 `_{TENANT_ID}` ，而已使用核心混音添加的字段(如 `fullName`)不是。

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
| `"/properties/person/properties/name/properties/fullName"` | (返回对由核心混 `fullName` 音器提供的字段的引用。) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (返回对自定义混 `loyaltyLevel` 音提供的字段的引用。) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>处理(XDM)描 `xdm:sourceProperty` 述符 `xdm:destinationProperty` 的和属 [!DNL Experience Data Model] 性时，必须从JSON指 `properties` 针字符串 **中排除任** 何键。 有关详 [!DNL Schema Registry] 细信息，请参阅描述符的API开 [发人](../xdm/api/descriptors.md) 员指南子指南。

## JSON修补程序

API有许多PATCH操作， [!DNL Platform] 它们接受JSON修补程序对象的请求负载。 JSON修补程序是用于描述对JSON[文档所做更改的标准化格式](https://tools.ietf.org/html/rfc6902)(RFC 6902)。 它允许您定义JSON的部分更新，无需在请求主体中发送整个文档。

### JSON修补程序对象示例

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`:修补操作的类型。 虽然JSON修补程序支持多种不同的操作类型，但API中的所有PATCH操 [!DNL Platform] 作并非都与每种操作类型兼容。 可用的操作类型有：
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`:要更新的JSON结构部分，使用JSON指针 [表示法标](#json-pointer) 识。

JSON Patch对象可能需 `op`要其他属性，具体取决于中所示的操作类型。 有关不同JSON修补程序操作及其所需语法的详细信息，请参阅JSON [修补程序文档](http://jsonpatch.com/)。

## JSON模式

JSON模式是一种用于描述和验证JSON数据结构的格式。 [体验模式模型](../xdm/home.md) (XDM)利用JSON功能对所摄取的客户体验数据的结构和格式实施限制。 有关JSON模式的更多信息，请参阅 [官方文档](https://json-schema.org/)。

## 后续步骤

此文档引入了与为管理基于JSON的资源相关的一些技术和语法 [!DNL Experience Platform]。 有关使用API的更多信 [!DNL Platform] 息（包括最佳实践和常见问题解答），请参阅平台疑 [难解答指南](troubleshooting.md)。