---
keywords: Experience Platform；主页；数据科学Workspace；热门主题；数据科学工作区；数据科学
solution: Experience Platform
title: 数据科学Workspace概述
description: 本指南概述了与Adobe Experience Platform中的数据科学Workspace相关的主要概念。
exl-id: bef25073-0dfb-453d-8c32-7f44d917d62d
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '2411'
ht-degree: 0%

---

# 数据科学工作区概述

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

Adobe Experience Platform [!DNL Data Science Workspace]使用机器学习和人工智能从您的数据中释放见解。 [!DNL Data Science Workspace]已集成到Adobe Experience Platform中，可帮助您跨Adobe解决方案使用您的内容和数据资源做出预测。

所有技能水平的数据科学家都将发现复杂、易用的工具，这些工具支持机器学习方法的快速开发、培训和调整 — 人工智能技术的所有好处，但又没有复杂性。

使用[!DNL Data Science Workspace]，数据科学家可以轻松创建由机器学习提供支持的智能服务API。 这些服务可与其他Adobe服务(包括Adobe Target和Adobe Analytics Cloud)配合使用，帮助您在Web、桌面和移动应用程序中自动提供个性化、有针对性的数字体验。

本指南提供了与[!DNL Data Science Workspace]相关的主要概念的概述。

## 简介

当今的企业高度重视挖掘大数据以实现预测和洞察，从而帮助他们个性化客户体验并为客户（和业务）带来更多价值。
尽管从数据获取见解很重要，但需要付出高昂的代价。 它通常需要熟练的数据科学家来进行密集且耗时的数据研究，以开发提供智能服务的机器学习模型或方法。 过程漫长，技术复杂，很难找到熟练的数据科学家。

借助[!DNL Data Science Workspace]，Adobe Experience Platform允许您在整个企业内引入以体验为中心的人工智能，通过以下方式简化和加快数据到洞见的代码转换：
- 机器学习框架和运行时
- 集成访问存储在Adobe Experience Platform中的数据
- 基于[!DNL Experience Data Model] (XDM)构建的统一数据架构
- 机器学习/人工智能和管理大型数据集所需的计算能力
- 预先构建的机器学习方法，可加快向人工智能驱动的体验的飞跃
- 简化不同技能级别的数据科学家食法的创作、重用和修改
- 只需单击几下即可发布和共享智能服务（无需开发人员），并可进行监控和再培训，以持续优化个性化客户体验

所有技能水平的数据科学家将更快地获得洞察力并更高效地获得数字体验。

## 快速入门

在深入了解[!DNL Data Science Workspace]的详细信息之前，请看下面这些关键术语的简短摘要：

| 搜索词 | 定义 |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Data Science Workspace] | [!DNL Experience Platform]中的[!DNL Data Science Workspace]使客户能够利用跨[!DNL Experience Platform]和Adobe解决方案的数据创建机器学习模型，以生成智能见解和预测，从而编织美妙的最终用户数字体验。 |
| 人工智能 | 人工智能是计算机系统的理论和发展，能够执行通常需要人类智能的任务，例如视觉感知、语音识别、决策和语言之间的翻译。 |
| 机器学习 | 机器学习是一个研究领域，它使计算机能够在不被明确编程的情况下进行学习。 |
| [!DNL Sensei] ML框架 | [!DNL Sensei] ML Framework是跨Adobe的统一机器学习框架，它利用[!DNL Experience Platform]上的数据以更快、可扩展和可重复使用的方式使数据科学家能够开发机器学习驱动的智能服务。 |
| [!DNL Experience Data Model] | [!DNL Experience Data Model] (XDM)是Adobe所领导的标准化工作，旨在为客户体验管理定义标准架构，例如[!DNL Profile]和[!DNL ExperienceEvent]。 |
| [!DNL JupyterLab] | [!DNL JupyterLab]是Project Jupyter的基于Web的开源接口，已紧密集成到[!DNL Experience Platform]中。 |
| 方法 | 方法是Adobe对模型规范的术语，它是一个顶级容器，表示构建和执行训练模型并因此帮助解决特定业务问题所需的特定机器学习、AI算法或算法、处理逻辑和配置组合。 |
| 模型 | 模型是机器学习方法的一个实例，它使用历史数据和配置进行培训以针对业务用例进行解析。 |
| 训练 | 训练是从标记数据中学习模式和洞察的过程。 |
| 已训练的模型 | 训练后的模型表示模型训练过程的可执行输出，其中一组训练数据应用于模型实例。 经过训练的模型将维护对从中创建的任何智能Web服务的引用。 训练后的模型适用于智能服务打分和创建。 对已训练模型的修改可以作为新版本进行跟踪。 |
| 评分 | 评分是使用经过训练的模型从数据生成洞察的过程。 |
| 服务 | 已部署的服务通过API公开人工智能、机器学习模型或高级算法的功能，以便其他服务或应用程序可以使用该功能来创建智能应用程序。 |

