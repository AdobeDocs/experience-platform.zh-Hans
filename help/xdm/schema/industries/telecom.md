---
solution: Experience Platform
title: 电信行业数据模型ERD
description: 查看实体关系图(ERD)，该图描述了电信行业的标准化数据模型，该数据模型与在Adobe Experience Platform中使用的体验数据模型(XDM)兼容。
exl-id: 96f267ce-a177-4384-a512-841c89d942ba
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 1%

---

# [!UICONTROL 电信] 行业数据模型ERD

以下实体关系图(ERD)代表电信行业的标准化数据模型。 ERD特意以非标准化方式呈现，并考虑数据如何存储在Adobe Experience Platform中。

>[!NOTE]
>
>如上所述的ERD是一项建议，建议您如何为此行业用例建模数据。 要在Platform中利用此数据模型，您必须自行构建推荐的架构及其关系。 请参阅管理指南 [模式](../../ui/resources/schemas.md) 和 [关系](../../tutorials/relationship-ui.md) ，以了解更多信息。

请使用以下图例来解释此ERD:

* 中显示的每个实体均基于 [体验数据模型(XDM)类](../composition.md#class).
* 对于给定实体，每行都标记为 **粗体** 表示字段组或数据类型，其提供的相关字段将以非粗体文本列出。
* 给定实体最重要的字段以红色突出显示。
* 所有可用于标识单个客户的资产都会标记为“identity”，其中一个资产会标记为“主要身份”。
* 实体关系被标记为非依赖关系，因为基于Cookie的事件通常无法确定执行交易的人员或个人。


![](../../images/industries/telecom.png)

>[!NOTE]
>
>体验事件实体包含“_ID”字段，该字段表示唯一标识符(`_id`)属性。 请参阅 [XDM ExperienceEvent](../../classes/experienceevent.md) 以详细了解此值的预期内容。

## [!UICONTROL 电信] 用例

下表概述了电信行业几个常见用例的推荐类和模式字段组。

| 用例 | 推荐的类和字段组 |
| --- | --- |
| 了解那些是向上销售或交叉销售机会的优秀候选客户，这些客户会根据其当前持有的资产和他们的浏览行为进行了解。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 追加销售详细信息]](../../field-groups/event/upsell-details.md)</li><li>[[!UICONTROL 升级详细信息]](../../field-groups/event/upgrade-details.md)</li></ul></li><li>**[[!UICONTROL XDM个人配置文件]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 电信订购]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL 人口统计详细信息]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 个人联系详细信息]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| 通过相关广告和自动个性化电子邮件重新定位放弃购买者。 在广告转换时隐藏广告。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 商务详细信息]](../../field-groups/event/upsell-details.md) （捕获购物车放弃）</li></ul></li><li>**[[!UICONTROL XDM个人配置文件]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 电信订购]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL 人口统计详细信息]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 个人联系详细信息]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| 当客户被标记为可能流失（基于员工交互或自动机器学习算法）时，将客户详细信息发送到数字和非数字渠道。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 促销活动营销详细信息]](../../field-groups/event/campaign-marketing-details.md)</li><li>[[!UICONTROL 渠道详细信息]](../../field-groups/event/channel-details.md)</li><li>包含个性化内容的自定义字段组</li></ul></li><li>**[[!UICONTROL XDM个人配置文件]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 人口统计详细信息]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 个人联系详细信息]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}
