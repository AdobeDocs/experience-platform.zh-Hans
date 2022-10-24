---
title: XDM业务帐户人员关系分类
description: 本文档概述了Experience Data Model(XDM)中的XDM业务帐户人员关系类。
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 3%

---

# [!UICONTROL XDM业务帐户人员关系] 类

>[!IMPORTANT]
>
>此类旨在供具有访问权限的组织使用 [Adobe Real-time Customer Data Platform B2B版](../../../rtcdp/b2b-overview.md). 您必须拥有Real-Time CDP B2B Edition的访问权限，才能参加此类 [实时客户资料](../../../profile/home.md).

[!UICONTROL XDM业务帐户人员关系] 是一个标准的体验数据模型(XDM)类，可捕获与业务帐户关联的人员所需的最低属性。

![XDM业务帐户人员关系类的结构，如在UI中所示](../../images/classes/b2b/business-account-person-relation.png)

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
| `isDeleted` | 布尔型 | 指示此帐户与人员关系是否已在Marketo Engage中删除。<br><br>使用 [Marketo源连接器](../../../sources/connectors/adobe-applications/marketo/marketo.md)，则在Marketo中删除的任何记录都会自动反映在实时客户资料中。 但是，与这些用户档案相关的记录仍可能会保留在数据湖中。 通过设置 `isDeleted` to `true`，则可以使用字段在查询数据湖时过滤掉已从源中删除的记录。 |
| `isDirect` | 布尔型 | 指示这是否是帐户与人员之间的直接关系。 |
| `isPrimary` | 布尔型 | 指示此人是否是此帐户上的主要联系人。 |
| `personID` | 字符串 | 帐户与人员关系中人员的唯一标识符。 |
| `personRoles` | 字符串数组 | 列出帐户与人员关系中人员的角色。 |
| `relationEndDate` | DateTime | 帐户与人员之间的关系结束的日期。 |
| `relationStartDate` | DateTime | 帐户与人员之间的关系开始的日期。 |
| `relationshipSource` | 字符串 | 帐户 — 人员关系的来源。 |

{style=&quot;table-layout:auto&quot;}

请参阅 [Real-Time CDP B2B版中的模式关系](../../tutorials/relationship-b2b.md) 了解此类在概念上如何与其他B2B类相关，以及如何在Adobe Experience Platform UI中建立这些关系。
