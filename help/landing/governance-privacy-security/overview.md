---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 管理、隐私和安全概述
topic: overview
description: Adobe Experience Platform提供多种服务和工具，使您能够放心地控制收集的体验数据，以符合您的业务实践、法律义务和开发流程。
exl-id: 1ab5a436-c5dd-4e7a-aba1-549f0613f224
translation-type: tm+mt
source-git-commit: 3f7808a08d033c5940d2115006c269b8c4079822
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 1%

---

# Adobe Experience Platform中的管理、隐私和安全

Adobe Experience Platform允许您采集、分析、优化和操作数据，从而大大增强客户体验。 这些数据庞大、复杂且极其宝贵。 根据您的数据操作性质、您的业务所在的法律管辖区以及您关于数据使用的组织策略，您必须仔细控制和监控客户体验数据的收集和使用，以保护您的业务利益。

Experience Platform提供多种服务和工具，使您能够放心地控制收集的体验数据，以符合您的业务实践、法律义务和开发流程。 以下各节介绍了每项服务，并提供了文档链接以获取更多信息。

服务可以分为三个域：

* [数据治理](#governance)
* [隐私](#privacy)
* [安全性](#security)

## 数据治理{#governance}

数据治理是一个基本概念，它与Experience Platform中的每项功能都交织在一起。 数据治理是您在整个平台旅程中控制和理解数据的能力。 这包括保持数据质量、数据传承、数据编目等。

### Adobe Experience Platform数据治理{#data-governance}

作为一项平台服务，Adobe Experience Platform数据治理允许您管理客户数据并确保遵守适用于数据使用的法规、限制和政策。 它在不同级别的Experience Platform（包括数据使用标签、数据使用策略、策略实施和数据谱系）中发挥关键作用。

有关详细信息，请参阅[数据治理概述](../../data-governance/home.md)。

### 目录和数据集{#catalog}

目录服务是平台内数据位置和谱系的记录系统。 虽然摄取到Experience Platform中的所有数据都作为文件和目录存储在数据湖中，但目录保留这些文件和目录的元数据和说明，以用于查找和监视。

Catalog将摄取的数据组织到数据集中，每个数据集都包含可用于标记和分类其包含的数据的元数据。

有关该服务的详细信息，请参阅[目录服务概述](../../catalog/home.md)。 要了解如何管理Experience Platform中的数据集，请参阅[数据集概述](../../catalog/datasets/overview.md)。

## 隐私权 {#privacy}

隐私是您的企业、立法者和客户的关键问题。 由于从您的工作流收集的个人数据几乎是所有Experience Platform的核心，因此平台提供支持这些计划的服务。

### Adobe Experience Platform Privacy Service {#privacy-service}

欧洲合并的一般数据保护规定(GDPR)和加利福尼亚消费者隐私法(CCPA)等法律隐私法规授予其管辖范围内的公民访问和删除您从他们那里收集和存储的个人数据的权利。

Adobe Experience Platform Privacy Service提供RESTful API和用户界面来帮助管理这些请求。 借助Privacy Service，您可以提交从Adobe Experience Cloud应用程序访问或删除私人或个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

有关详细信息，请参阅[Privacy Service概述](../../privacy-service/home.md)。

### 同意处理{#consent}

许多法律隐私法规都在数据收集、个性化和其他营销使用案例方面引入了主动和特定同意的要求。 为了满足这些要求，Experience Platform允许您捕获个别客户用户档案中的同意信息，并将这些偏好用作决定每个客户数据在下游平台工作流中使用方式的因素。

要了解如何使用Adobe标准处理客户同意和偏好数据，请参阅Experience Platform](./consent/adobe/overview.md)中关于[同意处理的概述。

有关如何根据IAB透明度和同意框架(TCF)2.0处理客户同意数据的信息，请参阅平台](./consent/iab/overview.md)中[IAB TCF 2.0支持的概述。

## 安全性 {#security}

数据的完整性和安全性对您的业务至关重要，而这种风险需要行业领先的安全功能。 为了应对这一挑战，平台提供了多种工具来帮助保护您的数据操作。

### 访问控制{#access-control}

Experience Platform使用Adobe Admin Console为各种平台功能提供基于角色的访问控制。 此功能利用Admin Console中的产品用户档案，将用户与权限和沙箱关联起来。

有关详细信息，请参阅[访问控制概述](../../access-control/home.md)。

### 沙盒 {#sandboxes}

Experience Platform旨在在全球范围内丰富数字体验应用程序。 公司经常并行运行多个数字体验应用程序，需要满足这些应用程序的开发、测试和部署的需要，同时确保操作合规性。

为了满足开发灵活性的需要，Experience Platform提供了沙箱，可将单个平台实例分为单独的虚拟环境，以帮助您根据自己的开发生命周期来开发数字体验应用程序。

有关详细信息，请参阅[沙箱概述](../../sandboxes/home.md)。

## 后续步骤

本文档概述了与数据管理、隐私和安全相关的各种平台服务和工具。 请参阅本指南中链接的文档，进一步了解这些功能。
