---
keywords: Experience Platform;home;Data Science Workspace;popular topics;data science workspace;data science
solution: Experience Platform
title: 数据科学工作区概述
topic: overview
description: 本指南概述了与数据科学工作区相关的主要概念。
translation-type: tm+mt
source-git-commit: f8d13b305a61f8606c4fa1ceee6d4518b5d83fda
workflow-type: tm+mt
source-wordcount: '2584'
ht-degree: 0%

---


# 数据科学工作区概述

Adobe Experience Platform [!DNL Data Science Workspace] 使用机器学习和人工智能从数据中释放洞察。 集成到Adobe Experience Platform，帮 [!DNL Data Science Workspace] 助您跨Adobe解决方案使用内容和数据资产进行预测。

所有技能级别的数据科学家都将发现复杂、易用的工具，它们支持机器学习方法的快速开发、培训和调整——人工智能技术的所有优势，而不必复杂。

借助 [!DNL Data Science Workspace]数据科学家可以轻松创建由机器学习提供支持的智能服务API。 这些服务与包括Adobe Target和Adobe Analytics Cloud在内的其他Adobe服务协同工作，帮助您在Web、桌面和移动应用程序中自动实现个性化、有针对性的数字体验。

本指南概述了与之相关的主要概念 [!DNL Data Science Workspace]。

## 简介

如今的企业将挖掘大数据作为重中之重来进行预测和洞察，帮助他们个性化客户体验，为客户和业务提供更多价值。
从数据到洞察同样重要，成本也很高。 它通常需要技能娴熟的数据科学家进行密集且耗时的数据研究，以开发支持智能服务的机器学习模型或方法。 过程漫长，技术复杂，而且很难找到熟练的数据科学家。

通过 [!DNL Data Science Workspace]Adobe Experience Platform，您可以在整个企业内引入注重体验的人工智能，通过以下方式简化并加速数据到洞察到代码的实现：
- 机器学习框架和运行时
- 集成访问存储在Adobe Experience Platform的数据
- 基于(XDM)的统 [!DNL Experience Data Model] 一模式
- 机器学习／人工智能和管理大数据集所必不可少的计算能力
- 预建的机器学习方法可加速向人工智能驱动体验的飞跃
- 为不同技能水平的数据科学家简化方法的创作、重用和修改
- 只需点击几下即可实现智能服务发布和共享——无需开发人员——还可进行监控和再培训，以持续优化个性化客户体验

所有技能级别的数据科学家都可以更快地获得更快、更有效的数字体验。

## 入门指南

在深入了解详情之 [!DNL Data Science Workspace]前，以下是主要术语的简要摘要：

| 搜索词 | 定义 |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Data Science Workspace] | [!DNL Data Science Workspace] 使客 [!DNL Experience Platform] 户能够创建机器学习模型，利用跨Adobe和解决 [!DNL Experience Platform] 方案的数据，生成智能洞察和预测，从而打造令人愉悦的最终用户数字体验。 |
| 人工智能 | 人工智能是计算机系统的理论和发展，能够执行通常需要人类智能的任务，如视觉感知、语音识别、决策和语言之间的翻译。 |
| 机器学习 | 机器学习是一个研究领域，它使计算机能够学习，而无需明确编程。 |
| [!DNL Sensei] ML Framework | [!DNL Sensei] ML Framework是跨Adobe的统一机器学习框架，它利用相关数据 [!DNL Experience Platform] ，以更快、可扩展和可重用的方式支持数据科学家开发机器学习驱动的智能服务。 |
| [!DNL Experience Data Model] | [!DNL Experience Data Model] (XDM)是由Adobe牵头的标准化工作，旨在为客户体验管 [!DNL Profile] 理定 [!DNL ExperienceEvent]义标准模式，如和。 |
| [!DNL JupyterLab] | [!DNL JupyterLab] 是Project Jupyter的一个基于web的开放源代码界面，并紧密集成到其中 [!DNL Experience Platform]。 |
| 菜谱 | 处方是模型规范的Adobe术语，是代表特定机器学习、AI算法或算法集合、处理逻辑和配置的顶级容器，用于构建和执行经过培训的模型，从而帮助解决特定的业务问题。 |
| 模型 | 模型是机器学习配方的实例，该配方使用历史数据和配置进行培训，以便为业务用例进行解决。 |
| 培训 | 培训是从标记数据中学习模式和洞察的过程。 |
| 训练模型 | 训练模型表示模型训练过程的可执行输出，其中一组训练数据被应用到模型实例。 经过培训的模型将保留对从其创建的任何智能Web服务的引用。 该模型适合于评分和创建智能Web服务。 可以将训练模型的修改作为新版本进行跟踪。 |
| 评分 | 评分是指使用经过培训的模型从数据生成洞察的过程。 |
| 服务 | 已部署的服务通过API公开人工智能、机器学习模型或高级算法的功能，以便其他服务或应用程序能够使用它来创建智能应用。 |

