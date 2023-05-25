---
title: XDM业务营销列表类
description: 本文档概述了Experience Data Model (XDM)中的XDM业务营销列表类。
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 2%

---

# [!UICONTROL XDM业务营销列表] 类

>[!IMPORTANT]
>
>此类供有权访问的组织使用 [Adobe Real-time Customer Data Platform B2B版本](../../../rtcdp/b2b-overview.md). 您必须有权访问Real-Time CDP B2B版本，此类才能参与 [Real-time Customer Profile](../../../profile/home.md).

[!UICONTROL XDM业务营销列表] 是一个标准体验数据模型(XDM)类，可捕获营销列表的最低要求属性。 利用营销列表，您可以优先考虑最有可能购买您的产品的潜在客户。

![XDM业务营销列表类的结构，如UI中所示](../../images/classes/b2b/business-marketing-list.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系统审计属性]](../../data-types/external-source-system-audit-attributes.md) | 如果营销列表来自外部源系统，则此对象将捕获该系统的审核属性。 |
| `marketingListKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 营销列表实体的复合标识符。 |
| `_id` | 字符串 | 记录的唯一标识符。 这是系统生成的值，与 `marketingListID`. |
| `isDeleted` | 布尔值 | 指示是否已在Marketo Engage中删除此营销列表实体。<br><br>使用时 [Marketo源连接器](../../../sources/connectors/adobe-applications/marketo/marketo.md)，则在Marketo中删除的任何记录都会自动反映在实时客户档案中。 但是，与这些用户档案相关的记录仍可能会保留在数据湖中。 通过设置 `isDeleted` 到 `true`，则可在查询数据湖时，使用字段过滤出已从源中删除的记录。 |
| `marketingListDescription` | 字符串 | 营销列表的描述。 |
| `marketingListID` | 字符串 | 营销列表实体的唯一ID。 |
| `marketingListName` | 字符串 | 营销列表的名称。 |

{style="table-layout:auto"}

请参阅指南，网址为 [Real-Time CDP B2B版本中的架构关系](../../tutorials/relationship-b2b.md) 了解此类在概念上如何与其他B2B类相关联，以及如何在Adobe Experience Platform UI中建立这些关系。
