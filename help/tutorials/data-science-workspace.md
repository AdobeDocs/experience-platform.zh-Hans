---
keywords: Experience Platform；主页；热门主题；dsw;DSW
solution: Experience Platform
title: 数据科学工作区教程
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace使用机器学习和人工智能从数据中创建洞察。 Data Science Workspace集成到Adobe Experience Platform中，可帮助您跨Adobe解决方案使用内容和数据资产进行预测。
exl-id: 7cfd71b1-584f-4588-bbcd-bc42a08a0bc0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1302'
ht-degree: 0%

---

# [!DNL Data Science Workspace] 教程

Adobe Experience Platform [!DNL Data Science Workspace]使用机器学习和人工智能从数据中创建洞察。 [!DNL Data Science Workspace]集成到Adobe Experience Platform中，可帮助您跨Adobe解决方案使用内容和数据资产进行预测。 所有技能水平的数据科学家都拥有复杂易用的工具，支持机器学习方法的快速开发、培训和调整 — 人工智能技术的所有优势，而不复杂。

要了解更多信息，请首先阅读[数据科学工作区概述](../data-science-workspace/home.md)。

## [!DNL Sensei Machine Learning] API

[!DNL Sensei Machine Learning] API为数据科学家提供了组织和管理机器学习服务的机制，从算法入门、实验到服务部署。

**提供以下API开发人员指南：**
- [引擎](../data-science-workspace/api/engines.md)  — 了解如何查找注册表、 [!DNL Docker] 创建引擎、创建功能管道引擎、检索引擎信息、更新引擎和删除引擎。
- [MLInstances（方法）](../data-science-workspace/api/mlinstances.md)  — 了解如何创建MLInstance、检索MLInstance的信息、更新MLInstance和删除MLInstance。
- [实验](../data-science-workspace/api/experiments.md)  — 学习如何创建实验、检索实验或实验运行信息、更新实验和删除实验。
- [模型](../data-science-workspace/api/models.md)  — 了解如何注册您自己的模型、检索模型的信息、更新模型、删除模型、为模型创建新的转码以及检索转码模型的详细信息。
- [MLServices](../data-science-workspace/api/mlservices.md)  — 了解如何创建MLService、检索MLService的信息、更新MLService和删除MLService。
- [洞察](../data-science-workspace/api/insights.md)  — 了解如何检索Insight的信息、添加新的Model Insight，以及检索算法的默认量度列表。

要了解更多信息并获取使用Sensei机器学习API执行CRUD操作所需的值，请访问[快速入门指南](../data-science-workspace/api/getting-started.md)。

## 如何使用[!DNL JupyterLab]笔记本

[!DNL JupyterLab] 是一个基于Web的用户界面， [!DNL Project Jupyter] 它与Adobe Experience Platform紧密集成。它为数据科学家提供了一个交互式开发环境，以便他们能够使用[!DNL Jupyter Notebooks]、代码和数据。 本文档概述了[!DNL JupyterLab]及其功能以及执行常见操作的说明。

**本指南将帮助您：**
- 访问并了解[!DNL JupyterLab]接口。
- 了解[!DNL JupyterLab]中的代码单元格和可用内核。
- 了解[!DNL Python]/R中的GPU和内存服务器配置。

要了解更多信息，请访问[JupyterLab用户指南](../data-science-workspace/jupyterlab/overview.md)。

## JupyterLab笔记本中的数据访问

目前，Data Science Workspace中的JupyterLab支持[!DNL Python]、R、PySpark和Scala的笔记本。 每个支持的内核都提供内置功能，允许您从笔记本内的数据集中读取平台数据。 但是，对分页数据的支持仅限于[!DNL Python]和R笔记本。 本指南重点介绍如何使用JupyterLab笔记本访问您的数据。

**本指南将帮助您：**
- 使用Python、R、PySpark或Scala笔记本读取、写入和查询平台数据。
- 了解每种笔记本类型的阅读限制。

要了解更多信息，请访问[JupyterLab Notebook数据访问开发人员指南](../data-science-workspace/jupyterlab/access-notebook-data.md)

## 将源文件打包以创作[!DNL Docker]菜谱

[!DNL Docker]图像允许您将应用程序打包并包含它需要的所有部件。 这包括一个包中的库和其他依赖项。 生成的[!DNL Docker]映像将使用在菜谱创建工作流期间提供给您的凭据推送到[!DNL Azure Container Registry]。

**本教程将帮助您：**
- 下载创建菜谱所需的先决条件。
- 了解基于[!DNL Docker]的模型创作。
- 为[!DNL Python]、R、PySpark或Scala([!DNL Spark])构建[!DNL Docker]图像。
- 获取[!DNL Docker]源文件URL。

要了解更多信息，请按照[将源文件打包到菜谱教程](../data-science-workspace/models-recipes/package-source-files-recipe.md)中。

## 导入菜谱

>[!NOTE]
>
>本教程要求您具有[!DNL Docker]源文件URL。 如果您没有[!DNL Docker]源文件URL，请访问[将源文件打包到菜谱教程](../data-science-workspace/models-recipes/package-source-files-recipe.md)中。

