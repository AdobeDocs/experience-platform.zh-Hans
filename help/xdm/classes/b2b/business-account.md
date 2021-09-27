---
title: XDM业务帐户类
description: 本文档概述了Experience Data Model(XDM)中的XDM业务帐户类。
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 2%

---

# [!UICONTROL XDM业务帐] 户类

>[!NOTE]
>
>此类仅适用于有权访问实时客户数据平台B2B版的组织。

[!UICONTROL XDM业务] 帐户是一种标准的体验数据模型(XDM)类，可捕获业务帐户所需的最低属性。

![](../../images/classes/b2b/business-account.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 帐户实体的复合标识符。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系统审核属性]](../../data-types/external-source-system-audit-attributes.md) | 如果帐户来自外部源系统，则此对象会捕获该系统的审核属性。 |
| `_id` | 字符串 | 记录的唯一标识符。 这是系统生成的值，与`accountID`分开。 |
| `accountID` | 字符串 | 帐户实体的唯一标识符。 |

请参阅Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md)中[模式关系指南，了解此类在概念上如何与其他B2B类相关联，以及如何在Adobe Experience Platform UI中建立这些关系。
