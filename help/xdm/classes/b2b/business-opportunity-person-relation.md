---
title: XDM业务机会人员关系类
description: 本文档概述了Experience Data Model(XDM)中的XDM Business Opportunity Person Relation类。
exl-id: 7be193d2-52eb-4b28-953b-5e0fc21d8f93
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 3%

---

# [!UICONTROL XDM业务机会人员关系] 类

>[!IMPORTANT]
>
>此类旨在供具有访问权限的组织使用 [Real-time Customer Data Platform B2B版](../../../rtcdp/b2b-overview.md). 您必须拥有Real-time CDP B2B Edition的访问权限，才能让此类参与 [实时客户资料](../../../profile/home.md).

[!UICONTROL XDM业务机会人员关系] 是一个标准的体验数据模型(XDM)类，可捕获与业务机会关联的人员的最低要求属性。

![](../../images/classes/b2b/business-opportunity-person-relation.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系统审核属性]](../../data-types/external-source-system-audit-attributes.md) | 如果业务人员关系来自外部源系统，则此对象会捕获该系统的审核属性。 |
| `opportunityKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 机会 — 人员关系中机会的组合标识符。 |
| `opportunityPersonKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 机会 — 人员关系实体的组合标识符。 |
| `personKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 机会 — 人员关系中人员的组合标识符。 |
| `_id` | 字符串 | 记录的唯一标识符。 这是系统生成的值，与类捕获的其他ID字段分开。 |
| `opportunityID` | 字符串 | 机会 — 人员关系中机会的唯一标识符。 |
| `opportunityPersonID` | 字符串 | 机会 — 人员关系实体的唯一标识符 |
| `isPrimary` | 布尔型 | 指示人员是否是此机会的主要联系人。 |
| `personID` | 字符串 | 机会 — 人员关系中人员的唯一标识符。 |
| `personRole` | 字符串 | 人员在机会 — 人员关系中的角色。 |

{style=&quot;table-layout:auto&quot;}

请参阅 [Real-time CDP B2B Edition中的模式关系](../../tutorials/relationship-b2b.md) 了解此类在概念上如何与其他B2B类相关，以及如何在Adobe Experience Platform UI中建立这些关系。
