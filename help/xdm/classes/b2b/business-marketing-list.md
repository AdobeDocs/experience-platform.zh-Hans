---
title: XDM业务营销列表类
description: 本文档概述了Experience Data Model(XDM)中的XDM Business Marketing List类。
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 3%

---

# [!UICONTROL XDM Business Marketing列] 表类

>[!NOTE]
>
>此类仅适用于有权访问B2B版实时客户数据平台的组织。

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
