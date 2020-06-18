---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 数据科学工作区教程
topic: tutorial
translation-type: tm+mt
source-git-commit: 4d7d61660e6691d77701db1c089b84eee7f60974
workflow-type: tm+mt
source-wordcount: '1253'
ht-degree: 0%

---


# 数据科学工作区教程

Adobe Experience Platform数据科学工作区使用机器学习和人工智能从数据中获得洞察。 数据科学工作区集成到Adobe Experience Platform中，可帮助您跨Adobe解决方案使用内容和数据资产进行预测。 所有技能级别的数据科学家都拥有复杂且易于使用的工具，这些工具支持机器学习方法的快速开发、培训和调整——人工智能技术的所有优势都没有复杂性。

要了解更多信息，请首先阅读数 [据科学工作区概述](../data-science-workspace/home.md)。

## Sensei Machine Learning API

Sensei机器学习API为数据科学家提供了组织和管理机器学习服务的机制，从算法入门到实验再到服务部署。

**提供以下API开发人员指南：**
- [引擎](../data-science-workspace/api/engines.md) -了解如何查找Docker注册表、创建引擎、创建功能管道引擎、检索引擎信息、更新引擎和删除引擎。
- [MLInstances（方法）](../data-science-workspace/api/mlinstances.md) -了解如何创建MLInstance、检索MLInstance的信息、更新MLInstance和删除MLInstance。
- [实验](../data-science-workspace/api/experiments.md) -学习如何创建实验、检索实验或实验运行信息、更新实验和删除实验。
- [模型](../data-science-workspace/api/models.md) -了解如何注册您自己的模型、检索模型信息、更新模型、删除模型、为模型创建新的转码以及检索转码模型的详细信息。
- [MLServices](../data-science-workspace/api/mlservices.md) —— 了解如何创建MLService、检索MLService的信息、更新MLService和删除MLService。
- [洞察](../data-science-workspace/api/insights.md) -了解如何检索Insight的信息、添加新的Model Insight以及检索算法的默认指标列表。

要了解更多信息并获取使用Sensei机器学习API执行CRUD操作所需的值，请访 [问入门指南](../data-science-workspace/api/getting-started.md)。

## 如何使用JupyterLab笔记本

[!DNL JupyterLab] 是基于Web的用户界面， [!DNL Project Jupyter] 并且紧密集成到Adobe Experience Platform中。 它为数据科学家提供一个交互式开发环境，以便与Jupyter笔记本、代码和数据一起使用。 本文档概述其 [!DNL JupyterLab] 功能以及执行常见操作的说明。

**本指南将帮助您：**
- 访问并了解该 [!DNL JupyterLab] 界面。
- 了解代码单元格和内的可用内核 [!DNL JupyterLab]。
- 了解Python/R中的GPU和内存服务器配置。
- 使用笔记本 [!DNL Platform] 阅读和查询数据。
- 了解笔记本数据限制。

要了解更多信息，请访 [问JupyterLab用户指南](../data-science-workspace/jupyterlab/overview.md)。

## 为Docker菜谱创作打包源文件

Docker图像允许您将应用程序打包到它需要的所有部件。 这包括在一个包中的所有库和其他依赖关系。 内置的Docker图像将使用在菜谱创建工作流程中提供给您的凭据推送到Azure容器注册表。

**本教程将帮助您：**
- 下载创建菜谱所需的先决条件。
- 了解基于Docker的模型创作。
- 为Python、R、PySpark或Scala(Spark)构建Docker图像。
- 获取Docker源文件URL。

要了解更多信息，请按照包 [源文件到菜谱教程中](../data-science-workspace/models-recipes/package-source-files-recipe.md)。

## 导入菜谱

>[!NOTE]
>本教程要求您具有Docker源文件URL。 如果您 [没有Docker源文件URL](../data-science-workspace/models-recipes/package-source-files-recipe.md) ，请访问将源文件打包到菜谱教程中。

导入菜谱教程提供有关如何配置和导入打包菜谱的洞察。 在本教程的结尾，您可以在Adobe Experience Platform数据科学工作区中创建、培训和评估模型。

**本教程将帮助您：**
- 为菜谱创建一组配置。
- 导入Python、R、PySpark或Scala(Spark)的基于Docker的菜谱。

