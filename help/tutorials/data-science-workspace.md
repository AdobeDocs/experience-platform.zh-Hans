---
keywords: Experience Platform;home;popular topics;dsw;DSW
solution: Experience Platform
title: 数据科学工作区教程
topic: tutorial
description: Adobe Experience Platform数据科学工作区使用机器学习和人工智能从数据中获得洞察。 数据科学工作区集成到Adobe Experience Platform，可帮助您跨Adobe解决方案使用内容和数据资产进行预测。
translation-type: tm+mt
source-git-commit: d3ece56d10b1940a5992906a65a50ffe2f7e4346
workflow-type: tm+mt
source-wordcount: '1210'
ht-degree: 0%

---


# [!DNL Data Science Workspace] 教程

Adobe Experience Platform [!DNL Data Science Workspace] 使用机器学习和人工智能从数据中获得洞察。 集成到Adobe Experience Platform，帮 [!DNL Data Science Workspace] 助您跨Adobe解决方案使用内容和数据资产进行预测。 所有技能级别的数据科学家都拥有复杂且易于使用的工具，这些工具支持机器学习方法的快速开发、培训和调整——人工智能技术的所有优势都没有复杂性。

要了解更多信息，请首先阅读数 [据科学工作区概述](../data-science-workspace/home.md)。

## [!DNL Sensei Machine Learning] API

API为数 [!DNL Sensei Machine Learning] 据科学家提供了组织和管理机器学习服务的机制，从算法入门到实验再到服务部署。

**提供以下API开发人员指南：**
- [引擎](../data-science-workspace/api/engines.md) -了解如何查找注册表、 [!DNL Docker] 创建引擎、创建功能管道引擎、检索引擎信息、更新引擎和删除引擎。
- [MLInstances（方法）](../data-science-workspace/api/mlinstances.md) -了解如何创建MLInstance、检索MLInstance的信息、更新MLInstance和删除MLInstance。
- [实验](../data-science-workspace/api/experiments.md) -学习如何创建实验、检索实验或实验运行信息、更新实验和删除实验。
- [模型](../data-science-workspace/api/models.md) -了解如何注册您自己的模型、检索模型信息、更新模型、删除模型、为模型创建新的转码以及检索转码模型的详细信息。
- [MLServices](../data-science-workspace/api/mlservices.md) —— 了解如何创建MLService、检索MLService的信息、更新MLService和删除MLService。
- [洞察](../data-science-workspace/api/insights.md) -了解如何检索Insight的信息、添加新的Model Insight以及检索算法的默认指标列表。

要了解更多信息并获取使用Sensei机器学习API执行CRUD操作所需的值，请访 [问入门指南](../data-science-workspace/api/getting-started.md)。

## How to use [!DNL JupyterLab] Notebooks

[!DNL JupyterLab] 是一个基于Web的用户界面，它 [!DNL Project Jupyter] 与Adobe Experience Platform紧密集成。 它为数据科学家提供了交互式开发环境，使他们能 [!DNL Jupyter notebooks]够处理、编码和数据。 本文档概述其 [!DNL JupyterLab] 功能以及执行常见操作的说明。

**本指南将帮助您：**
- 访问并了解该 [!DNL JupyterLab] 界面。
- 了解代码单元格和内的可用内核 [!DNL JupyterLab]。
- 了解/R中的GPU和内存服 [!DNL Python]务器配置。
- 使用笔记本 [!DNL Platform] 阅读和查询数据。
- 了解笔记本数据限制。

要了解更多信息，请访 [问JupyterLab用户指南](../data-science-workspace/jupyterlab/overview.md)。

## 将源文件打包以进行 [!DNL Docker] 菜谱创作

图 [!DNL Docker] 像允许您将应用程序打包并包含它需要的所有部件。 这包括在一个包中的所有库和其他依赖关系。 在菜谱创 [!DNL Docker] 建工作流中，使用提 [!DNL Azure Container Registry] 供给您的凭据将构建的图像推送到。

**本教程将帮助您：**
- 下载创建菜谱所需的先决条件。
- 了解基 [!DNL Docker] 于模型的创作。
- 为、 [!DNL Docker] R、 [!DNL Python]PySpark或Scala()构建图[!DNL Spark]像。
- 获取 [!DNL Docker] 源文件URL。

要了解更多信息，请按照包 [源文件到菜谱教程中](../data-science-workspace/models-recipes/package-source-files-recipe.md)。

## 导入菜谱

>[!NOTE]
>
>本教程要求您具有 [!DNL Docker] 源文件URL。 如果您 [没有源文件URL](../data-science-workspace/models-recipes/package-source-files-recipe.md) ，请访问将源文件包 [!DNL Docker] 导入菜谱教程。

导入菜谱教程提供有关如何配置和导入打包菜谱的洞察。 在本教程的结尾，您可以在Adobe Experience Platform创建、培训和评估模型 [!DNL Data Science Workspace]。

