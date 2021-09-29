---
title: XDM Business Campaign成员类
description: 本文档概述了Experience Data Model(XDM)中的XDM Business Campaign成员类。
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 3%

---

# [!UICONTROL XDM Business Campaign会] 员级（测试版）

>[!IMPORTANT]
>
>此课程作为Real-time Customer Data Platform B2B Edition的一部分提供，该B2B Edition目前处于测试阶段。 文档和功能可能会发生更改。

[!UICONTROL XDM Business Campaign会员] 资格是标准的体验数据模型(XDM)类，用于描述与业务活动关联的联系人或潜在客户。

![](../../images/classes/b2b/business-campaign-members.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 关联营销活动的组合标识符。 |
| `campaignMemberKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 促销活动成员身份实体的组合标识符。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系统审核属性]](../../data-types/external-source-system-audit-attributes.md) | 如果促销活动成员资格来自外部源系统，则此对象会捕获该系统的审核属性。 |
| `personKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 作为关联营销活动成员的人员的复合标识符。 |
| `_id` | 字符串 | 记录的唯一标识符。 这是系统生成的值，与`campaignMemberID`分开。 |
| `campaignID` | 字符串 | 关联营销活动的唯一ID。 |
| `campaignMemberID` | 字符串 | 促销活动成员资格实体的唯一ID。 |
| `personId` | 字符串 | 关联营销活动成员的人员的唯一ID。 |

{style=&quot;table-layout:auto&quot;}

请参阅Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md)中[模式关系指南，了解此类在概念上如何与其他B2B类相关联，以及如何在Adobe Experience Platform UI中建立这些关系。
