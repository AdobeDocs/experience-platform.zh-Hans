---
solution: Experience Platform
title: 金融服务行业数据模型ERD
description: 查看实体关系图(ERD)，该图描述了银行、金融服务和保险(BFSI)行业的标准化数据模型。 此数据模型与Adobe Experience Platform中使用的Experience Data Model (XDM)兼容。
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# [!UICONTROL 金融服务]行业数据模型ERD

以下实体关系图(ERD)代表银行、金融服务和保险(BFSI)行业的标准化数据模型。 ERD有意以非规范化的方式呈现，并考虑了数据存储在Adobe Experience Platform中的方式。

>[!NOTE]
>
>所描述的ERD是有关如何针对此行业用例建模数据的建议。 要在Experience Platform中使用此数据模型，您必须自行构建推荐的架构及其关系。 有关详细信息，请参阅UI中有关管理[架构](../../ui/resources/schemas.md)和[关系](../../tutorials/relationship-ui.md)的指南。

使用以下图例来解释此ERD：

* 中显示的每个实体都基于基础[体验数据模型(XDM)类](../composition.md#class)。
* 在父字段下缩进的字段表示属于父字段组的子字段或子字段。
* 给定实体的最重要字段以红色突出显示。
* 所有可用于识别单个客户的属性都标记为“身份”，其中某个属性标记为“主要身份”。
* 实体关系将标记为非依赖关系，因为基于Cookie的事件通常无法确定执行事务的人员或个人。

![金融业数据模型的ERD示例](../../images/industries/financial.png)

>[!NOTE]
>
>体验事件实体包含“_ID”字段，该字段表示由XDM ExperienceEvent类提供的唯一标识符(`_id`)属性。 有关此值的预期值的更多详细信息，请参阅[XDM ExperienceEvent](../../classes/experienceevent.md)上的参考文档。

## [!UICONTROL 金融服务]用例

下表概述了针对几种常见财务用例推荐的类和架构字段组。

| 用例 | 推荐的类和字段组 |
| --- | --- |
| 通过全渠道报告洞察和自动化历程来推动首选区段的大规模个性化，以增加首选奖励计划的注册。 | <ul><li>**[[!UICONTROL 产品]](../../classes/product.md)**：<ul><li>[[!UICONTROL 产品类别]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL 卡片操作]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL 报价请求详细信息]](../../field-groups/event/quote-request-details.md)</li><li>[[!UICONTROL 存款详细信息]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL 渠道详细信息]](../../field-groups/event/channel-details.md)</li><li>[[!UICONTROL 余额转帐]](../../field-groups/event/balance-transfers.md)</li></ul></li><li>**[[!UICONTROL XDM个人资料]](../../classes/individual-profile.md)**：<ul><li>[[!UICONTROL 人口统计详细信息]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 个人联系人详细信息]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 忠诚度详细信息]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 跨在线和离线渠道优化跨渠道个性化。 | <ul><li>**[[!UICONTROL 产品]](../../classes/product.md)**：<ul><li>[[!UICONTROL 产品类别]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL 渠道详细信息]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM个人资料]](../../classes/individual-profile.md)**：<ul><li>[[!UICONTROL 人口统计详细信息]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 个人联系人详细信息]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 忠诚度详细信息]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 通过使用从跨渠道行为分析中获得的洞察力，识别可能导致新产品选件的产品使用模式，创造新的收入机会。 | <ul><li>**[[!UICONTROL 策略]](../../classes/policy.md)**</li><li>**[[!UICONTROL 产品]](../../classes/product.md)**：<ul><li>[[!UICONTROL 产品类别]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL 卡片操作]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL 支持站点搜索]](../../field-groups/event/support-site-search.md)</li><li>[[!UICONTROL 存款详细信息]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL 渠道详细信息]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM个人资料]](../../classes/individual-profile.md)**：<ul><li>[[!UICONTROL 人口统计详细信息]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 个人联系人详细信息]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 忠诚度详细信息]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
