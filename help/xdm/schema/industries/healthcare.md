---
title: 医疗保健行业数据模型ERD
description: 查看描述医疗保健行业标准化数据模型的实体关系图(ERD)。 此数据模型与Experience Data Model (XDM)兼容，可在Adobe Experience Platform中使用。
exl-id: ebcf97ec-f5a4-46e5-b1ad-c80d55aa2c6e
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 4%

---

# [!UICONTROL 医疗保健] 行业数据模型ERD

以下实体关系图(ERD)代表医疗保健行业的标准化数据模型。 ERD有意以非规范化的方式呈现，并考虑了数据存储在Adobe Experience Platform中的方式。

>[!NOTE]
>
>所描述的ERD是有关如何针对此行业用例对数据进行建模的建议。 要在Platform中使用此数据模型，您必须自行构建推荐的架构及其关系。 请参阅有关管理的指南 [架构](../../ui/resources/schemas.md) 和 [关系](../../tutorials/relationship-ui.md) （在UI中）以了解更多信息。

使用以下图例来解释此ERD：

* 中显示的每个实体都基于一个基础 [Experience Data Model (XDM)类](../composition.md#class).
* 对于给定的实体，每个行均标记在 **粗体** 表示字段组或数据类型，其提供的相关字段以无粗体文本形式列于下方。
* 给定实体的最重要字段以红色突出显示。
* 可用于识别单个客户的所有属性均标记为“身份”，并且其中一个属性标记为“主要身份”。
* 实体关系将标记为非依赖关系，因为基于Cookie的事件通常无法确定执行事务的人员或个人。

![显示医疗保健行业数据模型的实体关系图的图像](../../images/industries/healthcare.png)

>[!NOTE]
>
>每个实体都包含一个“_ID”字段，该字段表示唯一字符串标识符(`_id`)属性。 此字段用于跟踪单个记录或事件的唯一性，防止数据重复，并在下游服务中查找该数据。 在某些情况下， `_id` 可以是 [通用唯一标识符(UUID)](https://tools.ietf.org/html/rfc4122) 或 [全局唯一标识符(GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>区分以下内容非常重要： **此字段不表示与个人相关的身份**&#x200B;而不是数据记录本身。 与人员、事件或业务实体相关的身份数据应委派给 [标识字段](../composition.md#identity) 由兼容的字段组提供。

## [!UICONTROL 医疗保健] 用例

下表概述了多个常见医疗保健用例的推荐类和架构字段组。

| 用例 | 推荐的类和字段组 |
| --- | --- |
| 改善购买保险的消费者的数字获取和体验。 示例包括： <ul><li>当人们访问包含一般信息（如计划、计划名称/层、医疗补助、健康计划等）的页面时，要了解他们的行为以及需要什么，以便发送促销电子邮件或在带有广告的第三方平台上定位他们。</li><li>当人们搜索心脏健康和疫苗信息时，向他们发送有关心脏健康的疫苗相关信息，以建立品牌意识，或让他们安排疫苗接种时间。</li></ul> | <ul><li>**[[!UICONTROL XDM 个人资料]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 医疗保健会员详细信息]](../../field-groups/profile/healthcare-member-details.md)</li><li>在以下内容之间建立关系字段： `planID` 属性和使用 [!UICONTROL 计划] 类。</li></ul></li><li>**[[!UICONTROL 付款人]](../../classes/payer.md)**</li><li>**[[!UICONTROL 规划]](../../classes/plan.md)**:<ul><li>[[!UICONTROL 医疗保健计划详细信息]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL 应用程序详细信息]](../../field-groups/event/application-details.md)</li><li>[[!UICONTROL Sitetool详细信息]](../../field-groups/event/sitetool-details.md)</li><li>[[!UICONTROL  营销活动详细信息]](../../field-groups/event/campaign-marketing-details.md)</li></ul></li></ul> |
| 通过基于过去在线行为和健康数据的定向广告，增加患者的数字获取。 | <ul><li>**[[!UICONTROL XDM 个人资料]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 医疗保健会员详细信息]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 提供商]](../../classes/provider.md)**：<ul><li>[[!UICONTROL 医疗保健提供商]](../../field-groups/provider/healthcare-provider.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL Web详细信息]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL 广告详细信息]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| 通过不同渠道跟踪保险营销，以了解客户如何发现保险公司，从而改进健康计划中的登记和帐户创建。 | <ul><li>**[[!UICONTROL XDM 个人资料]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 医疗保健会员详细信息]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 付款人]](../../classes/payer.md)**</li><li>**[[!UICONTROL 规划]](../../classes/plan.md)**:<ul><li>[[!UICONTROL 医疗保健计划详细信息]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL Web详细信息]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL 广告详细信息]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| 避免医疗保险中断。 | <ul><li>**[[!UICONTROL XDM 个人资料]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 医疗保健会员详细信息]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 规划]](../../classes/plan.md)**:<ul><li>[[!UICONTROL 医疗保健计划详细信息]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li></ul> |
| 使用直接到客户(DTC)广告向供应商促销药物信息。 | <ul><li>**[[!UICONTROL XDM 个人资料]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 医疗保健会员详细信息]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 药物]](../../classes/medication.md)**：<ul><li>[[!UICONTROL 医疗保健]](../../field-groups/medication/healthcare-medication.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**：<ul><li>[[!UICONTROL Web详细信息]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL 广告详细信息]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
