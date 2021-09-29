---
title: XDM Business Campaign类
description: 本文档概述了Experience Data Model(XDM)中的XDM Business Campaign类。
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 5%

---

# [!UICONTROL XDM Business ] Campaignclass（测试版）

>[!IMPORTANT]
>
>此课程作为Real-time Customer Data Platform B2B Edition的一部分提供，该B2B Edition目前处于测试阶段。 文档和功能可能会发生更改。

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

{style=&quot;table-layout:auto&quot;}

请参阅Real-time CDP B2B Edition](../../tutorials/relationship-b2b.md)中[模式关系指南，了解此类在概念上如何与其他B2B类相关联，以及如何在Adobe Experience Platform UI中建立这些关系。
