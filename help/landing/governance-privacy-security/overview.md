---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 管理、隐私和安全概述
description: Adobe Experience Platform提供了多种服务和工具，使您能够放心地控制收集的体验数据，以符合您的业务惯例、法律义务和开发流程。
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 1%

---

# Adobe Experience Platform中的管理、隐私和安全

Adobe Experience Platform允许您摄取、分析、优化和操作数据，以大大增强客户体验。 这些数据庞大、复杂且极具价值。 根据您的数据操作性质、您的业务运营所在的法律管辖区以及与数据使用有关的组织策略，您必须仔细控制和监控客户体验数据的收集和使用，以保护您的业务利益。

Experience Platform提供了多种服务和工具，使您能够放心地控制收集的体验数据，以符合您的业务惯例、法律义务和开发流程。 以下各节将介绍这些服务中的每项服务，并提供文档链接以获取进一步信息。

这些服务可分为三个域：

* [数据管理](#governance)
* [隐私](#privacy)
* [安全性](#security)

## 数据管理 {#governance}

数据管理是与Experience Platform中的所有功能交织在一起的基本概念。 数据管理是您在整个平台历程中控制和理解数据的能力。 这包括维护数据质量、数据谱系、数据编目等。

### Adobe Experience Platform数据管理 {#data-governance}

作为一项平台服务，Adobe Experience Platform数据管理允许您管理客户数据，并确保遵守适用于数据使用的法规、限制和政策。 它在不同级别（包括数据使用标签、数据使用策略、策略实施和数据谱系）的Experience Platform中发挥关键作用。

请参阅 [数据管理概述](../../data-governance/home.md) 以了解更多信息。

### 目录和数据集 {#catalog}

目录服务是平台内数据位置和谱系的记录系统。 虽然摄取到Experience Platform的所有数据都作为文件和目录存储在数据湖中，但Catalog会保存这些文件和目录的元数据和说明，以便进行查找和监控。

Catalog将摄取的数据整理到数据集中，每个数据集都包含可用于标记其中包含的数据并对其进行分类的元数据。

请参阅 [目录服务概述](../../catalog/home.md) 以了解有关该服务的详细信息。 要了解如何管理Experience Platform中的数据集，请参阅 [数据集概述](../../catalog/datasets/overview.md).

## 隐私 {#privacy}

隐私对您的业务、立法者和客户而言是一个关键问题。 由于从客户收集的个人数据是几乎所有Experience Platform工作流程的核心，因此Platform提供了支持这些计划的服务。

### Adobe Experience Platform Privacy Service {#privacy-service}

法律隐私法规(例如欧盟的《通用数据保护条例》(GDPR)和《加州消费者隐私法案》(CCPA))授予其管辖区的公民访问和删除您从他们那里收集和存储的个人数据的权利。

Adobe Experience Platform Privacy Service提供了RESTful API和用户界面来帮助管理这些请求。 通过Privacy Service，您可以提交从Adobe Experience Cloud应用程序访问或删除私有或个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

请参阅 [Privacy Service概述](../../privacy-service/home.md) 以了解更多信息。

### 同意处理 {#consent}

许多法律隐私法规在数据收集、个性化和其他营销用例方面都引入了主动和特定同意的要求。 为了满足这些要求，Experience Platform允许您捕获单个客户配置文件中的同意信息，并将这些首选项用作在下游Platform工作流中使用每个客户数据的决定性因素。

要了解如何使用Adobe标准处理客户同意和首选项数据，请参阅 [同意处理Experience Platform](./consent/adobe/overview.md).

有关如何根据IAB透明度和同意框架(TCF)2.0处理客户同意数据的信息，请参阅 [平台中的IAB TCF 2.0支持](./consent/iab/overview.md).

## 安全性 {#security}

数据的完整性和安全性对您的业务来说必不可少，而且这种风险需要业界领先的安全功能。 为了应对这一挑战，Platform提供了多种工具来帮助保护您的数据操作。

### 数据加密

所有平台数据在传输过程中和静态时都经过加密。 请参阅 [平台中的数据加密](./encryption.md) 以了解更多信息。

### 访问控制 {#access-control}

Experience Platform使用Adobe Admin Console为各种平台功能提供基于角色的访问控制。 此功能可利用Admin Console中的产品配置文件，将用户与权限和沙箱相关联。

请参阅 [访问控制概述](../../access-control/home.md) 以了解更多信息。

### 沙盒 {#sandboxes}

Experience Platform旨在在全球范围内丰富数字体验应用程序。 公司通常并行运行多个数字体验应用程序，需要满足这些应用程序的开发、测试和部署的需要，同时确保操作合规性。

为了满足开发灵活性的需求，Experience Platform提供了可将单个Platform实例分区为单独虚拟环境的沙盒，以帮助您根据自己的开发生命周期来改进数字体验应用程序。

请参阅 [沙箱概述](../../sandboxes/home.md) 以了解更多信息。

## 后续步骤

本文档概述了与数据管理、隐私和安全相关的各种平台服务和工具。 请参阅本指南中链接的文档，了解有关这些功能的更多信息。
