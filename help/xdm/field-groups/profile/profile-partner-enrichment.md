---
title: 配置文件合作伙伴扩充（示例）字段组
description: 了解“配置文件合作伙伴扩充（示例）”架构字段组。
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 13%

---


# [!UICONTROL 配置文件合作伙伴扩充（示例）] 架构字段组

[!UICONTROL 配置文件合作伙伴扩充（示例）] 是的标准架构字段组 [[!DNL XDM Individual Profile] 类](../../classes/individual-profile.md). 使用此字段组为客户用户档案提供与合作伙伴驱动的扩充功能相关的其他数据。

![的图表 [!UICONTROL 配置文件合作伙伴扩充（示例）] 字段组。](../../images/field-groups/profile-partner-enrichment-sample.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|-----------------------------|------------------------|-----------|----------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | 字符串 | 家庭中的年龄范围。 |
| [!UICONTROL 服饰附件] | `apparelAccessories` | 字符串 | 服装和附件数据。 |
| [!UICONTROL 自行车] | `bicycling` | 字符串 | 与自行车相关的信息。 |
| [!UICONTROL 有线电视] | `cableTv` | 字符串 | 与有线电视相关的信息。 |
| [!UICONTROL 国内学] | `domestics` | 字符串 | 家庭相关数据。 |
| [!UICONTROL 电子] | `electronics` | 字符串 | 电子信息。 |
| [!UICONTROL 食品和饮料] | `foodAndBeverage` | 字符串 | 食品和饮料数据。 |
| [!UICONTROL 鞋类] | `footwear` | 字符串 | 与鞋类相关的信息。 |
| [!UICONTROL 健康食品] | `healthFoods` | 字符串 | 健康食品数据。 |
| [!UICONTROL 健行] | `hiking` | 字符串 | 与登山有关的信息。 |
| [!UICONTROL householdId] | `householdId` | 字符串 | 家庭的唯一ID。 |
| [!UICONTROL individualId] | `individualId` | 字符串 | 个人的唯一ID。 |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | 字符串 | 推断的持卡人信息。 |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder` | 字符串 | 推断的高级持卡人详细信息。 |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | 字符串 | 匹配级别标志数据。 |
| [!UICONTROL 买方评级] | `buyerRating` | 字符串 | 买方评级信息。 |
| [!UICONTROL 捐赠者评级] | `donorRating` | 字符串 | 捐赠者评级详细信息。 |
| [!UICONTROL 投资评级] | `investmentRating` | 字符串 | 投资评级数据。 |
| [!UICONTROL ResponderRating] | `responderRating` | 字符串 | 响应者评级信息。 |
| [!UICONTROL 支出周转率] | `spendingVelocity` | 字符串 | 支出周转率详细信息。 |
| [!UICONTROL 支出量] | `spendingVolume` | 字符串 | 正在花费数量信息。 |
| [!UICONTROL recordId] | `recordId` | 字符串 | 唯一记录标识符。 |
| [!UICONTROL residenceId] | `residenceId` | 字符串 | 居住的唯一ID。 |
| [!UICONTROL 航行] | `sailing` | 字符串 | 航行相关数据。 |
| [!UICONTROL 季节性假日产品] | `seasonalHolidayProducts` | 字符串 | 季节性假日产品信息。 |
| [!UICONTROL 滑雪] | `skiing` | 字符串 | 与滑雪相关的数据。 |
| [!UICONTROL 网球] | `tennis` | 字符串 | 网球相关信息。 |
| [!UICONTROL tvShoppers] | `tvShoppers` | 字符串 | 电视购物信息。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅 [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-profile-enrichment/profile-partner-enrichment-sample.schema.json) 在公共XDM存储库中。
