---
keywords: Experience Platform；主页；数据科学工作区；热门主题；数据科学工作区；数据科学
solution: Experience Platform
title: 数据科学工作区概述
topic-legacy: overview
description: 本指南概述与Adobe Experience Platform中的数据科学工作区相关的关键概念。
exl-id: bef25073-0dfb-453d-8c32-7f44d917d62d
source-git-commit: 4119242fef46d916e90e1dfb95f7e8fb9e8902f0
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 0%

---

# 数据科学工作区概述

Adobe Experience Platform [!DNL Data Science Workspace] 使用机器学习和人工智能从数据中释放洞察信息。 集成到Adobe Experience Platform, [!DNL Data Science Workspace] 可帮助您跨Adobe解决方案使用内容和数据资产进行预测。

所有技能水平的数据科学家都会找到复杂且易于使用的工具，这些工具支持机器学习方法的快速开发、培训和调整 — 所有AI技术的好处，而不需要复杂性。

使用 [!DNL Data Science Workspace]，数据科学家可以轻松创建由机器学习提供支持的智能服务API。 这些服务可与其他Adobe服务(包括Adobe Target和Adobe Analytics Cloud)一起使用，帮助您在Web、桌面和移动设备应用程序中自动提供个性化、有针对性的数字体验。

本指南概述与 [!DNL Data Science Workspace].

## 简介

如今的企业高度重视挖掘大数据以进行预测和分析，这些预测和分析将帮助他们个性化客户体验并为客户乃至业务提供更多价值。
从数据到洞察信息，同样重要的是，成本也很高。 它通常需要技术娴熟的数据科学家来进行密集且耗时的数据研究，以开发机器学习模型或方法，从而推动智能服务。 这个过程很漫长，技术也很复杂，而且很难找到熟练的数据科学家。

使用 [!DNL Data Science Workspace], Adobe Experience Platform允许您在整个企业中引入以体验为中心的AI，通过以下功能简化并加速数据到分析到代码的转换：
- 机器学习框架和运行时
- 集成访问存储在Adobe Experience Platform中的数据
- 基于构建的统一数据模式 [!DNL Experience Data Model] (XDM)
- 机器学习/人工智能和管理大数据集所必不可少的计算能力
- 预建的机器学习方法，可加快向AI驱动体验的飞跃
- 为不同技能水平的数据科学家简化方法的创作、重用和修改
- 只需点击几下即可发布和共享智能服务（无需开发人员），并监控和再培训以持续优化个性化客户体验

所有技能水平的数据科学家都将更快地获得更快、更有效的数字体验。

## 快速入门

在深入研究 [!DNL Data Science Workspace]，以下是关键术语的简要摘要：

