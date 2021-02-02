---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Adobe Experience Platform的治理、隐私和安全
topic: overview
description: Experience Platform提供多种服务和工具，使您能够放心地控制收集的体验数据，以符合您的业务实践、法律义务和开发流程。
translation-type: tm+mt
source-git-commit: 6ec317dd790b6ad77d8181c1398934f9636c5f5f
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 0%

---


# Adobe Experience Platform的治理、隐私和安全

Adobe Experience Platform允许您采集、分析、优化和操作数据，以大大增强客户体验。 这些数据庞大、复杂且极具价值。 根据您的数据操作性质、您的业务所在的法律管辖地区以及您有关数据使用的组织政策，您必须仔细控制和监控客户体验数据的收集和使用，以保护您的业务利益。

Experience Platform提供多种服务和工具，使您能够放心地控制收集的体验数据，以符合您的业务实践、法律义务和开发流程。 以下各节介绍了每项服务，并提供了文档链接以获取更多信息。

服务可以分为三个域：

* [数据管理](#governance)
* [隐私](#privacy)
* [安全性](#security)

## 数据管理{#governance}

Experience Platform管理是一个基本概念，它与数据中的每项功能紧密交织。 数据管理代表您在整个平台旅程中控制和理解数据的能力。 这包括保持数据质量、数据承袭、数据编目等。

### Adobe Experience Platform数据治理{#data-governance}

作为一项平台服务，Adobe Experience Platform数据治理允许您管理客户数据并确保遵守适用于数据使用的法规、限制和政策。 它在Experience Platform的不同级别（包括数据使用标签、数据使用策略、策略实施和数据谱系）中起关键作用。

有关详细信息，请参阅[数据管理概述](../../data-governance/home.md)。

### 目录和数据集{#catalog}

目录服务是平台内数据位置和谱系的记录系统。 当所有被引入Experience Platform的数据作为文件和目录存储在数据湖中时，目录会保存这些文件和目录的元数据和描述，以便进行查找和监视。

Catalog将摄取的数据组织到数据集中，每个数据集都包含可用于标记其包含的数据并对其进行分类的元数据。

有关该服务的详细信息，请参阅[目录服务概述](../../catalog/home.md)。 要了解如何管理Experience Platform中的数据集，请参阅[数据集概述](../../catalog/datasets/overview.md)。

## 隐私权 {#privacy}

隐私是您的企业、立法者和客户的关键问题。 由于从Experience Platform收集的个人数据是几乎所有工作流的核心，因此平台提供支持这些计划的服务。

### Adobe Experience Platform Privacy Service{#privacy-service}

法律隐私法规(如欧洲合并的一般数据保护规定(GDPR)和加利福尼亚消费者隐私法(CCPA))授予其管辖范围内的公民访问和删除您从他们那里收集和存储的个人数据的权利。

Adobe Experience Platform Privacy Service提供RESTful API和用户界面来帮助管理这些请求。 通过Privacy Service，您可以提交从Adobe Experience Cloud应用程序访问或删除私人或个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

有关详细信息，请参阅[Privacy Service概述](../../privacy-service/home.md)。

### 同意收集{#consent}

许多法律隐私法规在数据收集、个性化和其他营销用例方面引入了主动明确同意的要求。 为了满足这些要求，Experience Platform允许您捕获单个客户用户档案的同意信息，并将这些偏好用作决定每个客户数据在下游平台工作流中的使用方式的因素。

要了解如何根据IAB透明度和同意框架(TCF)2.0收集和处理客户同意数据，请参阅平台](./consent/iab/overview.md)中[IAB TCF 2.0支持的概述。

<!-- For more information on the consent collection process using the Adobe standard, see the [consent collection overview]. -->

## 安全性 {#security}

数据的完整性和安全性对您的业务来说必不可少，而这一风险需要行业领先的安全功能。 为了应对这一挑战，平台提供了多种工具来帮助保护您的数据操作。

### 访问控制{#access-control}

Experience Platform使用Adobe Admin Console为各种平台功能提供基于角色的访问控制。 此功能利用Admin Console中的产品用户档案，将用户与权限和沙箱关联起来。

有关详细信息，请参阅[访问控制概述](../../access-control/home.md)。

### 沙盒 {#sandboxes}

Experience Platform旨在在全球范围内丰富数字体验应用程序。 公司通常并行运行多个数字体验应用程序，需要满足这些应用程序的开发、测试和部署的需要，同时确保操作合规性。

为了满足开发灵活性的需要，Experience Platform提供沙箱，将单个平台实例分为单独的虚拟环境，帮助您根据自己的开发生命周期开发数字体验应用程序。

有关详细信息，请参阅[沙箱概述](../../sandboxes/home.md)。

## 后续步骤

本文档概述了与数据管理、隐私和安全相关的各种平台服务和工具。 请参阅本指南中链接的文档，进一步了解这些功能。