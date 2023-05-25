---
solution: Experience Platform
title: 金融服务行业数据模型ERD
description: 查看实体关系图(ERD)，它描述了银行、金融服务和保险(BFSI)行业的标准化数据模型。 此数据模型与Experience Data Model (XDM)兼容，可在Adobe Experience Platform中使用。
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 3%

---

# [!UICONTROL 金融服务] 行业数据模型ERD

以下实体关系图(ERD)代表银行、金融服务和保险(BFSI)行业的标准化数据模型。 ERD有意以非规范化的方式呈现，并考虑了数据存储在Adobe Experience Platform中的方式。

>[!NOTE]
>
>所描述的ERD是有关如何针对此行业用例对数据进行建模的建议。 要在Platform中使用此数据模型，您必须自行构建推荐的架构及其关系。 请参阅有关管理的指南 [架构](../../ui/resources/schemas.md) 和 [关系](../../tutorials/relationship-ui.md) （在UI中）以了解更多信息。

使用以下图例来解释此ERD：

* 中显示的每个实体都基于一个基础 [Experience Data Model (XDM)类](../composition.md#class).
* 对于给定的实体，每个行均标记在 **粗体** 表示字段组或数据类型，其提供的相关字段以无粗体文本形式列于下方。
* 给定实体的最重要字段以红色突出显示。
* 可用于识别单个客户的所有属性均标记为“身份”，并且其中一个属性标记为“主要身份”。
* 实体关系将标记为非依赖关系，因为基于Cookie的事件通常无法确定执行事务的人员或个人。

![](../../images/industries/financial.png)

>[!NOTE]
>
>体验事件实体包含“_ID”字段，表示唯一标识符(`_id`)属性，该属性由XDM ExperienceEvent类提供。 参阅参考文档 [XDM ExperienceEvent](../../classes/experienceevent.md) 以了解有关此值的预期值的更多详细信息。

## [!UICONTROL 金融服务] 用例

下表概述了几个常见财务用例的建议类和架构字段组。

| 用例 | 推荐的类和字段组 |
| --- | --- |
| 通过全渠道报告洞察和自动化历程来大规模推动首选区段的个性化，以增加首选奖励计划的注册人数。 | <ul><li>**[[!UICONTROL 产品]](../../classes/product.md)**:<ul><li>[[!UICONTROL 产品类别]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL 信息卡操作]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL 报价请求详细信息]](../../field-groups/event/quote-request-details.md)</li><li>[[!UICONTROL 存款明细]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL 渠道详细信息]](../../field-groups/event/channel-details.md)</li><li>[[!UICONTROL 余额转帐]](../../field-groups/event/balance-transfers.md)</li></ul></li><li>**[[!UICONTROL XDM 个人资料]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 人口统计详细信息]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 个人联系人详细信息]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 忠诚度详细信息]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 跨在线和离线渠道优化跨渠道个性化。 | <ul><li>**[[!UICONTROL 产品]](../../classes/product.md)**:<ul><li>[[!UICONTROL 产品类别]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL 渠道详细信息]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM 个人资料]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 人口统计详细信息]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 个人联系人详细信息]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 忠诚度详细信息]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 利用从跨渠道行为分析中获得的洞察信息，识别可能导致新产品选件的产品使用模式，推动新的收入机会。 | <ul><li>**[[!UICONTROL 策略]](../../classes/policy.md)**</li><li>**[[!UICONTROL 产品]](../../classes/product.md)**:<ul><li>[[!UICONTROL 产品类别]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL 信息卡操作]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL 支持站点搜索]](../../field-groups/event/support-site-search.md)</li><li>[[!UICONTROL 存款明细]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL 渠道详细信息]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM 个人资料]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 人口统计详细信息]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 个人联系人详细信息]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 忠诚度详细信息]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
