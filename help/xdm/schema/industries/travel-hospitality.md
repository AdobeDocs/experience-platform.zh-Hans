---
solution: Experience Platform
title: 旅游和酒店业数据模型ERD
description: 查看实体关系图(ERD)，该图描述了旅游和酒店业的标准化数据模型，该数据模型与在Adobe Experience Platform中使用的体验数据模型(XDM)兼容。
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---

# [!UICONTROL 旅游和酒店业] 行业数据模型ERD

以下实体关系图(ERD)代表了旅游和服务业的标准化数据模型。 ERD特意以非标准化方式呈现，并考虑数据如何存储在Adobe Experience Platform中。

>[!NOTE]
>
>如上所述的ERD是一项建议，建议您如何为此行业用例建模数据。 要在Platform中利用此数据模型，您必须自行构建推荐的架构及其关系。 请参阅管理指南 [模式](../../ui/resources/schemas.md) 和 [关系](../../tutorials/relationship-ui.md) ，以了解更多信息。

请使用以下图例来解释此ERD:

* 中显示的每个实体均基于 [体验数据模型(XDM)类](../composition.md#class).
* 对于给定实体，每行都标记为 **粗体** 表示字段组或数据类型，其提供的相关字段将以非粗体文本列出。
* 给定实体最重要的字段以红色突出显示。
* 所有可用于标识单个客户的资产都会标记为“identity”，其中一个资产会标记为“主要身份”。
* 实体关系被标记为非依赖关系，因为基于Cookie的事件通常无法确定执行交易的人员或个人。

![](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>体验事件实体包含“_ID”字段，该字段表示唯一标识符(`_id`)属性。 请参阅 [XDM ExperienceEvent](../../classes/experienceevent.md) 以详细了解此值的预期内容。

## [!UICONTROL 旅游和酒店业] 用例

下表概述了旅游和酒店业几个常见用例的推荐类别和模式字段组。

| 用例 | 推荐的类和字段组 |
| --- | --- |
| 向市场内的客人和即将预订酒店的客人交叉销售餐饮和其他当地景点。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[保留详细信息](../../field-groups/event/reservation-details.md)</li><li>[住宿预订](../../field-groups/event/lodging-reservation.md)</li><li>[餐饮预订](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM个人配置文件](../../classes/individual-profile.md)**:<ul><li>[人口统计详细信息](../../field-groups/profile/demographic-details.md)</li><li>[个人联系详细信息](../../field-groups/profile/personal-contact-details.md)</li><li>[工作联系人详细信息](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| 向市场内的客人和即将预订酒店的客人提供上卖餐饮和其他当地景点。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[保留详细信息](../../field-groups/event/reservation-details.md)</li><li>[餐饮预订](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM个人配置文件](../../classes/individual-profile.md)**:<ul><li>[人口统计详细信息](../../field-groups/profile/demographic-details.md)</li><li>[个人联系详细信息](../../field-groups/profile/personal-contact-details.md)</li><li>[工作联系人详细信息](../../field-groups/profile/work-contact-details.md)</li><li>[忠诚度详细信息](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 向市场内的客人和即将预订酒店的客人提供追加销售的酒店和其他当地景点。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[保留详细信息](../../field-groups/event/reservation-details.md)</li><li>[住宿预订](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[XDM个人配置文件](../../classes/individual-profile.md)**:<ul><li>[人口统计详细信息](../../field-groups/profile/demographic-details.md)</li><li>[个人联系详细信息](../../field-groups/profile/personal-contact-details.md)</li><li>[工作联系人详细信息](../../field-groups/profile/work-contact-details.md)</li><li>[忠诚度详细信息](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 向市场上的客人和即将预订酒店的客人提供向上销售航班和其他当地景点。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[保留详细信息](../../field-groups/event/reservation-details.md)</li><li>[航班预订](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[XDM个人配置文件](../../classes/individual-profile.md)**:<ul><li>[人口统计详细信息](../../field-groups/profile/demographic-details.md)</li><li>[个人联系详细信息](../../field-groups/profile/personal-contact-details.md)</li><li>[工作联系人详细信息](../../field-groups/profile/work-contact-details.md)</li><li>[忠诚度详细信息](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}
