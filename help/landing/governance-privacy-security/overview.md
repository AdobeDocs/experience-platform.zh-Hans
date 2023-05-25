---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 治理、隐私和安全性概述
description: Adobe Experience Platform提供了多种服务和工具，使您能够放心地控制收集的体验数据，以遵守您的业务做法、法律义务和开发过程。
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 2%

---

# Adobe Experience Platform中的治理、隐私和安全性

Adobe Experience Platform允许您摄取、分析、优化和操作数据，从而极大地增强客户体验。 这些数据非常庞大、复杂而且极其宝贵。 根据数据运营的性质、业务运营的法律管辖区以及有关数据使用的组织政策，您必须仔细控制和监控客户体验数据的收集和使用情况，以保护您的业务利益。

Experience Platform提供了多种服务和工具，使您能够放心地控制收集的体验数据，以遵守您的业务做法、法律义务和开发流程。 以下各节介绍了其中每项服务，并提供了指向文档的链接以获取更多信息。

这些服务可以分为三个域：

* [数据治理](#governance)
* [隐私](#privacy)
* [安全性](#security)

## 数据治理 {#governance}

数据治理是一个基本概念，与Experience Platform中的每项功能交织在一起。 数据治理表示您能够控制和理解数据通过Platform的整个历程。 这包括维护数据质量、数据谱系、数据编目等。

### Adobe Experience Platform数据管理 {#data-governance}

作为Platform服务，Adobe Experience Platform数据管理允许您管理客户数据，并确保遵守适用于数据使用的法规、限制和策略。 它在各个级别的Experience Platform中发挥着关键作用，包括数据使用标签、数据使用策略、策略实施和数据谱系。

请参阅 [数据治理概述](../../data-governance/home.md) 了解更多信息。

### 目录和数据集 {#catalog}

目录服务是Platform中数据位置和族系的记录系统。 虽然摄取到Experience Platform中的所有数据都将作为文件和目录存储在Data Lake中，但Catalog会保存这些文件和目录的metadata和描述，以供查找和监控。

目录将摄取的数据整理到数据集中，每个数据集包含可用于标记和分类其中所包含数据的元数据。

请参阅 [目录服务概述](../../catalog/home.md) 以了解有关该服务的更多信息。 要了解如何管理Experience Platform中的数据集，请参阅 [数据集概述](../../catalog/datasets/overview.md).

## 隐私 {#privacy}

隐私对于您的企业、立法者和客户都是一个关键问题。 由于从客户那里收集的个人数据是几乎所有的Experience Platform工作流的核心，因此Platform提供服务来支持这些计划。

### Adobe Experience Platform Privacy Service {#privacy-service}

欧盟《通用数据保护条例》(GDPR)和《加州消费者隐私法案》(CCPA)等隐私法规授予辖区内公民访问和删除您从他们那里收集和存储的个人数据的权利。

Adobe Experience Platform Privacy Service提供RESTful API和用户界面，以帮助管理这些请求。 借助Privacy Service，您可以提交从Adobe Experience Cloud应用程序访问或删除私人或个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

请参阅 [Privacy Service概述](../../privacy-service/home.md) 了解更多信息。

### 同意处理 {#consent}

许多法律隐私法规在数据收集、个性化和其他营销用例方面引入了主动和特定同意要求。 为了满足这些要求，Experience Platform允许您捕获单个客户配置文件中的同意信息，并在下游平台工作流中如何使用每个客户的数据时，将这些首选项用作决定性因素。

要了解如何使用Adobe标准处理客户同意和偏好设置数据，请参阅 [Experience Platform中的同意处理](./consent/adobe/overview.md).

有关如何根据IAB透明度和同意框架(TCF) 2.0处理客户同意数据的信息，请参阅以下内容的概述： [平台中的IAB TCF 2.0支持](./consent/iab/overview.md).

## 安全性 {#security}

数据的完整性和安全性对于您的业务来说是不可或缺的，而且这种风险需要行业领先的安全功能。 为了迎接这一挑战， Platform提供了多种工具来帮助保护您的数据操作。

### 数据加密

所有Platform数据在传输和静止时都进行加密。 查看文档 [平台中的数据加密](./encryption.md) 了解更多信息。

### 访问控制 {#access-control}

Experience Platform使用Adobe Admin Console为各种Platform功能提供基于角色的访问控制。 此功能利用Admin Console中的产品配置文件，它将用户与权限和沙盒相关联。

请参阅 [访问控制概述](../../access-control/home.md) 了解更多信息。

### 沙盒 {#sandboxes}

构建Experience Platform是为了在全球范围内丰富数字体验应用程序。 公司通常并行运行多个数字体验应用程序，并且需要满足这些应用程序的开发、测试和部署需要，同时确保运营法规遵从性。

为了满足对开发灵活性的需求，Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的沙箱，以帮助您根据自己的开发生命周期改进数字体验应用程序。

有关更多信息，请参阅[沙盒概述](../../sandboxes/home.md)。

## 后续步骤

本文档概述了与数据管理、隐私和安全相关的各种Platform服务和工具。 请参阅本指南中链接的文档，了解有关这些功能的更多信息。