**本教程将帮助您：**
- 为菜谱创建一组配置。
- 导入 [!DNL Docker] 、R、 [!DNL Python]PySpark或Scala的基于菜谱([!DNL Spark])。

要了解更多信息，请按照导入打包的菜 [谱UI教程](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) 或API [教程操作](../data-science-workspace/models-recipes/import-packaged-recipe-api.md)。

## 训练和评估模型

在Adobe Experience Platform [!DNL Data Science Workspace]，机器学习模型是通过整合与模型意图相适合的现有Recipe来创建的。 然后，对模型进行训练和评估，通过微调其相关的超参数来优化其运行效率和功效。 菜谱是可重用的，这意味着可以使用单个菜谱创建多个模型并针对特定用途进行定制。

**本教程将帮助您：**
- 创建新模型。
- 为模型创建培训运行。
- 评估您的模型培训运行。

要开始，请按照培训和评估模型 [API教程](../data-science-workspace/models-recipes/train-evaluate-model-api.md) 或UI [教程](../data-science-workspace/models-recipes/train-evaluate-model-ui.md)。

## 使用模型洞察框架优化模型

模型洞察框架为数据科学家提供Adobe Experience Platform的工具， [!DNL Data Science Workspace] 为基于实验的最优机器学习模型快速、明智地做出选择。 该框架将提高机器学习工作流程的速度和效率，并提高数据科学家的易用性。 这是通过为每个机器学习算法类型提供一个默认模板来辅助模型调整来完成的。 最终结果使数据科学家和公民数据科学家能够为最终客户做出更好的模型优化决策。

**本教程将帮助您：**
- 配置菜谱代码。
- 定义自定义指标。
- 使用预建的评估指标和可视化图表。

要开始，请按照教程优 [化模型](../data-science-workspace/models-recipes/optimize-model.md)。

## 为模型评分

在Adobe Experience Platform, [!DNL Data Science Workspace] 可以通过将输入数据输入到现有的训练模型中来实现评分。 然后，将评分结果作为新批存储在指定的输出数据集中并可查看。

**本教程将帮助您：**
- 创建新的评分运行。
- 视图您的评分结果。

要开始，请按照模型API教 [程或UI教](../data-science-workspace/models-recipes/score-model-api.md) 程的 [得分进行操作](../data-science-workspace/models-recipes/score-model-ui.md)。

## 将模型发布为服务

Adobe Experience Platform [!DNL Data Science Workspace] 允许您将模型作为服务发布，使IMS组织内的用户无需创建自己的模型即可对数据进行评分。 这可以使用用户 [!DNL Platform] 界面或API完 [!DNL Sensei Machine Learning] 成。

**本教程将帮助您：**
- 将模型发布为服务。
- 使用服务通过服务库对数 [!DNL Platform] 据 [!UICONTROL 进行评分]。

要开始，请按照服务API教程或UI教 [程的形式](../data-science-workspace/models-recipes/publish-model-service-api.md) ，发布 [模型](../data-science-workspace/models-recipes/publish-model-service-ui.md)。

## 模型的计划培训和评分

Adobe Experience Platform [!DNL Data Science Workspace] 允许您在机器学习服务上设置定时评分和培训运行。 自动化培训和评分流程可以跟上数据中的模式，从而帮助保持和提高服务在一段时间内的效率。

**本教程将帮助您：**
- 配置计划评分
- 配置计划培训

要开始，请按照 [计划学习模型UI教程](../data-science-workspace/models-recipes/schedule-models-ui.md)。

## 创建特征管线

>[!NOTE]
>
>目前，功能管道仅通过API可用。

Adobe Experience Platform允许您构建和创建自定义特征管道，以在整个过程中大规模地执行特征工程 [!DNL Sensei Machine Learning Framework Runtime]。

**本指南将帮助您：**
- 实现功能管线类。
- 使用API创建功能管道引擎。

要了解更多信息，请访问创建功 [能管道的教程](../data-science-workspace/authoring/feature-pipeline.md)。

## 构建应 [!DNL Real-Time Machine Learning] 用程序(alpha)

在集线器和集线器上进行无缝计算的组合 [!DNL Edge] 可显着减少通常用于为超级个性化体验提供相关性和响应性的延迟。 因此， [!DNL Real-time Machine Learning] 为同步决策提供具有难以置信的低延迟的推论。 示例包括呈现个性化网页内容、呈现优惠和折扣，以减少客户流失并提高网店转化率。

**本指南将帮助您：**
- 了解体 [!DNL Real-time Machine Learning] 系结构
- 了解工作 [!DNL Real-time Machine Learning] 流程。
- 了解当前的功能 [!DNL Real-time Machine Learning]。
- 提供创建您自己的作品的后续步骤 [!DNL Real-time Machine Learning model]。

要了解更多信息，请访 [问实时机器学习概述](../data-science-workspace/real-time-machine-learning/home.md)。