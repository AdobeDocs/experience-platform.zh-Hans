---
solution: Experience Platform
title: 旅游和酒店业数据模型ERD
description: 查看实体关系图(ERD)，它描述了旅游和酒店业的标准化数据模型，与Experience Data Model (XDM)兼容，以便在Adobe Experience Platform中使用。
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 3%

---

# [!UICONTROL 旅游和酒店业] 行业数据模型ERD

以下实体关系图(ERD)表示旅行和酒店业的标准化数据模型。 ERD有意以非规范化的方式呈现，并考虑了数据存储在Adobe Experience Platform中的方式。

>[!NOTE]
>
>所描述的ERD是有关如何针对此行业用例对数据进行建模的建议。 要在Platform中使用此数据模型，您必须自行构建推荐的架构及其关系。 请参阅有关管理的指南 [架构](../../ui/resources/schemas.md) 和 [关系](../../tutorials/relationship-ui.md) （在UI中）以了解更多信息。

使用以下图例来解释此ERD：

* 中显示的每个实体都基于一个基础 [Experience Data Model (XDM)类](../composition.md#class).
* 对于给定的实体，每个行均标记在 **粗体** 表示字段组或数据类型，其提供的相关字段以无粗体文本形式列于下方。
* 给定实体的最重要字段以红色突出显示。
* 可用于识别单个客户的所有属性均标记为“身份”，并且其中一个属性标记为“主要身份”。
* 实体关系将标记为非依赖关系，因为基于Cookie的事件通常无法确定执行事务的人员或个人。

![](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>体验事件实体包含“_ID”字段，表示唯一标识符(`_id`)属性，该属性由XDM ExperienceEvent类提供。 参阅参考文档 [XDM ExperienceEvent](../../classes/experienceevent.md) 以了解有关此值的预期值的更多详细信息。

## [!UICONTROL 旅游和酒店业] 用例

下表概述了旅游和酒店业的几个常见用例的建议班级和架构字段组。

| 用例 | 推荐的类和字段组 |
| --- | --- |
| 向即将预订酒店的客人及市场内客人交叉销售餐饮和其他居民景点。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[预订详细信息](../../field-groups/event/reservation-details.md)</li><li>[住宿预订](../../field-groups/event/lodging-reservation.md)</li><li>[餐饮预订](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM 个人资料](../../classes/individual-profile.md)**:<ul><li>[人口统计详细信息](../../field-groups/profile/demographic-details.md)</li><li>[个人联系人详细信息](../../field-groups/profile/personal-contact-details.md)</li><li>[工作联系人详细信息](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| 向即将预订酒店的客人及市场内客人追加销售餐饮和其他居民景点。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[预订详细信息](../../field-groups/event/reservation-details.md)</li><li>[餐饮预订](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM 个人资料](../../classes/individual-profile.md)**:<ul><li>[人口统计详细信息](../../field-groups/profile/demographic-details.md)</li><li>[个人联系人详细信息](../../field-groups/profile/personal-contact-details.md)</li><li>[工作联系人详细信息](../../field-groups/profile/work-contact-details.md)</li><li>[忠诚度详细信息](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 向即将预订酒店的客人及市场内客人追加销售酒店和其他居民景点。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[预订详细信息](../../field-groups/event/reservation-details.md)</li><li>[住宿预订](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[XDM 个人资料](../../classes/individual-profile.md)**:<ul><li>[人口统计详细信息](../../field-groups/profile/demographic-details.md)</li><li>[个人联系人详细信息](../../field-groups/profile/personal-contact-details.md)</li><li>[工作联系人详细信息](../../field-groups/profile/work-contact-details.md)</li><li>[忠诚度详细信息](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 向即将预订酒店的市场内宾客和宾客追加销售航班和其他居民景点。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[预订详细信息](../../field-groups/event/reservation-details.md)</li><li>[航班预订](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[XDM 个人资料](../../classes/individual-profile.md)**:<ul><li>[人口统计详细信息](../../field-groups/profile/demographic-details.md)</li><li>[个人联系人详细信息](../../field-groups/profile/personal-contact-details.md)</li><li>[工作联系人详细信息](../../field-groups/profile/work-contact-details.md)</li><li>[忠诚度详细信息](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