下表概述了配方、模型、训练运行和评分运行之间的层次结构关系。

![](./images/home/recipe_hiearchy_ui.png)

## 了解 [!DNL Data Science Workspace]

借助[!DNL Data Science Workspace]，您的数据科学家可以简化在大型数据集中发现洞察内容的繁琐过程。 [!DNL Data Science Workspace]基于通用机器学习框架和运行时构建，可提供高级工作流管理、模型管理和可扩展性。 智能服务支持重复使用机器学习方法，以支持使用Adobe产品和解决方案创建的各种应用程序。

### 一站式数据访问

数据是人工智能和机器学习的基础。

[!DNL Data Science Workspace]已与Adobe Experience Platform完全集成，包括数据湖、[!DNL Real-Time Customer Profile]和[!DNL Unified Edge]。 一次浏览存储在Adobe Experience Platform中的所有组织数据，以及常见的大数据和深度学习库，例如[!DNL Spark] ML和[!DNL TensorFlow]。 如果您没有找到所需的内容，请使用XDM标准化架构摄取您自己的数据集。

### 预建的机器学习方法

[!DNL Data Science Workspace]包括针对常见业务需求（如零售预测和异常检测）的预建机器学习方法，因此数据科学家和开发人员不必从头开始。 目前提供三种配方：[产品购买预测](./pre-built-recipes/product-purchase-prediction.md)、[产品推荐](./pre-built-recipes/product-recommendations.md)和[零售额](./pre-built-recipes/retail-sales.md)。

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

如果您愿意，您可以根据自己的需求调整预建的配方、导入配方，或从头开始构建自定义配方。 无论您何时开始，一旦您培训并超调方法，创建自定义智能服务便不需要开发人员 — 只需单击几下，即可构建有针对性的个性化数字体验。

### 重点介绍数据科学家的工作流程

无论您拥有何种级别的数据科学专业知识，[!DNL Data Science Workspace]都有助于简化和加速查找数据洞察并将洞察应用于数字体验的过程。

### 数据探索

找到正确的数据并加以准备是构建有效方案最耗费人力的部分。 [!DNL Data Science Workspace]和Adobe Experience Platform将帮助您更快地从数据获取见解。

在Adobe Experience Platform上，您的跨渠道数据集中存储在XDM标准化架构中，因此数据更易于查找、理解和清理。 基于通用架构的单个数据存储可以为您节省无数个小时的数据探索和准备时间。

在浏览时，将R、[!DNL Python]或Scala与集成的、托管的[!DNL Jupyter Notebook]一起使用，以浏览[!DNL Experience Platform]上的数据目录。 使用这些语言之一，您还可以利用[!DNL Spark] ML和TensorFlow。 从头开始，或使用为特定业务问题提供的笔记本模板。

作为数据探索工作流的一部分，您还可以摄取新数据或使用现有功能来帮助准备数据。

### 创作

通过[!DNL Data Science Workspace]，您可以决定如何创作配方。

- 通过浏览预先构建的方法来满足您的业务需求，从而节省时间，您可以按原样使用，或对其进行配置以满足您的特定要求。
- 使用Jupyter Notebook中的创作运行时从头开始创建方法以开发和注册方法。
- 使用[!DNL Git]和[!DNL Data Science Workspace]之间可用的身份验证和集成，将在Adobe Experience Platform外部创作的方法上载到[!DNL Data Science Workspace]或从存储库（如[!DNL Git]）导入方法代码。

### 试验

数据科学Workspace为实验过程带来了极大的灵活性。 从你的配方开始。 然后，使用相同的核心算法并搭配独特的特征（如超调整参数）创建单独的实例。 您可以根据需要创建任意数量的实例，并根据需要多次对每个实例进行训练和评分。 在您培训这些人员时，[!DNL Data Science Workspace]将跟踪配方、方法实例和经过培训的实例以及评估指标，因此您不必这样做。

### 可操作

只要点击几下即可创建智能服务，只要您对自己的配方感到满意。 无需编码 — 您可以自行编码，无需征募开发人员或工程师。 最后，将智能服务发布到Adobe IO，为您的数字体验团队做好准备。

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### 持续改进

[!DNL Data Science Workspace]跟踪智能服务的调用位置及其执行情况。 随着数据的滚入，您可以评估智能服务准确性以结束循环，并根据需要重新训练配方以提高性能。 结果是客户个性化的精度不断细化。

### 访问新功能和数据集

一旦通过Adobe服务获得新技术和数据集，数据科学家就可以立即利用这些技术和数据集。 我们通过频繁更新将数据集和技术集成到平台中，因此您不必这样做。

### 安全与安心

保护数据安全是Adobe的首要任务。 Adobe使用为帮助遵守行业公认的标准、法规和认证而开发的安全流程和控制功能来保护您的数据。

安全内置在软件和服务中，是Adobe安全产品生命周期的一部分。
要了解Adobe数据和软件安全性、合规性及其他，请访问安全页面，网址为https://www.adobe.com/security.html。

