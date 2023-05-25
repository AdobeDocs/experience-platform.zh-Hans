---
keywords: Experience Platform；数据治理；客户人工智能；热门主题
solution: Experience Platform
feature: Customer AI
title: 客户人工智能中的数据治理
description: Adobe Experience Platform提供了多种服务和工具，使您能够放心地控制收集的体验数据，以遵守您的业务做法、法律义务和开发过程。
exl-id: de0836a4-7bc2-4f9c-95a9-c01dd9e2b03f
source-git-commit: 0fcdb358882fba7f7923e5d6fc1a947699276e18
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 9%

---

# 客户人工智能和数据治理

客户人工智能中的任何数据治理相关设置都是从Adobe Experience Platform继承来的。

## 数据治理 {#governance}

客户人工智能和Adobe Experience Platform数据管理之间的集成使您能够控制和理解数据通过Platform的整个历程。 这包括维护数据质量、数据谱系、数据编目等。

在Platform使用的数据集上创建的数据使用标签和策略可以在客户人工智能配置工作流中显示。 这些标签会阻止或警告使用已标记字段的用户。

此集成使您能够更高效地管理法规遵从性。 组织中的数据管理员可以设置策略以限制使用。 因此，您可以使用符合数据管理员定义的策略的数据。 阅读相关文档 [标签和策略](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/data-governance.html) 了解更多信息。

## 同意政策 {#consent-policy}

Customer AI遵循您的同意首选项。 一旦您 [设置并启用您的同意策略](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html?lang=zh-Hans#consent-policy)，客户人工智能将遵守从您那里收集的同意数据。 在模型的后续运行中，仅使用同意的数据对模型进行评分。 新分数将取代旧分数，并可用于分段。 此功能目前仅适用于HealthCare Shield客户和Privacy and Security shield客户。

您可以在此处了解有关此功能的更多信息：

[Customer AI入门](../../customer-ai/getting-started.md)
[Adobe Experience Platform与应用程序](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html)
[Adobe Experience Cloud架构图](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/experience-cloud.html)
