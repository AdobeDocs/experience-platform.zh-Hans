---
solution: Experience Platform
title: 零售行业数据模型
topic-legacy: overview
description: 查看零售行业的标准化数据模型，该数据模型与在Adobe Experience Platform中使用的体验数据模型(XDM)兼容。
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 2d7314f11837ca5c5ca1411553f20f58c4cad1ec
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 1%

---

# [!UICONTROL 零售] 行业数据模型

以下实体关系图(ERD)代表零售行业的标准化数据模型。 ERD特意以非标准化方式呈现，并考虑数据如何存储在Adobe Experience Platform中。

>[!NOTE]
>
>如上所述的ERD是一项建议，建议您如何为此行业用例建模数据。 要在Platform中利用此数据模型，您必须自行构建推荐的架构及其关系。 请参阅管理指南 [模式](../../ui/resources/schemas.md) 和 [关系](../../tutorials/relationship-ui.md) ，以了解更多信息。

请使用以下图例来解释此ERD:

* 中显示的每个实体均基于 [体验数据模型(XDM)类](../composition.md#class).
* 对于给定实体，每行都标记为 **粗体** 表示字段组或数据类型，其提供的相关字段将以非粗体文本列出。
* 给定实体最重要的字段以红色突出显示。
* 所有可用于标识单个客户的资产都会标记为“identity”，其中一个资产会标记为“主要身份”。
* 实体关系被标记为非依赖关系，因为基于Cookie的事件通常无法确定执行交易的人员或个人。

![](../../images/industries/retail.png)

>[!NOTE]
>
>体验事件实体包含“_ID”字段，该字段表示唯一标识符(`_id`)属性。 请参阅 [XDM ExperienceEvent](../../classes/experienceevent.md) 以详细了解此值的预期内容。

## [!UICONTROL 零售] 用例

下表概述了几种常见零售用例的推荐类和架构字段组。

| 用例 | 推荐的类和字段组 |
| --- | --- |
| 结合在线和离线数据源，并解决跨设备和在线/离线身份问题，以提供整体的跨渠道和跨设备归因报表。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[商务详细信息](../../field-groups/event/commerce-details.md)</li><li>[Web详细信息](../../field-groups/event/web-details.md)</li></ul></li><li>**[产品](../../classes/product.md)**:<ul><li>[产品目录](../../field-groups/product/product-catalog.md)</li><li>[产品类别](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| 为不同的客户群提供有针对性的个性化体验，以增加收入并帮助在全渠道编排中扩充平台。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[促销活动营销详细信息](../../field-groups/event/campaign-marketing-details.md)</li><li>[渠道详细信息](../../field-groups/event/channel-details.md)</li><li>[商务详细信息](../../field-groups/event/commerce-details.md)</li><li>[环境详细信息](../../field-groups/event/environment-details.md)</li><li>[Web详细信息](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM个人配置文件](../../classes/individual-profile.md)**:<ul><li>[人口统计详细信息](../../field-groups/profile/demographic-details.md)</li><li>[个人联系详细信息](../../field-groups/profile/personal-contact-details.md)</li><li>[工作联系人详细信息](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| 分析多接触点归因以提高营销效率。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[促销活动营销详细信息](../../field-groups/event/campaign-marketing-details.md)</li><li>[渠道详细信息](../../field-groups/event/channel-details.md)</li><li>[商务详细信息](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM个人配置文件](../../classes/individual-profile.md)**:<ul><li>[人口统计详细信息](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| 通过改进男女分类，提高电子邮件相关性。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[商务详细信息](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM个人配置文件](../../classes/individual-profile.md)**:<ul><li>[人口统计详细信息](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**[产品](../../classes/product.md)**:<ul><li>[产品目录](../../field-groups/product/product-catalog.md)</li><li>[产品类别](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| 引入忠诚度（合作伙伴）数据，以增加跨Web、电子邮件和数字营销渠道的相关产品信息。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[Web详细信息](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM个人配置文件](../../classes/individual-profile.md)**:<ul><li>[人口统计详细信息](../../field-groups/profile/demographic-details.md)</li><li>[忠诚度详细信息](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**[产品](../../classes/product.md)**:<ul><li>[产品目录](../../field-groups/product/product-catalog.md)</li><li>[产品类别](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| 通过自动化的个性化电子邮件重新定位购物车放弃者。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[商务详细信息](../../field-groups/event/commerce-details.md)</li><li>[Web详细信息](../../field-groups/event/web-details.md)</li></ul></li><li>**[产品](../../classes/product.md)**:<ul><li>[产品目录](../../field-groups/product/product-catalog.md)</li><li>[产品类别](../../field-groups/product/product-category.md)</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}

*\*虽然计划在将来的版本中构建标准产品类，但当前必须使用自定义类构建产品架构。 因此，您必须手动构建架构类的结构以及添加到该架构的任何字段组的结构。 请参阅 [创建自定义类](../../ui/resources/classes.md#create) ，以了解更多信息。*
