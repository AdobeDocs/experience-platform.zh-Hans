---
title: XDM业务机会类
description: 本文档概述了Experience Data Model(XDM)中的XDM Business Opportunity类。
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: 50e5fe8573d828f88867ed33fe86e974c85de60a
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 4%

---

# [!UICONTROL XDM业务机会] 类

>[!IMPORTANT]
>
>此类旨在供具有访问权限的组织使用 [Real-time Customer Data Platform B2B版](../../../rtcdp/b2b-overview.md). 您必须拥有Real-time CDP B2B Edition的访问权限，才能让此类参与 [实时客户资料](../../../profile/home.md).

[!UICONTROL XDM业务机会] 是一个标准的体验数据模型(XDM)类，可捕获业务机会的最低要求属性。

![XDM Business Opportunity类在UI中显示的结构](../../images/classes/b2b/business-opportunity.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 此机会所关联的帐户的组合标识符。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系统审核属性]](../../data-types/external-source-system-audit-attributes.md) | 如果商机来自外部源系统，则此对象将捕获该系统的审核属性。 |
| `opportunityKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 机会实体的组合标识符。 |
| `_id` | 字符串 | 记录的唯一标识符。 这是系统生成的值，它与 `opportunityID`. |
| `accountID` | 字符串 | 此机会所关联的帐户的唯一ID。 |
| `isDeleted` | 布尔型 | 指示此营销列表实体是否已在Marketo Engage中删除。<br><br>使用 [Marketo源连接器](../../../sources/connectors/adobe-applications/marketo/marketo.md)，则在Marketo中删除的任何记录都会自动反映在实时客户资料中。 但是，与这些用户档案相关的记录仍可能会保留在数据湖中。 通过设置 `isDeleted` to `true`，则可以使用字段在查询数据湖时过滤掉已从源中删除的记录。 |
| `opportunityDescription` | 字符串 | 机会的描述。 |
| `opportunityID` | 字符串 | 机会实体的唯一ID。 |
| `opportunityName` | 字符串 | 机会的名称。 |
| `opportunityStage` | 字符串 | 销售机会的销售阶段。 |
| `opportunityType` | 字符串 | 机会类型。 |

{style=&quot;table-layout:auto&quot;}

请参阅 [Real-time CDP B2B Edition中的模式关系](../../tutorials/relationship-b2b.md) 了解此类在概念上如何与其他B2B类相关，以及如何在Adobe Experience Platform UI中建立这些关系。
