---
title: Experience Platform Launch扩展
seo-title: Experience Platform Launch扩展
description: Launch 是 Adobe 推出的新一代标签管理功能。Launch 为客户提供了一种简单的方式来部署和管理所有用来加强相关客户体验的分析、营销和广告标签。
seo-description: Launch 是 Adobe 推出的新一代标签管理功能。Launch 为客户提供了一种简单的方式来部署和管理所有用来加强相关客户体验的分析、营销和广告标签。
translation-type: tm+mt
source-git-commit: 98c3356db178507e0a8d94b47030e9490e721e46

---


# Experience Platform Launch extensions {#experience-platform-launch-extensions}

Experience Platform Launch 是 Adobe 推出的新一代标签管理功能。Launch 为客户提供了一种简单的方式来部署和管理所有用来加强相关客户体验的分析、营销和广告标签。Launch是作为附带的增值功能提供给Adobe Experience Cloud客户的。

有关Experience Platform Launch功能的介绍，请参阅以下资源：
* Experience Platform Launch [documentation](https://docs.adobe.com/content/help/zh-Hans/launch/using/overview.translate.html)
* 体验平台启动 [快速开始视频](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/videos.html)。 开始 [Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU) and [Publishing流程概述](https://helpx.adobe.com/cn/analytics/how-to/adobe-launch-publishing-process.html)，然后转到下一个概念。

## 如何在Adobe实时CDP界面中查找Launch扩展 {#how-to-find-extensions-in-interface}

要在Adobe实时CDP界面中查找Launch扩展，请浏览到筛选器并 **[!UICONTROL Destinations > Catalog]** 在筛选 **[!UICONTROL Extensions]** 器中进行 **[!UICONTROL Types]** 选择。

![界面中的扩展过滤器](/help/rtcdp/destinations/assets/extensions-filter.png)

## Launch扩展的工作方式 {#how-extensions-work}

启动扩展将原始事件数据转发到多种类型的目标。 将扩展视为目标 **的事件转发** 类型。 这是与目标平台更简单的集成类型，目标平台仅转发原始事件数据。 这些示例包括 [Gainsight个性化扩展](/help/rtcdp/destinations/gainsight-extension.md) , [或客户扩展的确认声音](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md)。

**Adobe实时客户数据平台中的用户档案/细分导出目标** ，可捕获事件数据，将其与其他数据源组合，应用细分，并将细分和合格用户档案导出到目标。 例如， [Amazon S3云存储目标或](/help/rtcdp/destinations/amazon-s3-destination.md) Google Display &amp; Video 360广告目标 [](/help/rtcdp/destinations/google-dv360-destination.md)。

![Experience Platform Launch扩展与其他目标相比](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

## 使用Launch扩展的优势 {#extensions-benefits}

Experience Platform Launch面向现有Experience Cloud客户免费。 Launch通过易于使用的扩展简化了网站上的标记部署，您可以安装、配置、更新和删除这些扩展。 Launch在您的网站上占用的资源很少，并且允许您快速加载页面。

>[!IMPORTANT]
>
>虽然您无法将区段激活为启动扩展，但您可以设置规则，以仅在某些情况下转发事件数据。 阅读下文。

您可以创建 *规则* ，以确定何时将事件数据转发到扩展。 这一强大的功能使您能够仅在某些情况下转发事件数据，而不是在每次交互时发送事件数据。 有关详细信息，请阅读启动文档中的 [规则](https://docs.adobe.com/help/zh-Hans/launch/using/reference/manage-resources/rules.html)。

## 启动扩展的示例用例 {#extensions-use-cases}

启动扩展功能使您能够满足各种客户使用情况。 一些使用启动扩展的示例用例包括：

* 您可以通过Facebook像素扩展将网站或本机应用程序数据发送到Facebook。 Facebook像素指示访客导航到您的网站或应用程序的哪些部分，并将这些信息转发到Facebook，您可以通过Facebook重新定位访客。
* 您可以将网站和应用程序中的事件数据转发到Google Analytics中，以便根据这些数据进行分析和决策。
* 根据您在Launch中设置的规则，您可以根据用户与页面的交互方式在适当的时间打开客户端聊天框应用程序。


## 扩展类别 {#extension-categories}

Launch扩展可能属于Adobe实时CDP中的以下类别:

* [广告](/help/rtcdp/destinations/advertising-destinations.md)
* [Analytics](/help/rtcdp/destinations/analytics-destinations.md)
* [数据管理平台](/help/rtcdp/destinations/dmp-destinations.md)
* [电子邮件营销目标](/help/rtcdp/destinations/email-marketing-destinations.md)
* [个性化](/help/rtcdp/destinations/personalization-destinations.md)
* [调查](/help/rtcdp/destinations/survey-destinations.md)
* [客户之声](/help/rtcdp/destinations/voice-of-customer-destinations.md)
