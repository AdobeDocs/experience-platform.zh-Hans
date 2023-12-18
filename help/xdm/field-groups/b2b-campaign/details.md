---
title: XDM商业营销活动详细信息架构字段组
description: 了解XDM商业营销活动详细信息架构字段组。
exl-id: 3ef6c0b9-cba1-449e-8868-46446c00465f
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 5%

---

# [!UICONTROL XDM商业营销活动详细信息] 架构字段组

[!UICONTROL XDM商业营销活动详细信息] 是的标准架构字段组 [[!UICONTROL XDM商业营销活动] 类](../../classes/b2b/business-campaign.md)，用于捕获有关商业营销活动的详细信息。

![XDM商业营销活动详细信息字段组的结构，如UI中所示](../../images/field-groups/b2b/business-campaign-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `actualCost` | [[!UICONTROL 货币]](../../data-types/currency.md) | 表示商业营销活动的实际成本。 |
| `budgetedCost` | [[!UICONTROL 货币]](../../data-types/currency.md) | 表示业务营销活动的预算成本。 |
| `expectedRevenue` | [[!UICONTROL 货币]](../../data-types/currency.md) | 表示预计业务营销活动将产生的收入。 |
| `parentCampaignKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 父营销活动的复合ID（如果适用）。 |
| `campaignEndDate` | [!UICONTROL 日期时间] | 促销活动结束或即将结束的ISO 8601时间戳。 |
| `campaignProgressionName` | [!UICONTROL 字符串] | 促销活动进展名称。 |
| `campaignStartDate` | [!UICONTROL 日期时间] | 促销活动开始时间或开始时间的ISO 8601时间戳。 |
| `campaignStatus` | [!UICONTROL 字符串] | 营销活动的当前状态。 |
| `channelName` | [!UICONTROL 字符串] | 与此营销活动关联的渠道的名称。 |
| `expectedResponse` | [!UICONTROL 字符串] | 活动的预期响应。 |
| `integrationPartnerName` | [!UICONTROL 字符串] | 已与此营销活动集成的合作伙伴的名称。 |
| `isActive` | [!UICONTROL 布尔型] | 指示此营销活动是否处于活动状态。 |
| `isDeleted` | [!UICONTROL 布尔型] | 指示此营销活动是否已在Marketo Engage中删除。<br><br>使用时 [Marketo源连接器](../../../sources/connectors/adobe-applications/marketo/marketo.md)，则在Marketo中删除的任何记录都会自动反映在实时客户档案中。 但是，与这些用户档案相关的记录仍可能会保留在数据湖中。 通过设置 `isDeleted` 到 `true`中，您可以使用字段在查询数据湖时筛选出已从源中删除的记录。 |
| `lastActivityDate` | [!UICONTROL 日期时间] | 与促销活动关联的上一个活动的ISO 8601时间戳。 |
| `timeZone` | [!UICONTROL 字符串] | 营销活动进行操作的时区。 |
| `timeZoneDelivery` | [!UICONTROL 字符串] | 活动在其中运行的投放时区。 |
| `timeZoneName` | [!UICONTROL 字符串] | 营销活动在其中运行的时区的名称。 |
| `webinarHistorySyncDate` | [!UICONTROL 日期时间] | 此促销活动上次网络研讨会历史同步的ISO 8601时间戳。 |
| `webinarHistorySyncStatus` | [!UICONTROL 字符串] | 此营销活动的网络研讨会历史记录同步的状态。 |
| `webinarSessionDescription` | [!UICONTROL 字符串] | 与此营销活动关联的网络研讨会会话的描述。 |
| `webinarSessionName` | [!UICONTROL 字符串] | 与此营销活动关联的网络研讨会会话的名称。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign/campaign-details.schema.json).