下表概述了方法、模型、培训运行和评分运行之间的层次关系。

![](./images/home/recipe_hiearchy_ui.png)

## 了解 [!DNL Data Science Workspace]

通过 [!DNL Data Science Workspace]数据科学家可以简化在大数据集中发掘洞察的繁琐过程。 构建在通用的机器学习框架和运行时之上， [!DNL Data Science Workspace] 可提供高级工作流管理、模型管理和可伸缩性。 智能服务支持重新使用机器学习方法，为使用Adobe产品和解决方案创建的各种应用程序提供动力。

### 一站式数据访问

数据是人工智能和机器学习的基石。

[!DNL Data Science Workspace] 与Adobe Experience Platform（包括数据湖）、和等完 [!DNL Real-time Customer Profile]全集成 [!DNL Unified Edge]。 同时浏览存储在Adobe Experience Platform的所有组织数据，以及常见大数据和深入学习库，如 [!DNL Spark] ML和 [!DNL TensorFlow]。 如果您找不到所需内容，请使用XDM标准化模式收集您自己的数据集。

### 预建的机器学习方法

[!DNL Data Science Workspace] 包括预建的机器学习方法，可满足常见的业务需求，如零售销售预测和异常检测，因此数据科学家和开发人员无需从头开始开始。 目前提供三种方法， [产品购买预测](./pre-built-recipes/product-purchase-prediction.md)、 [产品推荐](./pre-built-recipes/product-recommendations.md)和零 [售销售](./pre-built-recipes/retail-sales.md)。

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

如果您愿意，您可以根据自己的需求调整预建菜谱，导入菜谱或从头开始开始，以构建自定义菜谱。 但是，一旦您开始对菜谱进行培训并进行优化，创建自定义智能服务就不需要开发人员——只需点击几下，您就可以构建有针对性的个性化数字体验。

### 侧重于数据科学家的工作流程

无论您具备何种数据科学专业知识 [!DNL Data Science Workspace] 水平，都能帮助简化并加速发现数据洞察并将其应用于数字体验的过程。

### 数据探索

寻找正确的数据并准备数据是构建有效配方最耗费劳动力的部分。 [!DNL Data Science Workspace] adobe experience platform将帮助您更快地从数据获得洞察。

在Adobe Experience Platform，跨渠道数据集中存储在XDM标准模式中，因此数据更易于查找、理解和清理。 基于普通模式的单一数据存储可以为您节省大量数据探索和准备时间。

在您浏览时，将R、 [!DNL Python]或Scala与集成的托管 [!DNL Jupyter Notebook] 一起使用，以浏览上的数据目录 [!DNL Platform]。 使用这些语言之一，您还可以利用 [!DNL Spark] ML和TensorFlow。 从头开始开始，或使用为特定业务问题提供的笔记本模板之一。

作为数据探索工作流程的一部分，您还可以获取新数据或使用现有功能来帮助准备数据。

### 创作

您 [!DNL Data Science Workspace]可以决定如何创作菜谱。

- 通过浏览预建的菜谱节省时间，该菜谱可满足您的业务需求，您可以按原样使用或配置以满足您的特定需求。
- 从头开始创建菜谱，使用Jupyter Notebook中的创作运行时开发和注册菜谱。
- 使用和之间提供的身份验证 [!DNL Data Science Workspace] 和集成，将Adobe Experience Platform以外创作的菜谱上传 [!DNL Git]到存储库中或从存储库导入菜谱 [!DNL Git] 代码 [!DNL Data Science Workspace]。

### 实验

