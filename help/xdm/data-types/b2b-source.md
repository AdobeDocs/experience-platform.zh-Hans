---
title: B2B源数据类型
description: 本文档概述了B2B源体验数据模型(XDM)数据类型。
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 3%

---

# [!UICONTROL B2B源数] 据类型

>[!NOTE]
>
>此数据类型仅适用于有权访问B2B版实时客户数据平台的组织。

[!UICONTROL B2B源] 是标准的体验数据模型(XDM)数据类型，它表示B2B实体(如帐户 [、](../classes/b2b/business-account.md)机会 [或营销活动](../classes/b2b/business-opportunity.md) [](../classes/b2b/business-campaign.md))的组合标识符。

当仅依赖基于字符串的标识符时，跨多个系统的ID之间可能存在重叠（例如，在一个CRM系统上，可以为一个机会提供一个字符串ID，但同一ID可能指的是一个完全不同的机会）。 在[实时客户资料](../../profile/home.md)中合并数据时，这可能会导致数据冲突。

[!UICONTROL B2B Source]数据类型允许您使用实体的原始字符串ID，并将其与特定于源的上下文信息合并，以确保它在平台系统中完全保持唯一，而不管它源自何种源。

![B2B源结构](../images/data-types/b2b-source.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `sourceID` | 字符串 | 源记录的唯一ID。 |
| `sourceInstanceID` | 字符串 | 源数据的实例或组织ID。 |
| `sourceKey` | 字符串 | 由`sourceId`、`sourceInstanceId`和`sourceType`组成的唯一标识符，采用以下格式连接在一起：`[sourceID]@$[sourceInstanceID].[sourceType]`。<br><br>某些源连接器(如Marketo)会为某些标识符自动连接此值。必须使用[数据准备`concat`函数](../../data-prep/functions.md#string)手动连接其他函数，例如：`concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | 字符串 | 提供源数据的平台的名称。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
