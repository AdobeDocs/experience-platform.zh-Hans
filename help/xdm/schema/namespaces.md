---
keywords: Experience Platform；主页；热门主题；架构；架构；xdm；体验数据模型；命名空间；命名空间；兼容性模式；已修复；
solution: Experience Platform
title: Experience Data Model(XDM)中的名称步调
description: 了解体验数据模型(XDM)中的名称步调如何允许您在将不同架构组件汇集在一起时扩展架构并防止字段冲突。
exl-id: b351dfaf-5219-4750-a7a9-cf4689a5b736
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---

# Experience Data Model(XDM)中的名称步调

体验数据模型(XDM)架构中的所有字段都具有关联的命名空间。 这些命名空间允许您扩展架构，并在不同架构组件汇集在一起时防止字段冲突。 本文档概述了XDM中的命名空间以及它们在 [架构注册表API](../api/overview.md).

命名空间允许您在一个命名空间中定义一个字段，作为表示不同命名空间中不同于同一字段的内容。 实际上，字段的命名空间会指示字段的创建者(例如标准XDM(Adobe)、供应商或您的组织)。

例如，假定XDM架构使用 [[!UICONTROL 个人联系详细信息] 字段组](../field-groups/profile/demographic-details.md)，它具有标准 `mobilePhone` 中存在的字段 `xdm` 命名空间。 在同一架构中，您还可以自由创建单独的 `mobilePhone` 字段(您的 [租户ID](../api/getting-started.md#know-your-tenant_id))。 这两个字段可以共存，同时具有不同的基本含义或限制。

## 名称步调语法

以下各节演示了如何使用XDM语法分配命名空间。

### 标准XDM {#standard}

标准XDM语法可深入分析命名空间在架构中的表示方式(包括 [如何在Adobe Experience Platform翻译](#compatibility))。

标准XDM使用 [JSON-LD](https://json-ld.org/) 用于将命名空间分配给字段的语法。 此命名空间以URI的形式提供(例如 `https://ns.adobe.com/xdm` 对于 `xdm` 命名空间)，或作为在 `@context` 架构的属性。

以下是标准XDM语法中产品的示例架构。 除 `@id` （由JSON-LD规范定义的唯一标识符）， `properties` 以命名空间开头，以字段名称结尾。 如果使用 `@context`，命名空间和字段名称之间用冒号(`:`)。 如果不使用前缀，则命名空间和字段名称将以斜杠(`/`)。

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
| `@context` | 一个对象，它定义了可用的简写前缀，而不是下面的完整命名空间URI `properties`. |
| `@id` | 记录的唯一标识符，由 [JSON-LD规范](https://json-ld.org/spec/latest/json-ld/#node-identifiers). |
| `xdm:sku` | 使用短前缀表示命名空间的字段示例。 在这种情况下， `xdm` 是命名空间(`https://ns.adobe.com/xdm`)和 `sku` 是字段名称。 |
| `https://ns.adobe.com/xdm/channels/application` | 使用完整命名空间URI的字段示例。 在这种情况下， `https://ns.adobe.com/xdm/channels` 是命名空间，和 `application` 是字段名称。 |
| `https://ns.adobe.com/vendorA/product/stockNumber` | 供应商资源提供的字段使用它们自己的唯一命名空间。 在本例中， `https://ns.adobe.com/vendorA/product` 是供应商命名空间，并且 `stockNumber` 是字段名称。 |
| `tenantId:internalSku` | 贵组织定义的字段会使用您的唯一租户ID作为其命名空间。 在本例中， `tenantId` 是租户命名空间(`https://ns.adobe.com/tenantId`)和 `internalSku` 是字段名称。 |

{style=&quot;table-layout:auto&quot;}

### 兼容性模式 {#compatibility}

在Adobe Experience Platform中，XDM模式在 [兼容性模式](../api/appendix.md#compatibility) 语法，该语法不使用JSON-LD语法来表示命名空间。 Platform而是将命名空间转换为父字段（以下划线开头），并将字段嵌套到其下。

例如，标准XDM `repo:createdDate` 转换为 `_repo.createdDate` 和将显示在兼容模式下的以下结构下：

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

使用 `xdm` 命名空间显示为根字段， `properties` 然后放下 `xdm:` 显示在 [标准XDM语法](#standard). 例如， `xdm:sku` 只是列为 `sku` 中。

以下JSON表示如何将上面显示的标准XDM语法示例转换为兼容性模式。

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

本指南概述了XDM命名空间以及它们在JSON中的显示方式。 有关如何使用API配置XDM模式的更多信息，请参阅 [架构注册API指南](../api/overview.md).