数据科学工作区为实验过程带来极大的灵活性。 开始您的菜谱。 然后，使用与特征（如超调参数）配对的相同核心算法创建单独的实例。 您可以创建所需数量的实例，并根据需要对每个实例进行培训和评分。 在培训菜谱 [!DNL Data Science Workspace] 、菜谱实例和经过培训的实例以及评估指标时，您无需进行培训。

### 操作化

当您对菜谱感到满意时，只需点击几下即可创建智能服务。 无需编码——您无需注册开发人员或工程师即可自行完成。 最后，将智能服务发布到AdobeIO，让您的数字体验团队可以享用。

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### 持续改进

[!DNL Data Science Workspace] 跟踪调用智能服务的位置及其执行方式。 数据滚入后，您可以评估智能服务的准确性以关闭循环，并根据需要重新培训菜谱以提高性能。 结果是不断改进客户个性化的精确度。

### 访问新功能和数据集

数据科学家可以在通过Adobe服务获得新技术和数据集后立即利用它们。 通过频繁的更新，我们将数据集和技术集成到平台中，这样您就不必再进行这些工作。

### 访问控制 [!DNL Data Science Workspace]

访问控制 [!DNL Experience Platform] 通过Adobe Admin Console [管理](https://adminconsole.adobe.com)。 此功能利用Admin Console中的产品用户档案，将用户与权限和沙箱关联起来。 有关更多 [信息](../access-control/home.md) ，请参阅访问控制概述。

>[!IMPORTANT]
>
>要使用，必 [!DNL Data Science Workspace]须启 [!UICONTROL 用“管理数据科学工作区] ”权限。

下表概述了启用或禁用此权限的效果：

| 权限 | 已启用 | 已禁用 |
|---|---|---|
| [!DNL Manage Data Science Workspace] | 提供对中所有服务的访问 [!DNL Data Science Workspace]。 | 禁用对中所有服务的API和 [!DNL Data Science Workspace] UI访问。 禁用后，将阻止路由 [!DNL Data Science Workspace] 到 **[!UICONTROL “模型]** ”和“ **[!UICONTROL 服务]** ”页面。 |

### 安全与心安理得

保护Adobe是重中之重。 Adobe通过为帮助遵守行业公认的标准、法规和认证而开发的安全流程和控制来保护您的数据。

作为Adobe安全产品生命周期的一部分，软件和服务中内置了安全性。
要了解Adobe数据和软件安全性、合规性等信息，请访问安全页面：https://www.adobe.com/security.html。

### 沙箱支持

沙箱是单个实例中的虚拟分区 [!DNL Experience Platform]。 每个 [!DNL Platform] 实例都支持一个生产沙箱和多个非生产沙箱，每个沙箱都维护自己的资源 [!DNL Platform] 库。 非生产沙箱允许您测试功能、运行实验并制作自定义配置，而不会影响您的生产沙箱。 有关沙箱的详细信息，请参阅 [沙箱概述](../sandboxes/home.md)。

目前， [!DNL Data Science Workspace] 存在以下几个沙箱限制：

- 计算资源跨生产沙箱和非生产沙箱进行共享。 生产沙箱的隔离设置将在将来提供。
- 目前[!DNL Spark] ，仅在生产沙箱中支持笔记本电脑和菜谱的Scala/和PySpark工作负载。 今后将提供对非生产沙箱的支持。

## [!DNL Data Science Workspace] 实际操作

预测和洞察可为您提供所需的信息，以便为访问您的网站、联系您的呼叫中心或参与其他数字体验的每位客户提供高度个性化的体验。 您的日常工作是如何进行的 [!DNL Data Science Workspace]。

### 定义问题

所有开始都有业务问题。 例如，在线呼叫中心需要情境来帮助他们将负面客户情绪转化为积极情绪。

有关客户的大量数据。 他们浏览了网站，将商品放入购物车，甚至下了订单。 他们可能以前收到过电子邮件、使用过优惠券或联系过呼叫中心。 然后，菜谱需要使用有关客户及其活动的可用数据来确定购买倾向，并推荐客户可能欣赏和使用的优惠。

![](./images/home/example_problem.png)

在呼叫中心联系时，客户仍在购物车中有两双鞋，但移走了一件衬衫。 有了此信息，智能服务可能会建议呼叫中心代理在呼叫期间为鞋子优惠20%的优惠券。 如果客户使用优惠券，则该信息会添加到数据集中，并且客户下次致电时预测结果会更好。

### 浏览和准备数据

根据定义的业务问题，您知道菜谱应查看客户的所有Web交易，包括网站访问、搜索、页面视图、链接、点击、购物车操作、收到的优惠、收到的电子邮件、呼叫中心互动等。

数据科学家通常花费75%的时间来创建探索和转换数据的配方。 数据通常来自多个存储库并保存在不同模式中——必须先合并并映射数据，才能用它创建菜谱。

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

如果您从头开始或配置现有菜谱，您可以在组织的集中标准化数据目录中开始数据搜索，这大大简化了寻找工作。 你甚至可能发现组织中的另一位数据科学家已经识别出了一个类似的数据集，并选择对该数据集进行微调，而不是从头开始开始。
Adobe Experience Platform的所有数据都符合标准化的XDM模式，无需创建复杂的模型来加入数据或从数据工程师那里获得帮助。

如果您不能立即找到所需数据，但它存在于Adobe Experience Platform以外，那么它是一个相对简单的任务，可以收集更多的数据集，这也将转变为标准化的XDM模式。\
您可以使 [!DNL Jupyter Notebook] 用来简化数据预处理——可能从笔记本模板或您以前习惯购买的笔记本开始。

![](./images/home/notebook_templates.png)

### 创作菜谱

如果您已经找到满足所有需求的菜谱，您可以继续尝试。 或者，您也可以稍微修改菜谱或从头开始创建菜谱——充分利用中的 [!DNL Data Science Workspace] 创作运行时 [!DNL Jupyter Notebook]。 使用创作运行时可确保您既可以使用培训和 [!DNL Data Science Workspace] 评分工作流，也可以稍后转换菜谱，以便在您的组织中存储菜谱并由其他人重复使用。

您还可以在创建智能服 [!DNL Data Science Workspace] 务时将菜谱导入并利用实验工作流。

### 试用配方

借助包含核心机器学习算法的菜谱，可以使用单个菜谱创建许多菜谱实例。 这些菜谱实例称为模型。 一个模型需要进行培训和评估以优化其运行效率和功效，这一过程通常由试验和错误组成。

![](./images/home/recipe_hiearchy_ui.png)

在培训模型时，会生成培训运行和评估。 [!DNL Data Science Workspace] 跟踪每个唯一模型及其培训运行的评估指标。 通过试验生成的评估指标将允许您确定最佳的培训运行。

![](./images/home/evaluation_metrics.png)

请访 [问本部分](https://www.adobe.io/apis/experienceplatform/home/tutorials/data-science-workspace/dsw-tutorials/trainmodel.html) ，获取有关如何在中培训和评估模型的教程 [!DNL Data Science Workspace]。

### 操作模型

当您选择了经过培训的最佳菜谱来满足您的业务需求时，您无需开发人员协助即可创建 [!DNL Data Science Workspace] 智能服务。 只需点击几下即可——无需编码。 您组织的其他成员无需重新创建模型即可访问发布的智能服务。

已发布的智能服务可配置为在新数据可用时不时使用新数据自动进行培训。 这可确保您的服务在时间持续时保持其效率和功效。

## 后续步骤

[!DNL Data Science Workspace] 帮助所有技能水平的数据科学家简化数据科学工作流程，从数据收集到算法再到智能服务。 借助精良的工 [!DNL Data Science Workspace] 具，您可以大幅缩短从数据到洞察的时间。

更重要的是 [!DNL Data Science Workspace] ，将Adobe领先营销平台的数据科学和算法优化能力交给企业数据科学家。 企业首次可以将专有算法引入该平台，利用Adobe强大的机器学习和AI功能大规模提供高度个性化的客户体验。

将品牌专业知识和Adobe的机器学习和人工智能技能结合在一起，企业有能力在客户提出要求之前为客户提供他们想要的东西，从而提升商业价值和品牌忠诚度。

有关其他信息（如完整的日常工作流程），请首先阅读数 [据科学工作区漫步文档](./walkthrough.md) 。

## Journey Orchestration

以下视频旨在帮助您理解 [!DNL Data Science Workspace]。

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)

