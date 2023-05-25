---
title: XDM业务机会人员关系类
description: 本文档概述了Experience Data Model (XDM)中的XDM业务机会人员关系类。
exl-id: 7be193d2-52eb-4b28-953b-5e0fc21d8f93
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 2%

---

# [!UICONTROL XDM业务机会人员关系] 类

>[!IMPORTANT]
>
>此类供有权访问的组织使用 [Adobe Real-time Customer Data Platform B2B版本](../../../rtcdp/b2b-overview.md). 您必须有权访问Real-Time CDP B2B版本，此类才能参与 [Real-time Customer Profile](../../../profile/home.md).

[!UICONTROL XDM业务机会人员关系] 是一个标准体验数据模型(XDM)类，可捕获与业务机会关联的人员的最低要求属性。

![XDM业务机会人员类的结构，如UI中所示](../../images/classes/b2b/business-opportunity-person-relation.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系统审计属性]](../../data-types/external-source-system-audit-attributes.md) | 如果业务人员关系来自外部源系统，则此对象捕获该系统的审核属性。 |
| `opportunityKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 机会 — 人员关系中机会的复合标识符。 |
| `opportunityPersonKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 机会 — 人员关系实体的复合标识符。 |
| `personKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 机会 — 人员关系中人员的复合标识符。 |
| `_id` | 字符串 | 记录的唯一标识符。 这是一个系统生成的值，与类捕获的其他ID字段不同。 |
| `isDeleted` | 布尔值 | 指示是否已在Marketo Engage中删除此营销列表实体。<br><br>使用时 [Marketo源连接器](../../../sources/connectors/adobe-applications/marketo/marketo.md)，则在Marketo中删除的任何记录都会自动反映在实时客户档案中。 但是，与这些用户档案相关的记录仍可能会保留在数据湖中。 通过设置 `isDeleted` 到 `true`，则可在查询数据湖时，使用字段过滤出已从源中删除的记录。 |
| `isPrimary` | 布尔值 | 指示此人是否为此机会的主要联系人。 |
| `opportunityID` | 字符串 | 机会 — 人员关系中机会的唯一标识符。 |
| `opportunityPersonID` | 字符串 | 机会 — 人员关系实体的唯一标识符 |
| `personID` | 字符串 | 机会 — 人员关系中人员的唯一标识符。 |
| `personRole` | 字符串 | 个人在机会 — 个人关系中的角色。 |

{style="table-layout:auto"}

请参阅指南，网址为 [Real-Time CDP B2B版本中的架构关系](../../tutorials/relationship-b2b.md) 了解此类在概念上如何与其他B2B类相关联，以及如何在Adobe Experience Platform UI中建立这些关系。
