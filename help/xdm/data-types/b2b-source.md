---
title: B2B源数据类型
description: 了解B2B Source Experience Data Model (XDM)数据类型。
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 3%

---

# [!UICONTROL B2B源] 数据类型

[!UICONTROL B2B源] 是一个标准体验数据模型(XDM)数据类型，它表示B2B实体(例如 [帐户](../classes/b2b/business-account.md)，和 [机会](../classes/b2b/business-opportunity.md)，或 [营销活动](../classes/b2b/business-campaign.md))。

如果仅依赖基于字符串的标识符，则跨多个系统的ID之间可能会重叠（例如，可以在一个CRM系统上为某个机会指定字符串ID，但同一ID可能引用完全不同的机会）。 这可能会导致在中合并数据时发生数据冲突 [Real-time Customer Profile](../../profile/home.md).

此 [!UICONTROL B2B源] 数据类型允许您使用实体的原始字符串ID，并将其与特定于源的上下文信息相结合，以确保它在Platform系统中保持完全唯一，而不管它来自哪个源。

![B2B源结构](../images/data-types/b2b-source.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `sourceID` | 字符串 | 源记录的唯一ID。 |
| `sourceInstanceID` | 字符串 | 源数据的实例或组织ID。 |
| `sourceKey` | 字符串 | 由以下各项组成的唯一标识符 `sourceId`， `sourceInstanceId`、和 `sourceType` 按以下格式连接在一起： `[sourceID]@[sourceInstanceID].[sourceType]`.<br><br>某些源连接器(如Marketo)会自动为某些标识符连接此值。 其他则必须使用 [数据准备 `concat` 函数](../../data-prep/functions.md#string)例如： `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | 字符串 | 提供源数据的平台的名称。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
