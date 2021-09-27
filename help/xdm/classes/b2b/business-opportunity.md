---
title: XDM业务机会类
description: 本文档概述了Experience Data Model(XDM)中的XDM Business Opportunity类。
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 5%

---

# [!UICONTROL XDM业务机] 会类

>[!NOTE]
>
>此类仅适用于有权访问B2B版实时客户数据平台的组织。

[!UICONTROL XDM业务机] 会是一种标准的体验数据模型(XDM)类，可捕获业务机会所需的最低属性。

![](../../images/classes/b2b/business-opportunity.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 此机会所关联的帐户的组合标识符。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系统审核属性]](../../data-types/external-source-system-audit-attributes.md) | 如果商机来自外部源系统，则此对象将捕获该系统的审核属性。 |
| `opportunityKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 机会实体的组合标识符。 |
| `_id` | 字符串 | 记录的唯一标识符。 这是系统生成的值，与`opportunityID`分开。 |
| `accountID` | 字符串 | 此机会所关联的帐户的唯一ID。 |
| `opportunityDescription` | 字符串 | 机会的描述。 |
| `opportunityID` | 字符串 | 机会实体的唯一ID。 |
| `opportunityName` | 字符串 | 机会的名称。 |
| `opportunityStage` | 字符串 | 销售机会的销售阶段。 |
| `opportunityType` | 字符串 | 机会类型。 |
