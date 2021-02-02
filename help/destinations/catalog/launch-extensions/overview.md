---
keywords: 启动扩展；启动扩展；启动目标；平台启动扩展；平台启动扩展；平台启动目标
title: Experience Platform Launch 扩展
seo-title: Experience Platform Launch 扩展
description: Launch 是 Adobe 推出的新一代标签管理功能。Launch 为客户提供了一种部署和管理所有分析、营销和广告标签的简便方法，这些标签是改善相关客户体验所必需的标签。
seo-description: Launch 是 Adobe 推出的新一代标签管理功能。Launch 为客户提供了一种部署和管理所有分析、营销和广告标签的简便方法，这些标签是改善相关客户体验所必需的标签。
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 19%

---


# Adobe Experience Platform Launch 扩展 {#overview.md}

Adobe Experience Platform Launch是Adobe的新一代标签管理功能。  Platform Launch 为客户提供了一种简单的方式来部署和管理所有用来改善相关客户体验的分析、营销和广告标记。Platform Launch作为一项附带的增值功能提供给Adobe Experience Cloud客户。

有关Experience Platform Launch功能的介绍，请参阅以下资源：
- Adobe Experience Platform Launch[文档](https://experienceleague.adobe.com/docs/launch/using/overview.html)
- Adobe Experience Platform Launch[快速开始视频](https://experienceleague.adobe.com/docs/launch/using/intro/get-started/videos.html?)。 开始[Adobe Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU)和[发布流程概述](https://helpx.adobe.com/cn/analytics/how-to/adobe-launch-publishing-process.html)，然后转到下一个概念。

## 如何在平台界面{#how-to-find-extensions-in-interface}中查找Platform Launch扩展

要在平台界面中查找平台启动扩展，请浏览至&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 目录]**，并在&#x200B;**[!UICONTROL 类型]**&#x200B;过滤器中选择&#x200B;**[!UICONTROL 扩展]**。

![界面中的扩展过滤器](../../assets/catalog/launch-extensions/filter.png)

## Platform Launch扩展的工作方式{#how-extensions-work}

Platform Launch扩展将原始事件数据转发到几种类型的目标。 将扩展视为&#x200B;**事件转发**&#x200B;类型的目标。 这是与目标平台的集成的一种更简单类型，目标平台仅转发原始事件数据。 这些示例包括[Gainsight个性化扩展](../personalization/gainsight.md)或[客户扩展的确认语音](../voice/confirmit-digital-feedback.md)。

**用户档案/细分** Adobe Experience Platform的出口目的地捕获事件数据，将其与其他数据源相结合，应用细分，并将细分和合格用户档案导出到目标。例如，[AmazonS3云存储目标](../cloud-storage/amazon-s3.md)或[Google Display &amp; Video 360广告目标](../advertising/google-dv360.md)。

![Experience Platform Launch扩展与其他目标](../../assets/common/launch-and-other-destinations.png)

## 使用Platform Launch扩展{#extensions-benefits}的优势

Adobe Experience Platform Launch对现有Experience Cloud客户免费。 Platform Launch通过易于使用的扩展简化了网站上的标记部署，您可以通过这些扩展进行安装、配置、更新和删除。 Platform Launch占用的网站空间很小，允许您快速加载页面。

>[!IMPORTANT]
>
>虽然您无法将区段激活到Platform Launch扩展，但您可以设置规则，在某些情况下只转发事件数据。 阅读下文。

您可以创建&#x200B;*规则*，这些规则确定何时将事件数据转发到扩展。 此功能强大，您只能在某些情况下转发事件数据，而不是在每次交互时发送事件数据。 有关详细信息，请阅读[Adobe Experience Platform Launch文档](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html)中的规则。

## 平台启动扩展{#extensions-use-cases}的示例使用案例

Platform Launch扩展使您能够满足各种客户使用案例。 使用Platform Launch扩展的一些示例用例包括：

- 您可以通过Facebook像素扩展将网站或本机应用程序数据发送到Facebook。 Facebook像素指示访客导航到您的网站或应用程序的哪些部分，并将该信息转发到Facebook，您可以通过Facebook重新定位访客。
- 您可以将事件数据从您的网站和应用程序转发到Google Analytics，以便根据这些数据进行分析并做出决策。
- 根据您在Platform Launch中设置的规则，您可以根据用户与页面的交互方式在适当的时间打开客户端聊天框应用程序。

## 扩展类别{#extension-categories}

Platform Launch扩展可以属于以下平台类别:

- [广告](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [数据管理平台](../data-management/overview.md)
- [电子邮件营销目标](../email-marketing/overview.md)
- [个性化](../personalization/overview.md)
- [调查](../survey/overview.md)
- [客户之声](../voice/overview.md)
