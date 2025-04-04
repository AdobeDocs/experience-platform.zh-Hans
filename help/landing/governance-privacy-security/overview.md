---
keywords: Experience Platform；首页；热门话题
solution: Experience Platform
title: 管理、隐私和安全性概述
description: Adobe Experience Platform提供了多种服务和工具，可让您自信地控制收集的体验数据，以符合您的业务实践、法律义务和开发过程。
feature: Data Governance,Privacy
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 8%

---

# Adobe Experience Platform中的治理、隐私和安全性

Adobe Experience Platform允许您摄取、分析、优化和操作数据，从而极大地增强客户体验。 这些数据非常庞大、复杂而且价值难以估量。 根据数据运营的性质、业务运营的法律管辖区以及组织有关数据使用的政策，您必须仔细控制和监控客户体验数据的收集和使用，以保护您的业务利益。

Experience Platform提供了多种服务和工具，可让您放心地控制收集的体验数据，以符合您的业务实践、法律义务和开发流程。 以下各节将介绍其中每项服务，并提供指向相应文档的链接，以便获取更多信息。

这些服务可以分为三个域：

* [数据治理](#governance)
* [隐私](#privacy)
* [安全性](#security)

## 数据治理 {#governance}

数据治理是一个基本概念，与Experience Platform中的每项功能交织在一起。 数据治理表示您能够控制和理解数据通过Experience Platform的整个历程。 这包括维护数据质量、数据谱系、数据编目等。

### Adobe Experience Platform数据管理 {#data-governance}

作为Experience Platform服务，Adobe Experience Platform数据管理允许您管理客户数据，并确保遵守适用于数据使用的法规、限制和策略。 它在各个级别的Experience Platform中发挥着关键作用，包括数据使用标签、数据使用策略、策略实施和数据谱系。

有关详细信息，请参阅[数据管理概述](../../data-governance/home.md)。

### 目录和数据集 {#catalog}

目录服务是Experience Platform中数据位置和谱系的记录系统。 虽然所有摄取到 Experience Platform 中的数据均作为文件和目录存储在数据湖中，但目录中容纳这些文件和目录的元数据和描述以供查找和监控。

目录将摄取的数据整理到数据集中，每个数据集包含可用于标记其所包含的数据并对其进行分类的元数据。

有关该服务的详细信息，请参阅[目录服务概述](../../catalog/home.md)。 要了解如何在Experience Platform中管理数据集，请参阅[数据集概述](../../catalog/datasets/overview.md)。

## 隐私 {#privacy}

隐私对于您的企业、立法者和客户都是一个关键问题。 由于从客户那里收集的个人数据是几乎所有的Experience Platform工作流的核心，因此Experience Platform提供了支持这些计划的服务。

### Adobe Experience Platform Privacy Service {#privacy-service}

欧盟《通用数据保护条例》(GDPR)和《加州消费者隐私法案》(CCPA)等隐私法规授予辖区内公民访问和删除您从他们那里收集和存储的个人数据的权利。

Adobe Experience Platform Privacy Service提供了RESTful API和用户界面来帮助管理这些请求。 借助Privacy Service，您可以提交从Adobe Experience Cloud应用程序访问或删除私人或个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

有关详细信息，请参阅[Privacy Service概述](../../privacy-service/home.md)。

### 同意处理 {#consent}

许多隐私法规在数据收集、个性化和其他营销用例方面引入了对主动和特定同意的要求。 为了满足这些要求，Experience Platform允许您捕获个别客户配置文件中的同意信息，并在如何在下游Experience Platform工作流中使用每个客户的数据时，将这些偏好设置用作决定性因素。

要了解如何使用Adobe标准处理客户同意和偏好设置数据，请参阅有关Experience Platform中的[同意处理](./consent/adobe/overview.md)的概述。

有关如何根据IAB透明度和同意框架(TCF) 2.0处理客户同意数据的信息，请参阅Experience Platform中对[IAB TCF 2.0支持的概述](./consent/iab/overview.md)。

## 安全性 {#security}

数据的完整性和安全性对于您的业务来说是不可或缺的，这种风险需要业界领先的安全功能。 为了迎接这一挑战，Experience Platform提供了多种工具来帮助保护您的数据操作。

### 数据加密

所有Experience Platform数据在传输和静止时都进行加密。 有关更多信息，请参阅介绍 [Experience Platform 中的数据加密](./encryption.md)的文档。

### 访问控制 {#access-control}

Experience Platform使用Adobe Admin Console为各种Experience Platform功能提供基于角色的访问控制。 此功能利用Admin Console中的产品配置文件，它将用户与权限和沙盒关联起来。

有关详细信息，请参阅[访问控制概述](../../access-control/home.md)。

### 沙盒 {#sandboxes}

Experience Platform旨在丰富全球范围内的数字体验应用程序。 公司通常并行运行多个数字体验应用程序，需要满足这些应用程序的开发、测试和部署需要，同时确保操作法规遵从性。

为了满足对开发灵活性的需求，Experience Platform提供了可将单个Experience Platform实例划分为多个单独的虚拟环境的沙箱，以帮助您根据自己的开发生命周期来改进数字体验应用程序。

有关更多信息，请参阅[沙盒概述](../../sandboxes/home.md)。

## 后续步骤

本文档概述了与数据管理、隐私和安全相关的各种Experience Platform服务和工具。 请参阅本指南中链接的文档以了解有关这些功能的更多信息。
