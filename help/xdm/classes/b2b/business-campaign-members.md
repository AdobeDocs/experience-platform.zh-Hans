---
title: XDM商业营销活动成员类
description: 了解Experience Data Model (XDM)中的XDM商业营销活动成员类。
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 2%

---

# [!UICONTROL XDM商业营销活动成员]类

>[!IMPORTANT]
>
>此类供具有[Adobe Real-time Customer Data Platform B2B版本](../../../rtcdp/b2b-overview.md)访问权限的组织使用。 您必须有权访问Real-Time CDP B2B版本，此类才能参与[实时客户个人资料](../../../profile/home.md)。

[!UICONTROL XDM商业营销活动成员]是一个标准体验数据模型(XDM)类，它描述了与商业营销活动关联的联系人或商机。

![ XDM商业营销活动成员类在UI中显示的结构](../../images/classes/b2b/business-campaign-members.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 关联营销活动的复合标识符。 |
| `campaignMemberKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 营销活动成员资格实体的复合标识符。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部Source系统审核属性]](../../data-types/external-source-system-audit-attributes.md) | 如果促销活动成员资格来自外部源系统，则此对象将捕获该系统的审核属性。 |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 作为相关营销活动成员的人员的复合标识符。 |
| `_id` | 字符串 | 记录的唯一标识符。 这是系统生成的值，与`campaignMemberID`不同。 |

{style="table-layout:auto"}

要了解此类如何在概念上与其他B2B类相关联，以及如何在Adobe Experience Platform UI中建立这些关系，请参阅Real-Time CDP B2B版本[&#128279;](../../tutorials/relationship-b2b.md)中有关架构关系的指南

有关与此类兼容的其他字段，请参阅[[!UICONTROL XDM商业营销活动成员详细信息]](../../field-groups/b2b-campaign-members/details.md)的字段组引用。
