---
title: XDM业务机会人员关系类
description: 本文档概述了Experience Data Model(XDM)中的XDM Business Opportunity Person Relation类。
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 3%

---

# [!UICONTROL XDM业务机会人员关] 系类

>[!NOTE]
>
>此类仅适用于有权访问B2B版实时客户数据平台的组织。

[!UICONTROL XDM Business Opportunity Person Relations是一] 个标准的体验数据模型(XDM)类，可捕获与业务机会关联的人员的最低要求属性。

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
