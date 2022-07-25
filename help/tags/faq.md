---
title: 标记疑难解答指南
description: 获取有关Adobe Experience Platform中标记的常见问题解答。
exl-id: c06b8e25-4d79-4a11-94da-94ac096b5e33
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 27%

---

# 标记疑难解答指南

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](./term-updates.md)。

本文档提供了有关Adobe Experience Platform中标记的常见问题解答。

## 什么是标记？

标记是由Adobe提供的新一代标签管理功能，内置于Adobe Experience Platform中。 标记使客户能够：

- 使用称为“扩展”**&#x200B;的集成部署客户端 Web 产品
- 以动态方式交付配置来更新本机移动设备应用程序中的客户端实现
- 始终捕获、定义和管理数据以及在其他供应商和 Adobe 提供的营销和广告产品之间共享数据

标记是一种高级代码和配置交付系统，可对各种条件进行评估并执行相应操作，从而高效部署客户端库和产品。 它们还提供了一种高度可伸缩的集成管理和构建方法，并具有一组用于程序化交互的强大API。

## 标记的成本是多少？

标记无需额外付费。 它们可供任何 [!DNL Adobe Experience Cloud] 客户。

## 我听说，现在已经推出了插件。是什么插件？

标记内置于Adobe Experience Platform中，且具有完全可扩展性。 客户、Adobe合作伙伴、代理以及营销或广告技术供应商可以构建标记扩展，以添加新功能或修改现有功能。 该系统允许合作伙伴和客户自行构建、管理和更新集成。这只是Adobe开放Adobe Experience Platform的一种方式，这样客户和合作伙伴便可以在其上构建产品和业务。 这样可以帮助所有人更轻松地将 Adobe 技术与由其他供应商提供的营销和广告技术相连接。

## 所有第三方扩展都将立即可用吗？

扩展已经可用于Adobe解决方案，以及大量日益增多的独立分析、营销、广告、同意供应商和技术。 我们将继续与合作伙伴一起扩展这个生态系统。由于扩展可以由技术所有者进行构建、管理和更新，因此客户无需等待Adobe工程团队来构建它们。

## 客户或合作伙伴何时可以构建扩展？

标记已打开其虚拟自助门户，扩展开发人员可以使用该门户自行构建与Adobe Cloud Platform的集成。

我们有许多客户还选择使用相同的扩展开发方法构建自己的专用扩展，以便仅在自己的公司内使用。

## 标记是否符合我公司的安全标准？

标记符合SOC-2和《格雷姆 — 里奇 — 比利雷法案》。 标记还提供了自托管功能。 您可以从自己的服务器或所选的CDN为JavaScript库和移动配置提供服务。 对于 I.T. 和安全团队来说，这使您能够运行自动化测试、将文件签入到您自己的版本控制系统中，以及完全遵循任何内部生产迁移过程（与安全相关或其他方面的过程）。

## 我何时可以移动到标记？

现在是转到标记的最佳时机。 迁移过程可以轻松地将DTM资产复制到标记中。 虽然我们建议进行大量测试，但我们还是尽可能多地实现了自动化（无需更改页面上的嵌入代码，以及自动迁移规则和数据元素）。

## 标记是否支持单页应用程序和我喜爱使用的框架？

可以。标记能够让用户和扩展开发人员灵活收集、管理和分发单页应用程序体验或Ajax密集型页面或网站中的数据。 无论您喜爱使用何种开发框架（Angular、React.js、Ember、Meteor 等），该产品均适用。

## 标记是否支持动态数据层？

可以。标记包括专门用于侦听动态数据层更改的扩展。

## 标记支持哪些事件类型？

事件类型通过扩展提供。支持的事件类型数量因扩展而异。 例如，YouTube 扩展包含四种视频事件类型：播放、暂停、结束和播放时间。通过扩展，标记可以支持任何其他浏览器事件类型或合成事件类型，如特定访客活动序列。

## 标记会加快（或减慢）我的网站运行速度吗？

标记旨在使用当今的最佳实践，尽可能高效地在您的网站上提供并运行营销和广告技术。 经证明，与提供类似功能的其他方法相比，如果使用得当，标记可以提高网站的性能。

## 标记支持哪些浏览器？

浏览器支持标记：

- [!DNL Chrome]（最新版）
- [!DNL Safari]（最新版）
- [!DNL Firefox]（最新版）
- [!DNL Microsoft Edge]（最新版）
- [!DNL Internet Explorer]（10 及更高版本）
- [!DNL iOS Safari]（最新版）
- [!DNL Android Chrome]（最新版）

浏览器支持标记应用程序界面：

- [!DNL Chrome]（最新版）
- [!DNL Safari]（最新版）
- [!DNL Firefox]（最新版）
- [!DNL Microsoft Edge]（最新版）

大多数Adobe客户端都利用当前浏览器中更新的Web平台功能来创建更好的用户体验，包括单页应用程序以及交互式Ajax密集型网站和页面。 由于大多数客户在其网站上转为使用更新的方法，因此他们需要诸如标记之类的解决方案来启用这些方法。

## 本机移动设备应用程序上是否可以使用标记？

是！标记现在支持新Adobe Experience Platform的移动属性和配置 [Mobile SDK](https://sdkdocs.com) 用于在本机移动设备应用程序环境中实施数据收集和交付。 请访问[文档](https://sdkdocs.com)以了解更多信息。

## UI为何会显示加载我的帐户时出错？

如果您收到一条消息，指出加载帐户时出错，则表示您的帐户不属于任何标记产品配置文件。 请参阅 [管理权限](../collection/permissions.md) 了解如何在Adobe Admin Console中配置产品配置文件以授予对数据收集UI的访问权限。

## 为何无法在UI中添加任何属性？

如果您在登录到数据收集UI时无法创建任何新属性，则意味着您的帐户不属于具有“管理属性”权限的产品配置文件。

请参阅 [管理权限](../collection/permissions.md) 了解如何在Adobe Admin Console中配置产品配置文件以授予“管理资产”权限。 有关标记不同权限的更多信息，请参阅 [标记的用户权限](./ui/administration/user-permissions.md).

## 如果我遇到其他问题，该怎么办？

如果您还有其他问题，可以在 [Adobe Experience Platform数据收集社区页面](https://adobe.com/go/launchme) Experience League，或加入 [面向标签开发人员的官方Slack组](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform).
