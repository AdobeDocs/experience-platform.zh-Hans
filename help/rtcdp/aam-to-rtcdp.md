---
title: 从Audience Manager演变到Real-Time CDP
description: 了解在计划从Audience Manager迁移到Real-Time CDP之前的注意事项。
source-git-commit: 147e95cce203933d591fc807d9d20bcbc06e68e3
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---


# 从Audience Manager演变到Real-Time CDP

随着贵组织不断发展使用Adobe Real-Time CDP，请探索这些注意事项以准备数据并了解这两种技术之间的关键差异。 本文面向从业者受众。

![Audience Manager到Real-Time CDP的演变图](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## 1.考虑Audience Manager中的数据架构

在考虑从Audience Manager到Real-Time CDP的演变时，现在是分析您的产品的重要时刻 [Audience Manager区段](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html?lang=en) 并确定 [信号](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html?lang=en)， [特征](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html?lang=en)、和 [规则](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html?lang=en#segment-builder-section) 是否构成了这些区段。

此外，请思考您当前在Audience Manager中使用的数据源。

Adobe建议您按以下方式为区段分类：

* 可以通过发送到Experience Platform的区段 [[!UICONTROL Audience Manager源连接器]](/help/sources/connectors/adobe-applications/audience-manager.md)，因为它们没有数据依赖性，没有目标或激活挑战，并且可以通过Real-time CDP创建其分段规则 [区段生成器](/help/segmentation/ui/segment-builder.md) 稍后。
* 区段，这些区段具有受支持的规则，但可能包含Real-Time CDP中不可用的数据。
* 无法在Real-time CDP中创建并且缺少功能的区段。

>[!TIP]
>
>Adobe Real-Time CDP优惠 [三类区段评估](/help/segmentation/home.md#evaluate-segments)： [!UICONTROL 批次]， [!UICONTROL 流]、和 [!UICONTROL Edge]. 在Audience Manager中使用实时区段的客户可能会受到Real-Time CDP中500个流区段的当前限制限制。 详细了解 [分段护栏](/help/profile/guardrails.md).

## 2.哪些区段对于通过发送至关重要 [!UICONTROL Audience Manager源连接器]？

基于其评估标准，没有数据依赖关系、无目标或激活挑战以及分段规则的区段可以通过Real-Time CDP数据收集创建，例如 [Adobe Experience Platform Web SDK](/help/edge/web-sdk-faq.md) 以后应通过Audience Manager源连接器发送。

## 3.您是否要使用 [!UICONTROL Experience Cloud受众] 将数据带回Audience Manager的目标？

如果区段包含的规则可在Real-Time CDP中受支持，但与Audience ManagerAudience Manager存在激活依赖关系，则可以通过 [Experience Cloud受众](/help/destinations/catalog/adobe/experience-cloud-audiences.md) 目标卡。

## 4.您目前在Audience Manager中找到了哪些可以开始迁移到Real-Time CDP的目的地？

Adobe强烈建议在Audience Manager中激活的区段 [基于人员的目标](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=en) 通过以下方式推送到Real-Time CDP [!UICONTROL Audience Manager源连接器]，然后通过Real-Time CDP激活。

Audience Manager中可用的所有基于人员的目标 —  [facebook](/help/destinations/catalog/social/facebook.md)， [[!UICONTROL Google客户匹配]](/help/destinations/catalog/advertising/google-customer-match.md)， [linkedIn](/help/destinations/catalog/social/linkedin.md)  — 也在Real-Time CDP中提供。

其他第一方数据和媒体战略合作伙伴，如 [pinterest](/help/destinations/catalog/advertising/pinterest.md)， [Snapchat](/help/destinations/catalog/advertising/snap-inc.md)， [TikTok](/help/destinations/catalog/social/tiktok.md)， [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md)、和 [[!UICONTROL 交易台]](/help/destinations/catalog/advertising/tradedesk.md) 可用。

Real-Time CDP目前以本地方式支持60多个目标， [目录](/help/destinations/catalog/overview.md)，其中20多个是支持第一方受众匹配的广告或社交目标。

## 后续步骤

阅读本页后，在开始从Audience Manager演变到Real-Time CDP时，您现在要了解第一组注意事项。
