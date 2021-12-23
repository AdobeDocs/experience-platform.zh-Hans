---
keywords: 标记扩展；标记扩展；launch目标；平台标记扩展；平台标记扩展；platform launch目标
title: 在Adobe Experience Platform中标记扩展
description: Adobe Experience Platform提供了新一代Adobe标签管理功能。 Platform为您提供了一种简单的方式来部署和管理所有用来改善相关客户体验的分析、营销和广告标签。
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: fe71294cb73a25c2c4708b0a6ebe04fc2b97afdf
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---

# 在Adobe Experience Platform中标记扩展

Adobe Experience Platform提供了新一代Adobe标签管理功能。 Platform为您提供了一种简单的方式来部署和管理所有用来改善相关客户体验的分析、营销和广告标签。 标记作为内置增值功能提供给Adobe Experience Cloud客户。

有关标记的简介，请参阅以下资源：

- [标记概述](../../../tags/home.md)
- [快速入门指南](../../../tags/quick-start/quick-start.md)

## 如何在Platform界面中查找标记扩展 {#how-to-find-extensions-in-interface}

要在Platform界面中查找扩展，请浏览 **[!UICONTROL 目标]** > **[!UICONTROL 目录]** 选择 **[!UICONTROL 扩展]** 在 **[!UICONTROL 类型]** 过滤器。

![界面中的扩展筛选器](../../assets/catalog/launch-extensions/filter.png)

## 标记扩展的工作原理 {#how-extensions-work}

A [标记扩展](../../../tags/home.md#extensions) 是可增强网站或移动设备应用程序功能的代码包。 这可能包括将原始事件数据发送到 [Google Analytics](/help/destinations/catalog/analytics/google-universal-analytics.md) 但它们也能发挥其他作用。

区分标记和事件转发扩展非常重要。 Platform目标用户界面中显示的扩展包括 *标记扩展*. 有关 [标记和事件转发之间的差异](/help/tags/ui/event-forwarding/overview.md#differences-between-event-forwarding-and-tags).



<!--

Extensions forward raw event data to several types of destinations. Think of extensions as an **Event Forwarding** type of destination. This is a simpler type of integration with destination platforms, which only forwards raw event data. Examples of those are the [Gainsight personalization extension](../personalization/gainsight.md) or the [Confirmit Voice of the Customer extension](../voice/confirmit-digital-feedback.md).

**Profile/Segment Export** destinations in Adobe Experience Platform capture event data, combine it with other data sources, apply segmentation, and export segments and qualified profiles to destinations. Examples of those are the [Amazon S3 cloud storage destination](../cloud-storage/amazon-s3.md) or the [Google Display & Video 360 advertising destination](../advertising/google-dv360.md).

![Tag extensions compared to other destinations](../../assets/common/launch-and-other-destinations.png)

-->

## 使用标记扩展的好处 {#extensions-benefits}

现有Experience Cloud客户可以免费使用Platform的标记功能。 系统通过易于使用的扩展简化了网站上的标记部署，这些扩展可以安装、配置、更新和删除。 标记在您的网站上占用的空间较小，可让您快速保持页面加载。

虽然无法激活区段以标记扩展，但您可以设置规则以仅在某些情况下转发事件数据。 与在每次交互中发送事件数据相比，这项强大的功能允许您仅在某些情况下转发事件数据。 有关更多信息，请参阅 [标记文档](../../../tags/ui/managing-resources/rules.md).

## 扩展的用例示例 {#extensions-use-cases}

通过扩展，您可以满足各种客户用例。 使用扩展的一些示例用例包括：

- 您可以通过Facebook像素扩展将网站或本机应用程序数据发送到Facebook。 Facebook像素指示访客导航到网站或应用程序的哪些部分，将该信息转发到Facebook，然后您可以通过Facebook重新定位访客。
- 您可以将事件数据从您的网站和应用程序转发到Google Analytics，以便根据这些数据进行分析并做出决策。
- 根据您设置的规则，您可以根据用户与页面进行交互的方式，在适当的时间打开客户端聊天框应用程序。

## 扩展类别 {#extension-categories}

扩展在Platform中可以属于以下类别：

- [广告](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [数据管理平台](../data-management/overview.md)
- [电子邮件营销目标](../email-marketing/overview.md)
- [个性化](../personalization/overview.md)
- [调查](../survey/overview.md)
- [客户之声](../voice/overview.md)
