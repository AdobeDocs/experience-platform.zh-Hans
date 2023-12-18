---
title: Partner Prospect Details (Sample)字段组
description: 了解Partner Prospect Details （示例）字段组(XDM)架构字段组。
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 9%

---

# [!UICONTROL Partner Prospect详细信息（示例）] 字段组

[!UICONTROL Partner Prospect详细信息（示例）] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md). 此 [!UICONTROL Partner Prospect详细信息（示例）] 提供与潜在客户配置文件相关的各种详细信息的示例框架。 此框架简化了组织和管理各种与潜在客户相关的信息的过程。

此字段组扩展 [单个目标客户配置文件类](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/prospect.html) 在合作伙伴的上下文中。

![的图表 [!UICONTROL Partner Prospect详细信息（示例）] 字段组。](../../images/field-groups/partner/partner-prospect-details-sample.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|---------------------------------------|-----------------------------|-----------|--------------------------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | 字符串 | 家庭中的年龄范围。 |
| [!UICONTROL 服饰附件] | `apparelAccessories` | 字符串 | 喜好或参与服装/配饰。 |
| [!UICONTROL 自行车] | `bicycling` | 字符串 | 或参与骑车活动。 |
| [!UICONTROL 有线电视] | `cableTv` | 字符串 | 指示与有线电视的互动。 |
| [!UICONTROL 国内学] | `domestics` | 字符串 | 国内活动的偏好或参与。 |
| [!UICONTROL 电子] | `electronics` | 字符串 | 对电子设备的兴趣或参与。 |
| [!UICONTROL 食品和饮料] | `foodAndBeverage` | 字符串 | 对食品/饮料的偏好或参与。 |
| [!UICONTROL 鞋类] | `footwear` | 字符串 | 对鞋类产品的兴趣或参与。 |
| [!UICONTROL 健康食品] | `healthFoods` | 字符串 | 对保健食品的偏好或参与。 |
| [!UICONTROL 健行] | `hiking` | 字符串 | 对登山活动的兴趣或参与。 |
| [!UICONTROL householdId] | `householdId` | 字符串 | 家庭的唯一标识符。 |
| [!UICONTROL individualId] | `individualId` | 字符串 | 个人的唯一标识符。 |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | 字符串 | 成为持卡人的推论。 |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder]` | 字符串 | 成为高级持卡人的推论。 |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | 字符串 | 匹配级别的指示器。 |
| [!UICONTROL 买方评级] | `buyerRating` | 字符串 | 与购买行为相关的评级。 |
| [!UICONTROL 捐赠者评级] | `donorRating` | 字符串 | 与捐赠者行为相关的评级。 |
| [!UICONTROL 投资评级] | `investmentRating` | 字符串 | 与投资行为相关的评级。 |
| [!UICONTROL ResponderRating] | `responderRating` | 字符串 | 与响应者行为相关的评级。 |
| [!UICONTROL 支出周转率] | `spendingVelocity` | 字符串 | 支出的速度或比率。 |
| [!UICONTROL 支出量] | `spendingVolume` | 字符串 | 支出的金额或数量。 |
| [!UICONTROL recordId] | `recordId` | 字符串 | 记录的唯一标识符。 |
| [!UICONTROL residenceId] | `residenceId` | 字符串 | 住宅的唯一标识符。 |
| [!UICONTROL 航行] | `sailing` | 字符串 | 指示对航行活动的兴趣或参与。 |
| [!UICONTROL 季节性假日产品] | `seasonalHolidayProducts` | 字符串 | 指示节假日产品的偏好设置或参与情况。 |
| [!UICONTROL 滑雪] | `skiing` | 字符串 | 表示对滑雪活动的兴趣或参与。 |
| [!UICONTROL 网球] | `tennis` | 字符串 | 表示对网球活动的兴趣或参与。 |
| [!UICONTROL tvShoppers] | `tvShoppers` | 字符串 | 指示参与电视购物。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅 [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-prospect/merkle/prospect-details-partner-sample.schema.json) 在公共XDM存储库中。
