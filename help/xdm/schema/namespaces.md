---
keywords: Experience Platform；主页；热门主题；架构；架构；xdm；体验数据模型；命名空间；命名空间；兼容模式；xed；
solution: Experience Platform
title: Experience Data Model (XDM)中的命名空间
description: 了解Experience Data Model (XDM)中的命名空间如何允许您扩展架构并在不同架构组件组合在一起时防止字段冲突。
exl-id: b351dfaf-5219-4750-a7a9-cf4689a5b736
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# Experience Data Model (XDM)中的命名空间

>[!IMPORTANT]
>
>在XDM中，命名空间（本页的主题）用于区分架构中的字段。 这与Identity Service中的身份命名空间概念不同，该概念使用命名空间来区分身份值。 有关详细信息，请阅读有关Identity Service](../../identity-service/features/namespaces.md)中的[命名空间的文档。

体验数据模型(XDM)架构中的所有字段都有关联的命名空间。 利用这些命名空间，可扩展架构并在将不同的架构组件组合在一起时防止字段冲突。 本文档概述了XDM中的命名空间以及它们在[架构注册表API](../api/overview.md)中的表示方式。

命名空间允许您在一个命名空间中定义一个字段，因为这意味着与不同命名空间中的相同字段不同。 实际上，字段的命名空间指示创建字段的人员(例如标准XDM (Adobe)、供应商或您的组织)。

例如，考虑使用[[!UICONTROL 个人联系人详细信息]字段组](../field-groups/profile/demographic-details.md)的XDM架构，该字段组的标准`mobilePhone`字段存在于`xdm`命名空间中。 在同一架构中，您也可以在不同的命名空间（您的[租户ID](../api/getting-started.md#know-your-tenant_id)）下创建单独的`mobilePhone`字段。 这两个字段可以共存，但具有不同的底层含义或约束。

## 命名空间语法

以下部分演示了如何在XDM语法中分配命名空间。

### 标准XDM {#standard}

标准XDM语法为insight提供了命名空间在架构中的表示方式(包括[它们在Adobe Experience Platform](#compatibility)中的翻译方式)。

标准XDM使用[JSON-LD](https://www.w3.org/TR/json-ld11/#basic-concepts)语法为字段分配命名空间。 此命名空间采用URI的形式（如`xdm`命名空间的`https://ns.adobe.com/xdm`），或作为在架构的`@context`属性中配置的速记前缀。

以下是标准XDM语法中产品的模式示例。 除`@id`（由JSON-LD规范定义的唯一标识符）之外，`properties`下的每个字段均以命名空间开头并以字段名称结尾。 如果使用在`@context`下定义的速记前缀，则命名空间和字段名称用冒号(`:`)分隔。 如果不使用前缀，则命名空间和字段名称用斜杠(`/`)分隔。

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
| `@context` | 一个对象，它定义了`properties`下可以使用的速记前缀，而不是完整的命名空间URI。 |
| `@id` | [JSON-LD规范](https://www.w3.org/TR/json-ld11/#node-identifiers)定义的记录的唯一标识符。 |
| `xdm:sku` | 使用速记前缀表示命名空间的字段示例。 在这种情况下，`xdm`是命名空间(`https://ns.adobe.com/xdm`)，`sku`是字段名。 |
| `https://ns.adobe.com/xdm/channels/application` | 使用完整命名空间URI的字段示例。 在这种情况下，`https://ns.adobe.com/xdm/channels`是命名空间，`application`是字段名。 |
| `https://ns.adobe.com/vendorA/product/stockNumber` | 供应商资源提供的字段使用自己的唯一命名空间。 在此示例中，`https://ns.adobe.com/vendorA/product`是供应商命名空间，`stockNumber`是字段名。 |
| `tenantId:internalSku` | 您的组织定义的字段使用您的唯一租户ID作为其命名空间。 在此示例中，`tenantId`是租户命名空间(`https://ns.adobe.com/tenantId`)，`internalSku`是字段名。 |

{style="table-layout:auto"}

### 兼容模式 {#compatibility}

在Adobe Experience Platform中，XDM架构以[兼容模式](../api/appendix.md#compatibility)语法表示，该语法不使用JSON-LD语法表示命名空间。 相反，Experience Platform将命名空间转换为父字段（以下划线开头），并将字段嵌套在其下。

例如，标准XDM `repo:createdDate`已转换为`_repo.createdDate`，并在兼容模式下显示在以下结构下：

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

使用`xdm`命名空间的字段在`properties`下显示为根字段，并删除以[标准XDM语法](#standard)显示的`xdm:`前缀。 例如，`xdm:sku`仅被列为`sku`。

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

本指南概述了XDM命名空间以及它们在JSON中的表示方式。 有关如何使用API配置XDM架构的更多信息，请参阅[架构注册表API指南](../api/overview.md)。
