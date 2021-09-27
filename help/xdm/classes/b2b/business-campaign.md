---
title: XDM Business Campaign类
description: 本文档概述了Experience Data Model(XDM)中的XDM Business Campaign类。
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 4%

---

# [!UICONTROL XDM业务营] 销活动类

>[!NOTE]
>
>此类仅适用于有权访问B2B版实时客户数据平台的组织。

[!UICONTROL XDM业务] 营销活动是一种标准的体验数据模型(XDM)类，可捕获业务营销活动所需的最低属性。

![](../../images/classes/b2b/business-campaign.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 营销活动实体的组合标识符。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系统审核属性]](../../data-types/external-source-system-audit-attributes.md) | 如果营销活动来自外部源系统，则此对象会捕获该系统的审核属性。 |
| `_id` | 字符串 | 记录的唯一标识符。 这是系统生成的值，与`campaignID`分开。 |
| `campaignDescription` | 字符串 | 营销活动的描述。 |
| `campaignID` | 字符串 | 促销活动实体的唯一标识符。 |
| `campaignName` | 字符串 | 营销活动的名称。 |
| `campaignType` | 字符串 | 营销活动类型或目标受众。 |
