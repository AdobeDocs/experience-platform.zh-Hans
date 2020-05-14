---
title: 快速开始Launch
seo-title: Adobe Experience Platform Web SDK快速开始Launch
description: 使用Experience Platform Web SDK扩展收集数据的快速开始指南
seo-description: 使用Experience Platform Web SDK扩展收集数据的快速开始指南
translation-type: tm+mt
source-git-commit: 2ccb2c17590780f7f1bd5e553164209763ab9e24
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 3%

---


# 欢迎

本指南将带您了解如何在Launch中设置Adobe Experience Platform Web SDK。 要能够使用此功能，您需要将其列入白名单。 如果您想继续等待列表，请联系您的CSM。

- 启用 [第一方域(CNAME)](https://docs.adobe.com/content/help/zh-Hans/core-services/interface/ec-cookies/cookies-first-party.html) 。 如果您已经拥有Analytics的CNAME，则应使用该CNAME。 在开发中测试无需CNAME即可正常工作，但在开始生产之前，您需要CNAME
- 有权使用Adobe Experience Platform Data Platform。 如果您尚未购买Platform，我们将为您提供Experience Platform Data Services Foundation，以便在SDK中以有限方式使用，不收取任何额外费用。
- 正在使用最新版的访客ID服务

## 创建配置ID

您可以在启动项中使用边缘配 [置工具创建配](../fundamentals/edge-configuration.md) 置ID。 这将允许边缘网络向各种解决方案发送数据。 有关如何查找每个选项的详细信息，请参阅 [边缘配置工具](../fundamentals/edge-configuration.md) 页。

>[!NOTE]
>
>您的组织必须列入此功能的白名单。 请联系您的CSM，让列表参与最终的白名单。

## 准备模式

Experience Platform Edge Network将数据作为XDM。 XDM是一种数据格式，允许您定义模式。 模式定义边缘网络希望数据的格式。 要发送数据，您需要定义模式。

- [创建模式](../../xdm/tutorials/create-schema-ui.md)
- 将Adobe Experience Platform Web SDK混合添加到您创建的模式

## 在Launch中安装SDK

登录到启动并安装扩 `AEP Web SDK` 展。 在安装SDK时，将提示您配置扩展。 输入您在上面请求的配置ID。 该扩展将自动填充您的组织ID。

有关不同配置选项的更多详细信息，请 [参阅配置SDK](../fundamentals/configuring-the-sdk.md)。

## 根据您的模式创建数据元素

在启动项中，通过将扩展更改为AEP Web SDK并将类型设置为XDM对象，创建引用模式的数据元素。 这将加载模式，并允许您将数据元素映射到模式的不同部分。

![启动项中的日期元素](../../assets/edge_data_element.png)

## 发送事件

安装扩展后，开始通过将AEP Web SDK扩展的“sendEvent”操作添加到规则来发送事件。 请务必将刚创建的事件元素作为XDM数据添加到该数据中。 我们建议您在每次加载页面时至少发送一个事件。

有关如何跟踪事件的更多详细信息，请参阅 [跟踪事件](../fundamentals/tracking-events.md)。

## 后续步骤

数据流动后，您可以执行以下操作。

- [构建模式](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html)
- [了解调试](../fundamentals/debugging.md)
- 了解如何 [个性化体验](../fundamentals/rendering-personalization-content.md)
- 了解如何将数据发送到多个解决方案
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
