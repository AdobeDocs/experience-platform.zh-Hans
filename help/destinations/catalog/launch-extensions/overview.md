---
keywords: launch扩展；launch扩展；launch目标；platform launch扩展；platform launch扩展；platform launch目标
title: Adobe Experience Platform Launch扩展
description: Adobe Experience Platform Launch是Adobe推出的新一代标签管理功能。  Platform Launch 为客户提供了一种简单的方式来部署和管理所有用来改善相关客户体验的分析、营销和广告标记。
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: 20a9103dd96116f3099bccc9eeb678be5ac2bb79
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 12%

---

# Adobe Experience Platform Launch 扩展

Adobe Experience Platform Launch是Adobe推出的新一代标签管理功能。  Platform Launch 为客户提供了一种简单的方式来部署和管理所有用来改善相关客户体验的分析、营销和广告标记。platform launch以内置增值功能的形式提供给Adobe Experience Cloud客户。

有关Experience Platform Launch功能的简介，请参阅以下资源：

- Adobe Experience Platform Launch [documentation](https://experienceleague.adobe.com/docs/launch/using/home.html)
- Adobe Experience Platform Launch [快速入门视频](https://experienceleague.adobe.com/docs/launch/using/intro/get-started/videos.html?)。 从[Adobe Experience Platform Launch简介](https://www.youtube.com/embed/rwqqkG1SERU)和[发布流程概述](https://helpx.adobe.com/cn/analytics/how-to/adobe-launch-publishing-process.html)开始，然后转到下一个概念。

## 如何在Platform界面{#how-to-find-extensions-in-interface}中查找Platform launch扩展

要在Platform界面中查找Platform launch扩展，请浏览到&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 目录]**&#x200B;并在&#x200B;**[!UICONTROL 类型]**&#x200B;筛选器中选择&#x200B;**[!UICONTROL 扩展]**。

![界面中的扩展筛选器](../../assets/catalog/launch-extensions/filter.png)

## platform launch扩展的工作原理{#how-extensions-work}

platform launch扩展会将原始事件数据转发到多种类型的目标。 将扩展视为&#x200B;**事件转发**&#x200B;类型的目标。 这是与目标平台的更简单集成类型，目标平台仅转发原始事件数据。 例如，[Gainsight个性化扩展](../personalization/gainsight.md)或[客户扩展的确认语音](../voice/confirmit-digital-feedback.md)。

**Adobe Experience Platform中的配** 置文件/区段导出目标可捕获事件数据，将其与其他数据源组合，应用分段，并将区段和符合条件的配置文件导出到目标。例如，[Amazon S3云存储目标](../cloud-storage/amazon-s3.md)或[Google Display &amp; Video 360广告目标](../advertising/google-dv360.md)。

![Experience Platform Launch扩展与其他目标的比较](../../assets/common/launch-and-other-destinations.png)

## 使用Platform launch扩展{#extensions-benefits}的好处

Adobe Experience Platform Launch对现有Experience Cloud客户免费。 platform launch通过易于使用的扩展简化了网站上的标记部署，这些扩展可以安装、配置、更新和删除。 platform launch在您的网站上占用的空间很小，允许您快速保持页面加载。

>[!IMPORTANT]
>
>虽然您无法激活区段以Platform launch扩展，但可以设置规则以仅在某些情况下转发事件数据。 请阅读下文。

您可以创建&#x200B;*规则*&#x200B;来确定何时将事件数据转发到扩展。 与在每次交互中发送事件数据相比，这项强大的功能允许您仅在某些情况下转发事件数据。 有关更多信息，请参阅[Adobe Experience Platform Launch文档](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html)中的规则。

## platform launch扩展{#extensions-use-cases}的用例示例

platform launch扩展使您能够满足各种客户用例。 使用Platform launch扩展的一些示例用例包括：

- 您可以通过Facebook像素扩展将网站或本机应用程序数据发送到Facebook。 Facebook像素指示访客导航到网站或应用程序的哪些部分，将该信息转发到Facebook，然后您可以通过Facebook重新定位访客。
- 您可以将事件数据从您的网站和应用程序转发到Google Analytics，以便根据这些数据进行分析并做出决策。
- 您可以根据用户与页面交互的方式，根据您在Platform launch中设置的规则，在适当的时间打开客户端聊天框应用程序。

## 扩展类别{#extension-categories}

platform launch扩展可以在Platform中属于以下类别：

- [广告](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [数据管理平台](../data-management/overview.md)
- [电子邮件营销目标](../email-marketing/overview.md)
- [个性化](../personalization/overview.md)
- [调查](../survey/overview.md)
- [客户之声](../voice/overview.md)
