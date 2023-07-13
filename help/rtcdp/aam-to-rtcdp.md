---
title: 从 Audience Manager 演进到 Real-Time CDP
description: 在规划从 Audience Manager 迁移到 Real-Time CDP 之前了解注意事项。
source-git-commit: 147e95cce203933d591fc807d9d20bcbc06e68e3
workflow-type: ht
source-wordcount: '538'
ht-degree: 100%

---


# 从 Audience Manager 演进到 Real-Time CDP

随着您的组织发展为使用 Adobe Real-Time CDP，请探索这些注意事项以准备您的数据并了解这两种技术之间的关键区别。本文针对的受众为从业人员。

![从 Audience Manager 演进到 Real-Time CDP 的示意图](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## 1. 考虑 Audience Manager 中的数据架构

当您考虑从 Audience Manager 演进到 Real-Time CDP 时，现在是分析 [Audience Manager 区段](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html?lang=en)并确定有哪些[信号](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html?lang=en)、[特征](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html?lang=en)和[规则](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html?lang=en#segment-builder-section)组成这些区段的关键时刻。

此外，请考虑您当前在 Audience Manager 中使用的数据源。

Adobe 建议将区段分为以下几类：

* 可通过 [[!UICONTROL Audience Manager 源连接器]](/help/sources/connectors/adobe-applications/audience-manager.md)发送到 Experience Platform 的区段，这是因为这些区段没有数据依赖关系、没有目标或激活方面的困难并可稍后通过 Real-time CDP [区段生成器](/help/segmentation/ui/segment-builder.md)创建其分段规则。
* 具有可支持但可能包含在 Real-Time CDP 中不可用的规则的区段。
* 无法在 Real-time CDP 中创建且缺少功能的区段。

>[!TIP]
>
>Adobe Real-Time CDP 提供[三种类型的区段评估](/help/segmentation/home.md#evaluate-segments)：[!UICONTROL 批量]、[!UICONTROL 流式]和[!UICONTROL 边缘]。在 Audience Manager 中使用实时区段的客户可能会被当前 Real-Time CDP 中 500 个流式区段的限制所限。阅读有关[分段护栏](/help/profile/guardrails.md)的详细信息。

## 2. 通过 [!UICONTROL Audience Manager 源连接器]发送哪些区段至关重要？

根据其评估标准，应通过 Audience Manager 源连接器发送没有数据依赖关系、没有目标或激活方面的困难并可稍后通过 [Adobe Experience Platform Web SDK](/help/edge/web-sdk-faq.md) 等 Real-Time CDP 数据收藏集创建其分段规则的区段。

## 3. 您是否将使用 [!UICONTROL Experience Cloud 受众]目标将数据带回 Audience Manager？

可通过 [Experience Cloud 受众](/help/destinations/catalog/adobe/experience-cloud-audiences.md)目标卡片将具有可在 Real-Time CDP 中支持的规则但与 Audience Manager 具有激活依赖关系的区段发送到 Audience Manager。

## 4. 今天您在 Audience Manager 中有哪些目标可开始迁移到 Real-Time CDP？

Adobe 强烈建议通过 [!UICONTROL Audience Manager 源连接器]将在 Audience Manager 中激活的发往[基于人员的目标](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=en)的区段推送到 Real-Time CDP，然后通过 Real-Time CDP 激活。

在 Audience Manager 中可找到的所有基于人的目标（[Facebook](/help/destinations/catalog/social/facebook.md)、[[!UICONTROL Google 目标客户匹配功能]](/help/destinations/catalog/advertising/google-customer-match.md)、[LinkedIn](/help/destinations/catalog/social/linkedin.md)）在 Real-Time CDP 中也可找到。

还可找到其他第一方数据和媒体战略合作伙伴，如 [Pinterest](/help/destinations/catalog/advertising/pinterest.md)、[Snapchat](/help/destinations/catalog/advertising/snap-inc.md)、[TikTok](/help/destinations/catalog/social/tiktok.md)、[Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md) 和 [[!UICONTROL The Trade Desk]](/help/destinations/catalog/advertising/tradedesk.md)。

Real-Time CDP 当前原生支持该[目录](/help/destinations/catalog/overview.md)中的 60 多个目标，其中有 20 多个目标是支持第一方受众匹配的广告或社交目标。

## 后续步骤

阅读本页后，您现在总结了一组重要的注意事项，当您开始从 Audience Manager 演进到 Real-Time CDP 时需要遵守这些注意事项。
