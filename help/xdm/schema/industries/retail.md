---
solution: Experience Platform
title: 零售业数据模型
description: 查看零售业的标准化数据模型，该模型与Experience Data Model (XDM)兼容，可用于Adobe Experience Platform。
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 5ceb261dbf1cac58d0cfe620875b8fa7c761abf2
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 4%

---

# [!UICONTROL 零售] 行业数据模型

以下实体关系图(ERD)代表零售业的标准化数据模型。 ERD有意以非规范化的方式呈现，并考虑了数据存储在Adobe Experience Platform中的方式。

>[!NOTE]
>
>所描述的ERD是有关如何针对此行业用例建模数据的建议。 要在Platform中使用此数据模型，您必须自行构建推荐的架构及其关系。 请参阅有关管理的指南 [架构](../../ui/resources/schemas.md) 和 [关系](../../tutorials/relationship-ui.md) （在UI中）以了解更多信息。

使用以下图例来解释此ERD：

* 中所示的每个实体均以基础实体 [Experience Data Model (XDM)类](../composition.md#class).
* 对于给定实体，每个行均标记在 **粗体** 表示字段组或数据类型，下面以无粗体文本形式列出了它提供的相关字段。
* 给定实体的最重要字段以红色突出显示。
* 所有可用于识别单个客户的属性都标记为“身份”，其中某个属性标记为“主要身份”。
* 实体关系将标记为非依赖关系，因为基于Cookie的事件通常无法确定执行事务的人员或个人。

![](../../images/industries/retail.png)

>[!NOTE]
>
>体验事件实体包含“_ID”字段，该字段表示唯一标识符(`_id`)属性，由XDM ExperienceEvent类提供。 参阅参考文档 [XDM ExperienceEvent](../../classes/experienceevent.md) 以了解有关此值的预期值的更多详细信息。

## [!UICONTROL 零售] 用例

下表概述了多个常见零售业用例的推荐类和架构字段组。

| 用例 | 推荐的类和字段组 |
| --- | --- |
| 整合在线和离线数据源，并解析跨设备标识和在线/离线标识，以提供整体的跨渠道和跨设备归因报表。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[商业详细信息](../../field-groups/event/commerce-details.md)</li><li>[Web详细信息](../../field-groups/event/web-details.md)</li></ul></li><li>**[产品](../../classes/product.md)**:<ul><li>[产品目录](../../field-groups/product/product-catalog.md)</li><li>[产品类别](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| 为各个区段提供有针对性的个性化体验，以增加收入，并帮助增强全渠道编排的平台。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[营销活动详细信息](../../field-groups/event/campaign-marketing-details.md)</li><li>[渠道详细信息](../../field-groups/event/channel-details.md)</li><li>[商业详细信息](../../field-groups/event/commerce-details.md)</li><li>[环境详细信息](../../field-groups/event/environment-details.md)</li><li>[Web详细信息](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM 个人资料](../../classes/individual-profile.md)**:<ul><li>[人口统计详细信息](../../field-groups/profile/demographic-details.md)</li><li>[个人联系人详细信息](../../field-groups/profile/personal-contact-details.md)</li><li>[工作联系人详细信息](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| 分析多点接触归因以提高营销效率。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[营销活动详细信息](../../field-groups/event/campaign-marketing-details.md)</li><li>[渠道详细信息](../../field-groups/event/channel-details.md)</li><li>[商业详细信息](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM 个人资料](../../classes/individual-profile.md)**:<ul><li>[人口统计详细信息](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| 通过改进男女分段，提高电子邮件相关性。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[商业详细信息](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM 个人资料](../../classes/individual-profile.md)**:<ul><li>[人口统计详细信息](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**[产品](../../classes/product.md)**:<ul><li>[产品目录](../../field-groups/product/product-catalog.md)</li><li>[产品类别](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| 摄取忠诚度（合作伙伴）数据以增加跨Web、电子邮件和数字营销渠道的相关产品信息。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[Web详细信息](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM 个人资料](../../classes/individual-profile.md)**:<ul><li>[人口统计详细信息](../../field-groups/profile/demographic-details.md)</li><li>[忠诚度详细信息](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**[产品](../../classes/product.md)**:<ul><li>[产品目录](../../field-groups/product/product-catalog.md)</li><li>[产品类别](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| 通过自动和个性化的电子邮件重新定位购物车放弃者。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[商业详细信息](../../field-groups/event/commerce-details.md)</li><li>[Web详细信息](../../field-groups/event/web-details.md)</li></ul></li><li>**[产品](../../classes/product.md)**:<ul><li>[产品目录](../../field-groups/product/product-catalog.md)</li><li>[产品类别](../../field-groups/product/product-category.md)</li></ul></li></ul> |

{style="table-layout:auto"}
