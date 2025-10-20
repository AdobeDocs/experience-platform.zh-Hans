---
title: Talon.One Source概述
description: 了解Adobe Experience Platform上的Talon.One源
badge: Beta 版
hide: true
hidefromtoc: true
source-git-commit: 558a9d6ff3222acbf77edea0a82ef50725cd6203
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 3%

---

# [!DNL Talon.One]

>[!AVAILABILITY]
>
>[!DNL Talon.One]源处于Beta版。 有关使用测试版标记源的更多信息，请阅读源概述中的[条款和条件](../../home.md#terms-and-conditions)。

通过[!DNL Talon.One]，您可以轻松创建、管理和优化针对客户的个性化营销活动。 使用这个强大的平台运行折扣、分发优惠券、启动反向链接计划、设置忠诚度计划并提供游戏化激励 — 所有这些都通过一个可扩展的系统来帮助您吸引和奖励您的受众。

您可以使用Adobe Experience Platform源目录中的[!DNL Talon.One]源从[!DNL Talon.One]帐户中摄取批次和流式会员数据。

* [Talon.One流事件](../../tutorials/ui/create/loyalty/talon-one-streaming.md)
* [Talon.One批处理Source连接器](../../tutorials/ui/create/loyalty/talon-one-batch.md)

>[!TIP]
>
>忠诚度数据是指最终用户的忠诚度计划信息，如忠诚度积分、花费的忠诚度积分、当前级别、授予的优惠券、推荐和成就。

## 先决条件 {#prerequisites}

为以下凭据提供值以验证和连接[!DNL Talon.One Batch Source Connector]。

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| 域 | 与您的[!DNL Talon.One]应用程序环境关联的唯一URL。 确保输入域时不包含协议或路径。 | `acmetalonone.us-east4` |
| [!DNL Talon.One]管理API密钥 | 管理API密钥是用于验证和授权访问[!DNL Talon.One]的管理API的凭据。 这将处理如下操作： <ul><li>正在导入优惠券</li><li>检索营销活动数据</li><li>管理应用程序和端点</li></ul> | `ManagementKey-v1 {YOUR_MANAGEMENT_KEY}` |

## 映射 {#mapping}

为了帮助您根据每个效果对象的唯一`effectType`值来映射该对象，您可以使用数据准备`array_to_map`函数。 这允许您轻松地将无序效果数组转换为符合要求的键值对。 有关指导，请参阅以下示例。

| 来源 | 目标 |
| ---- | --- |
| `array_to_map(data.effects, "effectType").addLoyaltyPoints.campaignId` | `_{TENANT_ID}.loyalty.pointsGained[0].promotionId` |
| `array_to_map(data.effects, "effectType").addLoyaltyPoints.props.value` | `_{TENANT_ID}.loyalty.pointsGained[0].value` |
| `array_to_map(data.effects, "effectType").deductLoyaltyPoints.campaignId` | `_{TENANT_ID}.loyalty.pointsRedemption[0].promotionId` |
| `array_to_map(data.effects, "effectType").acceptCoupon.campaignId` | `_{TENANT_ID}.loyalty.couponRedemption[0].campaignId` |
| `array_to_map(data.effects, "effectType").deductLoyaltyPoints.props.value` | `_{TENANT_ID}.loyalty.pointsRedemption[0].value` |
| `array_to_map(data.effects, "effectType").acceptCoupon.props.value` | `_{TENANT_ID}.loyalty.couponRedemption[0].id` |
| `array_to_map(data.effects, "effectType").setDiscount.campaignId` | `_{TENANT_ID}.loyalty.discounts[0].promotionId` |
| `array_to_map(data.effects, "effectType").setDiscount.props.value` | `_{TENANT_ID}.loyalty.discounts[0].value` |
| `data.created` | `timestamp` |
| `data.attributes.params.profileId` | `personID` |
| `data.attributes.integrationId` | `_id` |
| `data.attributes.params.cartItems[*].name` | `productListItems[*].name` |
| `data.attributes.params.cartItems[*].category` | `productListItems[*].productCategories[0].categoryID` |
| `data.attributes.params.cartItems[*].sku` | `productListItems[*].SKU` |

{style="table-layout:auto"}

## 后续步骤

请阅读以下文档，了解如何将[!DNL Talon.One]帐户连接到Experience Platform并摄取批次和流式处理忠诚度数据。

* [Talon.One流事件](../../tutorials/ui/create/loyalty/talon-one-streaming.md)
* [Talon.One批处理Source连接器](../../tutorials/ui/create/loyalty/talon-one-batch.md)