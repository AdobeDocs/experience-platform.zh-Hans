---
title: XDM商业营销活动成员详细信息架构字段组
description: 了解XDM商业营销活动成员详细信息架构字段组。
exl-id: 597629c8-7f41-4c1c-95b6-aed5e16cee72
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 3%

---

# [!UICONTROL XDM商业营销活动成员详细信息]架构字段组

[!UICONTROL XDM商业营销活动成员详细信息]是[[!UICONTROL XDM商业营销活动成员]类](../../classes/b2b/business-campaign-members.md)的标准架构字段组，可捕获有关商业营销活动的详细信息。

![显示在UI中的XDM商业营销活动成员详细信息字段组的结构](../../images/field-groups/b2b/business-campaign-member-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `acquiredByCampaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | 获取此营销活动成员的营销活动的复合ID。 |
| `acquiredByCampaignID` | [!UICONTROL 字符串] | 获取此营销活动成员的营销活动的字符串标识符。 |
| `firstRespondedDate` | [!UICONTROL 日期时间] | 人员首次响应营销活动时间的ISO 8601时间戳。 |
| `hasReachedSuccess` | [!UICONTROL 布尔值] | 指示此营销活动成员是否已导致成功转化。 |
| `hasResponded` | [!UICONTROL 布尔值] | 指示此营销活动成员是否已响应营销活动。 |
| `isDeleted` | [!UICONTROL 布尔值] | 指示此营销活动成员是否已在Marketo Engage中删除。<br><br>使用[Marketo源连接器](../../../sources/connectors/adobe-applications/marketo/marketo.md)时，在Marketo中删除的任何记录都会自动反映在实时客户配置文件中。 但是，与这些用户档案相关的记录仍可能会保留在数据湖中。 通过将`isDeleted`设置为`true`，您可以在查询数据湖时使用该字段过滤出已从源中删除的记录。 |
| `isExhausted` | [!UICONTROL 布尔值] | 指示此营销活动成员是否已用完所有营销活动交互。 |
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
* [完整架构](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.schema.json)
