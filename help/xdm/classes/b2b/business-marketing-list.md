---
title: XDM商业营销列表类
description: 了解Experience Data Model (XDM)中的XDM业务营销列表类。
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 3%

---

# [!UICONTROL XDM商业营销列表]类

>[!IMPORTANT]
>
>此类供具有[Adobe Real-time Customer Data Platform B2B版本](../../../rtcdp/b2b-overview.md)访问权限的组织使用。 您必须有权访问Real-Time CDP B2B版本，此类才能参与[实时客户个人资料](../../../profile/home.md)。

[!UICONTROL XDM业务营销列表]是一个标准体验数据模型(XDM)类，可捕获营销列表的最低要求属性。营销列表允许您优先考虑最有可能购买您的产品的潜在客户。

![&#x200B; XDM业务营销列表类在UI中显示的结构](../../images/classes/b2b/business-marketing-list.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL 外部Source系统审核属性]](../../data-types/external-source-system-audit-attributes.md) | 如果营销列表来自外部源系统，则此对象将捕获该系统的审核属性。 |
| `marketingListKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 营销列表实体的复合标识符。 |
| `_id` | 字符串 | 记录的唯一标识符。 这是系统生成的值，与`marketingListID`不同。 |
| `isDeleted` | 布尔值 | 指示此营销列表实体是否已在Marketo Engage中删除。<br><br>使用[Marketo源连接器](../../../sources/connectors/adobe-applications/marketo/marketo.md)时，在Marketo中删除的任何记录都会自动反映在实时客户配置文件中。 但是，与这些用户档案相关的记录仍可能会保留在数据湖中。 通过将`isDeleted`设置为`true`，您可以在查询数据湖时使用该字段过滤出已从源中删除的记录。 |
| `marketingListDescription` | 字符串 | 营销列表的描述。 |
| `marketingListID` | 字符串 | 营销列表实体的唯一ID。 |
| `marketingListName` | 字符串 | 营销列表的名称。 |

{style="table-layout:auto"}

请参阅有关Real-Time CDP B2B版本[&#128279;](../../tutorials/relationship-b2b.md)中的架构关系的指南，以了解此类如何在概念上与其他B2B类相关联，以及如何在Adobe Experience Platform UI中建立这些关系。
