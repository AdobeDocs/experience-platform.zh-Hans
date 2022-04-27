---
title: XDM Business Campaign成员类
description: 本文档概述了Experience Data Model(XDM)中的XDM Business Campaign成员类。
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: 0084492ed467c5996a94c5c55a79c9faf8f5046e
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 2%

---

# [!UICONTROL XDM Business Campaign成员] 类

>[!IMPORTANT]
>
>此类旨在供具有访问权限的组织使用 [Real-time Customer Data Platform B2B版](../../../rtcdp/b2b-overview.md). 您必须拥有Real-time CDP B2B Edition的访问权限，才能让此类参与 [实时客户资料](../../../profile/home.md).

[!UICONTROL XDM Business Campaign成员] 是一个标准的体验数据模型(XDM)类，用于描述与业务活动关联的联系人或潜在客户。

![XDM Business Campaign成员类在UI中显示的结构](../../images/classes/b2b/business-campaign-members.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 关联营销活动的组合标识符。 |
| `campaignMemberKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 促销活动成员身份实体的组合标识符。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系统审核属性]](../../data-types/external-source-system-audit-attributes.md) | 如果促销活动成员资格来自外部源系统，则此对象会捕获该系统的审核属性。 |
| `personKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 作为关联营销活动成员的人员的复合标识符。 |
| `_id` | 字符串 | 记录的唯一标识符。 这是系统生成的值，它与 `campaignMemberID`. |

{style=&quot;table-layout:auto&quot;}

要了解此类在概念上如何与其他B2B类相关以及如何在Adobe Experience Platform UI中建立这些关系，请参阅 [Real-time CDP B2B Edition中的模式关系](../../tutorials/relationship-b2b.md)

有关与此类兼容的其他字段，请参阅的字段组引用 [[!UICONTROL XDM Business Campaign成员详细信息]](../../field-groups/b2b-campaign-members/details.md).
