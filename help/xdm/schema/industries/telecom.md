---
solution: Experience Platform
title: 电信行业数据模型ERD
description: 查看实体关系图(ERD)，它描述电信业的标准化数据模型，与Experience Data Model (XDM)兼容，用于Adobe Experience Platform。
exl-id: 96f267ce-a177-4384-a512-841c89d942ba
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# [!UICONTROL 电信]行业数据模型ERD

以下实体关系图(ERD)代表电信行业的标准化数据模型。 ERD有意以非规范化的方式呈现，并考虑了数据存储在Adobe Experience Platform中的方式。

>[!NOTE]
>
>所描述的ERD是有关如何针对此行业用例建模数据的建议。 要在Experience Platform中使用此数据模型，您必须自行构建推荐的架构及其关系。 有关详细信息，请参阅UI中有关管理[架构](../../ui/resources/schemas.md)和[关系](../../tutorials/relationship-ui.md)的指南。

使用以下图例来解释此ERD：

* 中显示的每个实体都基于基础[体验数据模型(XDM)类](../composition.md#class)。
* 在父字段下缩进的字段表示属于父字段组的子字段或子字段。
* 给定实体的最重要字段以红色突出显示。
* 所有可用于识别单个客户的属性都标记为“身份”，其中某个属性标记为“主要身份”。
* 实体关系将标记为非依赖关系，因为基于Cookie的事件通常无法确定执行事务的人员或个人。


![电信行业数据模型的ERD示例](../../images/industries/telecom.png)

>[!NOTE]
>
>体验事件实体包含“_ID”字段，该字段表示由XDM ExperienceEvent类提供的唯一标识符(`_id`)属性。 有关此值的预期值的更多详细信息，请参阅[XDM ExperienceEvent](../../classes/experienceevent.md)上的参考文档。

## [!UICONTROL 电信]用例

下表概述了为电信业的几个常见用例推荐的类和架构字段组。

| 用例 | 推荐的类和字段组 |
| --- | --- |
| 根据客户的当前持有量和浏览行为，了解适合追加销售或交叉销售机会的客户。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL 追加销售详细信息]](../../field-groups/event/upsell-details.md)</li><li>[[!UICONTROL 升级详细信息]](../../field-groups/event/upgrade-details.md)</li></ul></li><li>**[[!UICONTROL XDM个人资料]](../../classes/individual-profile.md)**：<ul><li>[[!UICONTROL 电信订阅]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL 人口统计详细信息]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 个人联系人详细信息]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| 通过相关广告和自动个性化电子邮件重新定位购物车放弃者。 在广告转换时禁止广告。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL Commerce详细信息]](../../field-groups/event/upsell-details.md)（用于捕获购物车放弃次数）</li></ul></li><li>**[[!UICONTROL XDM个人资料]](../../classes/individual-profile.md)**：<ul><li>[[!UICONTROL 电信订阅]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL 人口统计详细信息]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 个人联系人详细信息]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| 当客户被标记为可能流失（基于员工互动或自动机器学习算法）时，将客户详细信息发送到数字和非数字渠道。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL 营销活动详细信息]](../../field-groups/event/campaign-marketing-details.md)</li><li>[[!UICONTROL 渠道详细信息]](../../field-groups/event/channel-details.md)</li><li>包含个性化内容的自定义字段组</li></ul></li><li>**[[!UICONTROL XDM个人资料]](../../classes/individual-profile.md)**：<ul><li>[[!UICONTROL 人口统计详细信息]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 个人联系人详细信息]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
