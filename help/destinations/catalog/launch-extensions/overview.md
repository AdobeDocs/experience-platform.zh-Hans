---
keywords: 标记扩展；标记扩展；Launch目标；Platform标记扩展；Platform标记扩展；platform launch目标
title: Adobe Experience Platform中的标记扩展
description: Adobe Experience Platform通过Adobe提供了新一代标签管理功能。 Platform为您提供了一种简单的方式来部署和管理所有用来加强相关客户体验的分析、营销和广告标记。
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---

# Adobe Experience Platform中的标记扩展

Adobe Experience Platform通过Adobe提供了新一代标签管理功能。 Platform为您提供了一种简单的方式来部署和管理所有用来加强相关客户体验的分析、营销和广告标记。 标记以内置增值功能的方式提供给Adobe Experience Cloud客户。

有关标记的简介，请参阅以下资源：

- [标记概述](../../../tags/home.md)
- [快速入门指南](../../../tags/quick-start/quick-start.md)

## 如何在Platform界面中找到标记扩展 {#how-to-find-extensions-in-interface}

要在Platform界面中查找扩展，请浏览 **[!UICONTROL 目标]** > **[!UICONTROL 目录]** 并选择 **[!UICONTROL 扩展]** 在 **[!UICONTROL 类型]** 筛选条件。

![界面中的“扩展”过滤器](../../assets/catalog/launch-extensions/filter.png)

## 标记扩展的工作方式 {#how-extensions-work}

A [标记扩展](../../../tags/home.md#extensions) 是一个代码包，用于增强网站或移动设备应用程序的功能。 这可能包括向目标（如）发送原始事件数据 [Google Analytics](/help/destinations/catalog/analytics/google-universal-analytics.md) 但是它们还可以用于其他功能。

区分标记扩展和事件转发扩展非常重要。 Platform目标用户界面中显示的扩展包括 *标记扩展*. 请参阅事件转发概述，了解有关 [标记和事件转发之间的区别](/help/tags/ui/event-forwarding/overview.md#differences-between-event-forwarding-and-tags).



<!--

Extensions forward raw event data to several types of destinations. Think of extensions as an **Event Forwarding** type of destination. This is a simpler type of integration with destination platforms, which only forwards raw event data. Examples of those are the [Gainsight personalization extension](../personalization/gainsight.md) or the [Confirmit Voice of the Customer extension](../voice/confirmit-digital-feedback.md).

**Profile/Segment Export** destinations in Adobe Experience Platform capture event data, combine it with other data sources, apply segmentation, and export audiences and qualified profiles to destinations. Examples of those are the [Amazon S3 cloud storage destination](../cloud-storage/amazon-s3.md) or the [Google Display & Video 360 advertising destination](../advertising/google-dv360.md).

![Tag extensions compared to other destinations](../../assets/common/launch-and-other-destinations.png)

-->

## 使用标记扩展的优势 {#extensions-benefits}

现有Experience Cloud客户可以免费使用Platform的标记功能。 通过易于使用的扩展（您可以安装、配置、更新和删除），该系统简化了您网站上的标记部署。 标记在您的网站上留下很小的痕迹，并允许您保持页面快速加载。

虽然无法激活受众来标记扩展，但您可以设置规则以仅在某些情况下转发事件数据。 此功能强大，您只能在特定情况下转发事件数据，而不是每次交互时发送事件数据。 有关详细信息，请阅读 [标记文档](../../../tags/ui/managing-resources/rules.md).

## 扩展的示例用例 {#extensions-use-cases}

通过扩展，您可以满足各种客户用例。 使用扩展的一些示例用例包括：

- 您可以通过Facebook pixel扩展将网站或本机应用程序数据发送到Facebook。 facebook Pixel指示访客导航到网站或应用程序的哪些部分，将该信息转发到Facebook，并且您可以通过Facebook重新定位访客。
- 您可以将网站和应用程序的事件数据转发到Google Analytics中，以便根据该数据分析和做出决策。
- 根据您设置的规则，您可以根据用户与页面的交互方式，在适当的时间打开客户端聊天盒应用程序。

## 扩展类别 {#extension-categories}

在Platform中，扩展可以属于以下类别：

- [Advertising](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [数据管理平台](../data-management/overview.md)
- [电子邮件营销目标](../email-marketing/overview.md)
- [个性化](../personalization/overview.md)
- [调查](../survey/overview.md)
- [客户的声音](../voice/overview.md)
