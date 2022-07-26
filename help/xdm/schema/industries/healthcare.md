---
title: 医疗保健行业数据模型ERD
description: 查看实体关系图(ERD)，该图描述了医疗保健行业的标准化数据模型。 此数据模型与Experience Data Model(XDM)兼容，可在Adobe Experience Platform中使用。
source-git-commit: 721059a87347e371228d00edeac141afa894af47
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 1%

---

# [!UICONTROL 医疗保健] 行业数据模型ERD

以下实体关系图(ERD)代表了医疗保健行业的标准化数据模型。 ERD特意以非标准化方式呈现，并考虑数据如何存储在Adobe Experience Platform中。

>[!NOTE]
>
>如上所述的ERD是一项建议，建议您如何为此行业用例建模数据。 要在Platform中利用此数据模型，您必须自行构建推荐的架构及其关系。 请参阅管理指南 [模式](../../ui/resources/schemas.md) 和 [关系](../../tutorials/relationship-ui.md) ，以了解更多信息。

请使用以下图例来解释此ERD:

* 中显示的每个实体均基于 [体验数据模型(XDM)类](../composition.md#class).
* 对于给定实体，每行都标记为 **粗体** 表示字段组或数据类型，其提供的相关字段将以非粗体文本列出。
* 给定实体最重要的字段以红色突出显示。
* 所有可用于标识单个客户的资产都会标记为“identity”，其中一个资产会标记为“主要身份”。
* 实体关系被标记为非依赖关系，因为基于Cookie的事件通常无法确定执行交易的人员或个人。

![显示保健行业数据模型的实体关系图的图像](../../images/industries/healthcare.png)

>[!NOTE]
>
>每个实体都包含一个“_ID”字段，它表示唯一字符串标识符(`_id`)属性。 此字段用于跟踪单个记录或事件的唯一性，防止重复数据，并在下游服务中查找该数据。 在某些情况下， `_id` 可以 [通用唯一标识符(UUID)](https://tools.ietf.org/html/rfc4122) 或 [全局唯一标识符(GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>要区分这一点很重要 **此字段不表示与个人相关的身份**，而是数据本身的记录。 与人员、事件或业务实体相关的身份数据应降级为 [身份字段](../composition.md#identity) 由兼容的字段组提供。

## [!UICONTROL 医疗保健] 用例

下表概述了几个常见医疗保健用例的推荐类和模式字段组。

| 用例 | 推荐的类和字段组 |
| --- | --- |
| 提高消费者购买保险的数字化购买体验。 示例包括： <ul><li>当用户访问包含一般信息（如计划、计划名称/层级、医疗补助、健康计划等）的页面时，了解他们的行为以及他们想要查找的内容，以便发送促销电子邮件或通过广告将他们定位到第三方平台。</li><li>当人们搜索心脏健康和疫苗信息时，把与疫苗相关的心脏健康信息发送给他们，以树立品牌意识或让他们安排疫苗接种。</li></ul> | <ul><li>**[[!UICONTROL XDM个人配置文件]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 医疗保健会员详细信息]](../../field-groups/profile/healthcare-member-details.md)</li><li>在 `planID` 属性和架构 [!UICONTROL 计划] 类。</li></ul></li><li>**[[!UICONTROL 付款人]](../../classes/payer.md)**</li><li>**[[!UICONTROL 规划]](../../classes/plan.md)**:<ul><li>[[!UICONTROL 医疗保健计划详细信息]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 应用程序详细信息]](../../field-groups/event/application-details.md)</li><li>[[!UICONTROL 站点工具详细信息]](../../field-groups/event/sitetool-details.md)</li><li>[[!UICONTROL  促销活动营销详细信息]](../../field-groups/event/campaign-marketing-details.md)</li></ul></li></ul> |
| 通过基于过去在线行为和健康数据的定向广告，增加患者的数字化获取。 | <ul><li>**[[!UICONTROL XDM个人配置文件]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 医疗保健会员详细信息]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 提供程序]](../../classes/provider.md)**:<ul><li>[[!UICONTROL 医疗保健提供商]](../../field-groups/provider/healthcare-provider.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Web详细信息]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL 广告详细信息]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| 通过跟踪保险通过不同渠道的营销活动，改进健康计划中的注册和帐户创建，以便了解客户如何了解保险公司。 | <ul><li>**[[!UICONTROL XDM个人配置文件]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 医疗保健会员详细信息]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 付款人]](../../classes/payer.md)**</li><li>**[[!UICONTROL 规划]](../../classes/plan.md)**:<ul><li>[[!UICONTROL 医疗保健计划详细信息]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Web详细信息]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL 广告详细信息]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| 避免医疗保险的漏洞。 | <ul><li>**[[!UICONTROL XDM个人配置文件]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 医疗保健会员详细信息]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 规划]](../../classes/plan.md)**:<ul><li>[[!UICONTROL 医疗保健计划详细信息]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li></ul> |
| 使用直接联系客户(DTC)广告向提供商促销药品信息。 | <ul><li>**[[!UICONTROL XDM个人配置文件]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 医疗保健会员详细信息]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 药物]](../../classes/medication.md)**:<ul><li>[[!UICONTROL 一种保健药物]](../../field-groups/medication/healthcare-medication.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Web详细信息]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL 广告详细信息]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
