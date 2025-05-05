---
title: XDM商业营销活动类
description: 了解Experience Data Model (XDM)中的XDM商业营销活动类。
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---

# [!UICONTROL XDM商业营销活动]类

>[!IMPORTANT]
>
>此类供具有[Adobe Real-time Customer Data Platform B2B版本](../../../rtcdp/b2b-overview.md)访问权限的组织使用。 您必须有权访问Real-Time CDP B2B版本，此类才能参与[实时客户个人资料](../../../profile/home.md)。

[!UICONTROL XDM商业营销活动]是一个标准体验数据模型(XDM)类，可捕获商业营销活动的最低要求属性。

![ XDM商业营销活动类在UI中显示的结构](../../images/classes/b2b/business-campaign.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 营销活动实体的复合标识符。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部Source系统审核属性]](../../data-types/external-source-system-audit-attributes.md) | 如果促销活动来自外部源系统，则此对象将捕获该系统的审核属性。 |
| `_id` | 字符串 | 记录的唯一标识符。 这是系统生成的值，与`campaignID`不同。 |
| `campaignDescription` | 字符串 | 营销活动的描述。 |
| `campaignID` | 字符串 | 营销活动实体的唯一标识符。 |
| `campaignName` | 字符串 | 营销活动的名称。 |
| `campaignType` | 字符串 | 营销活动类型或目标受众。 |

{style="table-layout:auto"}

要了解此类如何在概念上与其他B2B类相关联，以及如何在Adobe Experience Platform UI中建立这些关系，请参阅Real-Time CDP B2B版本[&#128279;](../../tutorials/relationship-b2b.md)中有关架构关系的指南

有关与此类兼容的其他字段，请参阅[[!UICONTROL XDM商业营销活动详细信息]](../../field-groups/b2b-campaign/details.md)的字段组引用。
