---
keywords: launch extensions;launch extension;launch destinations
title: Experience Platform Launch扩展
seo-title: Experience Platform Launch扩展
description: Launch 是 Adobe 推出的新一代标签管理功能。 Launch 为客户提供了一种简单的方式来部署和管理所有用来改善相关客户体验的分析、营销和广告标记。
seo-description: Launch 是 Adobe 推出的新一代标签管理功能。 Launch 为客户提供了一种简单的方式来部署和管理所有用来改善相关客户体验的分析、营销和广告标记。
translation-type: tm+mt
source-git-commit: 15323134f0c626cad2c4e90b3e1c0662cf7e57dd
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 21%

---


# Experience Platform Launch extensions {#experience-platform-launch-extensions}

Experience Platform Launch 是 Adobe 推出的新一代标签管理功能。 Launch 为客户提供了一种简单的方式来部署和管理所有用来改善相关客户体验的分析、营销和广告标记。Launch作为附带的增值功能提供给Adobe Experience Cloud客户。

有关Experience Platform Launch功能的介绍，请参阅以下资源：
* Experience Platform Launch [documentation](https://docs.adobe.com/content/help/zh-Hans/launch/using/overview.translate.html)
* Experience Platform Launch [快速开始视频](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/videos.html)。 开始 [介绍Experience Platform Launch和](https://www.youtube.com/embed/rwqqkG1SERU) 发布流程概 [述](https://helpx.adobe.com/cn/analytics/how-to/adobe-launch-publishing-process.html)，然后转到下一个概念。

## 如何在Adobe实时CDP界面中查找Launch扩展 {#how-to-find-extensions-in-interface}

要在Adobe实时CDP界面中查找启动扩展，请浏 **[!UICONTROL 览到目标]** >目 **[!UICONTROL 录]** ，然后 **[!UICONTROL 在类型过]** 滤器中选择 **** 扩展。

![界面中的扩展过滤器](/help/rtcdp/destinations/assets/extensions-filter.png)

## Launch扩展的工作方式 {#how-extensions-work}

启动扩展将原始事件数据转发到几种类型的目标。 将扩展视为目 **标的事件** 转发类型。 这是与目标平台的集成的一种更简单类型，目标平台仅转发原始事件数据。 例如Gainsight个性化 [扩展](/help/rtcdp/destinations/gainsight-extension.md)[或客户扩展的确认声音](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md)。

**用户档案/细分** Adobe实时客户数据平台捕获事件数据，将其与其他数据源相结合，应用细分，并将细分和合格用户档案导出到目标。 例如， [AmazonS3云存储目](/help/rtcdp/destinations/amazon-s3-destination.md) 标或Google Display &amp; Video 360广告目标 [](/help/rtcdp/destinations/google-dv360-destination.md)。

![Experience Platform Launch扩展与其他目标](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

## 使用Launch扩展的优势 {#extensions-benefits}

Experience Platform Launch对现有Experience Cloud客户是免费的。 Launch通过易于使用的扩展简化了网站上的标记部署，您可以安装、配置、更新和删除这些扩展。 Launch占用的网站空间很小，可让您快速保持页面加载。

>[!IMPORTANT]
>
>虽然您无法将区段激活为启动扩展，但您可以设置规则，以仅在某些情况下转发事件数据。 阅读下文。

您可以创建 *规则* ，确定何时将事件数据转发到扩展。 此功能强大，您只能在某些情况下转发事件数据，而不是在每次交互时发送事件数据。 有关详细信息，请阅读启动文档中 [的规则](https://docs.adobe.com/help/zh-Hans/launch/using/reference/manage-resources/rules.html)。

## Launch扩展的示例使用案例 {#extensions-use-cases}

启动扩展使您能够满足各种客户使用案例。 一些使用启动扩展的示例用例包括：

* 您可以通过Facebook像素扩展将网站或本机应用程序数据发送到Facebook。 Facebook像素指示访客导航到您的网站或应用程序的哪些部分，并将该信息转发到Facebook，您可以通过Facebook重新定位访客。
* 您可以将事件数据从您的网站和应用程序转发到Google Analytics，以便根据这些数据进行分析并做出决策。
* 根据您在Launch中设置的规则，您可以根据用户与页面的交互方式在适当的时间打开客户端聊天框应用程序。


## 扩展类别 {#extension-categories}

在Adobe实时CDP中，Launch扩展可能属于以下类别:

* [广告](/help/rtcdp/destinations/advertising-destinations.md)
* [Analytics](/help/rtcdp/destinations/analytics-destinations.md)
* [数据管理平台](/help/rtcdp/destinations/dmp-destinations.md)
* [电子邮件营销目标](/help/rtcdp/destinations/email-marketing-destinations.md)
* [个性化](/help/rtcdp/destinations/personalization-destinations.md)
* [调查](/help/rtcdp/destinations/survey-destinations.md)
* [客户之声](/help/rtcdp/destinations/voice-of-customer-destinations.md)
