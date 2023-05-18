---
keywords: Experience Platform；数据管理；客户人工智能；热门主题
solution: Experience Platform
feature: Customer AI
title: 客户人工智能中的数据管理
description: Adobe Experience Platform提供了多种服务和工具，使您能够放心地控制收集的体验数据，以符合您的业务惯例、法律义务和开发流程。
exl-id: de0836a4-7bc2-4f9c-95a9-c01dd9e2b03f
source-git-commit: f0bd35d8fb592900c61ed4a1a74d05901bc32810
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 6%

---

# 客户人工智能和数据管理

Customer AI中任何与数据管理相关的设置都继承自Adobe Experience Platform。

## 数据治理 {#governance}

Customer AI与Adobe Experience Platform数据管理之间的集成让您能够在整个Platform历程中控制和理解数据。 这包括维护数据质量、数据谱系、数据编目等。

在Customer AI配置工作流中，可以显示在Platform使用的数据集上创建的数据使用标签和策略。 这些标签可停止或警告使用标记字段的用户。

利用此集成，您可以更高效地管理法规遵从性。 组织中的数据管理员可以设置策略以限制使用。 因此，您可以使用符合数据管理者定义策略的数据。 请阅读相关文档 [标签和策略](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/data-governance.html) 以了解更多。

## 同意策略 {#consent-policy}

Customer AI遵循您的同意首选项。 在您设置同意策略并按此处所述启用该策略后，Customer AI将对从您收集的同意数据予以执行。 只有同意的数据才用于在模型的后续运行中对模型进行评分。 新分数将取代旧分数，可用于分段。 此功能仅适用于HealthCare Shield客户和隐私和安全防护客户。

您可以在此处了解有关此功能的更多信息：

[Customer AI快速入门](../../customer-ai/getting-started.md)
[Adobe Experience Platform和应用程序](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html)
[Adobe Experience Cloud架构图](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/experience-cloud.html)