## [!DNL Data Science Workspace]正在操作

预测和见解可为访问您网站、联系您的呼叫中心或参与其他数字体验的每个客户提供高度个性化的体验提供所需的信息。 以下是[!DNL Data Science Workspace]的日常工作方式。

### 定义问题

这一切都始于一个商业问题。 例如，在线呼叫中心需要上下文来帮助他们将负面客户情绪转变为积极。

有关客户的数据很多。 他们浏览网站，将商品放入购物车，甚至下订单。 他们可能以前曾收到过电子邮件、使用过优惠券，或联系过呼叫中心。 因此，方法需要使用有关客户及其活动的可用数据来确定购买倾向，并推荐客户可能会喜欢和使用的选件。

![](./images/home/example_problem.png)

与呼叫中心联系时，客户购物车中仍有两双鞋，但移除了衬衫。 有了这些信息，智能服务可能建议呼叫中心代理在呼叫期间提供鞋子20%的优惠券。 如果客户使用优惠券，该信息会添加到数据集中，并且下次客户致电时预测会变得更加准确。

### 探索并准备数据

根据定义的业务问题，您知道方法应查看客户的所有Web交易，包括网站访问、搜索、页面查看、点击链接、购物车操作、已接收优惠、已接收电子邮件、呼叫中心交互等。

数据科学家通常花费高达75%的时间来创建探索和转换数据的方法。 数据通常来自多个存储库，并保存在不同的架构中 — 必须先对其进行组合和映射，然后才能用于创建方法。

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

如果您从头开始或配置现有方法，则可以在一个集中且标准化的数据目录中开始您的数据搜索，这会大大简化寻找。 您甚至可能会发现贵组织中的另一位数据科学家已经识别了一个类似的数据集，然后选择优化该数据集，而不是从头开始。
Adobe Experience Platform中的所有数据都符合标准化的XDM架构，从而无需创建复杂模型以联接数据或获取数据工程师的帮助。

如果您没有立即找到所需的数据，但它存在于Adobe Experience Platform之外，则摄取其他数据集是一项相对简单的任务，该数据集还将转换为标准化的XDM架构。\
您可以使用[!DNL Jupyter Notebook]简化数据预处理 — 可能从笔记本模板或以前用于购买倾向的笔记本开始。

![](./images/home/notebook_templates-new.png)

### 创作方法

如果您已找到满足所有需求的处方，则可以继续试验。 或者，您可以修改方法一点或从头开始创建方法 — 利用[!DNL Jupyter Notebook]中的[!DNL Data Science Workspace]创作运行时。 使用创作运行时可确保您既可以使用[!DNL Data Science Workspace]培训和评分工作流，又可以稍后转换方法，以便组织中的其他人可以存储并重用它。

您还可以将方法导入[!DNL Data Science Workspace]，并在创建智能服务时利用试验工作流。

### 试验配方

使用包含核心机器学习算法的配方，可以使用单一配方创建多个配方实例。 这些方法实例称为模型。 模型需要训练和评估来优化其运行效率和功效，这个过程通常包括反复试验。

![](./images/home/recipe_hiearchy_ui.png)

在训练模型时，将生成训练运行和评估。 [!DNL Data Science Workspace]跟踪每个唯一模型及其训练运行的评估指标。 通过试验生成的评估指标将允许您确定表现最佳的训练运行。

![](./images/home/evaluation_metrics.png)

访问[API](./models-recipes/train-evaluate-model-api.md)或[UI](./models-recipes/train-evaluate-model-ui.md)教程，了解如何在[!DNL Data Science Workspace]中训练和评估模型。

### 使模型可操作

当您选择了经过最佳培训的方法来满足您的业务需求时，您无需开发人员帮助即可在[!DNL Data Science Workspace]中创建智能服务。 只需点击几下即可 — 无需编码。 您组织的其他成员无需重新创建模型即可访问发布的智能服务。

发布的智能服务可配置为在新的数据可用时自动不时地对其进行训练。 这可以确保您的服务随着时间的流逝而保持其效率和功效。

## 后续步骤

[!DNL Data Science Workspace]有助于简化和简化数据科学工作流程，从数据收集到算法，再到面向所有技能级别的数据科学家的智能服务。 使用[!DNL Data Science Workspace]提供的复杂工具，您可以显着缩短从数据到见解的时间。

更重要的是，[!DNL Data Science Workspace]将Adobe领先营销平台的数据科学和算法优化功能交给了企业数据科学家。 企业可以首次将专有算法引入该平台，利用Adobe强大的机器学习和AI功能大规模提供高度个性化的客户体验。

结合品牌专业知识和Adobe的机器学习与人工智能能力，企业能够在客户提出要求之前为他们提供他们想要的东西，从而提高商业价值和品牌忠诚度。

有关其他信息（如完整的日常工作流程），请先阅读[数据科学Workspace演练](./walkthrough.md)文档。

## 其他资源

以下视频旨在支持您了解[!DNL Data Science Workspace]。

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)