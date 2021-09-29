---
title: XDM业务营销列表成员类
description: 本文档概述了Experience Data Model(XDM)中的XDM Business Marketing List Members类。
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 3%

---

# [!UICONTROL XDM业务营销列] 表会员类（测试版）

>[!IMPORTANT]
>
>此课程作为Real-time Customer Data Platform B2B Edition的一部分提供，该B2B Edition目前处于测试阶段。 文档和功能可能会发生更改。

[!UICONTROL XDM业务营销列] 表会员资格是标准的体验数据模型(XDM)类，用于描述与营销列表关联的成员、人员或联系人。

![](../../images/classes/b2b/business-marketing-list-members.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系统审核属性]](../../data-types/external-source-system-audit-attributes.md) | 如果营销列表成员资格来自外部源系统，则此对象会捕获该系统的审核属性。 |
| `marketingListKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 人员所属的营销列表的复合标识符。 |
| `marketingListMemberKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 营销列表成员资格实体的组合标识符。 |
| `personKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 作为营销列表成员的人员的组合标识符。 |
| `_id` | 字符串 | 记录的唯一标识符。 这是系统生成的值，与`marketingListMemberID`分开。 |
| `marketingListID` | 字符串 | 营销列表的唯一ID。 |
| `marketingListMemberID` | 字符串 | 营销列表成员资格实体的唯一ID。 |
| `personId` | 字符串 | 人员的唯一ID。 |

{style=&quot;table-layout:auto&quot;}

请参阅Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md)中[模式关系指南，了解此类在概念上如何与其他B2B类相关联，以及如何在Adobe Experience Platform UI中建立这些关系。