要了解更多信息，请按照导入打包的菜 [谱UI教程](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) 或API [教程操作](../data-science-workspace/models-recipes/import-packaged-recipe-api.md)。

## 训练和评估模型

在Adobe Experience Platform数据科学工作区中，机器学习模型是通过整合与模型意图相适应的现有Recipe来创建的。 然后，对模型进行训练和评估，通过微调其相关的超参数来优化其运行效率和功效。 菜谱是可重用的，这意味着可以使用单个菜谱创建多个模型并针对特定用途进行定制。

**本教程将帮助您：**
- 创建新模型。
- 为模型创建培训运行。
- 评估您的模型培训运行。

要开始，请按照培训和评估模型 [API教程](../data-science-workspace/models-recipes/train-evaluate-model-api.md) 或UI [教程](../data-science-workspace/models-recipes/train-evaluate-model-ui.md)。

## 使用模型洞察框架优化模型

模型洞察框架为Adobe Experience Platform科学工作区中的数据科学家提供工具，让他们快速、明智地选择基于实验的最佳机器学习模型。 该框架将提高机器学习工作流程的速度和效率，并提高数据科学家的易用性。 这是通过为每个机器学习算法类型提供一个默认模板来辅助模型调整来完成的。 最终结果使数据科学家和公民数据科学家能够为最终客户做出更好的模型优化决策。

**本教程将帮助您：**
- 配置菜谱代码。
- 定义自定义指标。
- 使用预建的评估指标和可视化图表。

要开始，请按照教程优 [化模型](../data-science-workspace/models-recipes/optimize-model.md)。

## 为模型评分

Adobe Experience Platform数据科学工作区中的评分可以通过将输入数据输入到现有的训练模型中来实现。 然后，将评分结果作为新批存储在指定的输出数据集中并可查看。

**本教程将帮助您：**
- 创建新的评分运行。
- 视图您的评分结果。

要开始，请按照模型API教 [程或UI教](../data-science-workspace/models-recipes/score-model-api.md) 程的 [得分进行操作](../data-science-workspace/models-recipes/score-model-ui.md)。

## 将模型发布为服务

Adobe Experience Platform数据科学工作区允许您将模型作为服务发布，使IMS组织内的用户无需创建自己的模型即可对数据进行评分。 这可以使用用户 [!DNL Platform] 界面或Sensei Machine Learning API来完成。

**本教程将帮助您：**
- 将模型发布为服务。
- 使用服务通过服务库对数据 [!DNL Platform] 进行评分。

要开始，请按照服务API教程或UI教 [程的形式](../data-science-workspace/models-recipes/publish-model-service-api.md) ，发布 [模型](../data-science-workspace/models-recipes/publish-model-service-ui.md)。

## 模型的计划培训和评分

Adobe Experience Platform数据科学工作区允许您在机器学习服务上设置定期评分和培训运行。 自动化培训和评分流程可以跟上数据中的模式，从而帮助保持和提高服务在一段时间内的效率。

**本教程将帮助您：**
- 配置计划评分
- 配置计划培训

要开始，请按照 [计划学习模型UI教程](../data-science-workspace/models-recipes/schedule-models-ui.md)。

## 创建特征管线

>[!NOTE]
>目前，功能管道仅通过API可用。

Adobe Experience Platform允许您通过Sensei机器学习框架运行时构建和创建自定义功能管道以大规模执行功能工程。

**本指南将帮助您：**
- 实现功能管线类。
- 使用API创建功能管道引擎。

要了解更多信息，请访问创建功 [能管道的教程](../data-science-workspace/authoring/feature-pipeline.md)。

## 构建实时机器学习应用程序(alpha)

在集线器和边缘上的无缝计算相结合可显着减少过去在为超级个性化体验提供相关性和响应性方面所涉及的延迟。 因此，实时机器学习为同步决策提供了极低延迟的推理。 示例包括呈现个性化网页内容、呈现优惠和折扣，以减少客户流失并提高网店转化率。

**本指南将帮助您：**
- 了解实时机器学习架构。
- 了解实时机器学习工作流程。
- 了解实时机器学习的当前功能。
- 提供创建您自己的实时机器学习模型的后续步骤。

要了解更多信息，请访 [问实时机器学习概述](../data-science-workspace/real-time-machine-learning/home.md)。