导入菜谱教程提供有关如何配置和导入打包菜谱的洞察。 在本教程结束前，您可以在Adobe Experience Platform [!DNL Data Science Workspace]中创建、培训和评估模型。

**本教程将帮助您：**
- 为菜谱创建一组配置。
- 导入[!DNL Docker]的[!DNL Python]、R、PySpark或Scala([!DNL Spark])的基于菜谱。

要了解更多信息，请按照导入打包菜谱[UI教程](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md)或[API教程](../data-science-workspace/models-recipes/import-packaged-recipe-api.md)操作。

## 训练和评估模型

在Adobe Experience Platform [!DNL Data Science Workspace]中，机器学习模型是通过合并适合模型意图的现有菜谱来创建的。 然后，对模型进行训练和评估，通过微调其相关的超参数来优化其运行效率和效能。 菜谱是可重用的，这意味着可以使用单个菜谱创建多个模型并针对特定用途进行定制。

**本教程将帮助您：**
- 创建新模型。
- 为模型创建培训运行。
- 评估您的模型培训运行。

要开始，请按照培训并评估模型[API教程](../data-science-workspace/models-recipes/train-evaluate-model-api.md)或[UI教程](../data-science-workspace/models-recipes/train-evaluate-model-ui.md)。

## 使用Model Insights框架优化模型

模型洞察框架为数据科学家提供Adobe Experience Platform [!DNL Data Science Workspace]中的工具，让他们快速、明智地选择基于实验的最佳机器学习模型。 该框架将提高机器学习工作流程的速度和效率，并提高数据科学家的易用性。 这是通过为每个机器学习算法类型提供一个默认模板来协助模型调整来完成的。 最终结果使数据科学家和公民数据科学家能够为最终客户做出更好的模型优化决策。

**本教程将帮助您：**
- 配置菜谱代码。
- 定义自定义量度。
- 使用预建的评估指标和可视化图表。

要开始，请按照[优化模型](../data-science-workspace/models-recipes/optimize-model.md)上的教程操作。

## 为模型打分

通过将输入数据输入到现有的训练模型中，可以在Adobe Experience Platform[!DNL Data Science Workspace]中获得评分。 然后，将评分结果作为新批存储在指定的输出数据集中并可查看。

**本教程将帮助您：**
- 创建新得分运行。
- 视图您的评分结果。

要开始，请按照模型[API教程](../data-science-workspace/models-recipes/score-model-api.md)或[UI教程](../data-science-workspace/models-recipes/score-model-ui.md)的得分操作。

## 将模型发布为服务

Adobe Experience Platform [!DNL Data Science Workspace]允许您将模型作为服务发布，使IMS组织内的用户无需创建自己的模型即可对数据进行评分。 这可以使用[!DNL Platform]用户界面或[!DNL Sensei Machine Learning] API来完成。

**本教程将帮助您：**
- 将模型发布为服务。
- 通过[!DNL Platform] [!UICONTROL Service Gallery]使用服务对数据进行评分。

要开始，请按照服务[API教程](../data-science-workspace/models-recipes/publish-model-service-api.md)或[UI教程](../data-science-workspace/models-recipes/publish-model-service-ui.md)发布模型。

## 模型的计划培训和评分

Adobe Experience Platform [!DNL Data Science Workspace]允许您在机器学习服务上设置计划评分和培训运行。 自动化培训和评分流程有助于跟上数据中的模式，从而保持和提高服务的效率。

**本教程将帮助您：**
- 配置计划评分
- 配置计划培训

要开始，请按照[计划模型UI教程](../data-science-workspace/models-recipes/schedule-models-ui.md)。

## 创建特征管线

>[!NOTE]
>
>目前，功能管道仅可通过API使用。

Adobe Experience Platform允许您构建和创建自定义功能管线，以通过[!DNL Sensei Machine Learning Framework Runtime]大规模执行功能工程。

**本指南将帮助您：**
- 实现功能管线类。
- 使用API创建功能管道引擎。

要了解更多信息，请访问教程，了解[创建功能管道](../data-science-workspace/authoring/feature-pipeline.md)。

## 构建[!DNL Real-Time Machine Learning]应用程序(alpha)

在集线器和[!DNL Edge]上进行无缝计算的组合，可显着减少过去在为个性化体验提供相关和响应式服务时所涉及的延迟。 因此，[!DNL Real-time Machine Learning]为同步决策提供具有难以置信的低延迟的推理。 示例包括呈现个性化网页内容、呈现优惠和折扣，以减少客户流失并提高网店转化率。

**本指南将帮助您：**
- 了解[!DNL Real-time Machine Learning]体系结构。
- 了解[!DNL Real-time Machine Learning]工作流。
- 了解[!DNL Real-time Machine Learning]的当前功能。
- 提供创建您自己的[!DNL Real-time Machine Learning model]的后续步骤。

要了解更多信息，请访问[实时机器学习概述](../data-science-workspace/real-time-machine-learning/home.md)。
