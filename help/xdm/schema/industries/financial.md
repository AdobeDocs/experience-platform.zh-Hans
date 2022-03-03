---
solution: Experience Platform
title: 金融服务行业数据模型ERD
topic-legacy: overview
description: 查看实体关系图(ERD)，该图描述银行、金融服务和保险(BFSI)行业的标准化数据模型。 此数据模型与Experience Data Model(XDM)兼容，可在Adobe Experience Platform中使用。
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: 345380c9d4e371bc90acee1f35e75f9da8f9394e
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 1%

---

# [!UICONTROL 金融服务] 行业数据模型ERD

以下实体关系图(ERD)代表银行、金融服务和保险(BFSI)行业的标准化数据模型。 ERD特意以非标准化方式呈现，并考虑数据如何存储在Adobe Experience Platform中。

>[!NOTE]
>
>如上所述的ERD是一项建议，建议您如何为此行业用例建模数据。 要在Platform中利用此数据模型，您必须自行构建推荐的架构及其关系。 请参阅管理指南 [模式](../../ui/resources/schemas.md) 和 [关系](../../tutorials/relationship-ui.md) ，以了解更多信息。

请使用以下图例来解释此ERD:

* 中显示的每个实体均基于 [体验数据模型(XDM)类](../composition.md#class).
* 对于给定实体，每行都标记为 **粗体** 表示字段组或数据类型，其提供的相关字段将以非粗体文本列出。
* 给定实体最重要的字段以红色突出显示。
* 所有可用于标识单个客户的资产都会标记为“identity”，其中一个资产会标记为“主要身份”。
* 实体关系被标记为非依赖关系，因为基于Cookie的事件通常无法确定执行交易的人员或个人。

![](../../images/industries/financial.png)

>[!NOTE]
>
>体验事件实体包含“_ID”字段，该字段表示唯一标识符(`_id`)属性。 请参阅 [XDM ExperienceEvent](../../classes/experienceevent.md) 以详细了解此值的预期内容。

## [!UICONTROL 金融服务] 用例

下表概述了几个常见财务用例的推荐类和架构字段组。

| 用例 | 推荐的类和字段组 |
| --- | --- |
| 通过全渠道报告分析和自动化旅程，大规模推动首选区段的个性化，以增加对首选奖励计划的注册。 | <ul><li>**[[!UICONTROL 产品]](../../classes/product.md)**:<ul><li>[[!UICONTROL 产品类别]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 卡片操作]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL 报价请求详细信息]](../../field-groups/event/quote-request-details.md)</li><li>[[!UICONTROL 存款详细信息]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL 渠道详细信息]](../../field-groups/event/channel-details.md)</li><li>[[!UICONTROL 余额转移]](../../field-groups/event/balance-transfers.md)</li></ul></li><li>**[[!UICONTROL XDM个人配置文件]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 人口统计详细信息]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 个人联系详细信息]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 忠诚度详细信息]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 优化线上和线下渠道的跨渠道个性化。 | <ul><li>**[[!UICONTROL 产品]](../../classes/product.md)**:<ul><li>[[!UICONTROL 产品类别]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 渠道详细信息]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM个人配置文件]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 人口统计详细信息]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 个人联系详细信息]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 忠诚度详细信息]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 利用跨渠道行为分析获得的洞察信息，识别可能导致新产品选件的产品使用模式，从而创造新的收入机会。 | <ul><li>**[[!UICONTROL 策略]](../../classes/policy.md)**</li><li>**[[!UICONTROL 产品]](../../classes/product.md)**:<ul><li>[[!UICONTROL 产品类别]](../../field-groups/product/product-category.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 卡片操作]](../../field-groups/event/card-actions.md)</li><li>[[!UICONTROL 支持网站搜索]](../../field-groups/event/support-site-search.md)</li><li>[[!UICONTROL 存款详细信息]](../../field-groups/event/deposit-details.md)</li><li>[[!UICONTROL 渠道详细信息]](../../field-groups/event/channel-details.md)</li></ul></li><li>**[[!UICONTROL XDM个人配置文件]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 人口统计详细信息]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 个人联系详细信息]](../../field-groups/profile/personal-contact-details.md)</li><li>[[!UICONTROL 忠诚度详细信息]](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
