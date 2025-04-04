---
solution: Experience Platform
title: 旅游和酒店业数据模型ERD
description: 查看实体关系图(ERD)，该关系图描述旅游和酒店业的标准化数据模型，与Experience Data Model (XDM)兼容，用于Adobe Experience Platform。
exl-id: 4d454160-9066-4702-815b-9509942f709e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# [!UICONTROL 旅游和酒店业]行业数据模型ERD

以下实体关系图(ERD)表示旅行和酒店业的标准化数据模型。 ERD有意以非规范化的方式呈现，并考虑了数据存储在Adobe Experience Platform中的方式。

>[!NOTE]
>
>所描述的ERD是有关如何针对此行业用例建模数据的建议。 要在Experience Platform中使用此数据模型，您必须自行构建推荐的架构及其关系。 有关详细信息，请参阅UI中有关管理[架构](../../ui/resources/schemas.md)和[关系](../../tutorials/relationship-ui.md)的指南。

使用以下图例来解释此ERD：

* 中显示的每个实体都基于基础[体验数据模型(XDM)类](../composition.md#class)。
* 在父字段下缩进的字段表示属于父字段组的子字段或子字段。
* 给定实体的最重要字段以红色突出显示。
* 所有可用于识别单个客户的属性都标记为“身份”，其中某个属性标记为“主要身份”。
* 实体关系将标记为非依赖关系，因为基于Cookie的事件通常无法确定执行事务的人员或个人。

![旅游服务业数据模型的示例ERD](../../images/industries/travel-hospitality.png)

>[!NOTE]
>
>体验事件实体包含“_ID”字段，该字段表示由XDM ExperienceEvent类提供的唯一标识符(`_id`)属性。 有关此值的预期值的更多详细信息，请参阅[XDM ExperienceEvent](../../classes/experienceevent.md)上的参考文档。

## [!UICONTROL 旅游和酒店业]用例

下表概述了为旅游和酒店业的多个常见用例推荐的课程和架构字段组。

| 用例 | 推荐的类和字段组 |
| --- | --- |
| 即将预订酒店的客人可以交叉销售餐饮和其他本地景点。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[预订详细信息](../../field-groups/event/reservation-details.md)</li><li>[住宿预订](../../field-groups/event/lodging-reservation.md)</li><li>[餐饮预订](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM个人资料](../../classes/individual-profile.md)**：<ul><li>[人口统计详细信息](../../field-groups/profile/demographic-details.md)</li><li>[个人联系人详细信息](../../field-groups/profile/personal-contact-details.md)</li><li>[工作联系人详细信息](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| 即将预订酒店的客人还可以向市场内的客人出售高级餐厅和其他本地景点。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[预订详细信息](../../field-groups/event/reservation-details.md)</li><li>[餐饮预订](../../field-groups/event/dining-reservation.md)</li></ul></li><li>**[XDM个人资料](../../classes/individual-profile.md)**：<ul><li>[人口统计详细信息](../../field-groups/profile/demographic-details.md)</li><li>[个人联系人详细信息](../../field-groups/profile/personal-contact-details.md)</li><li>[工作联系人详细信息](../../field-groups/profile/work-contact-details.md)</li><li>[忠诚度详细信息](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 向即将预订酒店的市场内客人和客人追加销售酒店和其他本地景点。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[预订详细信息](../../field-groups/event/reservation-details.md)</li><li>[住宿预订](../../field-groups/event/lodging-reservation.md)</li></ul></li><li>**[XDM个人资料](../../classes/individual-profile.md)**：<ul><li>[人口统计详细信息](../../field-groups/profile/demographic-details.md)</li><li>[个人联系人详细信息](../../field-groups/profile/personal-contact-details.md)</li><li>[工作联系人详细信息](../../field-groups/profile/work-contact-details.md)</li><li>[忠诚度详细信息](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |
| 向即将预订酒店的客人和市场内客人出售航班和其他居民景点。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[预订详细信息](../../field-groups/event/reservation-details.md)</li><li>[航班预订](../../field-groups/event/flight-reservation.md)</li></ul></li><li>**[XDM个人资料](../../classes/individual-profile.md)**：<ul><li>[人口统计详细信息](../../field-groups/profile/demographic-details.md)</li><li>[个人联系人详细信息](../../field-groups/profile/personal-contact-details.md)</li><li>[工作联系人详细信息](../../field-groups/profile/work-contact-details.md)</li><li>[忠诚度详细信息](../../field-groups/profile/loyalty-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
