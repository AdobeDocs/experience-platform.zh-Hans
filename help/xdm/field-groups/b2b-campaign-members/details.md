---
title: XDM商业营销活动成员详细信息架构字段组
description: 了解XDM商业营销活动成员详细信息架构字段组。
exl-id: 597629c8-7f41-4c1c-95b6-aed5e16cee72
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 4%

---

# [!UICONTROL XDM商业营销活动成员详细信息] 架构字段组

[!UICONTROL XDM商业营销活动成员详细信息] 是的标准架构字段组 [[!UICONTROL XDM商业营销活动成员] 类](../../classes/b2b/business-campaign-members.md)，用于捕获有关商业营销活动的详细信息。

![XDM业务营销活动成员详细信息字段组的结构，如UI中所示](../../images/field-groups/b2b/business-campaign-member-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `acquiredByCampaignKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 获取此营销活动成员的营销活动的复合ID。 |
| `acquiredByCampaignID` | [!UICONTROL 字符串] | 获取此营销活动成员的营销活动的字符串标识符。 |
| `firstRespondedDate` | [!UICONTROL 日期时间] | 人员首次响应营销活动时间的ISO 8601时间戳。 |
| `hasReachedSuccess` | [!UICONTROL 布尔型] | 指示此营销活动成员是否已导致成功转化。 |
| `hasResponded` | [!UICONTROL 布尔型] | 指示此营销活动成员是否已响应营销活动。 |
| `isDeleted` | [!UICONTROL 布尔型] | 指示此营销活动成员是否已在Marketo Engage中删除。<br><br>使用时 [Marketo源连接器](../../../sources/connectors/adobe-applications/marketo/marketo.md)，则在Marketo中删除的任何记录都会自动反映在实时客户档案中。 但是，与这些用户档案相关的记录仍可能会保留在数据湖中。 通过设置 `isDeleted` 到 `true`中，您可以使用字段在查询数据湖时筛选出已从源中删除的记录。 |
| `isExhausted` | [!UICONTROL 布尔型] | 指示此营销活动成员是否已用完所有营销活动交互。 |
| `lastStatus` | [!UICONTROL 字符串] | 营销活动成员的最后一个状态。 |
| `memberStatus` | [!UICONTROL 字符串] | 营销活动成员的当前状态。 |
| `memberStatusReason` | [!UICONTROL 字符串] | 营销活动成员当前状态背后的原因。 |
| `membershipDate` | [!UICONTROL 日期时间] | 营销活动成员当前状态背后的原因。 |
| `nurtureCadence` | [!UICONTROL 字符串] | 向营销活动成员展示营销活动相关信息的时间间隔。 |
| `nurtureTrackName` | [!UICONTROL 字符串] | 此营销活动成员遵循的培养计划的名称。 |
| `reachedSuccessDate` | [!UICONTROL 日期时间] | 促销活动成员成功转化时间的ISO 8601时间戳。 |
| `webinarConfirmationUrl` | [!UICONTROL 字符串] | 营销活动成员的网络研讨会确认URL。 |
| `webinarRegistrationID` | [!UICONTROL 字符串] | 营销活动成员的网络研讨会注册ID。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.schema.json)
