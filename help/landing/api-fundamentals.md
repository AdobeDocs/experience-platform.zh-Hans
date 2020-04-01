---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform API基础知识
topic: getting started
translation-type: tm+mt
source-git-commit: c94f065a5d56ac495dd2d541531aaec94c187612

---


# Adobe Experience Platform API基础知识

Adobe Experience Platform API采用了若干重要的底层技术和语法，以便有效管理基于JSON的平台资源。 本文档简要概述了这些技术，并提供了指向外部文档的链接以了解更多信息。

## JSON指针 {#json-pointer}

JSON指针是用于标识JSON文档中特定值的标准化字符串语法([RFC 6901](https://tools.ietf.org/html/rfc6901))。 JSON指针是由字符分隔的令牌字符串，它指定对象键或数组索引，令牌可以是字符串或数字。 `/` JSON指针字符串用于平台API的许多PATCH操作，如本文档后面所述。 有关JSON指针的详细信息，请参阅 [JSON指针概述文档](https://rapidjson.org/md_doc_pointer.html)。

### JSON模式对象示例

```json
{
    "type": "object",
    "title": "Loyalty Member Details",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Loyalty Program Mixin.",
    "definitions": {
        "loyalty": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "description": "The current loyalty program level to which the individual member belongs.",
                            "type": "string",
                            "enum": [
                                "platinum",
                                "gold",
                                "silver",
                                "bronze"
                            ],
                            "meta:enum": {
                                "platinum": "Platinum",
                                "gold": "Gold",
                                "silver": "Silver",
                                "bronze": "Bronze"
                            },
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    }
}
```

### 基于模式对象的JSON指针示例

| JSON指针 | 解析为 |
|--- | ---|
| `"/title"` | “忠诚会员详细信息” |
| `"/definitions/loyalty"` | (返回对象的内 `loyalty` 容) |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/definitions/loyalty/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!Note]
>处理Experience Data Model(XDM) `xdm:sourceProperty` 描述符 `xdm:destinationProperty` 的和属性时，必须从JSON Pointer字符串中排 `properties` 除任 **何键** 。 有关详细信息，请参阅模式注册API开发人员指南 [子指南](../xdm/api/descriptors.md) 。

## JSON修补程序

平台API有许多PATCH操作，它们接受JSON修补对象的请求负载。 JSON修补程序是用于描述对JSON文档所做更改的标准化格式([RFC 6902](https://tools.ietf.org/html/rfc6902))。 它允许您定义对JSON的部分更新，无需在请求主体中发送整个文档。

### JSON修补对象示例

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`:修补操作的类型。 虽然JSON修补程序支持多种不同的操作类型，但并非平台API中的所有PATCH操作都与每种操作类型兼容。 可用的操作类型有：
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`:要更新的JSON结构部分，使用 [JSON指针表示法进行标识](#json-pointer) 。

根据中指示的操作类 `op`型，JSON Patch对象可能需要其他属性。 有关不同JSON修补程序操作及其所需语法的详细信息，请参阅 [JSON修补程序文档](http://jsonpatch.com/)。

## JSON模式

JSON模式是用于描述和验证JSON数据结构的格式。 [体验数据模型(XDM)](../xdm/home.md) 利用JSON模式功能对所摄取的客户体验数据的结构和格式实施限制。 有关JSON模式的详细信息，请参阅官 [方文档](https://json-schema.org/)。

## 后续步骤

此文档引入了与管理Experience Platform的基于JSON的资源相关的一些技术和语法。 有关使用Platform API的更多信息（包括最佳实践和常见问题解答），请参阅 [Platform疑难解答指南](troubleshooting.md)。