| 搜索词 | 定义 |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Data Science Workspace] | [!DNL Data Science Workspace] within [!DNL Experience Platform] 使客户能够利用跨站点的数据创建机器学习模型 [!DNL Experience Platform] 和Adobe解决方案，以生成智能的洞察和预测，从而打造令人愉悦的最终用户数字体验。 |
| 人工智能 | 人工智能是计算机系统的理论和发展，能够执行通常需要人类智能的任务，如视觉感知、语音识别、决策和语言之间的翻译。 |
| 机器学习 | 机器学习是一个研究领域，它使计算机能够学习，而不用被明确编程。 |
| [!DNL Sensei] ML框架 | [!DNL Sensei] ML框架是跨Adobe的统一机器学习框架，可利用 [!DNL Experience Platform] 以更快、可扩展和可重用的方式，让数据科学家在开发机器学习驱动的智能服务方面获得能力。 |
| [!DNL Experience Data Model] | [!DNL Experience Data Model] (XDM)是Adobe在定义标准架构(例如 [!DNL Profile] 和 [!DNL ExperienceEvent]，用于客户体验管理。 |
| [!DNL JupyterLab] | [!DNL JupyterLab] 是适用于Project Jupyter的基于Web的开源界面，并紧密集成到 [!DNL Experience Platform]. |
| 方法 | 方法是Adobe对模型规范的术语，它是一个顶级容器，代表构建和执行训练模型所需的特定机器学习、AI算法或算法组合、处理逻辑和配置，从而帮助解决特定业务问题。 |
| 模型 | 模型是机器学习方法的一个实例，该方法使用历史数据和配置进行培训，以针对业务用例进行求解。 |
| 培训 | 培训是从标记数据中学习模式和洞察信息的过程。 |
| 训练模型 | 训练模型表示模型训练过程的可执行输出，其中一组训练数据被应用到模型实例。 经过培训的模型将保留对从中创建的任何智能Web服务的引用。 训练好的模型适合于评分和创建智能Web服务。 可以将对训练模型的修改作为新版本进行跟踪。 |
| 评分 | 评分是使用经过训练的模型从数据生成洞察的过程。 |
| 服务 | 已部署的服务通过API公开人工智能、机器学习模型或高级算法的功能，以便其他服务或应用程序能够使用该服务来创建智能应用程序。 |

下图概述了“方法”、“模型”、“培训运行”和“评分运行”之间的层次结构关系。

![](./images/home/recipe_hiearchy_ui.png)

## 了解 [!DNL Data Science Workspace]

使用 [!DNL Data Science Workspace]，您的数据科学家可以简化在大型数据集中发现洞察的繁琐流程。 构建于通用的机器学习框架和运行时之上， [!DNL Data Science Workspace] 提供高级工作流管理、模型管理和可扩展性。 智能服务支持重复使用机器学习方法来为使用Adobe产品和解决方案创建的各种应用程序提供支持。

### 一站式数据访问

数据是人工智能和机器学习的基石。

[!DNL Data Science Workspace] 与Adobe Experience Platform，包括数据湖， [!DNL Real-time Customer Profile]和 [!DNL Unified Edge]. 同时浏览存储在Adobe Experience Platform中的所有组织数据，以及常见的大数据和深层学习库，例如 [!DNL Spark] ML和 [!DNL TensorFlow]. 如果找不到所需内容，请使用XDM标准化架构摄取您自己的数据集。

### 预建的机器学习方法

[!DNL Data Science Workspace] 包括预建的机器学习方法，可满足常见的业务需求，如零售销售预测和异常检测，因此数据科学家和开发人员不必从头开始。 目前提供了三种配方， [产品购买预测](./pre-built-recipes/product-purchase-prediction.md), [产品推荐](./pre-built-recipes/product-recommendations.md)和 [零售销售](./pre-built-recipes/retail-sales.md).

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

如果您愿意，可以根据需要调整预建方法、导入方法或从头开始构建自定义方法。 但是，您开始培训并超调配方后，创建自定义智能服务并不需要开发人员 — 只需点击几下，您就可以打造有针对性的个性化数字体验。

### 以数据科学家为核心的工作流

无论您具备多大的数据科学专业知识， [!DNL Data Science Workspace] 有助于简化并加速在数据中找到洞察并将其应用于数字体验的过程。

### 数据探索

找到正确的数据并准备数据是构建有效方法中劳动密集程度最高的部分。 [!DNL Data Science Workspace] 而Adobe Experience Platform将帮助您更快地从数据获取分析。

在Adobe Experience Platform上，您的跨渠道数据将集中存储在XDM标准化架构中，因此数据更易于查找、理解和清理。 基于通用模式的单一数据存储可以为您节省无数个小时的数据探索和准备。

浏览时，使用R， [!DNL Python]，或通过集成、托管的 [!DNL Jupyter Notebook] 浏览上的数据目录 [!DNL Platform]. 使用其中一种语言，您还可以 [!DNL Spark] ML和TensorFlow。 从头开始，或使用为特定业务问题提供的笔记本模板之一。

在数据探索工作流中，您还可以摄取新数据或使用现有功能来帮助进行数据准备。

### 创作

使用 [!DNL Data Science Workspace]，您可以决定创作方法。

- 浏览可满足您业务需求的预建方法，节省时间，您可以按原样使用或配置，以满足您的特定要求。
- 使用Jupyter Notebook中的创作运行时从头开始创建方法，以开发和注册方法。
- 将在Adobe Experience Platform以外创作的方法上传到 [!DNL Data Science Workspace] 或从存储库导入方法代码，例如 [!DNL Git]，使用 [!DNL Git] 和 [!DNL Data Science Workspace].

### 实验

数据科学工作区为实验过程提供了巨大的灵活性。 从你的配方开始。 然后，使用与特定特性（如超调参数）配对的相同核心算法创建一个单独的实例。 您可以根据需要创建任意数量的实例，并根据需要多次对每个实例进行培训和评分。 你训练他们时， [!DNL Data Science Workspace] 跟踪方法、方法实例和经过培训的实例，以及评估量度，因此您不必这样做。

### 操作化

当您对自己的食谱感到满意时，只需点击几下，即可创建一项智能服务。 无需编码 — 您无需邀请开发人员或工程师，即可自行完成。 最后，将智能服务发布到AdobeIO，以便您的数字体验团队使用。

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### 持续改进

[!DNL Data Science Workspace] 跟踪智能服务的调用位置及其执行情况。 当数据滚入时，您可以评估智能服务的准确性以关闭环路，并根据需要重新培训配方以提高性能。 这样，客户个性化的精准度就得到了不断的提升。

### 访问新增功能和数据集

数据科学家一旦通过Adobe服务提供新技术和数据集，就可以利用它们。 通过频繁更新，我们会致力于将数据集和技术集成到平台中，因此您不必再进行此类更新。

### 安全与心安

保护数据是Adobe的首要任务。 Adobe通过旨在帮助遵守行业公认的标准、法规和认证的安全流程和控制来保护您的数据。

作为Adobe安全产品生命周期的一部分，安全性内置于软件和服务中。
要了解Adobe数据和软件安全性、合规性等信息，请访问安全页面： https://www.adobe.com/security.html。

## [!DNL Data Science Workspace] 操作

预测和分析可为您提供所需的信息，以便向访问您的网站、联系您的呼叫中心或参与其他数字体验的每位客户提供高度个性化的体验。 下面是您的日常工作如何通过 [!DNL Data Science Workspace].

### 定义问题

一切都始于商业问题。 例如，在线呼叫中心需要上下文以帮助他们将负面客户情绪转化为正面情绪。

有关客户的大量数据。 他们浏览了网站，将商品放入购物车，甚至下了订单。 他们可能已收到电子邮件、使用优惠券或以前联系过呼叫中心。 然后，方法需要使用有关客户及其活动的可用数据来确定购买倾向，并推荐客户可能喜欢和使用的选件。

![](./images/home/example_problem.png)

在呼叫中心联系时，客户在购物车中仍有两双鞋，但移除了一件衬衫。 有了此信息，智能服务可能会建议呼叫中心代理在呼叫期间为鞋子提供20%的优惠券。 如果客户使用优惠券，则该信息会添加到数据集，并且下次客户调用时，预测会得到更好的结果。

### 探索和准备数据

根据定义的业务问题，您知道方法应查看客户的所有Web交易，包括网站访问、搜索、页面查看、点击链接、购物车操作、收到的选件、收到的电子邮件、呼叫中心交互等。

数据科学家通常花费多达75%的时间来创建探索和转换数据的方法。 数据通常来自多个存储库，并保存在不同的架构中 — 必须先对数据进行合并和映射，然后才能用于创建方法。

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

如果您从头开始或配置现有方法，则可以在组织的集中且标准化的数据目录中开始数据搜索，这样可以大大简化搜索过程。 您甚至可能会发现，组织中的其他数据科学家已经识别了一个类似的数据集，并选择对该数据集进行微调，而不是从头开始。
Adobe Experience Platform中的所有数据都遵循标准化的XDM模式，无需创建复杂的模型来连接数据或从数据工程师那里获得帮助。

如果您没有立即找到所需的数据，但该数据存在于Adobe Experience Platform之外，则摄取其他数据集相对而言是一项简单的任务，该任务还将转换为标准化的XDM架构。\
您可以使用 [!DNL Jupyter Notebook] 简化数据预处理 — 可能从您以前用于购买倾向的笔记本电脑模板开始。

![](./images/home/notebook_templates-new.png)

### 创作方法

如果您已经找到满足所有需求的方法，则可以继续进行实验。 或者，您也可以稍微修改方法或从头开始创建一个方法 — 利用 [!DNL Data Science Workspace] 在运行时中创作 [!DNL Jupyter Notebook]. 使用创作运行时可确保您可以同时使用 [!DNL Data Science Workspace] 培训和评分工作流，稍后转换方法，以便它可以被组织中的其他人存储和重用。

您还可以将方法导入 [!DNL Data Science Workspace] 并在创建智能服务时利用实验工作流。

### 试试配方

使用包含核心机器学习算法的方法，可以使用单个方法创建许多方法实例。 这些方法实例称为模型。 模型需要进行培训和评估，以优化其运行效率和效能，这一过程通常包括试错。

![](./images/home/recipe_hiearchy_ui.png)

在您培训模型时，会生成培训运行和评估。 [!DNL Data Science Workspace] 跟踪每个唯一模型的评估量度及其培训运行情况。 通过实验生成的评估量度将允许您确定效果最佳的培训运行。

![](./images/home/evaluation_metrics.png)

访问 [API](./models-recipes/train-evaluate-model-api.md) 或 [UI](./models-recipes/train-evaluate-model-ui.md) 关于如何在 [!DNL Data Science Workspace].

### 实施该模式

如果您选择了经过培训的最佳方法来满足您的业务需求，则可以在 [!DNL Data Science Workspace] 无需开发人员帮助。 只需点击几下，无需编码。 您组织的其他成员可以访问已发布的智能服务，而无需重新创建模型。

已发布的智能服务可配置为在新数据可用时，使用新数据自动不时地对其进行培训。 这可确保您的服务在持续的时间内保持其效率和功效。

## 后续步骤

[!DNL Data Science Workspace] 帮助简化数据科学工作流程，从数据收集到算法，再到面向所有技能水平的数据科学家的智能服务。 使用复杂的工具 [!DNL Data Science Workspace] 提供，您可以显着缩短从数据到分析的时间。

更重要的是， [!DNL Data Science Workspace] 将Adobe领先营销平台的数据科学和算法优化功能交给企业数据科学家。 企业首次将专有算法引入该平台，利用Adobe强大的机器学习和AI功能，大规模提供高度个性化的客户体验。

凭借品牌专业知识、Adobe的机器学习和AI技能的结合，企业有能力在客户要求前，先为客户提供他们想要的东西，从而提高商业价值和品牌忠诚度。

有关其他信息（如完整的日常工作流），请首先阅读 [Data Science Workspace演练](./walkthrough.md) 文档。

## 其他资源

以下视频旨在支持您对 [!DNL Data Science Workspace].

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)