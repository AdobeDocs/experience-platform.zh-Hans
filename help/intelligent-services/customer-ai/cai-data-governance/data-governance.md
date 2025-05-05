---
keywords: Experience Platform；数据治理；客户人工智能；热门主题
solution: Experience Platform
feature: Customer AI
title: 客户人工智能中的数据治理
description: Adobe Experience Platform提供了多种服务和工具，可让您自信地控制收集的体验数据，以符合您的业务实践、法律义务和开发过程。
exl-id: de0836a4-7bc2-4f9c-95a9-c01dd9e2b03f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 1%

---

# 客户人工智能和客户人工智能中的数据治理

客户人工智能中的任何数据管理相关设置都是从Adobe Experience Platform继承来的。

## 数据治理 {#governance}

客户人工智能和Adobe Experience Platform数据管理之间的集成使您能够控制和理解数据通过Experience Platform的整个历程。 这包括维护数据质量、数据谱系、数据编目等。

在Experience Platform使用的数据集上创建的数据使用标签和策略可以在客户人工智能配置工作流中显示。 这些标签会阻止或警告使用已标记字段的用户。

此集成允许您更有效地管理合规性。 组织中的数据管理员可以设置策略来限制使用。 因此，您可以使用符合数据管理员定义的策略的数据。 阅读有关[标签和策略](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/data-governance.html?lang=zh-Hans)的文档以了解更多信息。

## 同意政策 {#consent-policy}

Customer AI遵循您的同意首选项。 在您[设置并启用您的同意策略](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html?lang=zh-Hans#consent-policy)后，客户人工智能将尊重从您那里收集的同意数据。 在模型的后续运行中，仅使用同意的数据对模型进行评分。 新分数将替换旧分数，并可用于分段。 此功能目前仅适用于HealthCare Shield客户和Privacy and Security shield客户。

您可以在此处了解有关此功能的更多信息：

[Customer AI入门](../../customer-ai/getting-started.md)
[Adobe Experience Platform和应用程序](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=zh-Hans)
[Adobe Experience Cloud架构图](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/experience-cloud.html?lang=zh-Hans)
