---
title: XDM业务营销列表成员类
description: 本文档概述了Experience Data Model(XDM)中的XDM Business Marketing List Members类。
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 2%

---

# [!UICONTROL XDM业务营销列表成员] 类

>[!IMPORTANT]
>
>此类旨在供具有访问权限的组织使用 [Adobe Real-time Customer Data Platform B2B版](../../../rtcdp/b2b-overview.md). 您必须拥有Real-Time CDP B2B Edition的访问权限，才能参加此类 [实时客户资料](../../../profile/home.md).

[!UICONTROL XDM业务营销列表成员] 是一个标准的体验数据模型(XDM)类，用于描述与营销列表关联的成员、人员或联系人。

![XDM业务营销列表成员类的结构，如在UI中所示](../../images/classes/b2b/business-marketing-list-members.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系统审核属性]](../../data-types/external-source-system-audit-attributes.md) | 如果营销列表成员资格来自外部源系统，则此对象会捕获该系统的审核属性。 |
| `marketingListKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 人员所属的营销列表的复合标识符。 |
| `marketingListMemberKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 营销列表成员资格实体的组合标识符。 |
| `personKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 作为营销列表成员的人员的组合标识符。 |
| `_id` | 字符串 | 记录的唯一标识符。 这是系统生成的值，它与 `marketingListMemberID`. |
| `isDeleted` | 布尔型 | 指示此营销列表成员实体是否已在Marketo Engage中删除。<br><br>使用 [Marketo源连接器](../../../sources/connectors/adobe-applications/marketo/marketo.md)，则在Marketo中删除的任何记录都会自动反映在实时客户资料中。 但是，与这些用户档案相关的记录仍可能会保留在数据湖中。 通过设置 `isDeleted` to `true`，则可以使用字段在查询数据湖时过滤掉已从源中删除的记录。 |
| `marketingListID` | 字符串 | 营销列表的唯一ID。 |
| `marketingListMemberID` | 字符串 | 营销列表成员资格实体的唯一ID。 |
| `personId` | 字符串 | 人员的唯一ID。 |

{style=&quot;table-layout:auto&quot;}

请参阅 [Real-Time CDP B2B版中的模式关系](../../tutorials/relationship-b2b.md) 了解此类在概念上如何与其他B2B类相关，以及如何在Adobe Experience Platform UI中建立这些关系。
