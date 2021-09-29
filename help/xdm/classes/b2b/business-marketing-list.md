---
title: XDM业务营销列表类
description: 本文档概述了Experience Data Model(XDM)中的XDM Business Marketing List类。
exl-id: 510c5608-054d-4bed-91eb-22d84b5dc625
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!UICONTROL XDM Business Marketing Listclass(] 测试版)

>[!IMPORTANT]
>
>此课程作为Real-time Customer Data Platform B2B Edition的一部分提供，该B2B Edition目前处于测试阶段。 文档和功能可能会发生更改。

[!UICONTROL XDM Business Marketing List] 是一个标准的体验数据模型(XDM)类，可捕获营销列表所需的最低属性。市场营销列表允许您优先考虑最有可能购买您产品的潜在客户。

![](../../images/classes/b2b/business-marketing-list.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系统审核属性]](../../data-types/external-source-system-audit-attributes.md) | 如果营销列表来自外部源系统，则此对象会捕获该系统的审核属性。 |
| `marketingListKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 营销列表实体的组合标识符。 |
| `_id` | 字符串 | 记录的唯一标识符。 这是系统生成的值，与`marketingListID`分开。 |
| `marketingListDescription` | 字符串 | 营销列表的描述。 |
| `marketingListID` | 字符串 | 营销列表实体的唯一ID。 |
| `marketingListName` | 字符串 | 营销列表的名称。 |

{style=&quot;table-layout:auto&quot;}

请参阅Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md)中[模式关系指南，了解此类在概念上如何与其他B2B类相关联，以及如何在Adobe Experience Platform UI中建立这些关系。
