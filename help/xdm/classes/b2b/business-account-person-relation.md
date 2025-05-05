---
title: XDM业务帐户人员关系类
description: 了解Experience Data Model (XDM)中的XDM业务帐户人员关系类。
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 12%

---

# [!UICONTROL XDM业务帐户人员关系]类

>[!IMPORTANT]
>
>此类供具有[Adobe Real-time Customer Data Platform B2B版本](../../../rtcdp/b2b-overview.md)访问权限的组织使用。 您必须有权访问Real-Time CDP B2B版本，此类才能参与[实时客户个人资料](../../../profile/home.md)。

[!UICONTROL XDM业务帐户人员关系]是一个标准体验数据模型(XDM)类，可捕获与业务帐户关联的人员的最低要求属性。

![ XDM业务帐户人员关系类在UI中显示的结构](../../images/classes/b2b/business-account-person-relation.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 帐户 — 人员关系中帐户的复合标识符。 |
| `accountPersonKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 帐户 — 人员关系实体的复合标识符。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部Source系统审核属性]](../../data-types/external-source-system-audit-attributes.md) | 如果帐户 — 人员关系来自外部源系统，则此对象将捕获该系统的审核属性。 |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 帐户 — 人员关系中人员的复合标识符。 |
| `_id` | 字符串 | 记录的唯一标识符。 这是一个系统生成的值，与类捕获的其他ID字段不同。 |
| `accountID` | 字符串 | 帐户 — 人员关系中帐户的唯一标识符。 |
| `accountPersonID` | 字符串 | 帐户 — 人员关系实体的唯一标识符。 |
| `currencyCode` | 字符串 | 用于帐户与人员之间的关系的 ISO 4217 货币代码。 |
| `isActive` | 布尔值 | 指示帐户和人员之间的关系是否有效。 |
| `isDeleted` | 布尔值 | 指示此帐户 — 人员关系是否已在Marketo Engage中删除。<br><br>使用[Marketo源连接器](../../../sources/connectors/adobe-applications/marketo/marketo.md)时，在Marketo中删除的任何记录都会自动反映在实时客户配置文件中。 但是，与这些用户档案相关的记录仍可能会保留在数据湖中。 通过将`isDeleted`设置为`true`，您可以在查询数据湖时使用该字段过滤出已从源中删除的记录。 |
| `isDirect` | 布尔值 | 指示这是否是帐户和人员之间的直接关系。 |
| `isPrimary` | 布尔值 | 指示此人是否为此帐户的主要联系人。 |
| `personID` | 字符串 | 帐户 — 人员关系中人员的唯一标识符。 |
| `personRoles` | 字符串数组 | 列出帐户 — 人员关系中人员的角色。 |
| `relationEndDate` | 日期时间 | 帐户与人员之间的关系结束的日期。 |
| `relationStartDate` | 日期时间 | 帐户与人员之间的关系开始的日期。 |
| `relationshipSource` | 字符串 | 帐户 — 人员关系的来源。 |

{style="table-layout:auto"}

请参阅有关Real-Time CDP B2B版本[&#128279;](../../tutorials/relationship-b2b.md)中的架构关系的指南，以了解此类如何在概念上与其他B2B类相关联，以及如何在Adobe Experience Platform UI中建立这些关系。
