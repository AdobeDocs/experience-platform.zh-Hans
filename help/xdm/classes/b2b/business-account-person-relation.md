---
title: XDM业务帐户人员关系分类
description: 本文档概述了Experience Data Model(XDM)中的XDM业务帐户人员关系类。
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 3%

---

# [!UICONTROL XDM业务帐户人员关] 系类

>[!NOTE]
>
>此类仅适用于有权访问B2B版实时客户数据平台的组织。

[!UICONTROL XDM业务帐户人] 员关系是一种标准的体验数据模型(XDM)类，可捕获与业务帐户关联的人员的最低要求属性。

![](../../images/classes/b2b/business-account-person-relation.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 帐户与人员关系中帐户的组合标识符。 |
| `accountPersonKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 帐户 — 人员关系实体的组合标识符。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系统审核属性]](../../data-types/external-source-system-audit-attributes.md) | 如果帐户与人员关系来自外部源系统，则此对象会捕获该系统的审核属性。 |
| `personKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 帐户与人员关系中人员的组合标识符。 |
| `_id` | 字符串 | 记录的唯一标识符。 这是系统生成的值，与类捕获的其他ID字段分开。 |
| `accountID` | 字符串 | 帐户与人员关系中帐户的唯一标识符。 |
| `accountPersonID` | 字符串 | 帐户 — 人员关系实体的唯一标识符。 |
| `currencyCode` | 字符串 | 用于帐户与人员之间关系的ISO 4217货币代码。 |
| `isActive` | 布尔型 | 指示帐户与人员之间的关系是否有效。 |
| `isDirect` | 布尔型 | 指示这是否是帐户与人员之间的直接关系。 |
| `isPrimary` | 布尔型 | 指示此人是否是此帐户上的主要联系人。 |
| `personID` | 字符串 | 帐户与人员关系中人员的唯一标识符。 |
| `personRole` | 字符串 | 人员在帐户与人员关系中的角色。 |
| `relationEndDate` | DateTime | 帐户与人员之间的关系结束的日期。 |
| `relationStartDate` | DateTime | 帐户与人员之间的关系开始的日期。 |
