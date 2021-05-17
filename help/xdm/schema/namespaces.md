---
keywords: Experience Platform；主页；热门主题；模式;模式;xdm；体验数据模型；命名空间;命名空间；兼容模式；固定；
solution: Experience Platform
title: 体验数据模型(XDM)中的命名空间
topic-legacy: overviews
description: 了解体验模式模型(XDM)中命名空间如何让您在将不同模式组件整合在一起时扩展并防止字段冲突。
source-git-commit: b4c4f8f7e428d27f389bff5591a03925b6afa6d8
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---


# 体验数据模型(XDM)中的命名空间

体验数据模型(XDM)模式中的所有字段都有关联的命名空间。 这些命名空间允许您扩展模式并防止字段冲突，因为不同的模式组件将在一起。 此文档概述了
XDM及其在[模式注册表API](../api/overview.md)中的表示方式。

命名空间允许您在一个命名空间中定义一个字段，表示不同命名空间中的同一字段不同的内容。 实际上，字段的命名空间会指示字段的创建者(如标准XDM(Adobe)、供应商或您的组织)。

例如，考虑使用[[!UICONTROL 个人联系详细信息]字段组](../field-groups/profile/demographic-details.md)的XDM模式，该字段具有存在于`xdm`命名空间中的标准`mobilePhone`字段。 在同一模式下，您还可以在其他命名空间（您的[租户ID](../api/getting-started.md#know-your-tenant_id)）下自由创建单独的`mobilePhone`字段。 这两个字段可以共存，同时具有不同的基本含义或约束。

## 命名空间语法

以下几节说明如何以XDM语法分配命名空间。

### 标准XDM {#standard}

标准XDM语法提供了有关命名空间在模式中如何表示的洞察(包括在Adobe Experience Platform](#compatibility)中如何翻译它们)。[

标准XDM使用[JSON-LD](https://json-ld.org/)语法将命名空间分配给字段。 此命名空间以URI(如`xdm`命名空间的`https://ns.adobe.com/xdm`)或在模式的`@context`属性中配置的速记前缀的形式提供。

以下是标准XDM语法中产品的示例模式。 除`@id`（JSON-LD规范定义的唯一标识符）外，`properties`开始下的每个字段均带有命名空间，以字段名称结尾。 如果使用在`@context`下定义的速记前缀，则命名空间和字段名称以冒号(`:`)分隔。 如果不使用前缀，则命名空间和字段名称以斜杠(`/`)分隔。

```json
{
  "$id": "https://ns.adobe.com/xdm/schemas/mySchema",
  "title": "Product",
  "description": "Represents the definition of a Project",
  "@context": {
    "xdm": "https://ns.adobe.com/xdm",
    "repo": "http://ns.adobe.com/adobecloud/core/1.0/",
    "schema": "http://schema.org",
    "tenantId": "https://ns.adobe.com/tenantId"
  },
  "properties": {
    "@id": {
      "type": "string"
    },
    "xdm:sku": {
      "type": "string"
    },
    "xdm:name": {
      "type": "string"
    },
    "repo:createdDate": {
      "type": "string",
      "format": "datetime"
    },
    "https://ns.adobe.com/xdm/channels/application": {
      "type": "string"
    },
    "schema:latitude": {
      "type": "number"
    },
    "https://ns.adobe.com/vendorA/product/stockNumber": {
      "type": "string"
    },
    "tenantId:internalSku": {
      "type": "number"
    }
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `@context` | 一个对象，它定义可以用来代替`properties`下的完整命名空间URI的短记前缀。 |
| `@id` | 由[JSON-LD规范](https://json-ld.org/spec/latest/json-ld/#node-identifiers)定义的记录的唯一标识符。 |
| `xdm:sku` | 使用短前缀表示命名空间的字段示例。 在这种情况下，`xdm`是命名空间(`https://ns.adobe.com/xdm`),`sku`是字段名。 |
| `https://ns.adobe.com/xdm/channels/application` | 使用完整命名空间URI的字段示例。 在这种情况下，`https://ns.adobe.com/xdm/channels`是命名空间,`application`是字段名称。 |
| `https://ns.adobe.com/vendorA/product/stockNumber` | 供应商资源提供的字段使用其自己的唯一命名空间。 在此示例中，`https://ns.adobe.com/vendorA/product`是供应商命名空间,`stockNumber`是字段名。 |
| `tenantId:internalSku` | 您的组织定义的字段使用您的唯一租户ID作为其命名空间。 在此示例中，`tenantId`是租户命名空间(`https://ns.adobe.com/tenantId`),`internalSku`是字段名。 |

{style=&quot;table-layout:auto&quot;}

### 兼容性模式 {#compatibility}

在Adobe Experience Platform中，XDM模式以[兼容模式](../api/appendix.md#compatibility)语法表示，该语法不使用JSON-LD语法来表示命名空间。 而是，平台将命名空间转换为父字段（以下划线开头）并嵌套其下的字段。

例如，标准XDM `repo:createdDate`将转换为`_repo.createdDate`，并将显示在兼容模式下的以下结构下：

```json
"_repo": {
  "type": "object",
  "properties": {
    "createdDate": {
      "type": "string",
      "format": "datetime"
    }
  }
}
```

使用`xdm`命名空间的字段在`properties`下显示为根字段，并删除[标准XDM语法](#standard)中将显示的`xdm:`前缀。 例如，`xdm:sku`仅作为`sku`列出。

以下JSON表示如何将上面显示的标准XDM语法示例转换为兼容模式。

```json
{
  "$id": "https://ns.adobe.com/xdm/schemas/mySchema",
  "title": "Product",
  "description": "Represents the definition of a Project",
  "properties": {
    "_id": {
      "type": "string"
    },
    "sku": {
      "type": "string"
    },
    "name": {
      "type": "string"
    },
    "_repo": {
      "type": "object",
      "properties": {
        "createdDate": {
          "type": "string",
          "format": "datetime"
        }
      }
    },
    "_channels": {
      "type": "object",
      "properties": {
        "application": {
          "type": "string"
        }
      }
    },
    "_schema": {
      "type": "object",
      "properties": {
        "application": {
          "type": "string"
        }
      }
    },
    "_vendorA": {
      "type": "object",
      "properties": {
        "product": {
          "type": "object",
          "properties": {
            "stockNumber": {
              "type": "string"
            }
          }
        }
      }
    },
    "_tenantId": {
      "type": "object",
      "properties": {
        "internalSku": {
          "type": "number"
        }
      }
    }
  }
}
```

## 后续步骤

本指南概述了XDM命名空间以及它们在JSON中的表示方式。 有关如何使用API配置XDM模式的详细信息，请参阅[模式注册表API指南](../api/overview.md)。
