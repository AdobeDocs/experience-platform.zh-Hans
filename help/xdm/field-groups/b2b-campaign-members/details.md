---
title: XDM Business Campaign成员详细信息架构字段组
description: 本文档概述了XDM Business Campaign成员详细信息架构字段组。
source-git-commit: 0084492ed467c5996a94c5c55a79c9faf8f5046e
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 4%

---

# [!UICONTROL XDM Business Campaign成员详细信息] 架构字段组

[!UICONTROL XDM Business Campaign成员详细信息] 是的标准架构字段组 [[!UICONTROL XDM Business Campaign成员] 类](../../classes/b2b/business-campaign-members.md)，可捕获有关业务活动的详细信息。

![XDM Business Campaign“成员详细信息”字段组在UI中显示的结构](../../images/field-groups/b2b/business-campaign-member-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `acquiredByCampaignKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 获取此营销活动成员的营销活动的组合ID。 |
| `acquiredByCampaignID` | [!UICONTROL 字符串] | 获取此促销活动成员的促销活动的字符串标识符。 |
| `firstRespondedDate` | [!UICONTROL DateTime] | 人员首次响应营销活动时的ISO 8601时间戳。 |
| `hasReachedSuccess` | [!UICONTROL 布尔型] | 指示此营销活动成员是否成功转化。 |
| `hasResponded` | [!UICONTROL 布尔型] | 指示此营销活动成员是否响应了营销活动。 |
| `isDeleted` | [!UICONTROL 布尔型] | 指示此促销活动成员是否已在Marketo Engage中删除。<br><br>使用 [Marketo源连接器](../../../sources/connectors/adobe-applications/marketo/marketo.md)，则在Marketo中删除的任何记录都会自动反映在实时客户资料中。 但是，与这些用户档案相关的记录仍可能会保留在数据湖中。 通过设置 `isDeleted` to `true`，则可以使用字段在查询数据湖时过滤掉已从源中删除的记录。 |
| `isExhausted` | [!UICONTROL 布尔型] | 指示该营销活动成员是否已用尽所有营销活动交互。 |
| `lastStatus` | [!UICONTROL 字符串] | 营销活动成员的最后状态。 |
| `memberStatus` | [!UICONTROL 字符串] | 营销活动成员的当前状态。 |
| `memberStatusReason` | [!UICONTROL 字符串] | 促销活动成员当前状态背后的原因。 |
| `membershipDate` | [!UICONTROL DateTime] | 促销活动成员当前状态背后的原因。 |
| `nurtureCadence` | [!UICONTROL 字符串] | 向营销活动成员显示营销活动相关信息的时间间隔。 |
| `nurtureTrackName` | [!UICONTROL 字符串] | 此活动成员所受的培养计划的名称。 |
| `reachedSuccessDate` | [!UICONTROL DateTime] | 为促销活动成员成功转换时的ISO 8601时间戳。 |
| `webinarConfirmationUrl` | [!UICONTROL 字符串] | 网络研讨会确认URL，用于营销活动成员。 |
| `webinarRegistrationID` | [!UICONTROL 字符串] | 网络研讨会成员的注册ID。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.schema.json)
