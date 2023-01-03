---
title: XDM Business Campaign类
description: 本文档概述了Experience Data Model(XDM)中的XDM Business Campaign类。
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 4%

---

# [!UICONTROL XDM Business Campaign] 类

>[!IMPORTANT]
>
>此类旨在供具有访问权限的组织使用 [Adobe Real-time Customer Data Platform B2B版](../../../rtcdp/b2b-overview.md). 您必须拥有Real-Time CDP B2B Edition的访问权限，才能参加此类 [实时客户资料](../../../profile/home.md).

[!UICONTROL XDM Business Campaign] 是一个标准的体验数据模型(XDM)类，可捕获业务活动所需的最低属性。

![XDM Business Campaign类在UI中显示的结构](../../images/classes/b2b/business-campaign.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 营销活动实体的组合标识符。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部源系统审核属性]](../../data-types/external-source-system-audit-attributes.md) | 如果营销活动来自外部源系统，则此对象会捕获该系统的审核属性。 |
| `_id` | 字符串 | 记录的唯一标识符。 这是系统生成的值，它与 `campaignID`. |
| `campaignDescription` | 字符串 | 营销活动的描述。 |
| `campaignID` | 字符串 | 促销活动实体的唯一标识符。 |
| `campaignName` | 字符串 | 营销活动的名称。 |
| `campaignType` | 字符串 | 营销活动类型或目标受众。 |

{style=&quot;table-layout:auto&quot;}

要了解此类在概念上如何与其他B2B类相关以及如何在Adobe Experience Platform UI中建立这些关系，请参阅 [Real-Time CDP B2B版中的模式关系](../../tutorials/relationship-b2b.md)

有关与此类兼容的其他字段，请参阅的字段组引用 [[!UICONTROL XDM Business Campaign详细信息]](../../field-groups/b2b-campaign/details.md).
